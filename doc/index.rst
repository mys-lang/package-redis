|discord|_
|test|_
|stars|_

About
=====

A `Redis`_ client in the `Mys programming language`_.

Project: https://github.com/mys-lang/package-redis

Examples
========

String
------

.. code-block:: mys

   from redis import Client

   func main():
       client = Client()
       client.connect()
       client.set("my_key", b"my_value")
       print(client.get("my_key"))
       client.disconnect()

Build and run:

.. code-block:: myscon

   ❯ mys run
    ✔ Reading package configuration (0 seconds)
    ✔ Building (0.01 seconds)
   b"my_value"

List
----

.. code-block:: mys

   from redis import Client

   func main():
       client = Client()
       client.connect()
       client.lpush("bar", b"1")
       client.rpush("bar", b"2")
       print(client.lpop("bar"))
       print(client.rpop("bar"))
       client.disconnect()

Build and run:

.. code-block:: myscon

   ❯ mys run
    ✔ Reading package configuration (0 seconds)
    ✔ Building (0.01 seconds)
   b"1"
   b"2"

Hash
----

.. code-block:: mys

   from redis import Client

   func main():
       client = Client()
       client.connect()
       client.hset("fie", "a", b"x")
       client.hset("fie", "b", b"y")
       print(client.hget("fie", "a"))
       print(client.hgetall("fie"))
       client.hdel("fie", "a")
       print(client.hgetall("fie"))
       client.disconnect()

Build and run:

.. code-block:: myscon

   ❯ mys run
    ✔ Reading package configuration (0 seconds)
    ✔ Building (0.01 seconds)
   b"x"
   {"b": b"y", "c": b"z", "a": b"x"}
   {"b": b"y", "c": b"z"}

Publish
-------

.. code-block:: mys

   from redis import Client

   func main():
       client = Client()
       client.connect()
       client.publish("my_channel", b"my_payload")
       client.disconnect()

Build and run:

.. code-block:: myscon

   ❯ mys run
    ✔ Reading package configuration (0 seconds)
    ✔ Building (0.01 seconds)

Subscribe
---------

.. code-block:: mys

   from redis import Client
   from redis import PublishMessage
   from redis import SubscribeMessage
   from redis import UnsubscribeMessage

   func main():
       client = Client()
       client.connect()
       client.subscribe("my_channel")

       while True:
           match client.get_message():
               case PublishMessage() as publish_message:
                   print(publish_message)
               case SubscribeMessage() as subscribe_message:
                   print(subscribe_message)
               case UnsubscribeMessage() as unsubscribe_message:
                   print(unsubscribe_message)

Build and run, and publish ``hi`` on ``my_channel`` in another terminal:

.. code-block:: myscon

   ❯ mys run
    ✔ Reading package configuration (0 seconds)
    ✔ Building (0.01 seconds)
   SubscribeMessage(channel="my_channel", number_of_subscriptions=1)
   PublishMessage(channel="my_channel", payload=b"hi")

Pipeline
--------

Multiple commands in flight simultaniously.

.. code-block:: mys

   from redis import Client

   func main():
       client = Client()
       client.connect()
       client.set_write("foo", b"bar")
       client.get_write("foo")
       client.set_read()
       print(client.get_read())
       client.disconnect()

Build and run:

.. code-block:: myscon

   ❯ mys run
    ✔ Reading package configuration (0 seconds)
    ✔ Building (0.01 seconds)
   b"bar"

API
===

.. mysfile:: src/lib.mys

.. _Redis: https://redis.io

.. |discord| image:: https://img.shields.io/discord/777073391320170507?label=Discord&logo=discord&logoColor=white
.. _discord: https://discord.gg/GFDN7JvWKS

.. |test| image:: https://github.com/mys-lang/package-redis/actions/workflows/pythonpackage.yml/badge.svg
.. _test: https://github.com/mys-lang/package-redis/actions/workflows/pythonpackage.yml

.. |stars| image:: https://img.shields.io/github/stars/mys-lang/package-redis?style=social
.. _stars: https://github.com/mys-lang/package-redis

.. _Mys programming language: https://mys-lang.org
