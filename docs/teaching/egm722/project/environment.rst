environment.yml
==================

One of the required elements for your repository is an ``environment.yml`` file, which can be used by
**conda** or other package management software to create an environment to run your project's code.

As an example, here is the ``environment.yml`` for the ``egm722`` environment, in its entirety:

.. code-block:: yaml

    name: egm722
    channels:
      - conda-forge
      - defaults
    dependencies:
      - python=3.8.8
      - geopandas=0.9.0
      - cartopy=0.18.0
      - notebook=6.2.0
      - rasterio=1.2.0
    prefix: C:\Users\e16006469\Anaconda3\envs\egm722

This shows that there are 5 listed **dependencies** (packages to install): 

- python (version 3.8.8)
- geopandas (version 0.9.0)
- cartopy (version 0.18.0)
- notebook (version 6.2.0)
- rasterio (version 1.2.0). 

To create your own ``environment.yml`` file, you'll need to open a *text* editor (**NOT** Microsoft Word). 

The easiest thing to do is to copy the text from above and adapt it to your specific project, starting with the
environment ``name``.

I recommend leaving the ``channels`` as-is, unless you add a dependency that is not available through 
either **conda-forge** or the **default** channels.

After that, add only those dependencies that you explicitly need to install, remembering that many of
those packages will have their own dependencies. 

You can choose whether to specify specific versions or not, though remember that this can sometimes make 
it more difficult to install dependencies. In general, it's probably safer to leave these off, unless there
are reasons for requiring a specific version -- if you're not sure, just ask.
