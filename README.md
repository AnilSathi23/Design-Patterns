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
- Single Responsibility Principle (SRP)
- Open-Closed Principle (OCP)
- Liskov Substitution Principle (LSP)
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


```java
//Without SRP
class Invoice {
    public void calculateTotal() {
        // Code to calculate total
    }

    public void printInvoice() {
        // Code to print invoice
    }

    public void saveToDatabase() {
        // Code to save invoice to a database
    }
}

//With SRP

class Invoice {
    public void calculateTotal() {
        // Code to calculate total
    }
}

class InvoicePrinter {
    public void printInvoice(Invoice invoice) {
        // Code to print the invoice
    }
}

class InvoiceRepository {
    public void saveToDatabase(Invoice invoice) {
        // Code to save the invoice to a database
    }
}

```

## Open/Closed Principle (OCP)

A software entity (such as a class, module, or function) should be open for extension but closed for modification.

### Explanation

- Open for Extension: You can add new functionality to a class or module without altering its existing code.
- Closed for Modification: Once a class or module is implemented, its existing code shouldn't be modified. This protects the stability of the system while allowing for adaptability.

```java
//Example Without Following OCP:
class NotificationService {
    public void sendNotification(String type) {
        if (type.equals("Email")) {
            System.out.println("Sending Email Notification...");
        } else if (type.equals("SMS")) {
            System.out.println("Sending SMS Notification...");
        }
    }
}
```

Adding a new notification type (e.g., "Push Notification") requires modifying the sendNotification method, which violates the principle.

```java
//Example Following OCP:
// Base interface
interface Notification {
    void send();
}

// Email Notification
class EmailNotification implements Notification {
    public void send() {
        System.out.println("Sending Email Notification...");
    }
}

// SMS Notification
class SMSNotification implements Notification {
    public void send() {
        System.out.println("Sending SMS Notification...");
    }
}

// Main Service
public class NotificationService {
    public void sendNotification(Notification notification) {
        notification.send();
    }
}

public class Main {
    public static void main(String[] args) {
        NotificationService service = new NotificationService();

        Notification email = new EmailNotification();
        Notification sms = new SMSNotification();

        service.sendNotification(email); // Output: Sending Email Notification...
        service.sendNotification(sms);   // Output: Sending SMS Notification...
    }
}
```

### In this example:

- The NotificationService class is closed for modification because we don’t alter its code when adding a new notification type.
- The system is open for extension because you can create new classes (e.g., PushNotification) that implement the Notification interface.

### Benefits of Following OCP:

- Scalability: Adding new features doesn’t require changes to the core code.
- Maintainability: Reduces the likelihood of introducing bugs when adding new functionality.
- Flexibility: Promotes modular and extensible design.

## Liskov Substitution Principle (LSP)

LSP emphasizes that objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program. In other words, a subclass must adhere to the behavior and contract of its parent class, ensuring that the program remains functional and predictable.

### Explanation:

- If a program is written using a superclass, it should work the same if that superclass is replaced with one of its subclasses.
- Subclasses should not violate the expectations set by the superclass, such as method behaviors or constraints.

```java
//Example Without Following LSP:
class Rectangle {
    private int width;
    private int height;

    public void setWidth(int width) {
        this.width = width;
    }

    public void setHeight(int height) {
        this.height = height;
    }

    public int getArea() {
        return width * height;
    }
}
//Now, a subclass for Square might break the principle if its behavior diverges:
class Square extends Rectangle {
    @Override
    public void setWidth(int width) {
        super.setWidth(width);
        super.setHeight(width); // Sets both width and height to maintain a square
    }

    @Override
    public void setHeight(int height) {
        super.setWidth(height);
        super.setHeight(height); // Sets both height and width
    }
}
//Using Square in place of Rectangle can cause unexpected behavior:
Rectangle rect = new Square();
rect.setWidth(5);
rect.setHeight(10); // Breaks expectations: width and height are no longer independent
System.out.println(rect.getArea()); // Output is 100, not the expected 50
```

### Example Following LSP:
To follow the Liskov Substitution Principle, avoid forcing subclasses to modify inherited behaviors:

```java
interface Shape {
    int getArea();
}

class Rectangle implements Shape {
    private int width;
    private int height;

    public void setWidth(int width) {
        this.width = width;
    }

    public void setHeight(int height) {
        this.height = height;
    }

    @Override
    public int getArea() {
        return width * height;
    }
}

class Square implements Shape {
    private int side;

    public void setSide(int side) {
        this.side = side;
    }

    @Override
    public int getArea() {
        return side * side;
    }
}
```

Here, Rectangle and Square implement the same Shape interface, but they do not override or change behaviors unexpectedly. Both classes are independent and interchangeable.

### Benefits of Following LSP:

- Predictability: Ensures that subclasses behave consistently with their parent classes.
- Maintainability: Reduces the risk of bugs when replacing or extending functionality.
- Code Reusability: Promotes modular and interchangeable design.