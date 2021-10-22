week 2 - hyperspectral image analysis
=====================================

overview
--------

In the lectures and reading this week, you've learned about hyperspectral remote sensing and a number of different methods for analyzing hyperspectral data. In this practical, we'll gain some experience working with hyperspectral data, using a few examples written in python.

objectives
----------

- Open and view data using xarray
- Perform atmospheric correction using dark object subtraction
- Use spectral angle matching to compare spectral signatures and identify surfaces
- Gain some familiarity with `Spectral Python (SPy) <https://www.spectralpython.net/>`__, a python package for analyzing hyperspectral images.

data provided
-------------

In the **data** folder, you should have the following files:
::

    └─ data/
        ├─ solar_spectra.csv
        └─ spectral_library.csv

You'll need to download the hyperspectral data from Blackboard, or from the `Google Drive link <https://drive.google.com/file/d/18EHJpSbkbARJ2Rt6NndBSPe9SlcYr_iO/view?usp=sharing>`__ - be sure to save it to the ``data`` folder.

getting started
---------------

Once you clone the repository, you can set up the conda environment using the provided ``environment.yml`` file.

To get started working through the practical, launch the jupyter notebook (``Hyperspectral Image Analysis.ipynb``).

