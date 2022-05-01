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
      - python=3.9
      - geopandas
      - cartopy
      - notebook
      - rasterio
      - pyepsg

Below, I will walk through the different sections of the file to help explain what they are.


name
-----

The first line of the file tells **conda** what to call the new environment - in this example, the new environment will be
called ``egm722``. In your ``environment.yml`` file, you should change this to a name that fits with your project - don't
just re-use the ``egm722`` name!


channels
---------

The next heading is the **channels** heading, which tells **conda** where to look for packages.
Under the **channels** heading, you can see that we've added two channels, listed in order of preference:

- conda-forge
- defaults

This means that when we tell **conda** to install packages, it will first look on the **conda-forge** channel; if the
package is not available on that channel, it will look on the other default channels.


dependencies
-------------

Underneath the **channels** heading is the **dependencies** heading. This is where we tell **conda** what packages need
to be installed, and (optionally) what versions it should try to install.

.. warning::

    Be cautions when specifying version numbers. If you are overly specific with versions, it will make it more
    difficult for **conda** to install the environment.

In the example above, we see that there are 5 listed **dependencies** (packages to install):

- python (version 3.9)
- geopandas (any version)
- cartopy (any version)
- notebook (any version)
- rasterio (any version)
- pyepsg (any version)

This will create an environment with python version 3.9, and install the ``geopandas``, ``cartopy``, ``notebook``,
``rasterio``, and ``pyepsg`` packages.

This list might seem quite short - for example, you will have noticed in the practicals that we use a number of
packages that aren't named here. This is because when **conda** installs these packages, it will also install any
and all dependencies for those packages - we don't need to explicitly list every single package that needs to be
installed in order for those packages to also be installed.

In addition to specifying a specific version (``python=3.9``), we could also specify a range of versions. For example,
we could tell **conda** to create an environment with a python version greater than 3.5 like this:

.. code-block:: yaml

    - python>3.5

For more explanation for how to specify versions, or version ranges, see
`the conda documentation <https://docs.conda.io/projects/conda-build/en/latest/resources/package-spec.html#package-match-specifications>`__.

creating your own file
-----------------------

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
