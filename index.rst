:tocdepth: 1

.. sectnum::

.. Metadata such as the title, authors, and description are set in metadata.yaml

.. TODO: Delete the note below before merging new content to the main branch.

.. note::

   **This technote is a work-in-progress.**

Abstract
========

Summary of crowded field processing performance with the pipe_crowd prototype
code. 

Test cases
==========

To test the performance of pipe_crowd, four datasets were chosen, with varying
degree of crowding. Below is a brief description of these datasets from
u/kherner/PREOPS-597_20220120.::

"instrument": "DECam", "visit":205419 High crowding 
"instrument": "DECam", "visit":223501 Medium crowindg
"instrument": "DECam", "visit":428066 Low crowding 

In addition to these three fields, we also select a high latitude field from the
HiTS SN survey.::

"instrument": "DECam", "visit":288970 Control  u/sullivan/DM-30831-HiTS2014-templates_test/20211011T191211Z

Below is the result of running pipe_crowd without any modifications to the code
and using its default configuration.

.. figure:: /_static/high.png
    :name: high

    Small region of the high crowding field (left; inset shows PSF model used),
    recontructed image (centre), and residuals (right). Pixels in red are
    masked. 

.. figure:: /_static/medium.png
    :name: med

    Same for medium crowding field.

.. figure:: /_static/low.png
    :name: low

    Same for low crowding field.

.. figure:: /_static/control.png
    :name: control

    Same for control field.

Issues identified 
=================

Through successive runs of pipe_crowd using default parameters, the following
issues were identified:

 #. Poor performance in iterative source detection. Essentially, source detection
    in the residual images produce no additional sources. 
 #. PSF model has wings. Produces oversubtract residual images.
 #. Centroid coordinates are NaN after first iteration

Testing PSF model performance
-----------------------------

In the crowded fields the first potential issue identified was the presence of
wings in the PSF model produced by ProcCCD/CharactrizeImage. Below we show two
examples of PSF models for an medium crowded field and the control field. 
 
.. figure:: /_static/psf_crowded.png
    :name: crowded

    PSF model for a crowded field. Notice the wings of the distribution are
    non-zero. This model was recontructed using the XXX method. The wings of the
    models are very clear in the recontructed model image (left). In the right
    panel the counts along the central row/colum are shown.


.. figure:: /_static/psf_non-crowded.png
    :name: hips

    Same as above, but for the PSF model in a non-crowded field (Control/HiTS).

Since the winged PSF can potentially oversubtract flux from neighbor sources,
this could affect source detection in the residual images. This could be the
culprit for the iterative source detection not yielding additional. This effect
was confirmed by inspecting the residual images.

We attempt to replace the PSF model with the SimplePSF one, which is described
by a 2D normal distribution. However, this had no effect in identifying more
sources in iteration > 1. 

Centroiding
------------

Centroiding removes too many (all) new sources. 


.. figure:: /_static/centroid_issue.png
    :name: centroid-issue

    In the low crowding test, on iteration > 1 several new sources are detected
    using simple threshold source detection, these are marked in yellow. Red
    show sources identified in iteration = 0. This shows the success of source
    detection, however the centroid task produces unwanted NaNs that remove
    these new sources for i > 1. 

This was solved by brute force updating the spurious centroid positions
with the less accurate coarse positions. See `code block <https://github.com/balbinot/pipe_crowd/blob/f17b8620bc995ff39539f10e4c0dd4acdc456594/python/lsst/pipe/crowd/crowd.py#LL272C1-L278C94>`__ 

TODO: investigate point of failure of centroid()

Deblending
----------

TODO: make plots

Performance 
===========

TODO: Summary of the performance after XM with Gaia (external catalogue).

People
======

This project is part of in-kind contribution program NED-UTR-S3. The main people
involved are:

* `Eduardo Balbinot <http://balbinot.github.io>`__ (Leiden) - from Nov 2022 to present
* Zuzanna Kostrzewa-Rutkowska (Leiden) - from ? to Sep 2022.

Add content here
================

Add content here.
See the `reStructuredText Style Guide <https://developer.lsst.io/restructuredtext/style.html>`__ to learn how to create sections, links, images, tables, equations, and more.

.. Make in-text citations with: :cite:`bibkey`.
.. Uncomment to use citations
.. .. rubric:: References
.. 
.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :style: lsst_aa
