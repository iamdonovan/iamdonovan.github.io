setting up conda/anaconda
==========================

.. note::

    There are many, many ways to install **conda** - I will link to two here. Note that you only need to choose **one**.

introduction
-------------

**conda** is an open-source package management system, intended to make it easier to work on different projects that
may have different, potentially conflicting, package requirements. Originally developed for python packages, but it
can be used to package and distribute software packages for any language, including **R**.

**conda** can be used from both the command-line as well as via a graphical user interface (GUI). The instructions below
will help you install **either** a GUI frontend (**Anaconda Navigator**), **or** a command-line interface
(**mambaforge**).

installing anaconda navigator
------------------------------

To begin, navigate to https://docs.anaconda.com/anaconda/install/, which contains detailed, operating-system dependent
instructions for installing Anaconda. Anaconda is available for Windows, macOS, and Linux operating systems; most of
the instructions for this course will be given using Windows, but I am happy to work with you on setting yourself up
in another operating system if need be.

Follow the linked instructions for downloading and installing Anaconda. When the installation is finished, move on to
the next step, :doc:`environment`.

installing mambaforge
-----------------------

If you feel comfortable using a command-line interface, I recommend installing **mambaforge**.

Go to the `mambaforge <https://github.com/conda-forge/miniforge#mambaforge>`__ GitHub page, and select the
installer for your computer's operating system.

Once it has downloaded, you can either double-click on the installer (Windows), or by following the instructions
in the `install <https://github.com/conda-forge/miniforge#install>`__ section (Linux/MacOS).

