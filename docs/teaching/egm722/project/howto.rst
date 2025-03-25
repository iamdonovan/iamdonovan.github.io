EGM722: A how-to Guide
======================

Introduction
------------

EGM722 is a module that is designed to introduce students to programming through the python programming language,
using a variety of software tools. Interactive programming exercises are provided in the form of ``jupyter`` notebooks,
and are intended to introduce students to geospatial packages such as ``cartopy``, ``geopandas``, and ``rasterio``,
among others. Additional exercises guide users through fundamental git skills such as adding/committing changes to code,
creating and merging branches, and resolving conflicts.


Setup and installation
----------------------

Getting started
^^^^^^^^^^^^^^^

To get started with the exercises, at a minimum, you will need to make sure that both ``git`` and ``conda`` are
installed on your computer. If you do not already have ``git`` installed, you can download the installer for your
operating system from the `official download site <https://git-scm.com/downloads>`__.

To install ``conda``, there are a few options:

- **Anaconda Navigator**: If you are most comfortable with a graphical interface, you can download Anaconda Navigator
  from:  https://www.anaconda.com/download/success
- **miniforge**: If you are comfortable with (or wanting to learn) a command line interface, you can download
  miniforge, a more lightweight conda provider, from: https://conda-forge.org/download/

Optional steps
^^^^^^^^^^^^^^

**GitHub**: While it is not strictly necessary to open a GitHub account to be able to work through the programming
exercises, it is recommended, so that you are able to create a fork of this repository to complete the exercises
intended to familiarize you with version control using git and GitHub. You can sign up for a free account
at https://github.com.

**PyCharm/VSCode**: I also highly recommend that you use an integrated development environment (IDE) to help you with
writing your code. Again, this is not strictly necessary to work through the jupyter exercises, but some exercises
require the use of some sort of IDE. For python, PyCharm and VSCode are two of the most popular (freely available!)
choices, and there is a wealth of tutorials available for getting set up with them.

Download links:

- **PyCharm Community Edition**: https://www.jetbrains.com/pycharm/download/ (be sure to scroll down to the
  **Community Edition** link!)
- **VSCode**: https://visualstudio.microsoft.com/downloads/ (be sure to choose **Visual Studio Code**, not
  **Visual Studio**!)

Download/clone the egm722 repository
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The EGM722 repository is hosted at: https://github.com/iamdonovan/egm722

If you have create a GitHub account, you should first fork the repository to your own account. Once you have done this,
you can clone your fork using the following command:

.. code-block:: text

    git clone https://github.com/{your_username}/egm722.git

making sure to replace ``{your_username}`` with your actual **GitHub** username!

If you do not have a GitHub account, you can still clone the EGM722 repository using the following command:

.. code-block:: text

    git clone https://github.com/iamdonovan/egm722.git


Setting up the conda environment
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Once you have successfully cloned the repository, you can then create a conda environment to work through the exercises.

To do this, use the **environment.yml** file provided in the repository. If you have Anaconda Navigator installed,
you can do this by selecting **Import** from the bottom of the **Environments** panel.

Otherwise, from a command prompt or terminal, run the following command from the directory where you cloned the EGM722
repository:

.. code-block:: text

    conda env create -f environment.yml

The contents of **environment.yml** are as follows:

.. code-block:: yaml

    name: egm722
    channels:
      - conda-forge
      - defaults
    dependencies:
      - python
      - geopandas
      - cartopy>=0.21
      - jupyterlab
      - ipywidgets
      - rasterio
      - pyepsg
      - folium

And the packages that EGM722 requires are:

- ``geopandas``: for working with spatial vector data (https://geopandas.org/en/stable/)
- ``cartopy``, version 0.21 or greater: for creating maps (https://scitools.org.uk/cartopy/docs/latest/)
- ``jupyterlab``: for running the interactive notebook exercises (https://jupyter.org/)
- ``ipywidgets``: for interactive plotting in jupyter notebooks (https://ipywidgets.readthedocs.io/en/stable/)
- ``rasterio``: for working with raster data (https://rasterio.readthedocs.io/en/stable/)
- ``pyepsg``: for access to EPSG codes (https://pyepsg.readthedocs.io/en/latest/)
- ``folium``: for creating interactive HTML maps (https://python-visualization.github.io/folium/latest/)
- ``rasterstats``: for computing zonal statistics (https://pythonhosted.org/rasterstats/)
- ``earthaccess``: for accessing NASA Earth science datasets (https://earthaccess.readthedocs.io/en/latest/)

The final two dependencies, ``rasterstats`` and ``earthaccess``, are not included in **environments.yml** file, to
give students practice installing packages using both **Anaconda Navigator** or the ``conda`` command-line interface.

Additional setup steps
^^^^^^^^^^^^^^^^^^^^^^

Once you have cloned the repository and created the ``conda`` environment, you should be able to launch ``jupyter-lab``
and get started on the first exercise. For full instructions for each exercise, be sure to visit the
:doc:`class website <../practicals/index>`.

There are some additional recommended setup steps that may make life easier, enabling you to configure ``jupyter`` and
your IDE of choice. For full setup steps, visit the :doc:`complete setup guide <../setup/index>` available on the
class website.

Methods
-------

In general, the goal behind

Week 1
^^^^^^


Week 2
^^^^^^


Week 3
^^^^^^


Week 4
^^^^^^


Week 5
^^^^^^


Expected Results
----------------

Week 1
^^^^^^


Week 2
^^^^^^


Week 3
^^^^^^


Week 4
^^^^^^


Week 5
^^^^^^


Troubleshooting: where to go to get help
----------------------------------------

Common issues that may come up when working through the exercises include:


If you encounter any issues that you do not understand or aren’t able to work through, you can still report the issue
to find help. Please ensure that when reporting your issues, you are as specific as possible – include full error
messages/traceback, either in the form of copied/pasted text or screenshots. It can also be helpful to describe what
type of computer and operating system you have.

You can report your issue in the following ways/places:

1. **Blackboard discussion forum**: Post your issue in the relevant discussion forum on the module Blackboard page.
2. **Weekly Office Hours drop-in sessions**: check the Blackboard calendar for full details. This is often a helpful
   way to get small issues resolved quickly, as it avoids the asynchronous back and forth that can happen on the
   discussion forums.
3. **GitHub issues**: if you have a GitHub account, you can report your problem by opening an issue on the EGM722
   GitHub repository: https://github.com/iamdonovan/egm722/issues


References
----------

