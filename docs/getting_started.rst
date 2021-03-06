Getting Started
===============

PyFilesystem is a Python-only module and can be installed from source or with `pip <http://www.pip-installer.org/>`_. PyFilesystem works on Linux, Mac and OSX.

Installing
----------

To install with pip, use the following::

	pip install fs

Or to upgrade to the most recent version::

	pip install fs --upgrade

You can also install the cutting edge release by checking out the source via GIT::

    git clone https://github.com/PyFilesystem/pyfilesystem.git pyfilesystem-read-only
    cd pyfilesystem-read-only
    python setup.py install

Whichever method you use, you should now have the `fs` module on your path (version number may vary)::

    >>> import fs
    >>> fs.__version__
    '0.5.0'

You should also have the command line applications installed. If you enter the following in the command line, you should see a tree display of the current working directory::

    fstree -l 2

Because the command line utilities use PyFilesystem, they also work with any of the supported filesystems. For example::

    fstree ftp://ftp.mozilla.org -l 2

See :doc:`commands` for more information on the command line applications.

Prerequisites
-------------

PyFilesystem requires at least **Python 2.6**. There are a few other dependencies if you want to use some of the more advanced filesystem interfaces, but for basic use all that is needed is the Python standard library.

    * Boto (required for :mod:`fs.s3fs`) https://github.com/boto/boto
    * Paramiko (required for :class:`fs.ftpfs.FTPFS`) http://www.lag.net/paramiko/
    * wxPython (required for :mod:`fs.browsewin`) http://www.wxpython.org/


Quick Examples
--------------

Before you dive in to the API documentation, here are a few interesting things you can do with PyFilesystem.

The following will list all the files in your home directory::

    >>> from fs.osfs import OSFS
    >>> home_fs = OSFS('~/') # 'c:\Users\<login name>' on Windows
    >>> home_fs.listdir()

Here's how to browse your home folder with a graphical interface::

	>>> home_fs.browse()

This will display the total number of bytes store in '.py' files your home directory::

    >>> sum(home_fs.getsize(f) for f in home_fs.walkfiles(wildcard='*.py'))
