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

Issues identified 
=================

Through successive runs of pipe_crowd using default parameters, the following
issues were identified:

 #. Poor performance in iterative source detection. Essentially, source detection
    in the residual images produce no additional sources. 
 #. PSF model has wings. Produces oversubtract residual images.
 #. Centroid coordinates are NaN after first iteration


Testing PSF model performance
=============================

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
===========

Define centroiding

Example tables with NaN

Fix. 

Cause unknown.

Deblending
==========

Performance 
===========

Summary of the performance after XM with Gaia (external catalogue).

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
