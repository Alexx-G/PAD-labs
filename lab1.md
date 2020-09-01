# Messaging agents / Message brokers

Messaging agents are the key for decoupling communication between different components in distributed systems.
This lab has 2 parts:
- [Implement a (simple) message broker](#part-1)
- [Use \*RPC as broker's API](#part-2)

# Prerequisites

- Git;
- Concurrency primitives and thread-safe collections;
- Network programming:
    - OSI Model;
    - Network and Transport protocols;
- Data representation and serialization/deserialization;
- Basic understanding of communication protocols and APIs;

# Part 1

Implement a message broker that will decouple communication between different project components.
Use TCP or UDP as transport and any serialization format (preferable XML or JSON).

## Objectives

- Define a communication protocol/API for the message broker;
- Use [BSD Sockets](https://en.wikipedia.org/wiki/Berkeley_sockets), or the closest implementation in the language you've chosen, for data transport;
- Use thread-safe collections to store messages in the broker to allow MPMC (multiple producers, multiple consumers) or SPMC (single producer, multiple consumers) communication;

## Tasks

The first task is required and you must implement it in order to pass the lab. Each of the following tasks will add `+1` to your grade. Some tasks may have "bonus points".

- [**Mandatory** - Implement a simple message broker](#mandatory---implement-a-simple-message-broker)
- [Pub/Sub pattern](#implement-pubsub-pattern)
- [Message Persistence](#implement-message-persistence)
- [Last will and testament](#implement-last-will-and-testament)

### Mandatory - implement a simple message broker

A minimal requirement for this lab is to build a simple message broker that allows to route a message from consumer to producer via a message queue, explicitly specified by both consumers and producers.
Implementing this task allows allows you to pass this lab and get grade 5 or 6.
While this architecture is quite simple, it already allows to decouple communication between different components using broker and its routing.

**Workflow example:**
0. The message broker is up and running;
1. A producer - P1, sends a few messages (M1, M2, M3) to the queue Q1;
2. A consumer - C1, polls a message from the queue Q1 and receives the message M1;
3. Another consumer - C2, connects to the broker, polls a message from the queue Q1 and receives the message M2;

You might *assume* the following:
- Both consumer and producer **know** broker's address, no need for service discovery;
- Queue list is dynamic and a queue is created when a consumer connects to the broker;
- Only one producer can send messages to a queue;
- A consumer can poll for one message at a time;
- There might be more than 1 consumers polling the same queue at the same time. Thus, the message broker must be able to work with multiple connection. Implementation is up to you (either thread per connection, non-blocking IO etc).

**Requirements:**
- Define broker's communication protocol. It must be documented and included in the report;
  - The protocol must define message structure - meta-info fields (e.g. queue name, sender ID etc) and payload;
  - Payload must not be altered in any way by the broker;
- Choose a transport protocol and use Sockets for data transport;
- Producers must specify the queue messages will be sent to;
- Consumers have to specify the queue as well in order to poll/read a message;
- Consumers read messages using polling mechanism;

> **Message polling**
> 
> Message polling mechanism implies that consumers actively check broker status to see whether there are any new messages.

**Bonus point:**
- Implement MPMC (multiple producers, multiple consumers) per queue, that allows multiple producers to sends message to the same queue;

![Message queue](images/lab1-message-queue.gif)

### Implement Pub/Sub pattern

So far consumers were polling message broker to get new messages.
While message polling is a relatively simple to implement, it might put a lot of network pressure on the message broker in case there are a lot of consumers (it indeed depends on implementation, polling interval, transport protocol etc).
Normally message brokers offer an event-driven interface by implementing Pub/Sub pattern.
This way, producers still publish messages to a certain queue, however consumers "subscribe" to new messages from certain queues.
How the routing mechanism is implemented, it's up to you to decide. The routing implementation can rely on queues explicitly, or introduce a different abstraction that can be used for routing (e.g. message topic).

> **Message topic**
> 
> Message topic is a logical identifier of a communication channel between producers and consumers via the message broker.
> Topic's role is quite similar to a single message queue - grouping messages in order to be able to route them.
> However, topics allow to abstract over implementation, making the routing mechanism more transparent to both producers and consumers.

![Publisher Subscriber](images/lab1-pubsub.gif)

**Workflow example:**

0. The message broker is up and running;
1. A producer - P1, sends a message to the topic T1 **and** T2
2. A consumer - C1, connects to the broker, subscribes to the topic T1;
3. Another consumer - C2, connects to the broker and subscribes to topics T1 **and** T2;
4. Broker routes messages as follows
    4.1. All messages from the topic T1 are dispatched to C1 **and** C2;
    4.2. All messages from the topic T2 are dispatched to C2;
    4.3. Once a message is dispatched to consumers **currently** subscribed to the matching topic, it's removed from broker's storage;

**Requirements:**
- Consumers must be able to subscribe to different message topics;
- Subscribing to a non-existing topic must result in an explicit error on consumer side;
    - Alternatively, you might implement a configurable feature that would allow to create the topic, in case it doesn't exist;

**Note:** There are multiple ways to abstract over how message brokers implement the routing mechanism. For example - [RabbitMQ](https://www.rabbitmq.com/getstarted.html)

**Bonus point:** Implement an advanced routing mechanism that would allow consumers to use either regular expressions (RegExp) or simplified patterns to subscribe for topics.
Examples:
- Simple wildcards - subscribing to `Google*` will route all messages with topic that starts with "Google" (e.g. "Google.Nest")
- RegExp - subscribing to `Google\.Nest\.(error|warning)` will route all messages with topic that matches either "Google.Nest.error" or "Google.Nest.warning"

### Implement message persistence

Once a message broker becomes an "event hub" of your system, any data loss might cause data-integrity problems.
Thus it's important to ensure that messages are persisted in case a broker is restarted unexpectedly.

**Requirements:**
- The message broker periodically creates a **persistent** backup of messages that haven't been consumed yet;
- When message broker starts and there's an existing backup, it can be used to recover to the state before the restart;

**Bonus point:**
- There might be 2 types of messages - transient and persistent, a producer specifies message type;
- The backup is created only for persistent messages;


### Implement "last will and testament"

Since message brokers are used for distributed systems there's always a chance that either a producer or consumer can fail and disconnect abnormally.
And often, it's required to know when a consumer or producer disconnected unexpectedly, either for alerting or monitoring purposes.
One way of implementing this is "last will and testament" feature implemented in the [MQTT protocol](http://www.hivemq.com/blog/mqtt-essentials-part-8-last-will-and-testament).

**Requirements:**
- Message broker protocol must support specifying the message and topic for "last will and testament";
- Extend message broker protocol to support "graceful shutdown" message, to distinguish normal disconnect and unexpected one;
- When a client closes connection without sending "graceful shutdown" message, broker must publish the message to corresponding topic;

# Part 2

Use an RPC framework to replace Socket-based APIs. An RPC (or RMI in OOP) framework allows abstracting a procedure/method invocation over transport.
There are quite a few existing frameworks that allows implementing RPC easier:
- [Apache Thrift](https://thrift.apache.org/)
- [gRPC](https://grpc.io/docs/what-is-grpc/introduction/)
- [Apache Avro](https://avro.apache.org/)
- etc

An \*RPC framework attempts to solve several problems:
- Data representation - underlying data format used by the framework (protobuf for gRPC, thrift for Apache Thrift etc);
- Data transport - transport protocol used by the framework. For example gRPC uses HTTP/2, with built-in encryption and authentication, under the hood;
- Unified API - re-using the same API style for different components;
- Schema evolution - it's difficult to maintain and evolve an API, [schema evolution](https://martin.kleppmann.com/2012/12/05/schema-evolution-in-avro-protocol-buffers-thrift.html) is supported by most RPC frameworks;

## Objectives

- Study and apply an RPC framework to re-implement broker's API

## Tasks

### Replace Socket-based API with \*RPC framework

In the first part you've implemented message broker's API using Sockets and a protocol, defined by you. Use \*RPC for all components (broker itself, producer, consumer) to replace Socket communication and your custom protocol.
Any action handled by the broker (get message, subscribe, publish message, connect, disconnect etc) must be implemented via \*RPC.
