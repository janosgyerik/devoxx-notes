# vert.x

A toolkit to build micro-service applications.

Presentation slides:

http://devoxx0workshop0slides-vertxdemos.rhcloud.com/

## Micro-services

Benefits:

- asynchronous evolution
- better local understanding
- scalability
- integration / polyglot

Cons:

- global debug
- deployment
- latency (multi-hop)
- dynamic availability

## vert.x

- framework
- unopinionated
- reactive
- polyglot
- distributed

## Reactor pattern

http://www.reactivemanifesto.org/

- Asynchronous message passing / event loop
  + get a message
  + find a handler
  + call the handler
- Handlers are always called in the same thread (event-loop)
- Handlers must never block the thread calling them
- The threads don't wait, don't sleep, always do something useful

Asynchronous architecture, any component may fail, and the application should react and continue working.

http://devoxx0workshop0slides-vertxdemos.rhcloud.com/#/21

## Verticles

An agent-like model. Not fully agent like AKKA.

Verticles are chunks of code that get deployed and run by Vert.x
Applications can be in any language.

Verticles can be deployed independently.

Verticles are loosely coupled.

Verticles can evolve asynchronously.

Micro-services interact using the event bus.

