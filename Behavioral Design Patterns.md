Java design patterns are best practices that developers use to solve common problems when designing software. These patterns provide reusable solutions and help ensure that code is robust, maintainable, and scalable. They fall into three main categories:

1. **Creational Patterns**: These deal with object creation, ensuring that objects are created in a controlled manner.
   - Example: Singleton, Factory, Builder, Prototype.

2. **Structural Patterns**: These deal with the composition of classes or objects to form larger structures.
   - Example: Adapter, Composite, Decorator, Proxy, Bridge.

3. **Behavioral Patterns**: These focus on the interaction and communication between objects.
   - Example: Observer, Strategy, Command, State.

Each pattern is designed to tackle a specific type of problem in software development. If you'd like, I can explain any of these patterns in detail or give you examples in Java code! Just let me know.

# Behavioral Patterns

## Observer

The **Observer Pattern** is a behavioral design pattern that establishes a one-to-many relationship between objects. This means that when one object (the subject) changes its state, all its dependents (observers) are notified automatically. It's particularly useful in scenarios where changes in one object need to be reflected in others, like in event handling systems or GUIs.

---

### Key Points:
1. **Subject**: Maintains a list of observers and notifies them of any state changes.
2. **Observer**: Defines an update method, which gets called when the subject's state changes.
3. **Loose Coupling**: The subject and observers are loosely coupled, meaning the subject doesn’t need to know the concrete implementation of the observers.

---

### Java Example:

Imagine we have a scenario where a news agency notifies subscribers when news is updated.

#### Step-by-Step Implementation:

```java
// Step 1: Create the Observer interface
public interface Observer {
    void update(String news); // Method called when there's an update
}

// Step 2: Create the Subject interface
import java.util.ArrayList;
import java.util.List;

public abstract class Subject {
    protected List<Observer> observers = new ArrayList<>();

    public void attach(Observer observer) {
        observers.add(observer); // Add observer
    }

    public void detach(Observer observer) {
        observers.remove(observer); // Remove observer
    }

    public void notifyObservers(String news) {
        for (Observer observer : observers) {
            observer.update(news); // Notify all observers
        }
    }
}

// Step 3: Implement the Concrete Subject
public class NewsAgency extends Subject {
    private String news;

    public void setNews(String news) {
        this.news = news;
        notifyObservers(news); // Notify when news is updated
    }
}

// Step 4: Implement Concrete Observers
public class EmailSubscriber implements Observer {
    private String name;

    public EmailSubscriber(String name) {
        this.name = name;
    }

    @Override
    public void update(String news) {
        System.out.println(name + " received news via Email: " + news);
    }
}

public class SMSSubscriber implements Observer {
    private String name;

    public SMSSubscriber(String name) {
        this.name = name;
    }

    @Override
    public void update(String news) {
        System.out.println(name + " received news via SMS: " + news);
    }
}

// Step 5: Test the Observer Pattern
public class ObserverPatternDemo {
    public static void main(String[] args) {
        NewsAgency newsAgency = new NewsAgency();

        Observer emailSubscriber1 = new EmailSubscriber("Alice");
        Observer emailSubscriber2 = new EmailSubscriber("Bob");
        Observer smsSubscriber = new SMSSubscriber("Charlie");

        // Attach observers
        newsAgency.attach(emailSubscriber1);
        newsAgency.attach(emailSubscriber2);
        newsAgency.attach(smsSubscriber);

        // Update news and notify observers
        newsAgency.setNews("Breaking News: Observer Pattern Explained!");
    }
}
```

---

### Explanation:
1. **Subject Interface (`Subject`)**:
   - Manages a list of observers and notifies them of changes.
2. **Concrete Subject (`NewsAgency`)**:
   - Contains state (`news`) and updates all observers when its state changes.
3. **Observer Interface (`Observer`)**:
   - Defines an update method for receiving notifications.
4. **Concrete Observers (`EmailSubscriber`, `SMSSubscriber`)**:
   - Implement the update method to handle notifications.

---

### Output:
```
Alice received news via Email: Breaking News: Observer Pattern Explained!
Bob received news via Email: Breaking News: Observer Pattern Explained!
Charlie received news via SMS: Breaking News: Observer Pattern Explained!
```

---

### Use Cases:
- Event-driven systems (e.g., GUI components reacting to user actions).
- Notification services (e.g., weather updates, stock price alerts).
- Distributed systems requiring real-time updates.


## Strategy

The **Strategy Pattern** is a behavioral design pattern that allows you to define a family of algorithms, encapsulate each one in a separate class, and make them interchangeable. It enables the client to choose an algorithm's behavior at runtime, promoting flexibility and adhering to the Open/Closed Principle (open for extension, closed for modification).

---

### Key Points:
1. Encapsulates multiple algorithms or strategies.
2. Enables the client to switch between algorithms dynamically.
3. Reduces code duplication and enhances maintainability.

---

### Java Example:

Imagine we have a context where different payment methods (Credit Card, PayPal) are supported. The strategy pattern will allow the client to select the payment method dynamically.

#### Step-by-Step Implementation:

```java
// Step 1: Create the Strategy interface
public interface PaymentStrategy {
    void pay(int amount);
}

// Step 2: Implement concrete strategies
public class CreditCardPayment implements PaymentStrategy {
    private String cardNumber;

    public CreditCardPayment(String cardNumber) {
        this.cardNumber = cardNumber;
    }

    @Override
    public void pay(int amount) {
        System.out.println("Paid $" + amount + " using Credit Card: " + cardNumber);
    }
}

public class PayPalPayment implements PaymentStrategy {
    private String email;

    public PayPalPayment(String email) {
        this.email = email;
    }

    @Override
    public void pay(int amount) {
        System.out.println("Paid $" + amount + " using PayPal account: " + email);
    }
}

// Step 3: Create the Context class
public class ShoppingCart {
    private PaymentStrategy paymentStrategy;

    // Set the payment strategy dynamically
    public void setPaymentStrategy(PaymentStrategy paymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    // Execute the payment
    public void checkout(int amount) {
        if (paymentStrategy == null) {
            System.out.println("Please select a payment method.");
        } else {
            paymentStrategy.pay(amount);
        }
    }
}

// Step 4: Test the Strategy Pattern
public class StrategyPatternDemo {
    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();

        // Pay using Credit Card
        cart.setPaymentStrategy(new CreditCardPayment("1234-5678-9012-3456"));
        cart.checkout(100);

        // Pay using PayPal
        cart.setPaymentStrategy(new PayPalPayment("user@example.com"));
        cart.checkout(150);
    }
}
```

---

### Explanation:
1. **Strategy Interface (`PaymentStrategy`)**: Defines the common interface for all payment methods.
2. **Concrete Strategies (`CreditCardPayment`, `PayPalPayment`)**: Implement the payment logic for specific methods.
3. **Context Class (`ShoppingCart`)**: Uses a `PaymentStrategy` to execute a payment and allows dynamic selection of the strategy.
4. **Client (`StrategyPatternDemo`)**: Chooses the payment strategy and triggers the checkout process.

---

### Output:
```
Paid $100 using Credit Card: 1234-5678-9012-3456
Paid $150 using PayPal account: user@example.com
```

---

### Use Cases:
- Sorting algorithms where you can choose between different sorting techniques (e.g., Bubble Sort, Merge Sort).
- Payment processing systems with multiple payment methods.
- Validation frameworks where different validation strategies are applied.

This pattern is especially powerful in scenarios requiring flexibility and algorithmic variety. 

## Command

The **Command Pattern** is a behavioral design pattern that encapsulates a request as an object, thereby allowing users to parameterize objects with different requests, queue or log requests, and support undoable operations. It promotes loose coupling between the sender (invoker) and the receiver of the request by introducing a command interface.

---

### Key Points:
1. **Encapsulates a request** as an object.
2. Decouples the sender (which triggers the request) from the receiver (which performs the action).
3. Supports features like undo/redo functionality and request queuing.

---

### Java Example:

Imagine a scenario where a remote control can execute various commands like turning a light on or off.

#### Step-by-Step Implementation:

```java
// Step 1: Create the Command interface
public interface Command {
    void execute();
    void undo(); // Optional for undo functionality
}

// Step 2: Implement concrete commands
public class LightOnCommand implements Command {
    private Light light;

    public LightOnCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.turnOn();
    }

    @Override
    public void undo() {
        light.turnOff();
    }
}

public class LightOffCommand implements Command {
    private Light light;

    public LightOffCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.turnOff();
    }

    @Override
    public void undo() {
        light.turnOn();
    }
}

// Step 3: Create the Receiver class
public class Light {
    public void turnOn() {
        System.out.println("Light is ON");
    }

    public void turnOff() {
        System.out.println("Light is OFF");
    }
}

// Step 4: Create the Invoker class
public class RemoteControl {
    private Command command;

    public void setCommand(Command command) {
        this.command = command;
    }

    public void pressButton() {
        command.execute();
    }

    public void pressUndo() {
        command.undo();
    }
}

// Step 5: Test the Command Pattern
public class CommandPatternDemo {
    public static void main(String[] args) {
        // Create the receiver
        Light livingRoomLight = new Light();

        // Create command objects
        Command lightOn = new LightOnCommand(livingRoomLight);
        Command lightOff = new LightOffCommand(livingRoomLight);

        // Create the invoker
        RemoteControl remote = new RemoteControl();

        // Turn the light ON
        remote.setCommand(lightOn);
        remote.pressButton();

        // Turn the light OFF
        remote.setCommand(lightOff);
        remote.pressButton();

        // Undo the last action (turn the light ON again)
        remote.pressUndo();
    }
}
```

---

### Explanation:
1. **`Command` Interface**:
   - Defines the common methods (`execute` and `undo`) for all commands.
2. **Concrete Commands (`LightOnCommand`, `LightOffCommand`)**:
   - Implement the `Command` interface and encapsulate the logic for turning the light on and off.
3. **Receiver (`Light`)**:
   - Contains the actual business logic to perform the action.
4. **Invoker (`RemoteControl`)**:
   - Triggers commands using the `execute` method and can also reverse actions using `undo`.
5. **Client (`CommandPatternDemo`)**:
   - Configures the commands, receivers, and invokers.

---

### Output:
```
Light is ON
Light is OFF
Light is ON
```

---

### Use Cases:
- Implementing undo/redo functionality in text editors or drawing applications.
- Command-based queueing in task schedulers.
- Remote control systems for devices or appliances.

This pattern ensures that the sender doesn't need to know the specifics of the action being performed, making it highly extensible. 

## State

The **State Pattern** is a behavioral design pattern that allows an object to change its behavior when its internal state changes. It effectively implements a state machine where different states encapsulate specific behaviors, and the context delegates to the current state.

---

### Key Points:
1. Encapsulates state-specific behavior in separate classes.
2. Allows an object to alter its behavior dynamically as its state changes.
3. Promotes the Open/Closed Principle by allowing new states to be added without modifying existing code.

---

### Java Example:

Imagine a scenario where we have a vending machine, and it behaves differently depending on whether it is **Out of Stock**, **Accepting Payment**, or **Dispensing Item**.

---

#### Step-by-Step Implementation:

```java
// Step 1: Create the State interface
public interface State {
    void insertMoney();
    void dispenseItem();
}

// Step 2: Implement Concrete States
public class OutOfStockState implements State {
    public void insertMoney() {
        System.out.println("Cannot insert money. The machine is out of stock.");
    }

    public void dispenseItem() {
        System.out.println("Cannot dispense item. The machine is out of stock.");
    }
}

public class AcceptingPaymentState implements State {
    public void insertMoney() {
        System.out.println("Money inserted. You can now select an item.");
    }

    public void dispenseItem() {
        System.out.println("Please select an item before dispensing.");
    }
}

public class DispensingItemState implements State {
    public void insertMoney() {
        System.out.println("Item is being dispensed. Please wait.");
    }

    public void dispenseItem() {
        System.out.println("Dispensing your item. Thank you!");
    }
}

// Step 3: Create the Context class
public class VendingMachine {
    private State currentState;

    public VendingMachine() {
        // Default state is Out of Stock
        currentState = new OutOfStockState();
    }

    public void setState(State state) {
        this.currentState = state;
    }

    public void insertMoney() {
        currentState.insertMoney();
    }

    public void dispenseItem() {
        currentState.dispenseItem();
    }
}

// Step 4: Test the State Pattern
public class StatePatternDemo {
    public static void main(String[] args) {
        VendingMachine machine = new VendingMachine();

        // Out of stock
        machine.insertMoney();
        machine.dispenseItem();

        // Change state to Accepting Payment
        machine.setState(new AcceptingPaymentState());
        machine.insertMoney();
        machine.dispenseItem();

        // Change state to Dispensing Item
        machine.setState(new DispensingItemState());
        machine.insertMoney();
        machine.dispenseItem();
    }
}
```

---

### Explanation:
1. **State Interface (`State`)**:
   - Defines the common methods (`insertMoney` and `dispenseItem`) for all states.
2. **Concrete State Classes**:
   - **`OutOfStockState`**: Behavior when the machine is out of stock.
   - **`AcceptingPaymentState`**: Behavior when the machine is ready to accept money.
   - **`DispensingItemState`**: Behavior when the machine is dispensing an item.
3. **Context (`VendingMachine`)**:
   - Maintains the current state and delegates state-specific behavior to the current state object.
4. **Client (`StatePatternDemo`)**:
   - Manipulates the `VendingMachine` by changing its state and invoking methods.

---

### Output:
```
Cannot insert money. The machine is out of stock.
Cannot dispense item. The machine is out of stock.
Money inserted. You can now select an item.
Please select an item before dispensing.
Item is being dispensed. Please wait.
Dispensing your item. Thank you!
```

---

### Use Cases:
- **Workflow or State Machines**: Systems with well-defined state transitions, such as vending machines, elevators, or traffic lights.
- **Game Development**: Managing player states (e.g., idle, walking, attacking).
- **UI State Management**: Switching between different UI modes or states.

This pattern is particularly useful when an object’s behavior depends on its current state, and the state transitions are frequent. 