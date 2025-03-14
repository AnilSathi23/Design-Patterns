Java design patterns are best practices that developers use to solve common problems when designing software. These patterns provide reusable solutions and help ensure that code is robust, maintainable, and scalable. They fall into three main categories:

1. **Creational Patterns**: These deal with object creation, ensuring that objects are created in a controlled manner.
   - Example: Singleton, Factory, Builder, Prototype.

2. **Structural Patterns**: These deal with the composition of classes or objects to form larger structures.
   - Example: Adapter, Composite, Decorator, Proxy, Bridge.

3. **Behavioral Patterns**: These focus on the interaction and communication between objects.
   - Example: Observer, Strategy, Command, State.

Each pattern is designed to tackle a specific type of problem in software development. If you'd like, I can explain any of these patterns in detail or give you examples in Java code! Just let me know.

## Adapter 

The **Adapter Pattern**, also known as the **Wrapper Pattern**, is a structural design pattern that allows objects with incompatible interfaces to work together. It acts as a bridge between two classes by converting the interface of one class into another interface that a client expects.

### Key Points:
1. It is used when you have a class that doesn't match the interface you need.
2. It allows reusability of existing code without modifying it.
3. The adapter can be implemented using either class inheritance or object composition.

### Java Example:

Imagine you have a Media Player that only plays MP3 files, but you want to extend its functionality to play MP4 and VLC files. Here's how the Adapter Pattern can help:

```java
// Step 1: Create a target interface
public interface MediaPlayer {
    void play(String audioType, String fileName);
}

// Step 2: Create an existing class (Adaptee) with a different interface
public interface AdvancedMediaPlayer {
    void playVlc(String fileName);
    void playMp4(String fileName);
}

public class VlcPlayer implements AdvancedMediaPlayer {
    public void playVlc(String fileName) {
        System.out.println("Playing VLC file: " + fileName);
    }
    public void playMp4(String fileName) {
        // Do nothing
    }
}

public class Mp4Player implements AdvancedMediaPlayer {
    public void playVlc(String fileName) {
        // Do nothing
    }
    public void playMp4(String fileName) {
        System.out.println("Playing MP4 file: " + fileName);
    }
}

// Step 3: Create an adapter class that implements the target interface and uses the adaptee
public class MediaAdapter implements MediaPlayer {
    AdvancedMediaPlayer advancedMediaPlayer;

    public MediaAdapter(String audioType) {
        if (audioType.equalsIgnoreCase("vlc")) {
            advancedMediaPlayer = new VlcPlayer();
        } else if (audioType.equalsIgnoreCase("mp4")) {
            advancedMediaPlayer = new Mp4Player();
        }
    }

    public void play(String audioType, String fileName) {
        if (audioType.equalsIgnoreCase("vlc")) {
            advancedMediaPlayer.playVlc(fileName);
        } else if (audioType.equalsIgnoreCase("mp4")) {
            advancedMediaPlayer.playMp4(fileName);
        }
    }
}

// Step 4: Create the main class that uses the adapter
public class AudioPlayer implements MediaPlayer {
    MediaAdapter mediaAdapter;

    public void play(String audioType, String fileName) {
        if (audioType.equalsIgnoreCase("mp3")) {
            System.out.println("Playing MP3 file: " + fileName);
        } else if (audioType.equalsIgnoreCase("vlc") || audioType.equalsIgnoreCase("mp4")) {
            mediaAdapter = new MediaAdapter(audioType);
            mediaAdapter.play(audioType, fileName);
        } else {
            System.out.println("Invalid media type: " + audioType);
        }
    }
}

// Step 5: Test the Adapter Pattern
public class AdapterPatternDemo {
    public static void main(String[] args) {
        AudioPlayer audioPlayer = new AudioPlayer();

        audioPlayer.play("mp3", "song.mp3");
        audioPlayer.play("mp4", "movie.mp4");
        audioPlayer.play("vlc", "video.vlc");
        audioPlayer.play("avi", "unknown.avi");
    }
}
```

### Explanation:
1. **`MediaPlayer`** is the target interface expected by the client.
2. **`AdvancedMediaPlayer`**, with its concrete classes (`VlcPlayer` and `Mp4Player`), represents the incompatible interface.
3. **`MediaAdapter`** bridges the gap between `MediaPlayer` and `AdvancedMediaPlayer`, allowing the `AudioPlayer` to play MP4 and VLC files.
4. The client (`AdapterPatternDemo`) uses the `AudioPlayer` class, which internally leverages the adapter for unsupported media types.

### Output:
```
Playing MP3 file: song.mp3
Playing MP4 file: movie.mp4
Playing VLC file: video.vlc
Invalid media type: avi
```

This pattern is handy when integrating legacy systems or third-party APIs that have interfaces incompatible with your system. Let me know if you'd like further clarifications!

## Composite

The **Composite Pattern** is a structural design pattern that allows you to compose objects into tree-like structures to represent part-whole hierarchies. It lets clients interact with both individual objects and groups of objects in a uniform way. This pattern is often used in scenarios where you deal with a tree structure, like file systems or graphical user interfaces.

### Key Points:
1. You can treat individual objects (leaf nodes) and compositions of objects (composite nodes) uniformly.
2. Ideal for recursive structures like trees.
3. Simplifies client code by abstracting the distinction between single and composite objects.

### Java Example:

Let’s consider a scenario where we represent a company hierarchy (managers and employees) using the Composite Pattern.

```java
// Step 1: Create a Component interface
public interface Employee {
    void showDetails();
}

// Step 2: Create Leaf classes (individual objects)
public class Developer implements Employee {
    private String name;
    private String role;

    public Developer(String name, String role) {
        this.name = name;
        this.role = role;
    }

    @Override
    public void showDetails() {
        System.out.println("Developer: " + name + ", Role: " + role);
    }
}

public class Designer implements Employee {
    private String name;
    private String role;

    public Designer(String name, String role) {
        this.name = name;
        this.role = role;
    }

    @Override
    public void showDetails() {
        System.out.println("Designer: " + name + ", Role: " + role);
    }
}

// Step 3: Create a Composite class (group of objects)
import java.util.ArrayList;
import java.util.List;

public class Manager implements Employee {
    private String name;
    private List<Employee> employees;

    public Manager(String name) {
        this.name = name;
        this.employees = new ArrayList<>();
    }

    public void addEmployee(Employee employee) {
        employees.add(employee);
    }

    public void removeEmployee(Employee employee) {
        employees.remove(employee);
    }

    @Override
    public void showDetails() {
        System.out.println("Manager: " + name);
        for (Employee emp : employees) {
            emp.showDetails();
        }
    }
}

// Step 4: Test the Composite Pattern
public class CompositePatternDemo {
    public static void main(String[] args) {
        // Create leaf objects
        Employee dev1 = new Developer("Alice", "Frontend Developer");
        Employee dev2 = new Developer("Bob", "Backend Developer");
        Employee designer = new Designer("Charlie", "UI/UX Designer");

        // Create a composite object (Manager)
        Manager manager = new Manager("David");
        manager.addEmployee(dev1);
        manager.addEmployee(dev2);
        manager.addEmployee(designer);

        // Display the hierarchy
        System.out.println("Company Hierarchy:");
        manager.showDetails();
    }
}
```

### Explanation:
1. **Component Interface (`Employee`)**: Defines a common interface for both leaf and composite objects.
2. **Leaf Classes (`Developer`, `Designer`)**: Represent individual objects that cannot contain other objects.
3. **Composite Class (`Manager`)**: Represents a group of objects, which can include both leaf and other composite objects.
4. **Client (`CompositePatternDemo`)**: Treats both leaf and composite objects uniformly using the `Employee` interface.

### Output:
```
Company Hierarchy:
Manager: David
Developer: Alice, Role: Frontend Developer
Developer: Bob, Role: Backend Developer
Designer: Charlie, Role: UI/UX Designer
```

This example demonstrates how the Composite Pattern helps manage hierarchical structures while keeping the client code simple. Let me know if you'd like additional examples or clarification!

## Decorator

The **Decorator Pattern** is a structural design pattern that allows you to add new behaviors or responsibilities to an object dynamically, without altering its structure. This pattern is particularly useful when you want to extend the functionality of a class in a flexible and reusable way.

### Key Points:
1. Composed of a base component, concrete components, and decorators.
2. Decorators wrap components, adding extra behavior while still conforming to the component's interface.
3. Can be used to add or modify behaviors dynamically.

### Java Example:

Imagine a scenario where you want to extend a basic coffee with additional features like milk or sugar.

```java
// Step 1: Create the base component interface
public interface Coffee {
    String getDescription();
    double getCost();
}

// Step 2: Create a concrete component
public class BasicCoffee implements Coffee {
    @Override
    public String getDescription() {
        return "Basic Coffee";
    }

    @Override
    public double getCost() {
        return 5.0; // Base cost of coffee
    }
}

// Step 3: Create an abstract decorator class
public abstract class CoffeeDecorator implements Coffee {
    protected Coffee coffee;

    public CoffeeDecorator(Coffee coffee) {
        this.coffee = coffee;
    }

    @Override
    public String getDescription() {
        return coffee.getDescription();
    }

    @Override
    public double getCost() {
        return coffee.getCost();
    }
}

// Step 4: Create concrete decorators for additional functionalities
public class MilkDecorator extends CoffeeDecorator {
    public MilkDecorator(Coffee coffee) {
        super(coffee);
    }

    @Override
    public String getDescription() {
        return coffee.getDescription() + ", Milk";
    }

    @Override
    public double getCost() {
        return coffee.getCost() + 1.5; // Cost of milk
    }
}

public class SugarDecorator extends CoffeeDecorator {
    public SugarDecorator(Coffee coffee) {
        super(coffee);
    }

    @Override
    public String getDescription() {
        return coffee.getDescription() + ", Sugar";
    }

    @Override
    public double getCost() {
        return coffee.getCost() + 0.5; // Cost of sugar
    }
}

// Step 5: Test the Decorator Pattern
public class DecoratorPatternDemo {
    public static void main(String[] args) {
        // Start with a basic coffee
        Coffee basicCoffee = new BasicCoffee();

        // Add milk
        Coffee milkCoffee = new MilkDecorator(basicCoffee);

        // Add sugar
        Coffee sugarMilkCoffee = new SugarDecorator(milkCoffee);

        // Display the description and cost
        System.out.println("Description: " + sugarMilkCoffee.getDescription());
        System.out.println("Cost: $" + sugarMilkCoffee.getCost());
    }
}
```

### Explanation:
1. **`Coffee`** is the base interface, defining the core functionality.
2. **`BasicCoffee`** is the concrete component that implements the base functionality.
3. **`CoffeeDecorator`** is the abstract class that wraps a `Coffee` object and provides the foundation for adding new behavior.
4. **`MilkDecorator`** and **`SugarDecorator`** are the concrete decorators that extend the functionality of the `Coffee` dynamically.

### Output:
```
Description: Basic Coffee, Milk, Sugar
Cost: $7.0
```

This pattern provides a flexible and reusable way to add new features to an object without modifying its existing code. Let me know if you'd like further clarifications or another example!

## Proxy

The **Proxy Pattern** is a structural design pattern that provides a surrogate or placeholder for another object to control access to it. This is especially useful for resource-heavy or sensitive operations where direct access to the object needs to be restricted, delayed, or controlled.

### Key Points:
1. The proxy object acts as a substitute or intermediary for the real object.
2. Common use cases include lazy initialization, access control, logging, and remote method invocation.
3. Types of proxies include:
   - **Virtual Proxy**: Controls access to a resource-intensive object.
   - **Protection Proxy**: Manages access rights to the real object.
   - **Remote Proxy**: Represents an object in a different address space.

---

### Java Example:

Let’s consider a scenario where we want to control access to a resource-intensive object that loads a large image file. We'll use a proxy to avoid loading the image until it's actually needed.

#### Step-by-Step Implementation

1. **Create an interface** for the real object and the proxy to implement.
2. **Create the Real Subject** class that performs the actual work.
3. **Create the Proxy Class** that controls access to the Real Subject.

#### Code Example:

```java
// Step 1: Define the Subject interface
public interface Image {
    void display();
}

// Step 2: Implement the Real Subject (expensive object)
public class RealImage implements Image {
    private String fileName;

    public RealImage(String fileName) {
        this.fileName = fileName;
        loadImageFromDisk(); // Resource-intensive operation
    }

    private void loadImageFromDisk() {
        System.out.println("Loading image from disk: " + fileName);
    }

    @Override
    public void display() {
        System.out.println("Displaying image: " + fileName);
    }
}

// Step 3: Implement the Proxy Class
public class ProxyImage implements Image {
    private RealImage realImage;
    private String fileName;

    public ProxyImage(String fileName) {
        this.fileName = fileName;
    }

    @Override
    public void display() {
        if (realImage == null) {
            // Lazy initialization: load the real image only when needed
            realImage = new RealImage(fileName);
        }
        realImage.display();
    }
}

// Step 4: Test the Proxy Pattern
public class ProxyPatternDemo {
    public static void main(String[] args) {
        // Create a ProxyImage object
        Image image = new ProxyImage("test_image.jpg");

        // Image is not loaded yet
        System.out.println("First call to display:");
        image.display(); // Loads and displays the image

        // Image is already loaded
        System.out.println("\nSecond call to display:");
        image.display(); // Displays the already loaded image
    }
}
```

---

### Explanation:

1. **`Image` Interface**: Defines the common operations (`display`) for both the proxy and the real object.
2. **`RealImage` Class**: Represents the real object that performs the resource-intensive operation of loading an image from the disk.
3. **`ProxyImage` Class**: Acts as a placeholder and controls access to `RealImage`. It defers loading the image until it's required (lazy initialization).
4. **Client (`ProxyPatternDemo`)**: Interacts with the `Image` interface, unaware of whether it's dealing with a proxy or the real object.

---

### Output:
```
First call to display:
Loading image from disk: test_image.jpg
Displaying image: test_image.jpg

Second call to display:
Displaying image: test_image.jpg
```

### Use Cases:
- **Virtual Proxy**: Managing heavy initialization, as shown in the example.
- **Protection Proxy**: Restricting access based on permissions.
- **Remote Proxy**: Invoking methods on objects in another address space (e.g., RMI in Java).

## Bridge

The **Bridge Pattern** is a structural design pattern that separates an abstraction from its implementation, allowing the two to vary independently. It is particularly useful when you want to avoid a permanent binding between abstraction and its implementation or when changes in either should not affect the other.

### Key Points:
1. **Decouples abstraction and implementation**: The abstraction defines high-level control, and the implementation provides the low-level details.
2. **Improves extensibility**: You can add new abstractions and implementations independently.
3. **Promotes flexibility**: Allows switching between different implementations at runtime.

### Java Example:

Let’s consider a scenario where we have different types of shapes (like Circle and Rectangle) and each shape can have different colors (like Red and Blue).

#### Step-by-Step Implementation

```java
// Step 1: Define the Implementor interface (Bridge)
public interface Color {
    void applyColor();
}

// Step 2: Create Concrete Implementors
public class RedColor implements Color {
    @Override
    public void applyColor() {
        System.out.println("Applying Red Color");
    }
}

public class BlueColor implements Color {
    @Override
    public void applyColor() {
        System.out.println("Applying Blue Color");
    }
}

// Step 3: Define the Abstraction
public abstract class Shape {
    protected Color color; // Bridge to the Implementor

    public Shape(Color color) {
        this.color = color;
    }

    abstract void draw();
}

// Step 4: Create Refined Abstractions
public class Circle extends Shape {
    public Circle(Color color) {
        super(color);
    }

    @Override
    public void draw() {
        System.out.print("Drawing Circle with ");
        color.applyColor();
    }
}

public class Rectangle extends Shape {
    public Rectangle(Color color) {
        super(color);
    }

    @Override
    public void draw() {
        System.out.print("Drawing Rectangle with ");
        color.applyColor();
    }
}

// Step 5: Test the Bridge Pattern
public class BridgePatternDemo {
    public static void main(String[] args) {
        // Create objects with different abstraction-implementation combinations
        Shape redCircle = new Circle(new RedColor());
        Shape blueRectangle = new Rectangle(new BlueColor());

        // Draw the shapes
        redCircle.draw();
        blueRectangle.draw();
    }
}
```

---

### Explanation:

1. **`Color` Interface**: Acts as the bridge interface to connect different colors.
2. **Concrete Implementors (`RedColor`, `BlueColor`)**: Provide specific implementations of the `Color` interface.
3. **`Shape` Abstract Class**: Represents the abstraction and uses a `Color` object to delegate color-related functionality.
4. **Refined Abstractions (`Circle`, `Rectangle`)**: Extend the abstraction and provide specific details for different types of shapes.
5. **Client (`BridgePatternDemo`)**: Combines abstractions with implementations and uses them interchangeably.

---

### Output:
```
Drawing Circle with Applying Red Color
Drawing Rectangle with Applying Blue Color
```

### Use Cases:
- When you want to decouple an abstraction from its implementation.
- When there are multiple dimensions of variations (e.g., shapes and colors).
- When you need to switch between implementations dynamically.

This pattern is especially useful in scenarios with complex systems requiring flexibility.


