installing packages with pip
===============================

All of the packages that we will use in this module can be installed using ``conda``. However, in the course of
your programming project, and especially later on, you may come across packages that are not available through
any ``conda`` channels.

Most likely, if they are an officially distributed package of some sort, they will be available via the
`Python Package Index (PyPI) <https://pypi.org>`__, which means that they can be installed using a program called
``pip``.

To install a package using ``pip``, you should first install it into the ``conda`` environment you are working in, using
either **Anaconda Navigator** or the ``conda`` command line interface:

.. code-block:: text

    conda install -c conda-forge pip

Once ``pip`` is installed, open an **Anaconda Command Prompt**, activate the ``conda`` environment you
want to install the package into, and enter the following command:

.. code-block:: text

    pip install {package}

.. warning::

    Make sure that you have the correct environment activated! If you don't, ``pip`` will install the package into
    the ``base`` environment.

.. warning::

    Be sure to replace ``{package}`` with the `name of the package <https://www.youtube.com/watch?v=oh8iqi7u2Mc>`__
    that you want to install.

For more information on how to install packages using ``pip``, have a look at the
`official documentation <https://pip.pypa.io/en/stable/user_guide/>`__

It's also important to note that mixing ``pip`` and ``conda`` can cause issues with dependencies, so before you run
off to install everything using ``pip``, have a look at the following recommendations from the developers of ``conda``:

- https://www.anaconda.com/blog/using-pip-in-a-conda-environment
