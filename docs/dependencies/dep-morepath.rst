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

Create a ``main.py`` file in the ``/morepath`` directory with the following code:

..  code-block:: python

    import morepath

    class App(morepath.App):
        pass

    @App.path(path='')
    class Root(object):
        pass

    @App.view(model=Root)
    def hello_world(self, request):
        return "Hello world!"

    if __name__ == '__main__':
        config = morepath.setup()
        config.scan()
        config.commit()
        morepath.run(App())

And run it:

.. code-block:: bash

    $ python main.py
    Running <morepath.App 'Hello'> with wsgiref.simple_server on http://127.0.0.1:5000

Output should look like this::

    stuff

In your browser, go to http://127.0.0.1:8000/ 

In your Terminal window you should see something like:

.. code-block:: bash

    [19/Mar/2011 19:19:26] "GET / HTTP/1.1" 200 2057

Back in the Terminal window where you ran python main.py, 
type control-c to kill the server. 

Congratulations, you have run your first Morepath app!
