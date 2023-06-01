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
degree of crowding. Below is a brief description of these datasets.::

"instrument": "DECam", "visit":205419, "detector":11}) ## CROWDED lvl 99 u/kherner/PREOPS-597_20220120
"instrument": "DECam", "visit":223501, "detector":11}) ## CROWDED lvl 50 u/kherner/PREOPS-597_20220120
"instrument": "DECam", "visit":428066, "detector":11}) ## CROWDED lvl 10 u/kherner/PREOPS-597_20220120 
"instrument": "DECam", "visit":288970, "detector":13}) ## NON CROWDED u/sullivan/DM-30831-HiTS2014-templates_test/20211011T191211Z



Testing PSF model performance
=============================

 
.. figure:: /_static/psf_crowded.png
    :name: crowded

    PSF model for a crowded field. Notice the wings of the distribution are
    non-zero. 


.. figure:: /_static/psf_non-crowded.png
    :name: hips

    PSF model for a non-crowded field (HiPS).

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
