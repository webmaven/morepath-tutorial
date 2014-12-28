Morepath By Example
===================

|docs|

Purpose
-------

A short tutorial, suitable for beginners. See the `online version`_.


Instructions to build docs
--------------------------
To build your own doc for an offline use, just follow the next steps:


Download the project
####################
You'll need to retrieve the code before being able to build the documentation.
Assuming you have git installed, just type inside your terminal::

      $ git clone https://github.com/webmaven/morepath-tutorial.git


Install and activate a virtual environnement
############################################
`Virtualenv`_ will help you creates Python installations that doesn’t share libraries either with the globally installed packages, either with the other virtual environments. Let's create a virtual environment that will be used only for installing packages needed to build the morepath documentation, just type inside your terminal::

      $ virtualenv morepath_docs_env


You've just created an isolated Python environment under the morepath_docs_env folder.


Install requirements
####################
We will install some dependencies before being able to build morepath documentation. First, let's activate our virtual environment, that way, every installation will be made inside morepatch_docs_env folder. Just type inside your terminal::

      $ source morepath_docs_env/bin/activate


The virtualenv should stay active for all the following steps. After activating a virtualenv, the prompt of your terminal should be different, notice the ``(morepath_docs_env)`` for example, my prompt is now like this::

      (morepath_docs_env)lemeteore@localhost:~$

Then, go to the root of the morepath project::

      $ cd your/path/to/morepath-tutorial


And install the requirements using `pip`_ ::

      $ pip install -r docs_requirements.txt

All the python packages we need to build the documentation are listed inside the docs_requirements.txt file. Pip is able to read this file, an install the packages listed inside.

If everything went well, you should read this message ``Successfully installed sphinx Jinja2 Pygments docutils sphinx-bootstrap-theme markupsafe Cleaning up...``. Otherwise, you may have done something wrong.



Build html documentation
########################
To build the html documentation, just go to into the docs folder::

      $ cd docs

Then build the html documentation::

     $ make html


All the html pages will be generated and available under the _build/html/ folder.


Build pdf documentation
#######################
To build a pdf documentation, make sure to have pdf & latex related packages installed in your operating system. To install those under Debian Wheezy, just type inside your terminal::

      $ sudo aptitude install build-essential python-dev texlive-full


This is probably not the best way to do, as there is not an implicit need of all the packages that will be installed. After this install, you'll have the necessary packages to build a pdf documentation. Normally, you are still inside the docs folder. Just type in your terminal::

      $ make latexpdf

Everything should be available under the _build/latex directory.

License
#######
The MIT License (MIT) Copyright (c) 2014 Michael R. Bernstein


.. _online version:
   http://morepath-tutorial.readthedocs.org/en/latest/

.. |docs| image:: https://readthedocs.org/projects/morepath-tutorial/badge/?version=latest
    :alt: Documentation Status
    :scale: 100%
    :target: https://readthedocs.org/projects/morepath-tutorial/

.. _Virtualenv:
   http://virtualenv.readthedocs.org/en/latest/index.html

.. _pip:
   http://pip.readthedocs.org/en/latest/quickstart.html
