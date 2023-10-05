programming skills for phd researchers (using python)
======================================================

.. note::

    If you are unable to install all of the software on your own machine, you can still work through the exercises
    online by clicking the badge below:

    .. image:: https://mybinder.org/badge_logo.svg
        :target: https://mybinder.org/v2/gh/iamdonovan/intro-to-python/

    |br| This will (eventually) open an online interactive version of the material that you will be able to run from
    within your web browser.

.. toctree::
   :glob:
   :hidden:
   :maxdepth: 1

   setup/index
   lectures
   exercises/index
   resources

The aim of this workshop is to provide PhD Researchers with skills and experience to use programming tools for
specialized and reproducible analysis. The topics covered include (but are not limited to):

- Introduction to version control using git
- Introduction to the python programming language
- Reading and understanding error messages to fix issues
- Reading and transforming datasets
- Basic statistical analysis
- Project organization

Before moving on to the :doc:`practicals<exercises/index>` below, be sure to visit the
:doc:`setup<setup/index>` page to make sure that you have the software and materials set up in order to get started.

schedule
---------

+---------+-------------------------+--------------------------------+
| session | theme                   | exercise topic(s)              |
+---------+-------------------------+--------------------------------+
| 1       | git and conda           | :doc:`exercises/git`           |
|         |                         |                                |
|         |                         | :doc:`exercises/project`       |
+---------+-------------------------+--------------------------------+
| 2       | intro to python         | :doc:`exercises/intro`         |
|         |                         |                                |
|         |                         | :doc:`exercises/debugging`     |
+---------+-------------------------+--------------------------------+
| 3       | plotting                | :doc:`exercises/plotting`      |
+---------+-------------------------+--------------------------------+
| 4       | organization            |                                |
+---------+-------------------------+--------------------------------+
| 5       | statistical analysis    |                                |
+---------+-------------------------+--------------------------------+
| 6       | regression              |                                |
+---------+-------------------------+--------------------------------+
| 7       | byod\ [1]_ project work |                                |
+---------+-------------------------+--------------------------------+
| 8       | byod project work       |                                |
+---------+-------------------------+--------------------------------+

exercise solutions
-------------------

At the end of each of the exercises, I have provided a list of additional exercises for you to practice the skills and
concepts covered in each session. On the `GitHub <https://github.com/iamdonovan/intro-to-python>`__ page for the
workshop, you can find some example solutions that I have provided on the ``solutions`` branch. To get there, click the
link above, which should take you here:

.. image:: img/workshop_github.png
    :width: 720
    :align: center
    :alt: the workshop github page

|br| Next, click the button that says ``main`` to show a list of branches, then select ``solutions``:

.. image:: img/solutions_branch.png
    :width: 720
    :align: center
    :alt: the workshop github page, with the menu to select branches open and highlighted by a red box.

|br| This will show you the files included on the ``solutions`` branch - inside each folder, you should find script or
notebook file that contains example solutions for each of the exercise questions:

.. image:: img/example_solution.png
    :width: 720
    :align: center
    :alt: an example solution for one of the sets of exercise questions

|br| Remember that as we have discussed in the workshop, these solutions are not the only possible solutions to the
questions - there are potentially many different ways to answer the questions!

notes
-------

.. [1] "bring your own data"
