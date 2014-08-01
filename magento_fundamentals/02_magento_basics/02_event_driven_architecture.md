Event Driven Architecture
=========================

If you have a system as big as magento, you often have a need to get access to
an application. You have access to other modules or parts of the code. 

EDA is an architecture in which events are used to exchange messages in real
time between applications or between different parts of single application.

Event driven architecture is a style of application architecture centered on an
asynchronous "push"-based communication model. An event is a notable thing that
happens inside or outside your business. An event may signify a problem or
impendng problem, an opportunity, a threshold, or a deviation.

Magento is a system that pushes events. Always pushing the key players.

EDA
---

**Advantages**

* Easy development process
* Easy to enhance application parts
* application is flexible

**Disadvantages**

* The flow of the application is less logical and obvious
* Hard to control application interactions
* Time consuming to event handlers running

The event will dispatch, and then will check to see if there is any observers.
The key parts are passed. Some observers may not do anything. The execution flow
goes through all observers!


