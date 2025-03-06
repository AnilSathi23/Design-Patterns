# Design-Patterns

- A design pattern is a reusable, well-defined solution to a recurring problem within a specific context.
- Design patterns are not invented but discovered—they emerge from proven practices and shared experiences.
- Object-Oriented Programming (OOP) Building Blocks: Fundamental principles and concepts that form the foundation of OOP.

## Abstraction

 Abstraction focuses on hiding the implementation details of a class or method and exposing only the essential features to the user. This allows developers to work at a higher level of abstraction, concentrating on what an object does rather than how it does it.

Key points about abstraction in Java:

### Abstract Classes:
- A class can be declared as abstract using the abstract keyword.
- It may include abstract methods (methods without a body) as well as concrete methods (methods with an implementation).
- Abstract classes cannot be instantiated directly; instead, they must be extended by a subclass that provides the implementation for abstract methods.

### Interfaces:
- Interfaces are another way to achieve abstraction.
- They can contain abstract methods (by default, all methods in an interface are public and abstract) and, as of Java 8, default methods (with a body) and static methods.
- A class implements an interface to define the specific behavior of its methods.

### Benefits of Abstraction:
- Simplifies complex systems by focusing only on relevant details.
- Improves code maintainability and scalability.
- Provides a way to achieve loose coupling between components.


```java
// Abstract class
abstract class Animal {
    // Abstract method (no body)
    abstract void sound();

    // Regular method
    void eat() {
        System.out.println("This animal eats food.");
    }
}

// Subclass that provides implementation
class Dog extends Animal {
    void sound() {
        System.out.println("Woof!");
    }
}

class Cat extends Animal {
    void sound() {
        System.out.println("Meow!");
    }
}

// Main class to test abstraction
public class Main {
    public static void main(String[] args) {
        Animal dog = new Dog();
        dog.sound();
        dog.eat();

        Animal cat = new Cat();
        cat.sound();
    }
}
```

## Encapsulation

Encapsulation refers to the bundling of data (fields) and methods (functions) that operate on the data into a single unit, usually a class. Encapsulation is also about restricting direct access to some of the object's components, which is achieved through access modifiers.

## Key Aspects of Encapsulation:

### Data Hiding:

- Fields (variables) in a class are often declared as private to prevent unauthorized access.
- Access to these fields is controlled through public methods, known as getters and setters.

### Controlled Access:

- By using getter methods, you can read the value of private fields.

- By using setter methods, you can modify the value, potentially adding validation logic.

### Improved Maintainability:

- Since data is hidden, internal implementation details can be changed without affecting external code that uses the class.

- It ensures loose coupling between different components of a program.

```java
// Class with private data and public methods
class Student {
    // Private fields
    private String name;
    private int age;

    // Public getter for 'name'
    public String getName() {
        return name;
    }

    // Public setter for 'name'
    public void setName(String name) {
        this.name = name;
    }

    // Public getter for 'age'
    public int getAge() {
        return age;
    }

    // Public setter for 'age'
    public void setAge(int age) {
        if (age > 0) { // Validate age
            this.age = age;
        } else {
            System.out.println("Age must be positive.");
        }
    }
}

// Main class to demonstrate encapsulation
public class Main {
    public static void main(String[] args) {
        Student student = new Student();

        // Set data using setter methods
        student.setName("John");
        student.setAge(20);

        // Get data using getter methods
        System.out.println("Student Name: " + student.getName());
        System.out.println("Student Age: " + student.getAge());
    }
}
```

```java
//Behaviour enapsulation

class Account {
    private double balance;

    // Constructor to set initial balance
    public Account(double initialBalance) {
        if (initialBalance > 0) {
            this.balance = initialBalance;
        }
    }

    // Public method to deposit money
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited: " + amount);
        } else {
            System.out.println("Invalid deposit amount.");
        }
    }

    // Public method to withdraw money
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Withdrew: " + amount);
        } else {
            System.out.println("Invalid withdrawal amount.");
        }
    }

    // Public method to check balance
    public double getBalance() {
        return balance;
    }
}

// Main class to test behavior encapsulation
public class Main {
    public static void main(String[] args) {
        Account myAccount = new Account(100.0);

        myAccount.deposit(50.0);
        myAccount.withdraw(30.0);
        System.out.println("Current Balance: " + myAccount.getBalance());

        myAccount.withdraw(150.0); // This will show an error message
    }
}
```


## Inheritance

Inheritance allows a class (called the "child" or "subclass") to inherit the properties and methods of another class (called the "parent" or "superclass"). This helps in reusing code, establishing a hierarchy, and creating more organized and scalable systems.

## Key Points about Inheritance:

### Parent (Superclass) and Child (Subclass):

- The parent class contains common properties and methods.
- The child class inherits these members and can add its own unique functionality.

### extends Keyword:

- In Java, inheritance is achieved using the extends keyword


```java
// Parent class (Superclass)
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }

    void sleep() {
        System.out.println("This animal sleeps.");
    }
}

// Child class (Subclass)
class Dog extends Animal {
    void bark() {
        System.out.println("The dog barks.");
    }
}

// Main class to demonstrate inheritance
public class Main {
    public static void main(String[] args) {
        Dog myDog = new Dog();

        // Inherited methods
        myDog.eat();   // Calls the 'eat' method from Animal class
        myDog.sleep(); // Calls the 'sleep' method from Animal class

        // Method from Dog class
        myDog.bark();  // Calls the 'bark' method from Dog class
    }
}
```

## Polymorphism

Polymorphism comes from Greek, meaning "many forms." In Java, it refers to the ability of a method or an object to take on many forms, enabling flexibility and scalability in programming.

## Types of Polymorphism in Java

### Compile-Time Polymorphism (Static Binding):

- Achieved through method overloading.
- The method to be called is determined at compile-time based on the method signature (method name, parameters, and their types).

```java
class Calculator {
    // Overloaded methods with different parameter types
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }

    String add(String a, String b) {
        return a + b;
    }
}

public class Main {
    public static void main(String[] args) {
        Calculator calc = new Calculator();

        System.out.println(calc.add(5, 10));       // Calls the integer version
        System.out.println(calc.add(5.5, 2.3));   // Calls the double version
        System.out.println(calc.add("Hello, ", "World!")); // Calls the string version
    }
}
```
## Runtime Polymorphism (Dynamic Binding):

### Achieved through method overriding.

- The method to be called is determined at runtime based on the actual object.
- This is commonly used when a subclass provides its own implementation of a method defined in its superclass.

```java
class Animal {
    void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Dog barks");
    }
}

class Cat extends Animal {
    @Override
    void makeSound() {
        System.out.println("Cat meows");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Dog();  // Runtime decision
        myAnimal.makeSound();         // Output: Dog barks

        myAnimal = new Cat();         // Runtime decision
        myAnimal.makeSound();         // Output: Cat meows
    }
}
```

---
## SOLID Principles

### SOLID
- Single Responsibility
- Open-Closed
- Loskov Substitution
- Interface segregation
- Dependency Injection

### OTHER
- Don't repeat yourself (DRY)
- Encapsulate what changes
- Favour composition over inheritance
- Programming to interfaces

## Single Responsibility

Single Responsibility Principle (SRP) states that a class should have only one reason to change, meaning it should have only one responsibility or purpose.

## Key Points about SRP:

### Focus on a Single Responsibility:

- A class, function, or module should encapsulate a specific functionality or behavior.

- This keeps the design cohesive and easy to understand.

### Improved Maintainability:

- When a class has a single responsibility, changes in one aspect of the application (e.g., business logic or UI) will only affect the relevant class.

- This reduces the risk of unintentional side effects when modifying code.

### Separation of Concerns:

- SRP emphasizes dividing the application into distinct parts, where each part addresses a specific concern.

- This enhances modularity and allows for better code reuse.


```java
// Regular Java Class
class Report {
    public void generateReport() {
        // Code to generate the report
    }

    public void printReport() {
        // Code to print the report
    }
}
```

```java
// With SRP
class ReportGenerator {
    public void generateReport() {
        // Code to generate the report
    }
}

class ReportPrinter {
    public void printReport() {
        // Code to print the report
    }
}
```