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

Publish
-------

.. code-block:: mys

   from redis import Client

   func main():
       client = Client()
       client.connect()
       client.publish("my_channel", b"my_payload")
       client.disconnect()

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
