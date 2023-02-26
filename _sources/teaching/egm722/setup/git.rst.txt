installing git
===============

.. warning::

    The images/instructions below are for git version 2.30.1. There may be some small differences between the steps
    between that version, and the version that you download.

To install **git** (if you do not already have it installed, of course), first head to https://git-scm.com/downloads. 
Choose the version for your operating system, and download the installer.

The next instructions and images are for the Windows operating system; I am happy to provide additional instructions
for other operating systems, if needed.

After reading & accepting the license terms, install **git** to the default location:

.. image:: ../../../img/egm722/setup/git/install_location.png
    :width: 500
    :align: center
    :alt: selecting the location to install git

|br| Next, leave the selected components as-is:

.. image:: ../../../img/egm722/setup/git/selected_components.png
    :width: 500
    :align: center
    :alt: selecting the components to install

|br| Be sure to change the default editor from **vim** to something else (**vim** is
`somewhat notoriously confusing <https://imgur.com/v3uSDVk>`__ to use if you are not familiar with it). 
On Windows, I like `Notepad++ <https://notepad-plus-plus.org/downloads/>`__ but you may not already have 
this installed; in that case, change this to **Notepad**.

.. image:: ../../../img/egm722/setup/git/default_editor.png
    :width: 500
    :align: center
    :alt: selecting the default editor

|br| This step is optional, but as a result of
`recent discussions around the use of language <https://github.com/github/renaming>`__,
the default starting branch name for **git** will be changing from **master** to **main** in the near 
future, and **git** now gives you the option of choosing a different name in the meantime:

.. image:: ../../../img/egm722/setup/git/default_branch.png
    :width: 500
    :align: center
    :alt: changing the default branch name to main

|br| In addition to the graphical user interface (GUI) that we will install next, **git** can also be used as a command
line tool. **git** will install its own terminal (command line) emulator, but we can also configure it to work from
the Windows command prompt, and with third-party software such as an integrated development environment (IDE).

Many IDEs (such as PyCharm or Microsoft Visual Studio) come with built-in support for **git**, which can be extremely
useful when programming. To enable this, make sure to select the middle (**Recommended**) option below:

.. image:: ../../../img/egm722/setup/git/path.png
    :width: 500
    :align: center
    :alt: selecting how to use git in windows

|br| Keep the HTTPS transport backend using OpenSSL library, then click **Next**. Windows uses a different character
encoding to represent a `newline <https://en.wikipedia.org/wiki/Newline#Representation>`__ in text files compared to
Unix-style systems (e.g., Unix, Linux, macOS), which can cause problems when switching between them. To help smooth
things a bit, **git** provides the option to convert newline characters when checking out and committing files. I
recommend leaving this setting as is:

.. image:: ../../../img/egm722/setup/git/newline.png
    :width: 500
    :align: center
    :alt: selecting how to treat newline characters

|br| Git will also install a terminal (command line) emulator called **git** Bash, which enables you to use some
command-line tools that Windows does not include by default. Make sure the first option (**Use MinTTY**) is selected,
then click **Next**:

.. image:: ../../../img/egm722/setup/git/terminal_emulator.png
    :width: 500
    :align: center
    :alt: selecting which terminal emulator to use

|br| Git will also ask how you want **git pull** to behave – I recommend keeping the default setting here as well:

.. image:: ../../../img/egm722/setup/git/git_pull.png
    :width: 500
    :align: center
    :alt: selecting the default behavior for git pull

|br| Finally, you can leave the remaining options (choosing a credential helper, configuring extra options) as-is,
clicking **Next** each time. When you come to the final window, you should see an **Install** button:

.. image:: ../../../img/egm722/setup/git/install.png
    :width: 500
    :align: center
    :alt: the final installation wizard window

|br| Once **git** is installed, open a command prompt window. Type ``where git`` at the command prompt and press
**Enter**. You should see the following output:

.. image:: ../../../img/egm722/setup/git/success.png
    :width: 500
    :align: center
    :alt: a terminal window showing that git has successfully installed

|br| If you see an error message, post in the Discussion Forum and ask for help. If there are no errors, you can move
on to the next step.
