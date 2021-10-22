practicals
==========

setting up
----------

To get started with the exercises, you'll need to install both ``git`` and ``conda`` on your computer. You can follow the
instructions provided on Blackboard, or from the instructions for installing git from `here <https://git-scm.com/downloads>`__, 
and Anaconda from `here <https://docs.anaconda.com/anaconda/install/>`__. 

download/clone the repository
-----------------------------

Once you have these installed, **clone** the `repository <https://github.com/iamdonovan/egm722/>`__ to your computer by doing one of the following things:

1. Open GitHub Desktop and select **File** > **Clone Repository**. Select the **URL** tab, then enter the URL for this 
   repository.
2. Open **Git Bash** (from the **Start** menu), then navigate to your folder for this module.
   Now, execute the following command: ``git clone https://github.com/iamdonovan/egm722.git``. You should see some messages
   about downloading/unpacking files, and the repository should be set up.
3. You can also clone this repository by clicking the green "clone or download" button above, and select "download ZIP"
   at the bottom of the menu. Once it's downloaded, unzip the file and move on to the next step. I don't recommend this
   step, however, as it will be more difficult for you to download the material for each week, or to receive any updates I
   might make. 

create a conda environment
--------------------------

Once you have successfully cloned the repository, you can then create a ``conda`` environment to work through the exercises.

To do this, use the environment.yml file provided in the repository. If you have Anaconda Navigator installed,
you can do this by selecting **Import** from the bottom of the **Environments** panel. 

Otherwise, you can open a command prompt (on Windows, you may need to select an Anaconda command prompt). Navigate
to the folder where you cloned this repository and run the following command:
::

    C:\Users\iamdonovan> conda env create -f environment.yml

This will probably take some time (so feel free to catch up on Facebook or whatever kids do nowadays), but fortunately 
you will only have to do this once. If you

start jupyter-notebook
----------------------

From Anaconda Navigator, you can launch jupyter-notebook directly, and navigate to the folder where the first week's
practical material is located. Make sure that your egm722 environment is activated.

From the command-line, first open a terminal window or an **Anaconda Prompt**, and navigate to the folder where the
first week's practical material is located.

Activate your newly-created environment (``conda activate egm722``). Launch jupyter-notebook (``jupyter-notebook.exe``),
which should launch a web browser window, which should give you an overview of the current folder. 

alternative: binder link
------------------------

There is also a |binder| available, which will allow you to run the exercises remotely via your web browser. It may take some time to set up, particularly if it's been a while since anyone has used the link, but it should eventually work.

practicals
----------

.. note::

    The following linked pages are non-interactive overviews of the things covered in each practical. To actually run the practicals yourself, you'll need to go through the steps of cloning the github repository and setting up the environment outlined above, or follow the binder link to run the practicals online.

- [Week 1 - Introduction to git and programming with python](/egm722/practicals/week1)
- [Week 2 - Mapping with cartopy](/egm722/practicals/week2)
- [Week 3 - Working with vector data in python](/egm722/practicals/week3)
- [Week 4 - Working with raster data in python](/egm722/practicals/week4)
- [Week 5 - Additional exercises](/egm722/practicals/week5)


.. |binder| image:: https://mybinder.org/badge_logo.svg
     :target: https://mybinder.org/v2/gh/iamdonovan/egm722/main


