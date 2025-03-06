# Design-Patterns

Deign Pattern is a reuable and named solution to a recurring problem in a context.

Patterns are Discovered Not Created.

OOP Building Blocks

## Abstraction

In Java, abstraction is one of the core principles of object-oriented programming (OOP). It focuses on hiding the implementation details of a class or method and exposing only the essential features to the user. This allows developers to work at a higher level of abstraction, concentrating on what an object does rather than how it does it.

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

From Google
In Object-Oriented Programming (OOP), encapsulation means bundling data (attributes) with the methods that operate on that data into a single unit, essentially "wrapping" them together within a class, thereby hiding internal implementation details and providing controlled access to the data through public methods, like "getters" and "setters"; this protects the data from unauthorized modification and promotes modularity in your code.

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
//Data Encapsulation
// Class with encapsulated fields
class Employee {
    // Private fields (encapsulation)
    private String name;
    private int age;
    private double salary;

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
        if (age > 0) { // Age validation
            this.age = age;
        } else {
            System.out.println("Age must be positive.");
        }
    }

    // Public getter for 'salary'
    public double getSalary() {
        return salary;
    }

    // Public setter for 'salary'
    public void setSalary(double salary) {
        if (salary > 0) { // Salary validation
            this.salary = salary;
        } else {
            System.out.println("Salary must be positive.");
        }
    }
}

// Main class to demonstrate encapsulation
public class Main {
    public static void main(String[] args) {
        Employee emp = new Employee();

        // Setting fields using setter methods
        emp.setName("Alice");
        emp.setAge(30);
        emp.setSalary(50000);

        // Accessing fields using getter methods
        System.out.println("Employee Name: " + emp.getName());
        System.out.println("Employee Age: " + emp.getAge());
        System.out.println("Employee Salary: " + emp.getSalary());
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

From Google
In Object-Oriented Programming (OOP), inheritance is a mechanism where one class (called a child class or subclass) acquires the properties and behaviors of another class (called a parent class or superclass), allowing for code reuse and creating hierarchical relationships between classes; essentially, a child class "inherits" characteristics from its parent class, like how a real-world child inherits traits from their parents.


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

From Google
In object-oriented programming (OOP), polymorphism refers to the ability of an object to take on multiple forms, meaning a single method name can perform different actions depending on the object type it is called on; essentially, allowing you to use the same interface for different underlying types, like calling a "print" method on a circle and a square, even though they will output different results based on their shape.

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
---
## OOP Principles

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


```java
// Class responsible for managing book data
class Book {
    private String title;
    private String author;

    public Book(String title, String author) {
        this.title = title;
        this.author = author;
    }

    public String getTitle() {
        return title;
    }

    public String getAuthor() {
        return author;
    }
}

// Class responsible for printing book details
class BookPrinter {
    public void printDetails(Book book) {
        System.out.println("Book Title: " + book.getTitle());
        System.out.println("Book Author: " + book.getAuthor());
    }
}

// Main class to demonstrate SRP
public class Main {
    public static void main(String[] args) {
        Book book = new Book("1984", "George Orwell");
        BookPrinter printer = new BookPrinter();
        printer.printDetails(book);
    }
}
```