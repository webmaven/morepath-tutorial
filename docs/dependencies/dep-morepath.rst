.. _dep-morepath-label:

morepath
--------------------

.. _dep-django-what-label:

What is ``Morepath``?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Morepath is a new web-development framework written in Python.



.. _dep-morepath-why-label:

Why do I need ``morepath``?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For building our blog application!  


.. _dep-morepath-how-label:

Get ``Morepath``!
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

We don't want to install Morepath system wide, but rather in our local
virtualenv. We're also going to install ``SQLAlchemy``, a library which will make it easier for us to use a database from our Morepath app later.

.. code-block:: bash

    $ pip install morepath
    $ pip install sqlalchemy

.. _morepath-verify-label:

Verify It Works!
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

    $ python
    >>> import morepath
    
To quit the python prompt do::

    exit()

.. _morepath-app-create-label:

Verify you can create a new Morepath app
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Create a ``hello.py`` file with the following code:

..  code-block:: python

    import morepath

    class App(morepath.App):
        pass

    @App.path(path='')
    class Root(object):
        pass

    @App.view(model=Root)
    def hello_world(self, request):
        return "Hello World!"

    if __name__ == '__main__':
        config = morepath.setup()
        config.scan()
        config.commit()
        morepath.run(App())

And run it:

.. code-block:: bash

    $ python hello.py


Output should look like this::

    Running <__main__.App object at 0x7fda6fe86990> with wsgiref.simple_server on http://127.0.0.1:5000
    
In your browser, go to http://127.0.0.1:5000/ 

You should see in the browser the text 'Hello World', and in your terminal window you should see something like:

.. code-block:: bash

    127.0.0.1 - - [30/Nov/2014 09:03:20] "GET / HTTP/1.1" 200 12
    127.0.0.1 - - [30/Nov/2014 09:03:20] "GET /favicon.ico HTTP/1.1" 404 154

In the Terminal window where you ran python main.py, 
type control-c to kill the server. 

Congratulations, you have run your first Morepath app!

How does this work?
^^^^^^^^^^^^^^^^^^^

We'll go into more detail as we develop our blogging app, but here is a quick
overview of what this code is doing:

.. code-block:: python

    import morepath

    class App(morepath.App):
        pass

We import ``morepath``, and then we create a subclass of :class:`morepath.App`.
This class contains our application's configuration: what models and views are
available.  It can also be instantiated into a WSGI application object.

.. code-block:: python

    @App.path(path='')
    class Root(object):
        pass

We then set up a ``Root`` class. Morepath is model-driven and in order to
create any views, we first need at least one model, in this case the empty
``Root`` class.

We set up the model as the root of the website (the empty string ``''``
indicates the root, but ``'/'`` works too) using the :meth:`morepath.App.path`
decorator.

.. code-block:: python

    @App.view(model=Root)
    def hello_world(self, request):
        return "Hello World!"

Now we can create the "Hello world" view. It's just a function that takes
``self`` and ``request`` as arguments (we don't need to use either in this
case), and returns the string ``"Hello World!"``. The ``self`` argument of a
view function is the instance of the ``model`` class that is being viewed.

We then need to hook up this view with the :meth:`morepath.App.view` decorator.
We say it's associated with the ``Root`` model. Since we supply no explicit
``name`` to the decorator, the function is the default view for the ``Root``
model on ``/``.

.. code-block:: python

    if __name__ == '__main__':
        config = morepath.setup()
        config.scan()
        config.commit()
        morepath.run(App())

The ``if __name__ == '__main__'`` section is a way in Python to make the code
only run if the ``hello.py`` module is started directly with Python as
discussed above.

:func:`morepath.setup` sets up Morepath's default behavior, and returns a
Morepath config object.

We then ``scan()`` this module (or package) for configuration decorators (such
as :meth:`morepath.App.path` and :meth:`morepath.App.view`) and cause them to
be registered using :meth:`morepath.Config.commit`.

This step ensures your configuration (model routes, views, etc) is loaded
exactly once in a way that's reusable and extensible.
