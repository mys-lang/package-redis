About
=====

A `Redis`_ client in the `Mys programming language`_.

Project: https://github.com/mys-lang/package-redis

Examples
========

Set and get
-----------

.. code-block:: mys

   from redis import Client

   func main():
       client = Client()
       client.connect()
       client.set_string("my_key", "my_value")
       print(client.get_string("my_key"))
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

.. _Mys programming language: https://mys-lang.org
