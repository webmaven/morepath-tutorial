.. _tutorial-folders:

Step 1: Creating The Folder
============================

Before we get started, let's create the folders and files needed for this
application::

    /moreblog
        setup.py
        /moreblog
            __init__.py
            main.py
            model.py
            path.py
            view.py

The outer `moreblog` folder will not be a python package, but just somewhere we
drop our files. We will then put our actual package containing all of our code
into the inner `moreblog` folderfolder

As a first step, we need to list our dependencies and how to start the app in
``setup.py``:

.. code-block:: python

    from setuptools import setup, find_packages

    setup(name='moreblog',
        packages=find_packages(),
        install_requires=[
            'setuptools',
            'morepath',
            'transaction',
            'more.transaction',
            'zope.sqlalchemy >= 0.7.4',
            'sqlalchemy >= 0.9',
            'werkzeug',
            ],
        entry_points={
            'console_scripts': [
            'moreblog-start = moreblog.main:main'
            ]
        })

A few notes on the dependency packages: ``morepath`` specifies the latest
version (currently 0.9 at the time of this writing), ``transaction``,
``more.transaction``, ``zope.sqllchemy``, and ``sqlalchemy`` are all concerned
with database persistence, and ``werkzeug`` is the web server we'll be using
to run the app, chosen because it will auto refresh when files are edited
without requiring a restart.

``entry_points`` is defining a command that will start the app, in this case,
``moreblog-start``, when the package is installed.

Continue with :ref:`tutorial-schema`.

.. _Jinja2: http://jinja.pocoo.org/
