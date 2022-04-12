debugging exercise
===================

.. warning::

    Before proceeding, you should have completed all of the :doc:`../setup/index` steps, including installing an IDE
    such as PyCharm.

    **If you have not completed all of the steps above, stop now and go back to finish them!**

.. note::

    The example and instructions shown here are for PyCharm Community Edition 2021.3.3 -- if you are using a
    different IDE, such as VS Code or Spyder, the steps will be similar, broadly speaking, but they are different
    software packages with a different appearance and menu options.

    I will do my best to provide help with other options, but I can't promise a completely painless experience.

setup
-------

Before getting started with the exercise, there's one final bit of setup needed.

PyCharm provides a number of options for running scripts - the instructions below will show you how you can do this
using either the **Run** tool or the **Terminal** panel.

.. note::

    Again, this assumes that you have set up PyCharm according to the :doc:`instructions<../setup/pycharm>`, including
    creating a new project for your EGM722 practicals.

To be able to run a script using the green "run" button, or to use the debugging tools, you'll need to make sure that
you've configured a python interpreter already, following the instructions in :ref:`create project`
or :ref:`adding interpreter`.

In the upper right-hand corner of the PyCharm window, you should see this:

**buttons**

Click on **Add Configuration...** to open the **Run/Debug Configurations** window:

**run/debug**

Click on the **+** icon in the upper left to add a new configuration, and select **Python**:

**new python configuration**

Call this new configuration ``debug_exercise``, and set the **Script path** to be the path to **debugging_exercise.py**
in the **Week1** folder of your egm722 repository. Finally, make sure that the **Python interpreter is set to
your ``egm722`` environment, then click **OK** to finish the configuration.

You should see that the buttons in the upper right of the window have changed:

**new buttons**

running a script
-----------------

Once you have the script configured, you can press the green **Run** button (the triangle). When you do this,
you should see that the **Run Panel** opens at the bottom of the window:

**run panel**

This is where anything printed to the screen by your script will show, including all error messages. In fact, you
should see an error message already:

**error message**

If the script has run successfully, you should see the following:

.. code-block:: sh

    Process finished with exit code 0

If the exit code is any other value, it means that something hasn't gone according to plan. For more information about
python exit codes, have a look at the documentation for ``sys.exit()``
`here <https://docs.python.org/3.8/library/sys.html#sys.exit>`__.

Here, we can see that the process finished with exit code 1, which indicates that the interpreter raised an
**exception** (an error). Now that we have confirmed that the script that's supposed to have errors in it indeed
has errors, we'll use the debugging tools in order to fix those errors.

the error message
------------------

First, though, let's have another look at the error message...

- reading the error messages
- script location (line number, column number) in traceback
- opening the script and noticing the syntax highlighting
- fixing the error

commiting changes
------------------

.. note::

    You only need to do this once per fix - you can choose whether to use GitHub Desktop or the command-line tools.


github desktop
...............

With **GitHub Desktop** open, ...

- adding commits
- pushing commits

command-line tool
..................

At the bottom of the PyCharm window, you should see

- git status
- git add
- git commit
- git push (optional)


the debugging tools
--------------------

Once you've committed this fix, run the script again. You should see that there's now an error in a different spot:

**new error**

Because this error appears at line XX in the code, let's tell PyCharm to stop the script at that location. To do this,
click on the left-hand side of the code panel, just to the right of line XX. You should see a red dot appear:

**add a breakpoint**

This is a **breakpoint** - a spot for the interpreter to pause while we inspect what's going on in the script. Run the
script again, but this time press the green **debugging** button (it looks like a small bug).

You should see that the **Debugging Panel** has now opened in the bottom half of the window:

**debugging**

Things to cover:

- running the debugging tools (breakpoints, stepping, etc.)
- status of variables, modules, etc.
- fixing the errors


kinds of errors
----------------

- 3 kinds of errors (syntax, runtime, semantic) - point to lecture for week 2 (maybe move lecture topics around?)

In next


finishing up
-------------

Once you've identified and fixed the remaining bugs, ...

- committing the fixes and pushing to github
