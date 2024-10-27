setup
======

The first half of this workshop, :doc:`shell/index`, provides an introduction the Unix shell using ``bash``. In order
to work through these exercises on your own computer, you will need to make sure that you have a ``bash`` interpreter
installed. Depending on your operating system, this may already be done - use the contents menu on the right side of
this page for more information/instructions.


windows
---------

If you are using a Windows computer, you will need to install a ``bash`` emulator (if you have not already done so), as
they are not installed by default.

You will only need to install **one** of the options listed below, though I very much recommend installing ``git``
independently of the fact that the Windows version ships with a ``bash`` interpreter.

.. note::

    You will need to have Administrator rights on your computer in order to install either WSL or ``git``.

windows subsystem for linux
.............................

Since Windows 10, Windows has included support for installing Linux distributions via the "Windows Subsystem for Linux"
(WSL). This enables you to use Linux applications and utilities, including ``bash``, directly through Windows without
the need for installing a virtual machine or dual-boot.

To install WSL, please see `the official installation guide <https://learn.microsoft.com/en-us/windows/wsl/install>`__
from Microsoft.

git bash
.........

If you are not interested in installing WSL, you can also install `git <https://git-scm.com/>`__, a distributed version
control system software. In addition to ``git``, the Windows installer will also install **Git Bash**, a ``bash``
emulator.

Click `here <https://git-scm.com/download/win>`__ to download ``git`` for Windows, then follow the instructions provided
by the installation wizard. You can also have a look :doc:`here <../egm722/setup/git>` for more detailed instructions.

mac os x
---------

If you are using a Mac, congratulations! You don't actually have to install anything new, because OS X already comes
with ``bash`` installed.

Since Catalina, however, the default shell used by ``Terminal`` has been ``zsh`` ("z shell"). To check what shell your
``Terminal`` runs by default, open it up - at the top of the window, you should see either ``-bash`` or ``-zsh`` next
to your username.

If you see ``-zsh``, you have three options, in increasing levels of difficulty:

1. Just run the commands as-is. Because ``zsh`` is built on ``bash``, almost all of the programs/commands are the same,
   meaning that you could just use the terminal as-is.
2. At the initial command prompt, type ``bash`` and press **Enter**. This will open the ``bash`` interpreter, allowing
   you to run the commands through ``bash`` rather than ``zsh``. Note that if you close the window, you will need to
   run the ``bash`` command again after re-opening it, in order to continue using ``bash``.
3. Change your default shell from ``zsh`` to ``bash``. See, for example,
   `this guide <https://www.howtogeek.com/444596/how-to-change-the-default-shell-to-bash-in-macos-catalina/>`__
   for more detailed instructions on how to do this.

linux
-------

If you have a computer that already has a linux distribution (or other \*nix variety) installed, you really don't need
to do anything. Just launch a ``Terminal`` window to get started. Though, you may want to check that your terminal is
running ``bash``, rather than another shell.

To do this, type the following at the prompt:

.. code-block:: sh

    echo $0

If you see ``bash`` printed below the prompt, congratulations! You're all set to get started.

If you do not see ``bash``, you can still change to ``bash`` by typing the following at the command prompt:

.. code-block:: sh

    bash

You will now be able to run all of the commands used in the exercises. If you close the terminal window, you'll need to
remember to run the ``bash`` command again.

You can also use the ``chsh`` command to change your default shell - for more detailed instructions on how to do this,
see `this guide <https://www.howtogeek.com/669835/how-to-change-your-default-shell-on-linux-with-chsh/>`__.
