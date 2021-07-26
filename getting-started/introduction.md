## Introduction to MOAR

When microservice architecture started to get popular around 2012 everyone became experts of distributed systems, and just about the same time everyone discovered that distributed computing is hard.

We hear alot of successes with microservice architecture from huge software developers like Netflix and Spotify, but rarely applied successfully to a small- midscale business. That is because most of those projects fail miserably.

The reason for failure is that microservice architecture suits best when you have a large number of developers and you need to scale your architecture to multiple independent teams.

Trying to use the microservice architecture on a one-team project produces a lot of overhead, delays turns to shortcuts to produce results faster. That is why those project fails. Microservice architecture doesn't apply to those scenarios.

### What MOAR is

MOAR set constraints on a microservice system. These constraints makes your system easier to maintain, so you can run it with one team, and still get the benefits of a modularized microservice architecture.

These are the constraints.

#### Messages

All communication between services are done by messages. All messages consist of an envelope and a message body. The envelope is always the same attributes, and the body is the variable content of the messages you want to send.

The message body is always strongly typed, so when you update a message you will not accidently make a breaking change to your system.

**Message examples**

* Command: update-user
* Subscribe: user-updated
* Query: get-user
* Request: add-line-item-to-order

#### Services

A service is a name that bind functions together in a bounded context. It is not an application with its own lifecycle as in a microservice architecture. In MOAR you are encouraged to have many services within the same deployable application.

You can split services into several applications. There are several reasons to do this. You have several teams and want to cleanly split responsibilities. Or the service is better written in another language and technology stack. Maybe there are special security measures that force you to put the service behind a firewall.

But for the most time, services are developed and hosted together in the same application.

**Service examples**

* user-svc
* order-svc
* mail-svc
* payment-svc

#### Functions

A function takes a message, process it, and sends one or several new messages. A function belongs to a service in order to handle one kind of message. A function can never exist outside the context of a service.

The convention is to name the function after the service it belongs to and the message that it handles.

**Function examples**

* user-svc/get-user
* order-svc/add-line-item-to-order
* user-svc/update-user
* mail-svc/send-email

#### Stores

A store is a stock of data. Data is flowing into the store, and data is flowing out of the store. Most likely there is a database acting as the store, but it doesn't have to be.

Not all systems needs a store. If your system has no need for an internal state, then you don't need a store.

The store is often bound to the service and its bounded context. This means that you have one store for a service and services never share a store.

**Store examples**

* user-stor
* order-stor
* product-stor

#### Communication

There are only four ways to communicate.

* **Query**, when you need to ask a service for some data
* **Command**, when you want to send a message but don't expect a response
* **Request**, when you want something carried out and the result returned
* **Subscribe**, when you listen for a message to be published in order to act on it

These four operations are all you'll use inside the MOAR system. For external systems you build interfacing services that act as an adaptor between the external system and your MOAR system.

[Next / Simple Message Oriented Language &raquo;](smol.html)