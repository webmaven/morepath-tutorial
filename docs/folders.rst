.. _tutorial-folders:

Step 1: Creating The Folders
============================

Before we get started, let's create the folders needed for this
application::

    /moreblog

The `moreblog` folder is not a python package, but just something where we
drop our files. We will then put our database schema as well as main module
into this folder. It is done in the following way. The files inside
the `static` folder are available to users of the application via `HTTP`.
This is the place where css and javascript files go.  Inside the
`templates` folder Flask will look for `Jinja2`_ templates.  The
templates you create later in the tutorial will go in this directory.

Continue with :ref:`tutorial-schema`.

.. _Jinja2: http://jinja.pocoo.org/
