.. _tutorial-schema:

Step 2: Adding the DB Schema
============================

In ``model.py`` add the following code:

.. code-block:: python

    from sqlalchemy import (
        Column,
        Integer,
        Text,
        DateTime,
        ForeignKey,
        )
    from sqlalchemy.ext.declarative import declarative_base

    Base = declarative_base()

    class Post(Base):
        __tablename__ = 'post'

        id = Column(Integer, primary_key=True)
        title = Column(Text)
        content = Column(Text)

In this code, we are importing from `SQLAlchemy`_, a popular Python ORM, and
then creating a table-based model class (As well see later though, Morepath
models need not be based on a database, and can be almost any sort of object).

In our app, blog posts are very simple, and have an id, a title, and some content.

Next, in ``main.py``, add the following .. code:

.. code-block:: python

    import morepath
    import sqlalchemy
    from more.transaction import transaction_app
    from sqlalchemy.orm import scoped_session, sessionmaker
    from zope.sqlalchemy import register

    from werkzeug.serving import run_simple

    from . import model

    Session = scoped_session(sessionmaker())
    register(Session)

    class App(morepath.App):
        pass

    def main():
        engine = sqlalchemy.create_engine('sqlite:///morepath_sqlalchemy.db')
        Session.configure(bind=engine)
        model.Base.metadata.create_all(engine)
        model.Base.metadata.bind = engine

        morepath.autosetup()
        run_simple('localhost', 8080, App(), use_reloader=True)

With this code, we are setting up the app to be run from the console script, making
sure that the app has a database session, and also instantiatiating the database and
table for storing the blog posts.

.. _SQLAlchemy:
    http://sqlalchemy.org
