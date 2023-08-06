configuring jupyterlab
=======================

To be able to run **R** from JupyterLab, we have one final piece of configuration to do.

To begin, launch JupyterLab from either **Anaconda Navigator** or the **Anaconda Command Prompt** - in either case,
make sure that your ``intro-to-r`` environment is activated. You should see a browser window like this open up:

**jupyter opened**

If you don't see this exactly, don't worry. Click the blue **+** button in the upper left-hand corner of the window
to open the **Launcher**. Next, click on **R** under the **Console** heading (second one down), to open the
**R Console**:

**r console**

Finally, copy and paste (or type) the following into the console:

.. code-block:: r

    IRkernel::installspec()


