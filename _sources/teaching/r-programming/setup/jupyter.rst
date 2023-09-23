configuring jupyterlab
=======================

To be able to run **R** from JupyterLab, we have one (possibly two) final pieces of configuration to do.


changing the terminal (windows only)
-------------------------------------

If you are using Windows, we need to change the **terminal** from the default (**PowerShell**) to the **Command Prompt**
(**CMD.exe**). To begin, open the **Anaconda Command Prompt**, making sure that your ``intro-to-r`` environment is
activated.

At the command prompt, enter the following command:

.. code-block:: text

    jupyter lab --generate-config

You should see something like the following:

.. image:: img/generate_config.png
    :width: 600
    :align: center
    :alt: the command prompt, showing that the jupyter lab config file is being written

|br| Next, open the file (it should be located at ``%HOME%\.jupyter\jupyter_lab_config.py``, but check the output in
the command prompt) in **Notepad++** or a similar text editor, and search for ``c.ServerApp.terminado_settings``
(for me, this was at line 1062):

.. image:: img/jupyter_settings.png
    :width: 600
    :align: center
    :alt: the jupyter config file, showing the terminal setting

|br| Inside of the curly brackets, add the following text:

.. code-block:: python

    'shell_command': [r'C:\WINDOWS\System32\cmd.exe']

.. image:: img/jupyter_settings_updated.png
    :width: 600
    :align: center
    :alt: the jupyter config file, showing the updated terminal setting

|br|

.. note::

    **CMD.exe** is, by default, located at ``%windir%\system32\cmd.exe``. To double-check that your ``%windir%``
    location is, in fact, ``C:\WINDOWS``, you can type ``echo %windir%`` at the command prompt, and use the location
    printed out from that command.

Once you have changed the file, save the changes, then close it. Now, launch **JupyterLab** from the command prompt
(again, making sure that your ``intro-to-r`` environment is active):

.. code-block:: text

    jupyter lab

You should see a browser window like this open up:

.. image:: img/jupyterlab_open.png
    :width: 720
    :align: center
    :alt: jupyterlab open in a browser window

|br| If you don't see this exactly, don't worry. Click the blue **+** button in the upper left-hand corner of the window
to open the **Launcher**.

Next, click on **Terminal** under **Other** to launch a terminal window. You should see something like this:

.. image:: img/jupyter_terminal.png
    :width: 720
    :align: center
    :alt: jupyterlab open in a browser window, with a terminal window opened

|br| If you don't see a **Command Prompt** session with your ``intro-to-r`` environment activated, please let me know
and I will do my best to help troubleshoot.

using **R**
-------------

To check that **JupyterLab** is configured to run **R**, first launch **JupyterLab** from the
**Anaconda Command Prompt**, making sure that your ``intro-to-r`` environment is activated:

.. code-block:: text

    jupyter lab

You should see a browser window like this open up:

.. image:: img/jupyterlab_open.png
    :width: 720
    :align: center
    :alt: jupyterlab open in a browser window

|br|

.. note::

    If you don't see this exactly, don't worry. Click the blue **+** button in the upper left-hand corner of the window
    to open the **Launcher**.

Next, click on **R** under the **Console** heading (second one down), to open the **R Console**:

.. image:: img/r_console.png
    :width: 720
    :align: center
    :alt: jupyterlab open in a browser window

|br|

If you see ``R | Idle`` in the lower left-hand corner, as in the screenshot above, congratulations! You don't need to
do anything further.

If, however, you don't see this, go ahead and shut down JupyterLab (**File** > **Shutdown**). In your **Command Prompt**
window, open the **R** terminal by typing ``R`` at the prompt and pressing **Enter**.

Finally, copy and paste (or type) the following into the console, which will tell Jupyter about the **R** kernel:

.. code-block:: r

    IRkernel::installspec()

When this finishes, type ``q()`` and press enter to quit **R**.

To check that this has worked, re-launch JupyterLab and open the **R** console - you should now see that **R** is
connected to JupyterLab, as in the screenshot above.
