# RabbitMQ Integration Pack

Pack which allows integration with [RabbitMQ](http://www.rabbitmq.com/).

## Actions

* ``list_exchanges`` - List available exchanges.
* ``list_queues`` - List available queues.

Note: All of the actions invoke ``rabbitmqadmin`` tool and must run on the
same node where RabbitMQ server is running (they connect to the local 
instance).


## Sensors

* ``new_message`` - Sensor that triggers a rabbitmq.new_message with a payload containing the queue and the body

This sensor should only be used with ``fanout`` and ``topic`` exchanges,  this way it doesn't affect the behavior of the app since messages will still be delivered to other consumers / subscribers.
If it's used with ``direct`` or ``headers`` exchanges, those messages won't be delivered to other consumers so it will affect app behavior and potentially break it.

## Sensors Config

* ``host`` - RabbitMQ host to connect to
* ``user`` - User to connect to RabbitMQ
* ``password`` - Password to connect to RabbitMQ
* ``queues`` - Yaml list of queues to check for messages, like this:
```
sensor_config:
  poll_time: 5
  queues:
    - queue1
    - queue2
    - ....
```