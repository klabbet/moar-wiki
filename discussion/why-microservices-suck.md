## Why Microservices Suck

> Spoiler alter! They don't, it depends.

The idea of microservices is very appealing to both software developers and architects alike. You split your system into smaller isolated parts, constrained by the bounded context of the domain. Your system takes on properties that makes it easier to maintain compared to a monolith.

With microservices you have smaller isolated parts of code that each have their own application lifecycle. This means that you can build and deploy a part of the system, without affecting other parts. It means that you can replace a part of the system with no changes to the rest.

It also means that different parts of your domain can evolve at different pace. You gain additivity, meaning that you change the functionality of your system by adding to it, and not by changing the existing parts.

Services might have different requirements for load and uptime. You can give the user service 3 VCPUs but it's enough for your order service to have 2 VCPU, except when there is a marketing campaign and you can increase order service to 5 VCPUs. This is very attractive as you can choose to optimize some part of the system's performance to just throwing hardware at other parts.

Microservices also allow you to scale out the development team to several teams working on different services without them stepping on each other's toes (as much). You work with well defined interfaces between the teams which leads to good design and a longetivity of the code.

## So why does it suck?

It requires a lot of overhead. If you have several teams working on the same system, you need a lot of architects and shared resources to make sure that the system as a whole is moving in the right direction, that new services knows how to communicate with old, that you can trace, debug and just run the system that is managed by several teams.

This is not a big deal if you're Netflix, but if you have 5-6 developers working on 30 something microservices it will become a huge hassle.

The overhead of running a microservice system on just one team, is often too great for comfort. You spend as much time nurturing the system, as you do developing new functionality. Because of this, smaller teams often start taking shortcuts.

* Services start sharing databases which breaks isolation.
* The law of additivity is no longer respected and changes in one service ripples through the design.
* Services starts to grow out of "micro" because it is too much hassle adding a service.
* Bottlenecks starts to appear in system shared resources 
* Services have different conventions, making the system hard to maintain

Soon enough you have a system worse than a badly maintained monolith because yours use HTTP for function calls.

## We want MOAR

This is where MOAR is coming from. An architecture that is designed to work well for a small team, but also be able to scale up to several teams. It reduces the overhead by applying a set of constraints. As long as everyone follow these constraints you will have a system that is easy to maintain and that will grow with the size of your team.
