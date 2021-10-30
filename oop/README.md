# Object oriented programming

## Chapter II: Basis/Foundation of OOP
The basic techniques of oop are

* Capsulation
* Polymorphism
* Inheritance

Capsulation means that only the objects containing the data can change them. Other objects can only use defined routines to access the data.

Polymorphism is not explained well in the book. Polymorphism in OOP wants to set certain spots in the code where parts can easily be exchanged. The analogy used is light bulbs. You can change a light bulb when it matches the socket. The same should be used for moduls/code parts.

Inheritance is divided into inheritance of specifications and inheritance of implementations.
### Inheritance of specifications
This inheritance type is introduced as closely related to polymorphism. The analogy used is different electrical devices all having the same plug in the EU to all use the same voltage (230 V). This specification is inherited by an abstract specification to its children.
The inheritance of specificaton thus enables the polymorphistic property in that it enabled the exchange of those modules.

### Inheritance of implementations
This inheritance is explained as analogy to laws in the EU, which form a hierarchy from the city laws to NRW law going up to national law and then EU law. So the laws from EU are inherited to the next level and so forth. That way, the last party in the chain of inheritance has all the laws from the previous parties. More specific laws in the later parties override the ones from the previous parties.


## Chapter III: Principles of OO Designs
### Principle 1: Single Responsibility Principle
Modules are self-sustained and concise parts of an application. This can be code, a file, a group of files etc. Everything which can be considered a logical unit of an application and has a single purpose or task.
A module can have one or more tasks/purposes in a software system, which it is responsible for.

Modules can be comprised of other (sub)modules and can always be divided, when it gets too complicated.
The danger is increasing complexity when the connections between modules add up.

The principle says that every modules should only have one responsibility and vice versa.
Modulation of an application also increases its maintainability because only the modul which responsibility changed has to be changed. Also it might be used in other applications where exactly the same reponsibility is needed.

### Principle 2: Separation of Concerns

