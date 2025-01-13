# Design-Patterns
This repo contains the materials and code to demonstrate the design patterns

Design Patterns Gang of Four.

Deign Pattern is a reuable and named solution to a recurring problem in a context.

Patterns are Discovered Not Created.

Object Oriented Programming.

OOP Building Blocks

1) ABSTRACTION

From Google
In Object-Oriented Programming (OOP), "abstraction" means hiding the internal complexities of an object and only exposing the essential features or functionalities that a user needs to interact with, essentially presenting a simplified view of a system without revealing unnecessary details; a real-world example is using a remote control for a TV - you only need to press buttons to change channels, not understand the intricate electronics behind it

Is about identifying the essential details or characterestics of an object with an objective to hiding the complexity of how they are implemented.

In java the Abstraction is achieved through interfaces and abstract classes

![alt text](image.png)

![alt text](image-1.png)

In this case we can use Abstraction of and Engine to compose abstraciton of a car.

2) ENCAPSULATION

From Google
In Object-Oriented Programming (OOP), encapsulation means bundling data (attributes) with the methods that operate on that data into a single unit, essentially "wrapping" them together within a class, thereby hiding internal implementation details and providing controlled access to the data through public methods, like "getters" and "setters"; this protects the data from unauthorized modification and promotes modularity in your code.

Is all about hiding information. Here is the idea is to protect the applicaiton from one part of the application from other part. So in this case if you have to change one part you dont have to change the other part too.

![alt text](image-2.png)

For lot of people encapsulation is to set the member variables as private and provide setter and getter to control access to these variables.

Encapsulation can also seperate behaviour from other parts of the application

![alt text](image-3.png)

![alt text](image-5.png)

3) INHERITANCE

From Google
In Object-Oriented Programming (OOP), inheritance is a mechanism where one class (called a child class or subclass) acquires the properties and behaviors of another class (called a parent class or superclass), allowing for code reuse and creating hierarchical relationships between classes; essentially, a child class "inherits" characteristics from its parent class, like how a real-world child inherits traits from their parents.

4) POLYMORPHISM

From Google
In object-oriented programming (OOP), polymorphism refers to the ability of an object to take on multiple forms, meaning a single method name can perform different actions depending on the object type it is called on; essentially, allowing you to use the same interface for different underlying types, like calling a "print" method on a circle and a square, even though they will output different results based on their shape.