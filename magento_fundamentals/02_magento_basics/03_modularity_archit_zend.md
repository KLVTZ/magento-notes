Magento Directory Structure
===========================

These concepts are absolutely essential. You have to know the system is there
and there is an operation in magento and how it works.

* Describe module architecture
* listing steps to add new modules
* designing a modular website


Modular Programming
-------------------
Modularity is a general concept, typically defined as a continuum, describing
the degree to which a system's components may be seperated and recombined.
Thousands of files that are related in function.
Design technique that increases the extent to which softwre is composed of parts

A module functions internally knows very little about other modules. You want to
connect other modules by interfaces. You shouldn't directly relate another part
of an applicaton or a relationship with the module.

Dependency injection is important. You can do it very lightly, in some
circumstances.

Modules support being added and removed from system in a plugable fashion.

Known issues and limitations
* `Mage_Core` dependency (Basically, the entire application)
* Modules initialization (declaration files are always parsed)
* Code intersection (when code does the same thing, or when modules know about
  eachother
* Adminhtml Module (the code has namespace that is linear and organized) All the
  adminhtml module does is aggrevate all the modules in admin. Simple and
  elegant fix does exist. Keeping modules under our directory.
* Design intergration. This means tying your view to templates to do anything. 

Zend Framework
--------------
Magento uses the Zend Framework. Magento isn't a Zend MVC Application. Magento
has it's own MVC Architecture. Underneath magento architecture, you have the Zend
Framework. 
