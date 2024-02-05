conflict resolution (using git)
================================

Sometimes, despite our best efforts, we run into conflicts in life.

The same is true for programming - when working with other people (or even ourselves, sometimes), we may wind up with
different versions of a file (or files) that have *conflicting* changes - that is, a file (or files) has been edited on
multiple branches of a project, and **git** isn't able to determine which of these is the "correct" one.

When this happens, you will need to tell ``git`` what version of the file you want to keep by **resolving** the merge
conflict.


getting started
----------------

To get started, open up **GitHub Desktop** to your EGM722 repository - you should see that in addition to the ``week*``
branches (``week2``, ``week3``, ``week4``, ``week5``), there are two additional branches: ``recipe`` and
``conflict-recipe``:

**branches**

|br| The ``recipe`` branch is a **feature branch** that we are using to develop a recipe for spicy black bean soup,
contained in **recipe.txt**:

**changelog**

|br| And on the second branch, ``conflict-recipe``, we have the same file, but with some changes that have been added
by one of our collaborators, Bob\ [1]_:

**changelog**

This means that when we go to merge ``conflict-recipe`` into ``recipe``, we won't be able to do so automatically - the
two branches have a conflict that we will need to try to resolve.

creating the conflict
----------------------

Right now, we only have the "recipe" for a conflict\ [2]_ - in order to actually create the conflict, we have to
**merge** the conflicting branches.

You can do this in the exact same way that you merged the ``week2`` branch into ``main`` using **GitHub Desktop**.

First, make sure that you are currently on the ``recipe`` branch:

**recipe branch**

|br| Next, click on the **Branch** menu, then select **Merge into current branch...**. In the menu that opens, select
the local ``conflict-recipe`` branch:

**merging**

|br| This time, instead of a green checkmark indicating that there aren't any conflicts, you should see ...:

**conflict**

|br| Click on **{button}** to generate the conflict that we will resolve.

resolving the conflict
-----------------------

Once you have started the **merge conflict**, let's open the file to see what it looks like now - you can use a
**text editor** such as **Notepad** or **Notepad++**, or you can even use **PyCharm**.

We're looking for blocks of text like the following - this is how ``git`` indicates that there is a conflict between
two versions of a file:

.. code-block:: text

    <<<<<<< HEAD

    <some stuff>

    =======

    <some other stuff>

    >>>>>>> {other commit hash}

In order to resolve the conflict, we have to decide whether we want to:

1. keep only ``<some stuff>`` (the version on our currently active branch, ``recipe``);
2. keep only ``<some other stuff>`` (the version on the branch we're merging, ``conflict-recipe``);
3. keep some combination of ``<some stuff>`` and ``<some other stuff>``.

Most likely, you will end up deciding to use a combination of ``<some stuff>`` and ``<some other stuff>`` - in this
case, because the two versions of the file both contain changes that we're interested in keeping.

So, in your


merging the resolution
-----------------------

Now that we have edited the file so that the current version reflects how we want it to be, we're not quite done - we
need to finish the **merge**.

To do this, we first have to **add** the file to stage the changes:

Next, we **commit** the file:

And that's it - we have now successfully resolved the conflict between ``recipe`` and ``conflict-recipe``, and finished
developing a recipe for spicy black bean soup in the process.

next steps
-----------

Now that you have fully resolved the conflict by finishing the merge commit, you can go one further by merging
``recipe`` into ``main``.

Hopefully, there won't be any changes on ``recipe`` that conflict with ``main`` - this should be completely
straightforward, because the only file that has been changed is **recipe.txt**, which doesn't yet exist on ``main``.

To do this, you can merge ``recipe`` into ``main`` following the same procedure that you did at the beginning of the
:doc:`cartopy <cartopy>` exercise (remembering to use ``recipe`` instead of ``week2``).

notes
-------

.. [1] https://en.wikipedia.org/wiki/Alice_and_Bob

.. [2] yes, this was intentional. No, I am not sorry.