introduction to version control using git
==========================================

In this exercise, we'll get some practice using the **git** command-line interface for keeping track of the contents
of a folder.

navigating the command prompt
-------------------------------

To start, open the **Anaconda Command Prompt** for your ``intro-to-python`` environment.

.. note::

    These instructions assume that you are working from a **Windows** environment. If you are working on a different
    operating system (e.g., MacOS, ChromeOS, Linux), the instructions will be more or less the same, though some of the
    commands may differ slightly, and the name of the program you use will be different.

    For example, instead of the **Anaconda Command Prompt**, you should open a **Terminal**


You should start in your ``%HOME%`` directory (e.g., ``C:\Users\<your username>``)\ [#]_. At the command prompt, you can
see what directory you are currently in by looking at the text before the ``>`` symbol:

.. code-block:: text

    (intro-to-r) C:\Users\bob>

In the example above, ``(intro-to-python)`` tells me that I am currently using my ``intro-to-python`` conda environment,
while ``C:\Users\bob`` tells me that I am in my ``%HOME%`` folder (assuming that my username is ``bob``, that is).

When I *cloned* the workshop repository to my computer, I cloned it into a folder located in my ``%HOME%`` directory -
that is, the **absolute** path of the folder is:

.. code-block:: text

    C:\Users\bob\intro-to-python

If I want to navigate into this folder, I can use the **cd** command ("change directory"), along with the
**absolute** path, to do so:

.. code-block:: text

    cd C:\Users\bob\intro-to-python

If you run this command, replacing the path with whatever it is on your own computer, you should see that your
current directory changes to that folder:

.. image:: img/git/cd_absolute_path.png
    :width: 600
    :align: center
    :alt: the result of using the cd command

|br| You could also use a **relative** path - because I am already located in my ``%HOME%`` directory, I can also omit
this from the path, leaving just ``intro-to-python``:

.. code-block:: text

    cd intro-to-python

To see the contents of the directory, we can use the **dir** command\ [#]_:

.. code-block:: text

    dir

This will list all of the files and folders located within the current directory:

.. image:: img/git/dir_output.png
    :width: 600
    :align: center
    :alt: the result of using the dir command

|br| Now, use **cd** once again to navigate to the **01.git-intro** folder located within the repository:

.. code-block:: text

    cd 01.git-intro

and use the **dir** command again to view the contents of the folder - you should see two files, **ingredients.txt** and
**instructions.txt**, both with a size of 0 bytes - these are completely empty text files, that we will need to fill
up with our recipe ingredients and instructions.

creating a new branch
-----------------------

Before we do that, though, we'll create a new *branch* to our repository - this way, we can work on developing our
recipe without causing any problems with the ``main`` branch.

For this, we'll use the **git checkout** command, along with the **-b** flag:

.. code-block:: text

    git checkout -b <branch name>

Let's call the new branch ``recipe``, so the full command will be:

.. code-block:: text

    git checkout -b recipe

You should see the following message output:

.. image:: img/git/new_branch.png
    :width: 600
    :align: center
    :alt: checking out a new branch using git checkout

|br| And that's it. We can check what branches **git** is currently keeping track of using the **git branch** command:

.. image:: img/git/git_branch.png
    :width: 600
    :align: center
    :alt: the output of git branch in the command prompt

|br| Here, we have two branches: ``main``, the default/main branch of the repository, and ``recipe``, the new branch
that we just checked out. We can tell what branch we are currently working on by the color (green), as well as the
asterisk (``*``) to the left of the branch name.

editing the recipe
-------------------

Now that we have our new branch, let's make some changes to our files. First, open **ingredients.txt** in a text editor
(**Notepad**, **Notepad++**, or something similar, **NOT** MS Word!):


In this file, let's add the following ingredients:

.. code-block:: text

    1 T olive oil
    1 onion
    1 stalk celery
    2 carrots
    4 cloves garlic
    2 T chili powder
    1 T ground cumin
    1 pinch black pepper
    4 cups vegetable broth
    4 cups black beans
    1 can whole peeled tomatoes
    1 cup sweetcorn

Save the file (**CTRL** + **S**), but don't close the window just yet.

git status
------------

Back in the **Anaconda Command Prompt** window, let's see how we can use **git** to check the status of the files in
our repository, using **git status**:

.. code-block:: text

    git status

You should see something like this:

.. image:: img/git/status_modified.png
    :width: 600
    :align: center
    :alt: git status showing that one file has been modified

|br| This tells us the following information:

- we are currently on the ``recipe`` branch
- there are changes to the **ingredients.txt** file that have not been saved.

git diff
---------

If we want to see what changes, specifically, have been made, we can use **git diff**:

.. code-block:: text

    git diff

By itself, this tells us the changes that have been made to **all** files:

.. image:: img/git/git_diff.png
    :width: 600
    :align: center
    :alt: git diff showing that one file has been modified, with 12 lines added

|br| The very first line of the output:

.. code-block:: text

    diff --git a/01.git-intro/ingredients.txt b/01.git-intro/ingredients.txt

Tells us that we're looking at 2 versions of the same file: the old version (``a``), and the new version (``b``).

We'll ignore the next line for now, but the next two lines:

.. code-block:: text

    --- a/01.git-intro/ingredients.txt
    +++ b/01.git-intro/ingredients.txt

Tell us that the minus sign in the diff markup corresponds to the old version, while the plus sign corresponds to the
new version.

Next, this:

.. code-block:: text

    @@ -0,0 +1,12 @@

Tells us what the chunks of the files that **git diff** is showing. On the left, ``-0, 0`` means that we're seeing the
old version of the file starting at line 0, and the chunk is 0 lines long. On the right, ``+1,12`` means that we're
seeing the new version of the file starting at line 1, and the chunk is 12 lines long.

Next, we can see the actual changes: a ``+`` (typically colored green) at the start of the line indicates that this
line is in the new file, while a ``-`` (typically colored red) indicates that the line is in the old file.

Because the original version of the file is blank, all we should see here are additions - the same lines that we just
added to **ingredients.txt**.

staging changes
----------------

Now that we've added our ingredients, let's get ready to commit the changes. Remember that this is a two step process:
first, we have to *stage* our commits, using **git add**.

To stage **ingredients.txt**, enter the following command:

.. code-block:: text

    git add ingredients.txt

If we use **git status** again, we should see that we have changes "to be committed" for one file:

.. image:: img/git/git_add.png
    :width: 600
    :align: center
    :alt: git add showing that changes are to be committed

|br|

committing snapshots
---------------------

At this point, let's tell **git** to take a snapshot of our progress, using **git commit**.

For short commit messages, we can use this command with the **-m** flag:

.. code-block:: text

    git commit -m "this is a commit message"

Remember that we want our commit messages to:

- be short - we don't need to write pages and pages about what changes have been made;
- explain what was changed. For a longer commit message, this happens in the *title*; for shorter commit messages,
  such as those written using **git commit -m**, the title is the commit message;
- explain why something was changed. For a longer commit message, this happens in the *body*; for shorter commit
  messages, this happens in the title.

We should also be specific - remember that you are writing these for "*future you*" as much as for anyone else, so try
to write something that will still be clear to you several years from now!

In this commit, we have added a number of ingredients to our recipe, so a good commit message might say this:

.. code-block:: text

    git commit -m "add ingredients for spicy black bean soup"

As soon as you press **ENTER**, you should see the following message:

.. image:: img/git/git_commit.png
    :width: 600
    :align: center
    :alt: the output of git commit in the command prompt window

|br| This shows us the *branch* (``recipe``), as well as the **hash** corresponding to the commit; it also shows us
the commit message (or *title* for a longer commit message); it also tells us how many files have been changed, and how
many lines were changed and how.

Now, run **git status** again to see the current state of the working directory:

.. image:: img/git/status_commit.png
    :width: 600
    :align: center
    :alt: git status showing a clean working directory

adding instructions
---------------------

Now that we've added ingredients, we should also make sure to include instructions for our recipe. Open up
**instructions.txt** file (again, using a **text** editor!), and add the following instructions:

.. code-block:: text

    1. Chop onion, celery, carrots, and garlic.
    2. Heat oil in a large pot over medium-high heat.
    3. Saute onion, celery, and carrots for 5 minutes until soft, then add garlic. Stir for 1 minute.
    4. Season with chili powder, cumin, and pepper; cook for 1 additional minute.
    5. Stir in broth, 2 cups of beans, tomatoes, and corn; bring to a boil.
    6. Blend remaining beans until smooth, then stir into soup.
    7. Reduce heat to medium, and simmer for 15 additional minutes.

Now, stage these changes using **git add**:

.. code-block:: text

    git add instructions.txt

and commit the changes using **git commit**:

.. code-block:: text

    git commit -m "add instructions for cooking spicy black bean soup"


git log
--------

One way that we can keep track of the history of our repository is using **git log**, which allows us to scroll through
all of the different snapshots:

.. code-block:: text

    git log

.. image:: img/git/git_log.png
    :width: 600
    :align: center
    :alt: git log, showing the change history for the current repository

|br| This shows the commit history of the project in reverse chronological order, starting with the most recent. You
can see, for example, that the commit to add instructions for cooking the soup are at the top, showing the full *hash*
of the commit, the author of the commit, the date and time, and the title of the commit message.

You can also see this at the top:

.. code-block:: text

    (HEAD -> recipe)

We won't worry too much about what this means right now, but effectively ``HEAD`` means "the currently checked out
commit in the working directory"; it also tells us that the current branch checked out is ``recipe``. Whenever you add
a new commit, you see that ``HEAD`` updates to point to this most recent commit.

Further down, you can see this:

.. code-block:: text

    (origin/main, origin/HEAD, main)

This is the most recent commit on the local ``main`` branch, as well as the most recent commit in the remote repository
(``origin``).

If you want to see what files were changed with each commit, you can use **--stat**:

.. code-block:: text

    git log --stat

.. image:: img/git/git_log_stat.png
    :width: 600
    :align: center
    :alt: git log showing the change history of the current repository, including the files changed with each commit


customizing the recipe
-----------------------

Now that you have worked through some of the basics of using **git** to keep track of the files, it's time to spend
some time working on customizing and perfecting your soup recipe. For example, you might:

- decide that 2T of chili powder is far too much (or not nearly enough);
- want to add additional herbs or spices, such as ground coriander, oregano, or epazote;
- want to make it clear to use cooked beans (clarity is important!)

Whatever changes you make, remember to stage and commit them as we have practiced. Make sure that you also have a look
at tools like **git diff** and **git log** as you go, so that you see how things change as you continue to update
the files in the repository.

merging branches
-----------------

Once you have finished perfecting your soup recipe, it's time to combine this branch with the ``main`` branch. To do
this, you can first check out the ``main``:

.. code-block:: text

    git checkout main

Once you are back on the ``main`` branch, you can **merge** (combine) the two branches using **git merge**:

.. code-block:: text

    git merge recipe

This will update the current branch (``main``) with all of the changes committed to the ``recipe`` branch. You should
see something like the following output:

.. image:: img/git/git_merge.png
    :width: 600
    :align: center
    :alt: the output of a merge commit, showing that two branches have been merged

|br| Once all of the changes from a branch have been merged into ``main``, it can be a good idea to delete that branch,
to help keep the "tree" nicely pruned:

.. code-block::

    git branch -d recipe

notes
------

.. [#] In MacOS, it will most likely be ``/Users/<your username>``, and on Linux (including ChromeOS), it will most
  likely be ``/home/<your username>``.

.. [#] In MacOS/ChromeOS/Linux, use **ls** to "list" the contents of the directory, instead of **dir**

next steps
-----------

That's all for this lesson. If you are interested in continuing learning how to use the **git** command-line interface,
`learn git branching <https://learngitbranching.js.org/>`__ has a number of interactive exercises to help you practice
and develop your skills.

If you're not sure that the command line is for you, that's okay! You can download
`GitHub Desktop <https://desktop.github.com/>`__ (Windows and MacOS only), which provides a graphical user interface
for **git**.
