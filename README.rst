django-redis-sessions-fork
==========================

:info: Redis Session Backend For Django

.. image:: https://img.shields.io/travis/hellysmile/django-redis-sessions-fork.svg
    :target: https://travis-ci.org/hellysmile/django-redis-sessions-fork

.. image:: https://img.shields.io/coveralls/hellysmile/django-redis-sessions-fork.svg
    :target: https://coveralls.io/r/hellysmile/django-redis-sessions-fork

.. image:: https://img.shields.io/pypi/dm/django-redis-sessions-fork.svg
    :target: https://pypi.python.org/pypi/django-redis-sessions-fork

.. image:: https://img.shields.io/pypi/v/django-redis-sessions-fork.svg
    :target: https://pypi.python.org/pypi/django-redis-sessions-fork

Features
********

* Fast NoSQL Django sessions backend
* Invalidation via `TTL <http://redis.io/commands/ttl>`_
* Easy migrations from ``django.contrib.sessions``
* Fastest session serializers
* Backward migrations to ``django.contrib.sessions``

Installation
************

run ``pip install django-redis-sessions-fork``

or alternatively download the tarball and run ``python setup.py install``

set ``redis_sessions_fork.session`` as your session engine, like so

.. code-block:: python

    SESSION_ENGINE = 'redis_sessions_fork.session'

Configuration
*************

.. code-block:: python

    # all these options are defaults, you can skip anyone
    SESSION_REDIS_HOST = '127.0.0.1'
    SESSION_REDIS_PORT = 6379
    SESSION_REDIS_DB = 0
    SESSION_REDIS_PASSWORD = None
    SESSION_REDIS_PREFIX = None

    # if you prefer domain socket connection
    # you can just add this line instead of SESSION_REDIS_HOST and SESSION_REDIS_PORT
    SESSION_REDIS_UNIX_DOMAIN_SOCKET_PATH = '/var/run/redis/redis.sock'

    # you can also use redis from url
    SESSION_REDIS_URL = 'redis://127.0.0.1:6379/0'

    # also available setup connection via redis.ConnectionPool like
    SESSION_REDIS_CONNECTION_POOL = 'random.app.redis_connection_pool'

if you one of happy `heroku.com <http://heroku.com/>`_ users

you can skip redis configuration at all

``django-redis-sessions-fork`` already have prefiguration for redis clouds

Serializer's
************

Django>=1.5.3 `supports <https://docs.djangoproject.com/en/1.5/topics/http/sessions/#session-serialization>`_ different session serializers, such as ``django.contrib.sessions.serializers.PickleSerializer`` and ``django.contrib.sessions.serializers.JSONSerializer``

alternative you can use `ujson <https://github.com/esnme/ultrajson>`_ serializer, which is more faster then default

.. code-block:: console

    pip install ujson

then

.. code-block:: python

    SESSION_SERIALIZER = 'redis_sessions_fork.serializers.UjsonSerializer'

in addition it is possible to configure `ujson <https://github.com/esnme/ultrajson>`_ encoding, like

.. code-block:: python

    SESSION_REDIS_JSON_ENCODING = 'utf8' # default is 'latin-1'

Sessions migration
******************

add ``redis_sessions_fork`` to your ``INSTALLED_APPS``

.. code-block:: console

    # copy orm sessions to redis
    python manage.py migrate_sessions_to_redis
    # copy redis sessions to orm
    python manage.py migrate_sessions_to_orm
    # flush redis sessions
    python manage.py flush_redis_sessions
    # flush orm sessions
    python manage.py flush_orm_sessions

Tests
*****

.. code-block:: console

    pip install tox
    tox
