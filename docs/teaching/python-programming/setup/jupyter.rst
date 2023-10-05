configuring the jupyterlab terminal
=====================================

.. note::

    If you have taken the :doc:`R workshop <../../r-programming/index>`, you may not need to do this step - you can
    check by launching **Jupyter Lab**, then opening a **Terminal**.

    If you see a prompt that looks like the following:

    .. code-block:: text

        (intro-to-python) C:\Users\bob\github\intro-to-python>

    Then you have already changed the terminal from the default **PowerShell** to the **Command Prompt**, and you can
    move on to installing :doc:`PyCharm<pycharm>`.

If you are using Windows, we need to change the **terminal** from the default (**PowerShell**) to the **Command Prompt**
(**CMD.exe**). To begin, open the **Anaconda Command Prompt**, making sure that your ``intro-to-python`` environment is
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
(again, making sure that your ``intro-to-python`` environment is active):

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

|br| If you don't see a **Command Prompt** session with your ``intro-to-python`` environment activated, please let me
know and I will do my best to help troubleshoot.
