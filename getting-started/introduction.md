## Introduction to MOAR

When microservice architecture started to get popular around 2012 everyone was becoming distributed developers, and just about the same time everyone discovered that distributed computing is hard.

We hear alot of successes with microservice architecture from huge software developers like Netflix and Spotify, but we rarely hear it applied successfully to a small- midscale business. That is because most of those projects fail miserably.

The reason for failure is that microservice architecture suits best when you have a large number of developers and you need to scale your architecture to multiple independent teams.

Trying to use the microservice architecture on a one-team project produces a lot of overhead, delays and in turn shortcuts taken to produce results faster. That is why those project fails. Because microservice architecture doesn't apply to those scenarios.

### What MOAR is

MOAR set constraints on services and how services can communicate to each other. These constraints make your system much easier to maintain, so that you can run it with one team and still get the benefits of a modularized microservice architecture.

These are the most important constraints

#### Messages

All communication between services are done with messages. All messages have a common schema in their envelope, metadata of the message, and the body of the message is always strongly typed.

A message schema is versioned so when you update a message you do not accidently crash a service that cannot handle it.

**Message examples**

* Command: update-user
* Publish: user-updated
* Query: get-user
* Request: add-line-item-to-order

#### Services

A service is not an application or deployable unit as you are used to. It is just a name for the bounded context in which one or several functions implements the service interface. There is no code for the service, no build or deployment pipeline.

There are reasons when you want to extract a service to its own application, but this is something you want to avoid unless the benefits turn out greater than the costs.

**Service examples**

* user-svc
* order-svc
* mail-svc
* payment-svc

#### Functions

A function takes a message, process it, and sends one or several new messages. A function belongs to a service in order to handle one kind of message. A function can never exist outside the context of a service.

**Function examples**

* user-svc/get-user
* order-svc/add-line-item-to-order
* user-svc/update-user
* mail-svc/send-email

#### Communication

There are only four ways to communicate messages.

* **Query**, when you need to ask another service for some data
* **Command**, when you want to send a message but don't expect a response
* **Request**, when you want something carried out and the result returned
* **Subscribe**, when you listen for a message to be published in order to act on it

These four ways of sending messages are all that is needed to build a MOAR system, and the only way you are allowed to communicate between services. Only when you access external resources you are allowed to use communication tools like REST or RPC.

[Next / Protocol of MOAR](protocol.html)