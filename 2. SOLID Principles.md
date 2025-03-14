## SOLID Principles

The SOLID principles are a set of five design principles that aim to make software designs more understandable, flexible, and maintainable. These principles are particularly important in Object-Oriented Programming (OOP) and guide developers in creating robust systems.

### SOLID
- Single Responsibility Principle (SRP)
- Open-Closed Principle (OCP)
- Liskov Substitution Principle (LSP)
- Interface Segregation Principle (ISP)
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


## Interface Segregation Principle (ISP)

A class should not be forced to implement interfaces it does not use.

In simpler terms, this principle emphasizes that interfaces should be small and specific to the needs of the implementing classes, rather than large, generalized interfaces that force classes to implement unnecessary methods.

## Key Points:

### Keep Interfaces Focused:

- Avoid creating large, "fat" interfaces with too many methods.
- Instead, split them into smaller, more specific interfaces that cater to the needs of specific classes.

### Improves Flexibility:

- Classes implementing interfaces are not burdened with irrelevant or unnecessary methods, keeping them focused on their intended functionality.

### Prevents Implementation Overhead:

- When interfaces are too broad, implementing classes might have to include "empty" or unused methods, which can lead to confusion and unnecessary code.

Example Without Following ISP:

```java
// Large interface with methods that might not be relevant for all classes
interface Worker {
    void work();
    void eat();
    void sleep();
}

// A robot class is forced to implement methods it doesn't use
class Robot implements Worker {
    public void work() {
        System.out.println("Robot is working.");
    }

    public void eat() {
        // Robots don't eat
    }

    public void sleep() {
        // Robots don't sleep
    }
}
```
In this case, the Robot class is forced to implement the eat and sleep methods, even though they are irrelevant for its functionality.

Example Following ISP:

```java
// Split the large interface into smaller, focused interfaces
interface Workable {
    void work();
}

interface Eatable {
    void eat();
}

interface Sleepable {
    void sleep();
}

// A robot only implements what it needs
class Robot implements Workable {
    public void work() {
        System.out.println("Robot is working.");
    }
}

// A human implements all relevant interfaces
class Human implements Workable, Eatable, Sleepable {
    public void work() {
        System.out.println("Human is working.");
    }

    public void eat() {
        System.out.println("Human is eating.");
    }

    public void sleep() {
        System.out.println("Human is sleeping.");
    }
}
```

Now, the Robot class only implements the Workable interface, and it is not forced to implement unrelated methods like eat and sleep. Similarly, the Human class can implement all relevant interfaces.

### Benefits of ISP:

- **Enhances Code Clarity**: By keeping interfaces small and focused, they are easier to understand.
- **Improves Maintainability**: Changes in one interface won’t impact unrelated classes.
- **Increases Flexibility**: Classes only implement what they truly need.


## Dependency Injection

Dependency Injection is a design pattern that helps implement Inversion of Control (IoC). It allows a class to receive its dependencies from an external source rather than creating them itself. This promotes loose coupling between components and makes the code more modular, testable, and maintainable

### Types of Dependency Injection:

- **Constructor Injection**: Dependencies are passed to the class via its constructor.

```java
class Service {
    void execute() {
        System.out.println("Service executed.");
    }
}

class Client {
    private Service service;

    public Client(Service service) {
        this.service = service;
    }

    public void doWork() {
        service.execute();
    }
}

public class Main {
    public static void main(String[] args) {
        Service service = new Service();
        Client client = new Client(service);
        client.doWork();
    }
}

```

- **Setter Injection**: Dependencies are assigned using setter methods.

```java
class Client {
    private Service service;

    public void setService(Service service) {
        this.service = service;
    }

    public void doWork() {
        service.execute();
    }
}

public class Main {
    public static void main(String[] args) {
        Service service = new Service();
        Client client = new Client();
        client.setService(service);
        client.doWork();
    }
}
```

- **Interface Injection**: The dependency provides a method for the client to call, which is a less common approach.

Why Use Dependency Injection?

- **Loose Coupling**: Classes depend on abstractions (interfaces) rather than concrete implementations.
- **Improved Testability**: Dependencies can be easily replaced with mock objects for unit testing.
- **Better Maintainability**: Changes in one part of the system don't cascade through the codebase.

Real-World Usage:
Frameworks like Spring in Java automate dependency injection using annotations such as @Autowired. For example:

```java
@Component
class Service {
    void execute() {
        System.out.println("Service executed.");
    }
}

@Component
class Client {
    @Autowired
    private Service service;

    public void doWork() {
        service.execute();
    }
}
```