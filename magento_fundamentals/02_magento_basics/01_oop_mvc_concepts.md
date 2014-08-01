Object-Oriented Programming and Model-View-Controller Pattern
=============================================================

Magento keeps code modular. To modularize code means to encapsulate functions
into objects and thus provide a meta environment where we can play.

GOF
---
Gang of Four Design Patterns that are available, are implemented in Magento.
With Design patterns, however, magento does so in a different way.

GRASP Design Patterns
---------------------
These concepts are handy to know. They can help you crafting your modules.

* Information Expert
* Creator
* Low Coupling
* High Cohesion
* Polymorphism


MVC
---
**Pros:**

* Modular
* Flexible
* Standard structure
* Compartmentalized
* Better maintenance
* Easy migration
* Reusable model code

**Cons:**

* Performance degradation
* Requires lots of files
* Solves problems that may not occur
* 3 layers not always enough

something to always remember, magento uses thin controller approach. Business
logic should be handled by the model or view. The route is an arbituary thing,
the blocks is actually what matters.

The view is a view model. A view is a self-contained application.

A basic flow is the controller gets the request, and then the view will grab the
model. The model is respresenting your data retrieval. The important thing to
know is that the view renders the model into a form suitable for interaction.



