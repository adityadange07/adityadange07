**Comprehensive list of the Top 100 Core Java Interview Questions**, ideal for someone with **3–5 years of hands-on experience**. These questions cover everything from **OOPs, Collections, Multithreading, Exception Handling, Memory Management, Java 8 features**, and more.

---

## ✅ Top 100 Core Java Interview Questions
**[For 3–5 Years Experienced Java Developers]**

---

### 🔹 1–15: **OOPs Concepts & Basics**

## 1. What are the main principles of Object-Oriented Programming?

The **main principles of Object-Oriented Programming (OOP)** are a foundational framework for designing and structuring software using objects—entities that combine data and behavior. There are four core principles, often referred to as the "pillars" of OOP: **Encapsulation**, **Abstraction**, **Inheritance**, and **Polymorphism**. Here’s a clear explanation of each:

---

### 1. **Encapsulation**
- **Definition**: Encapsulation is the bundling of data (attributes) and the methods (functions) that operate on that data into a single unit, called an object, while restricting direct access to some of its components.
- **Key Idea**: Hide the internal details and expose only what’s necessary through a controlled interface (e.g., getters and setters).
- **How It Works**:
    - Use access modifiers (e.g., `private`, `public`) to protect data.
    - Objects manage their own state, preventing external code from messing with it directly.
- **Example**:
  ```java
  class BankAccount {
      private double balance; // Hidden from outside
      public void deposit(double amount) {
          if (amount > 0) balance += amount;
      }
      public double getBalance() {
          return balance;
      }
  }
  ```
    - You can’t touch `balance` directly; you must use `deposit()` or `getBalance()`.
- **Benefit**: Improves security, reduces complexity, and prevents unintended interference.

---

### 2. **Abstraction**
- **Definition**: Abstraction is the process of simplifying complex systems by exposing only the essential features while hiding the underlying implementation details.
- **Key Idea**: Provide a high-level view or interface without revealing "how it works."
- **How It Works**:
    - Use abstract classes or interfaces to define what an object can do, not how it does it.
    - Users interact with the abstraction, not the nitty-gritty.
- **Example**:
  ```java
  abstract class Shape {
      abstract double area(); // What to do
  }
  class Circle extends Shape {
      private double radius;
      double area() { return Math.PI * radius * radius; } // How it’s done
  }
  ```
    - You call `area()` without knowing the formula details.
- **Benefit**: Reduces complexity, improves maintainability, and allows flexibility in implementation.

---

### 3. **Inheritance**
- **Definition**: Inheritance is a mechanism where one class (child/subclass) inherits properties and behaviors (fields and methods) from another class (parent/superclass).
- **Key Idea**: Reuse and extend existing code to create hierarchical relationships.
- **How It Works**:
    - A subclass inherits from a superclass using keywords like `extends` (Java) or `:` (Python).
    - The child can override or add to the parent’s functionality.
- **Example**:
  ```java
  class Animal {
      void eat() { System.out.println("Eating..."); }
  }
  class Dog extends Animal {
      void bark() { System.out.println("Woof!"); }
  }
  ```
    - `Dog` inherits `eat()` and adds `bark()`.
- **Benefit**: Promotes code reuse, reduces redundancy, and models real-world "is-a" relationships (e.g., a Dog is an Animal).

---

### 4. **Polymorphism**
- **Definition**: Polymorphism allows objects of different classes to be treated as objects of a common superclass, enabling one interface to represent multiple forms or behaviors.
- **Key Idea**: "Many forms"—same method call, different outcomes based on the object type.
- **Types**:
    1. **Compile-Time (Overloading)**: Multiple methods with the same name but different parameters.
    2. **Run-Time (Overriding)**: Subclass provides a specific implementation of a superclass method.
- **Example**:
  ```java
  class Animal {
      void sound() { System.out.println("Some sound"); }
  }
  class Cat extends Animal {
      void sound() { System.out.println("Meow"); } // Overrides
  }
  Animal myPet = new Cat();
  myPet.sound(); // Outputs "Meow" (run-time polymorphism)
  ```
- **Benefit**: Increases flexibility, allows generic coding, and supports extensibility.

---

### **How They Work Together**
- **Encapsulation** protects a `Car` object’s `speed` variable, exposing it only via `getSpeed()`.
- **Abstraction** lets you call `drive()` on any `Vehicle` without knowing if it’s a `Car` or `Truck`.
- **Inheritance** lets `ElectricCar` inherit `Car`’s `drive()` method and add `chargeBattery()`.
- **Polymorphism** lets you call `start()` on a `Vehicle` reference, and `ElectricCar` runs its own version.

---

### **Why They Matter**
- **Modularity**: Break code into manageable, reusable objects.
- **Maintainability**: Easier to update or extend encapsulated, abstracted code.
- **Flexibility**: Polymorphism and inheritance adapt to changing requirements.
- **Real-World Modeling**: OOP mirrors how we think (e.g., a "Dog" as an "Animal").

These principles are implemented in languages like Java, C++, Python, and C#, and they’re fundamental to building robust, scalable software—whether it’s running on AWS or anywhere else!

---

## 2. What is the difference between abstraction and encapsulation?

**Abstraction** and **encapsulation** are two core principles of Object-Oriented Programming (OOP), and while they’re related and often work together, they serve distinct purposes. Here’s a clear breakdown of the differences:

---

### **Abstraction**
- **Definition**: Abstraction is the process of simplifying complex reality by exposing only the essential features of an object or system while hiding the unnecessary implementation details.
- **Purpose**: Focus on *what* an object does, not *how* it does it—think of it as providing a high-level interface.
- **Key Idea**: Reduce complexity by showing only the "big picture" to the user.
- **How It’s Achieved**:
    - Using **abstract classes** or **interfaces** to define a contract (what methods are available).
    - Hides internal logic from the outside world.
- **Example**:
  ```java
  abstract class Shape {
      abstract double area(); // User knows it calculates area, not how
  }
  class Rectangle extends Shape {
      private double length, width;
      double area() { return length * width; } // Details hidden
  }
  ```
    - You call `area()` without needing to know the formula.
- **Real-World Analogy**: A car driver uses the steering wheel (interface) without understanding the engine mechanics (implementation).
- **Focus**: External usability and simplification.

---

### **Encapsulation**
- **Definition**: Encapsulation is the bundling of data (attributes) and methods (functions) into a single unit (an object), while restricting direct access to some of that data to protect it from external interference.
- **Purpose**: Control *how* an object’s internal state is accessed or modified—think of it as data protection.
- **Key Idea**: Hide the internal workings and expose only a controlled interface (e.g., getters/setters).
- **How It’s Achieved**:
    - Using **access modifiers** like `private`, `protected`, and `public`.
    - Providing methods to interact with private data.
- **Example**:
  ```java
  class BankAccount {
      private double balance; // Data hidden
      public void deposit(double amount) {
          if (amount > 0) balance += amount; // Controlled access
      }
      public double getBalance() {
          return balance; // Read-only access
      }
  }
  ```
    - You can’t directly change `balance`; you must use `deposit()` or `getBalance()`.
- **Real-World Analogy**: A medicine capsule hides the ingredients inside; you consume it via the outer shell (interface).
- **Focus**: Internal security and integrity.

---

### **Key Differences**
| **Aspect**            | **Abstraction**                  | **Encapsulation**               |
|-----------------------|----------------------------------|---------------------------------|
| **Definition**        | Hiding complexity, showing essentials | Bundling data and methods, restricting access |
| **Purpose**           | Simplify interaction            | Protect data and control access |
| **Focus**             | What the object does            | How the object’s data is managed |
| **Mechanism**         | Abstract classes, interfaces    | Access modifiers, getters/setters |
| **Hides**             | Implementation details          | Data and internal state         |
| **Example**           | `area()` method in `Shape`      | `private balance` in `BankAccount` |
| **Outcome**           | User-friendly interface         | Secure, maintainable object     |

---

### **How They Relate**
- **Complementary**: Abstraction often relies on encapsulation to hide details. For example, an abstract `Shape` class uses encapsulation to hide `length` and `width` in `Rectangle`.
- **Teamwork Example**:
  ```java
  abstract class Machine {
      abstract void start(); // Abstraction: what it does
  }
  class CoffeeMaker extends Machine {
      private int waterLevel; // Encapsulation: hide data
      public void start() {
          if (waterLevel > 0) System.out.println("Brewing...");
      }
      public void setWaterLevel(int level) {
          if (level >= 0) waterLevel = level;
      }
  }
  ```
    - Abstraction: `start()` defines the behavior without revealing how.
    - Encapsulation: `waterLevel` is private, accessed only via `setWaterLevel()`.

---

### **Why It Matters**
- **Abstraction**: Lets developers work with systems at a high level (e.g., call `drive()` on a `Car` without knowing engine specifics).
- **Encapsulation**: Prevents misuse (e.g., setting a negative `balance`) and keeps code maintainable.

In short, **abstraction** is about simplifying the *interface* for the user, while **encapsulation** is about protecting the *internals* of the object. Together, they make OOP modular, secure, and user-friendly!

---

## 3. What is inheritance in Java? How does it work?

Inheritance in Java is a fundamental object-oriented programming concept that allows one class to inherit properties and behaviors (fields and methods) from another class. It promotes code reusability and establishes a relationship between classes, often described as an "is-a" relationship. For example, a "Dog" class can inherit from an "Animal" class because a dog *is an* animal.

### How Inheritance Works in Java
1. **Parent and Child Classes**:
  - The class being inherited from is called the *superclass* (or parent class).
  - The class that inherits is called the *subclass* (or child class).
  - Java uses the `extends` keyword to implement inheritance.

2. **Syntax**:
   ```java
   class Superclass {
       // Fields and methods
   }

   class Subclass extends Superclass {
       // Subclass can add its own fields and methods
       // It also inherits fields and methods from Superclass
   }
   ```

3. **Key Features**:
  - **Access to Superclass Members**: The subclass inherits all *public* and *protected* members (fields and methods) of the superclass. *Private* members are not directly accessible but can be accessed indirectly via public or protected methods (e.g., getters/setters).
  - **Method Overriding**: A subclass can provide its own implementation of an inherited method by overriding it. This is done using the same method name, return type, and parameters, optionally with the `@Override` annotation.
  - **Single Inheritance**: Java supports only single inheritance for classes, meaning a subclass can extend only one superclass. However, multiple inheritance can be achieved through interfaces.

4. **The `super` Keyword**:
  - Used to refer to the immediate superclass.
  - `super()` calls the superclass's constructor.
  - `super.methodName()` invokes a superclass method.

### Example
```java
// Superclass
class Animal {
    String name;

    // Constructor
    public Animal(String name) {
        this.name = name;
    }

    public void eat() {
        System.out.println(name + " is eating.");
    }
}

// Subclass
class Dog extends Animal {
    public Dog(String name) {
        super(name); // Call superclass constructor
    }

    // Override the eat method
    @Override
    public void eat() {
        System.out.println(name + " is eating bones.");
    }

    // Subclass-specific method
    public void bark() {
        System.out.println(name + " is barking.");
    }
}

// Main class to test inheritance
public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog("Rex");
        dog.eat();  // Output: Rex is eating bones.
        dog.bark(); // Output: Rex is barking.
    }
}
```

### How It Works in This Example
- The `Dog` class inherits the `name` field and `eat()` method from `Animal`.
- The `Dog` class overrides `eat()` to provide a specific implementation.
- The `bark()` method is unique to `Dog` and not present in `Animal`.
- When `dog.eat()` is called, the overridden method in `Dog` executes instead of the one in `Animal`.

### Types of Inheritance in Java
1. **Single Inheritance**: One class extends another (e.g., `Dog extends Animal`).
2. **Multilevel Inheritance**: A chain of inheritance (e.g., `Puppy extends Dog`, `Dog extends Animal`).
3. **Hierarchical Inheritance**: Multiple classes inherit from one superclass (e.g., `Dog` and `Cat` extend `Animal`).
  - **Note**: Java does not support *multiple inheritance* of classes (e.g., a class extending two superclasses) to avoid complexity and ambiguity, but interfaces can simulate this.

### Important Points
- Every class in Java implicitly inherits from the `Object` class, which is the root of the class hierarchy.
- Constructors are not inherited, but they can be invoked using `super()`.
- The `final` keyword can be used to prevent a class from being inherited (e.g., `final class Animal`).

Inheritance in Java allows for modular, reusable, and maintainable code by letting subclasses build upon or specialize the functionality of superclasses.

---

## 4. What is method overloading and method overriding?

In Java, **method overloading** and **method overriding** are two distinct concepts related to how methods are defined and used in classes. They both involve methods with similar names but differ in purpose, implementation, and context. Here's a detailed explanation of each:

---

### **Method Overloading**
Method overloading allows a class to have multiple methods with the **same name** but **different parameter lists**. It is a form of *compile-time polymorphism* (also called static polymorphism), meaning the method to be called is determined at compile time based on the method signature.

#### Key Features:
- **Same Method Name**: The methods must share the same name.
- **Different Parameters**: They must differ in the number, type, or order of parameters.
- **Return Type**: The return type can be the same or different; it doesn’t affect overloading.
- **Purpose**: Provides flexibility by allowing different ways to call a method based on input.

#### Example:
```java
class Calculator {
    // Method with one integer parameter
    public int add(int a) {
        return a + 10;
    }

    // Overloaded method with two integer parameters
    public int add(int a, int b) {
        return a + b;
    }

    // Overloaded method with double parameters
    public double add(double a, double b) {
        return a + b;
    }
}

public class Main {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println(calc.add(5));         // Output: 15
        System.out.println(calc.add(3, 4));     // Output: 7
        System.out.println(calc.add(2.5, 3.5)); // Output: 6.0
    }
}
```

#### How It Works:
- The compiler decides which `add` method to call based on the number and type of arguments passed.
- Overloading happens within the **same class**.

#### Rules:
- Changing only the return type isn’t enough for overloading; the parameter list must differ.
- Method overloading can also apply to constructors.

---

### **Method Overriding**
Method overriding occurs when a subclass provides a **specific implementation** of a method that is already defined in its superclass. It is a form of *runtime polymorphism* (also called dynamic polymorphism), meaning the method to be executed is determined at runtime based on the object’s actual type.

#### Key Features:
- **Same Method Signature**: The method in the subclass must have the same name, return type, and parameter list as the method in the superclass.
- **Inheritance Required**: Overriding happens between a superclass and a subclass.
- **Purpose**: Allows a subclass to customize or extend the behavior of the superclass method.
- **Annotation**: The `@Override` annotation is optional but recommended for clarity and error checking.

#### Example:
```java
class Animal {
    public void sound() {
        System.out.println("Some generic animal sound");
    }
}

class Dog extends Animal {
    @Override
    public void sound() {
        System.out.println("Woof Woof");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Animal();
        Animal myDog = new Dog(); // Polymorphism: Reference type Animal, object type Dog

        myAnimal.sound(); // Output: Some generic animal sound
        myDog.sound();   // Output: Woof Woof
    }
}
```

#### How It Works:
- The `Dog` class overrides the `sound()` method from `Animal`.
- When `sound()` is called on a `Dog` object, the overridden method in `Dog` executes, even if the reference type is `Animal`.
- The JVM determines the method to call at runtime based on the actual object type.

#### Rules:
- The method must be inherited from the superclass (cannot override `private` methods).
- The access level in the subclass cannot be more restrictive (e.g., cannot override a `public` method as `protected`).
- The return type must be the same or a *covariant* return type (a subclass of the original return type, introduced in Java 5).
- The `final` keyword on a method prevents it from being overridden.
- The `static` methods cannot be overridden (they can be redefined, but that’s not overriding).

---

### **Key Differences**
| Feature                | Method Overloading                          | Method Overriding                          |
|------------------------|---------------------------------------------|--------------------------------------------|
| **Definition**         | Multiple methods with same name, different parameters | Subclass redefines a superclass method     |
| **Polymorphism Type**  | Compile-time (static)                       | Runtime (dynamic)                          |
| **Class Relationship** | Occurs within the same class                | Occurs between superclass and subclass     |
| **Method Signature**   | Must differ (parameters)                    | Must be the same                           |
| **Return Type**        | Can differ                                  | Must be the same or covariant              |
| **Purpose**            | Flexibility in method usage                 | Specialization of inherited behavior       |
| **Keyword**            | No special keyword                          | `@Override` (optional but recommended)     |

---

### Combined Example:
```java
class Printer {
    // Overloaded methods
    public void print(String text) {
        System.out.println("Text: " + text);
    }

    public void print(int number) {
        System.out.println("Number: " + number);
    }
}

class AdvancedPrinter extends Printer {
    // Overriding the print(String) method
    @Override
    public void print(String text) {
        System.out.println("Advanced Print: " + text.toUpperCase());
    }
}

public class Main {
    public static void main(String[] args) {
        Printer printer = new Printer();
        AdvancedPrinter advPrinter = new AdvancedPrinter();

        printer.print("Hello");    // Output: Text: Hello
        printer.print(42);        // Output: Number: 42
        advPrinter.print("Hello"); // Output: Advanced Print: HELLO
        advPrinter.print(42);     // Output: Number: 42 (inherited, not overridden)
    }
}
```

- `Printer` demonstrates overloading with two `print` methods.
- `AdvancedPrinter` overrides the `print(String)` method but inherits `print(int)` unchanged.

In summary, **overloading** provides multiple ways to use a method name within a class, while **overriding** allows a subclass to redefine a superclass method for specific behavior. Both enhance flexibility and reusability in Java programming.

---

## 5. What is polymorphism? Explain with an example.

In Java, **polymorphism** is a core object-oriented programming concept that allows objects of different classes to be treated as objects of a common type. The term "polymorphism" comes from Greek, meaning "many forms," and it enables a single interface or method to work with different types of data or objects. It promotes flexibility and extensibility in code.

Polymorphism in Java is primarily achieved through **inheritance** and **method overriding**, and it manifests as **runtime polymorphism** (dynamic polymorphism) or **compile-time polymorphism** (static polymorphism via method overloading). Here, I'll focus on runtime polymorphism, as it’s the most commonly associated form with the term.

---

### How Polymorphism Works
- **Superclass Reference, Subclass Object**: A reference variable of a superclass type can refer to an object of any subclass type.
- **Method Overriding**: At runtime, the JVM determines which method to execute based on the actual object type, not the reference type.
- This is facilitated by **dynamic method dispatch**, where the overridden method in the subclass is called.

---

### Key Features
- **Type Compatibility**: A subclass "is-a" type of its superclass.
- **Runtime Decision**: The method to be invoked is decided at runtime based on the object’s actual type.
- **Code Reusability**: Polymorphism allows you to write generic code that works with multiple types.

---

### Example of Runtime Polymorphism
```java
// Superclass
class Animal {
    public void sound() {
        System.out.println("This is a generic animal sound.");
    }
}

// Subclass 1
class Dog extends Animal {
    @Override
    public void sound() {
        System.out.println("Woof Woof");
    }
}

// Subclass 2
class Cat extends Animal {
    @Override
    public void sound() {
        System.out.println("Meow Meow");
    }
}

// Main class to demonstrate polymorphism
public class Main {
    public static void main(String[] args) {
        // Superclass reference, different subclass objects
        Animal myAnimal;

        myAnimal = new Animal(); // Animal object
        myAnimal.sound();        // Output: This is a generic animal sound.

        myAnimal = new Dog();    // Dog object
        myAnimal.sound();        // Output: Woof Woof

        myAnimal = new Cat();    // Cat object
        myAnimal.sound();        // Output: Meow Meow

        // Array of Animal references
        Animal[] animals = {new Dog(), new Cat(), new Animal()};
        for (Animal animal : animals) {
            animal.sound();      // Calls the appropriate overridden method
        }
    }
}
```

#### Output:
```
This is a generic animal sound.
Woof Woof
Meow Meow
Woof Woof
Meow Meow
This is a generic animal sound.
```

---

### Explanation of the Example
1. **Class Hierarchy**:
  - `Animal` is the superclass with a `sound()` method.
  - `Dog` and `Cat` are subclasses that override the `sound()` method with their specific implementations.

2. **Polymorphic Behavior**:
  - The variable `myAnimal` is of type `Animal` (the superclass), but it can hold references to `Dog`, `Cat`, or `Animal` objects.
  - When `sound()` is called on `myAnimal`, the JVM checks the actual object type (`Dog`, `Cat`, or `Animal`) and invokes the overridden method from that class.

3. **Array Example**:
  - The `Animal[]` array holds objects of different types (`Dog`, `Cat`, `Animal`).
  - The loop calls `sound()` on each object, and the correct overridden method executes based on the object’s type, not the array’s reference type.

---

### Types of Polymorphism in Java
1. **Runtime Polymorphism (Dynamic)**:
  - Achieved through method overriding and inheritance (as shown in the example above).
  - The method call is resolved at runtime via the object’s actual type.

2. **Compile-time Polymorphism (Static)**:
  - Achieved through **method overloading** or **operator overloading** (though Java doesn’t support user-defined operator overloading).
  - Example: Multiple methods with the same name but different parameters (e.g., `add(int a)` and `add(int a, int b)`).
  - Resolved at compile time based on the method signature.

---

### Benefits of Polymorphism
- **Flexibility**: Write code that works with a superclass type and handles any subclass without modification.
- **Extensibility**: Easily add new subclasses without changing existing code (e.g., adding a `Bird` class with `sound()` as "Chirp Chirp").
- **Abstraction**: Focus on what an object does (e.g., `sound()`) rather than what it is (`Dog`, `Cat`).

---

### Real-World Analogy
Think of a remote control (superclass) that works with different devices (subclasses like TV, DVD player, etc.). You press the "play" button (method), and the action depends on the device (overridden behavior), but the interface remains the same.

In summary, polymorphism in Java allows a single method call to behave differently based on the object it’s invoked on, making it a powerful tool for building scalable and maintainable systems. The example above demonstrates runtime polymorphism using inheritance and method overriding.

---

## 6. What is the difference between static and non-static methods?

In Java, the difference between **static methods** and **non-static methods** (also called instance methods) lies in how they are associated with a class or its objects, how they are invoked, and their behavior. Here's a detailed comparison:

---

### **Static Methods**
- **Definition**: A static method belongs to the class itself rather than to any specific object of the class. It is defined using the `static` keyword.
- **Association**: Tied to the class, not an instance.
- **Invocation**: Called using the class name (e.g., `ClassName.methodName()`) without needing to create an object. However, it can also be called via an object reference (though this is discouraged for clarity).
- **Memory**: Exists in the class’s memory space and is loaded when the class is loaded by the JVM.
- **Access**: Can only directly access **static variables** and other **static methods** of the class. To access non-static members, an object must be created.

#### Example:
```java
class MathUtils {
    // Static variable
    static int counter = 0;

    // Static method
    public static int add(int a, int b) {
        counter++;
        return a + b;
    }
}

public class Main {
    public static void main(String[] args) {
        // Call static method using class name
        int result = MathUtils.add(3, 4);
        System.out.println("Result: " + result);           // Output: Result: 7
        System.out.println("Counter: " + MathUtils.counter); // Output: Counter: 1
    }
}
```

---

### **Non-Static Methods (Instance Methods)**
- **Definition**: A non-static method belongs to an instance (object) of the class and operates on the instance’s data.
- **Association**: Tied to a specific object of the class.
- **Invocation**: Called using an object reference (e.g., `objectName.methodName()`). You must create an instance of the class first.
- **Memory**: Exists only when an object is created, tied to that object’s memory space.
- **Access**: Can access both **static** and **non-static members** (fields and methods) of the class directly, including the instance’s own data via the `this` keyword.

#### Example:
```java
class Car {
    // Instance variable
    String color;

    // Constructor
    public Car(String color) {
        this.color = color;
    }

    // Non-static method
    public void displayColor() {
        System.out.println("Car color: " + color);
    }
}

public class Main {
    public static void main(String[] args) {
        // Create an object
        Car myCar = new Car("Red");
        // Call non-static method using object
        myCar.displayColor(); // Output: Car color: Red
    }
}
```

---

### **Key Differences**
| Feature                | Static Method                              | Non-Static Method                          |
|------------------------|--------------------------------------------|--------------------------------------------|
| **Keyword**            | Defined with `static`                      | No `static` keyword                        |
| **Belongs To**         | Class itself                               | Instance of the class                      |
| **Invocation**         | `ClassName.methodName()`                   | `objectName.methodName()`                  |
| **Object Requirement** | No object needed                           | Requires an object to be created           |
| **Access to Members**  | Can only access static members directly    | Can access both static and non-static members |
| **Memory Allocation**  | Loaded with the class (static memory)      | Tied to an object (heap memory)            |
| **Use of `this`**      | Cannot use `this` (no instance context)    | Can use `this` to refer to the current object |
| **Overriding**         | Cannot be overridden (class-specific)      | Can be overridden in subclasses            |
| **Example Use Case**   | Utility methods (e.g., `Math.sqrt()`)      | Object-specific behavior (e.g., `car.drive()`) |

---

### **Detailed Example Combining Both**
```java
class Example {
    static int staticCount = 0; // Static variable
    int instanceCount = 0;      // Instance variable

    // Static method
    public static void incrementStaticCount() {
        staticCount++;
        System.out.println("Static count: " + staticCount);
        // Cannot access instanceCount directly here
    }

    // Non-static method
    public void incrementInstanceCount() {
        instanceCount++;
        staticCount++; // Can access static members
        System.out.println("Instance count: " + instanceCount);
        System.out.println("Static count from instance: " + staticCount);
    }
}

public class Main {
    public static void main(String[] args) {
        // Call static method without an object
        Example.incrementStaticCount(); // Output: Static count: 1

        // Create objects
        Example obj1 = new Example();
        Example obj2 = new Example();

        // Call non-static method on objects
        obj1.incrementInstanceCount(); // Output: Instance count: 1, Static count: 2
        obj2.incrementInstanceCount(); // Output: Instance count: 1, Static count: 3

        // Static count is shared across all instances
        System.out.println("Final static count: " + Example.staticCount); // Output: 3
    }
}
```

---

### **Explanation of the Combined Example**
- **Static Method (`incrementStaticCount`)**:
  - Can only modify `staticCount` because it belongs to the class.
  - Doesn’t require an object and can’t access `instanceCount` directly.
- **Non-Static Method (`incrementInstanceCount`)**:
  - Operates on the specific object’s `instanceCount`.
  - Can also access and modify `staticCount` because static members are shared across all instances.
- **Behavior**:
  - `staticCount` is shared and increments with every call (static or instance method).
  - `instanceCount` is unique to each object (`obj1` and `obj2` have separate counts).

---

### **When to Use**
- **Static Methods**: Use for utility functions or operations that don’t depend on object state (e.g., `Math.max()`, `Arrays.sort()`).
- **Non-Static Methods**: Use for behaviors or operations tied to an object’s specific data (e.g., `toString()`, `setName()`).

In summary, static methods are class-level and don’t require an instance, while non-static methods are instance-level and operate on object-specific data. This distinction allows Java to support both class-wide utilities and object-oriented behaviors effectively.

---

## 7. Can a constructor be final, static, or abstract?

In Java, constructors have specific rules and characteristics that determine whether they can be declared with modifiers like `final`, `static`, or `abstract`. Let’s examine each case:

---

### **Can a Constructor Be `final`?**
- **No**, a constructor cannot be `final`.
- **Reason**: The `final` keyword in Java is used to prevent modification or overriding. For methods, it means they cannot be overridden by subclasses; for classes, it means they cannot be extended; and for variables, it means they cannot be reassigned. However, constructors are not inherited or overridden in the traditional sense—they are special methods invoked only when an object is created. Since there’s no concept of overriding a constructor in a subclass (subclasses call superclass constructors via `super()` but don’t override them), marking a constructor as `final` has no meaning and is not allowed.
- **Compiler Error**: If you try to declare a constructor as `final`, the Java compiler will throw an error like `illegal modifier for constructor; only public, protected, and private are permitted`.

#### Example (Invalid):
```java
class Test {
    final Test() { // Compiler error: illegal modifier
        System.out.println("Constructor");
    }
}
```

---

### **Can a Constructor Be `static`?**
- **No**, a constructor cannot be `static`.
- **Reason**: The `static` keyword ties a method or variable to the class itself rather than an instance. Constructors, however, are inherently tied to object creation—they initialize an instance of a class when the `new` keyword is used. A static constructor would imply it belongs to the class and doesn’t require an instance, which contradicts the purpose of a constructor. In Java, static initialization is handled by **static blocks** or static variable initializers, not constructors.
- **Alternative**: If you need class-level initialization, use a `static` block:
  ```java
  class Test {
      static int value;
      static {
          value = 10; // Static initialization
          System.out.println("Static block executed");
      }
  }
  ```
- **Compiler Error**: Declaring a constructor as `static` results in a compilation error like `modifier static not allowed here`.

#### Example (Invalid):
```java
class Test {
    static Test() { // Compiler error: illegal modifier
        System.out.println("Static constructor");
    }
}
```

---

### **Can a Constructor Be `abstract`?**
- **No**, a constructor cannot be `abstract`.
- **Reason**: The `abstract` keyword indicates that a method or class lacks an implementation and must be provided by a subclass. Constructors are not methods that can be overridden or implemented—they are special constructs for initializing objects. An `abstract` constructor would imply that it’s incomplete and needs to be defined in a subclass, but constructors are implicitly tied to instantiation. Moreover, an `abstract` class can have constructors (to initialize fields when a subclass is instantiated), but the constructor itself cannot be `abstract`.
- **Abstract Classes and Constructors**: An abstract class can have concrete constructors, which are called when a subclass object is created via `super()`. However, the constructor itself cannot be abstract.
- **Compiler Error**: Attempting to declare a constructor as `abstract` results in an error like `illegal modifier for constructor`.

#### Example (Invalid):
```java
abstract class Test {
    abstract Test(); // Compiler error: illegal modifier
}
```

#### Valid Example with Abstract Class:
```java
abstract class Animal {
    String name;

    // Concrete constructor in an abstract class
    public Animal(String name) {
        this.name = name;
    }
}

class Dog extends Animal {
    public Dog(String name) {
        super(name); // Calls the superclass constructor
    }
}
```

---

### **Summary**
| Modifier   | Can Be Used with Constructor? | Reason                                                                 |
|------------|-------------------------------|-----------------------------------------------------------------------|
| `final`    | No                            | Constructors are not inherited or overridden, so `final` is meaningless |
| `static`   | No                            | Constructors initialize instances, not classes; static doesn’t apply   |
| `abstract` | No                            | Constructors must be concrete for instantiation, not abstract          |

---

### **Allowed Modifiers for Constructors**
- Constructors can only have **access modifiers**: `public`, `protected`, `default` (package-private), or `private`.
- Example:
  ```java
  class Test {
      private Test() { // Private constructor (e.g., for singleton pattern)
          System.out.println("Private constructor");
      }
  }
  ```

In conclusion, constructors in Java cannot be `final`, `static`, or `abstract` because these modifiers conflict with their purpose: initializing objects during instantiation. Each has a distinct role elsewhere in Java, but not with constructors.

---

## 8. What is the difference between == and equals() in Java?

In Java, the `==` operator and the `equals()` method are used to compare objects or values, but they serve different purposes and behave differently depending on the context. Here's a detailed explanation of their differences:

---

### **`==` Operator**
- **Purpose**: The `==` operator compares the **references** (memory addresses) of two objects or the **values** of primitive data types.
- **Type**: It’s a binary operator, part of Java’s syntax.
- **Behavior**:
  - For **primitives** (e.g., `int`, `char`, `double`): Compares the actual values stored in the variables.
  - For **objects** (e.g., `String`, `Integer`, custom classes): Compares the memory addresses (references) to check if both variables point to the same object in memory.
- **Shallow Comparison**: It doesn’t look at the content or state of objects, only whether they are the same instance.

#### Example with Primitives:
```java
int a = 5;
int b = 5;
System.out.println(a == b); // Output: true (compares values: 5 == 5)
```

#### Example with Objects:
```java
String s1 = new String("Hello");
String s2 = new String("Hello");
System.out.println(s1 == s2); // Output: false (different objects in memory)
```

---

### **`equals()` Method**
- **Purpose**: The `equals()` method is used to compare the **content** or **logical equality** of two objects, typically based on their internal state (e.g., field values).
- **Type**: It’s a method defined in the `Object` class and can be overridden by subclasses to provide custom comparison logic.
- **Behavior**:
  - In the `Object` class, `equals()` by default behaves like `==` (compares references).
  - Many classes (e.g., `String`, `Integer`, `ArrayList`) override `equals()` to compare the actual contents rather than references.
  - For custom classes, you must override `equals()` to define what "equality" means.
- **Deep Comparison**: It examines the data within objects, depending on the implementation.

#### Example with Strings:
```java
String s1 = new String("Hello");
String s2 = new String("Hello");
System.out.println(s1.equals(s2)); // Output: true (compares content: "Hello" equals "Hello")
```

#### Example with Default `Object` Behavior:
```java
class Person {
    String name;
    Person(String name) {
        this.name = name;
    }
}

Person p1 = new Person("Alice");
Person p2 = new Person("Alice");
System.out.println(p1.equals(p2)); // Output: false (default equals() compares references)
```

---

### **Key Differences**
| Feature                | `==` Operator                          | `equals()` Method                       |
|------------------------|----------------------------------------|-----------------------------------------|
| **Type**               | Operator                               | Method                                  |
| **Comparison**         | Reference (memory address) for objects, value for primitives | Content (depends on implementation)     |
| **Default Behavior**   | Compares references (same as `Object.equals()`) | Compares references unless overridden   |
| **Use Case**           | Check if two variables point to the same object or primitives are equal | Check if two objects are logically equal |
| **Customizability**    | Not customizable                      | Can be overridden in a class            |
| **Applicable To**      | Primitives and objects                | Objects only                            |

---

### **Special Case: String Pool**
Strings in Java have a unique behavior due to the **String pool** (a memory optimization):
```java
String s1 = "Hello";     // Stored in String pool
String s2 = "Hello";     // Refers to the same pooled object
String s3 = new String("Hello"); // New object, not in pool

System.out.println(s1 == s2);     // Output: true (same reference in pool)
System.out.println(s1 == s3);     // Output: false (different references)
System.out.println(s1.equals(s3)); // Output: true (same content)
```
- Literal strings (e.g., `"Hello"`) are interned in the String pool, so `==` may return `true` if they share the same pooled reference.
- Using `new String()` creates a new object outside the pool, so `==` returns `false`.

---

### **Overriding `equals()` in Custom Classes**
If you want `equals()` to compare content in your own class, you must override it. Typically, you also override `hashCode()` to maintain consistency (if two objects are equal, their hash codes must be equal).

#### Example with Overridden `equals()`:
```java
class Person {
    String name;
    int age;

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true; // Same reference
        if (obj == null || getClass() != obj.getClass()) return false; // Null or different class
        Person other = (Person) obj; // Cast to Person
        return age == other.age && name.equals(other.name); // Compare fields
    }
}

public class Main {
    public static void main(String[] args) {
        Person p1 = new Person("Alice", 25);
        Person p2 = new Person("Alice", 25);
        System.out.println(p1 == p2);      // Output: false (different objects)
        System.out.println(p1.equals(p2)); // Output: true (same content)
    }
}
```

---

### **When to Use**
- Use `==`:
  - To compare primitive values (e.g., `int`, `double`).
  - To check if two object references point to the exact same instance.
- Use `equals()`:
  - To compare the content or logical equality of objects (e.g., two `String` objects with the same text).
  - When you need custom equality logic for your own classes.

---

### **Summary**
- `==` is a shallow comparison of references (or primitive values), while `equals()` is a deeper comparison of object contents (if overridden).
- Their behavior aligns with their purpose: `==` for identity, `equals()` for equivalence. Understanding their differences is crucial for accurate comparisons in Java.

---

## 9. What is the role of the `this` and `super` keywords?

In Java, the `this` and `super` keywords are used to refer to specific contexts within a class, helping to manage object instances, inheritance, and method or constructor calls. They play distinct but complementary roles in object-oriented programming. Here's a detailed explanation of each:

---

### **`this` Keyword**
The `this` keyword refers to the **current instance** of the class in which it is used. It is primarily employed to disambiguate between instance variables and parameters/local variables, or to invoke constructors and methods within the same object.

#### Roles of `this`:
1. **Distinguish Instance Variables from Parameters**:
  - When a method or constructor parameter has the same name as an instance variable, `this` is used to refer to the instance variable.
  - Example:
    ```java
    class Person {
        String name;

        Person(String name) {
            this.name = name; // 'this.name' refers to the instance variable
        }

        void setName(String name) {
            this.name = name; // Differentiates instance variable from parameter
        }
    }
    ```

2. **Invoke Another Constructor in the Same Class (Constructor Chaining)**:
  - `this()` calls another constructor in the same class, useful for reusing initialization logic.
  - Must be the first statement in the constructor.
  - Example:
    ```java
    class Student {
        String name;
        int age;

        Student(String name) {
            this(name, 0); // Calls the two-parameter constructor
        }

        Student(String name, int age) {
            this.name = name;
            this.age = age;
        }
    }
    ```

3. **Refer to the Current Object**:
  - Pass the current object to a method or return it.
  - Example:
    ```java
    class Example {
        void display() {
            System.out.println("Current object: " + this); // 'this' is the current instance
        }

        Example getInstance() {
            return this; // Returns the current object
        }
    }
    ```

4. **Invoke Instance Methods**:
  - Explicitly call another method of the same object (though this is often implicit).
  - Example:
    ```java
    class Test {
        void method1() {
            this.method2(); // Explicit call, though 'method2()' alone works too
        }

        void method2() {
            System.out.println("Method2 called");
        }
    }
    ```

#### Key Points:
- `this` cannot be used in `static` contexts (e.g., static methods or blocks) because it refers to an instance, and static members belong to the class, not an instance.
- It’s optional when there’s no naming conflict but required for clarity otherwise.

---

### **`super` Keyword**
The `super` keyword refers to the **immediate superclass** of the class in which it is used. It is used to access superclass members (fields, methods, or constructors) and is especially important in inheritance scenarios.

#### Roles of `super`:
1. **Call the Superclass Constructor**:
  - `super()` invokes the superclass’s constructor, often used to initialize inherited fields.
  - Must be the first statement in a subclass constructor.
  - Example:
    ```java
    class Animal {
        String type;

        Animal(String type) {
            this.type = type;
        }
    }

    class Dog extends Animal {
        String breed;

        Dog(String type, String breed) {
            super(type); // Calls Animal's constructor
            this.breed = breed;
        }
    }
    ```
  - If omitted, Java implicitly inserts a call to the superclass’s no-arg constructor (`super()`). If the superclass doesn’t have a no-arg constructor, you must explicitly call `super()` with arguments, or the code won’t compile.

2. **Access Superclass Methods**:
  - Call a method from the superclass, especially if it’s overridden in the subclass.
  - Example:
    ```java
    class Parent {
        void display() {
            System.out.println("Parent display");
        }
    }

    class Child extends Parent {
        @Override
        void display() {
            super.display(); // Calls Parent's display
            System.out.println("Child display");
        }
    }

    public class Main {
        public static void main(String[] args) {
            Child child = new Child();
            child.display();
            // Output:
            // Parent display
            // Child display
        }
    }
    ```

3. **Access Superclass Fields**:
  - Refer to a superclass field if it’s hidden by a subclass field with the same name.
  - Example:
    ```java
    class SuperClass {
        String name = "Super";
    }

    class SubClass extends SuperClass {
        String name = "Sub";

        void printNames() {
            System.out.println("Subclass name: " + name);      // "Sub"
            System.out.println("Superclass name: " + super.name); // "Super"
        }
    }
    ```

#### Key Points:
- Like `this`, `super` cannot be used in `static` contexts because it relates to instance-level inheritance.
- It’s essential for interacting with the superclass when subclass members shadow or override superclass members.

---

### **Key Differences**
| Feature                | `this` Keyword                          | `super` Keyword                         |
|------------------------|-----------------------------------------|-----------------------------------------|
| **Refers To**          | Current instance of the class           | Immediate superclass                    |
| **Primary Use**        | Disambiguate variables, call constructors/methods in the same class | Access superclass constructors, methods, or fields |
| **Constructor Call**   | `this()` calls another constructor in the same class | `super()` calls a superclass constructor |
| **Scope**              | Within the current class                | Links to the superclass                 |
| **Static Context**     | Not allowed                            | Not allowed                             |

---

### **Combined Example**
```java
class Vehicle {
    String brand;

    Vehicle(String brand) {
        this.brand = brand;
    }

    void info() {
        System.out.println("Brand: " + brand);
    }
}

class Car extends Vehicle {
    String model;

    Car(String brand, String model) {
        super(brand);    // Calls Vehicle's constructor
        this.model = model; // Refers to Car's instance variable
    }

    @Override
    void info() {
        super.info();    // Calls Vehicle's info method
        System.out.println("Model: " + this.model); // Refers to current object's model
    }
}

public class Main {
    public static void main(String[] args) {
        Car car = new Car("Toyota", "Camry");
        car.info();
        // Output:
        // Brand: Toyota
        // Model: Camry
    }
}
```

---

### **Summary**
- **`this`**: Focuses on the current object—used for self-reference, constructor chaining, or disambiguation within a class.
- **`super`**: Bridges to the superclass—used to leverage or extend inherited behavior, call superclass constructors, or access overridden/hidden members.

Both keywords are vital for managing object state and inheritance in Java, ensuring clear and precise interactions within and across class hierarchies.

---

## 10. What are access modifiers in Java?

In Java, **access modifiers** are keywords that define the visibility or accessibility of class members (fields, methods, constructors, etc.) and classes themselves. They control which parts of a program can access these members, enforcing encapsulation and security in object-oriented programming. Java provides four main access modifiers: `public`, `protected`, `default` (also called package-private), and `private`. Here's a detailed explanation of each:

---

### **1. `public`**
- **Definition**: The member is accessible from everywhere in the program, regardless of package or class boundaries.
- **Scope**: Unlimited—any class, subclass, or external code can access it.
- **Usage**: Used for members that need to be universally available, such as utility methods or public APIs.

#### Example:
```java
public class Example {
    public int number = 10;

    public void display() {
        System.out.println("Number: " + number);
    }
}

class Test {
    public static void main(String[] args) {
        Example ex = new Example();
        System.out.println(ex.number); // Accessible: 10
        ex.display();                 // Accessible
    }
}
```

---

### **2. `protected`**
- **Definition**: The member is accessible within the same package and also in subclasses (even if they are in different packages), provided the subclass inherits it.
- **Scope**: Package-level access + subclass access through inheritance.
- **Usage**: Useful for allowing controlled access to inherited members while still restricting broader visibility.

#### Example:
```java
package pkg1;

public class Parent {
    protected String name = "Parent";

    protected void show() {
        System.out.println("Name: " + name);
    }
}

package pkg2;

import pkg1.Parent;

class Child extends Parent {
    void test() {
        System.out.println(name); // Accessible via inheritance
        show();                  // Accessible via inheritance
    }
}

class Test {
    public static void main(String[] args) {
        Child child = new Child();
        child.test(); // Output: Parent, Name: Parent
        // child.name or child.show() not directly accessible here outside the subclass
    }
}
```
- **Note**: Outside the package, `protected` members are only accessible in subclasses, not directly via an object reference unless within the subclass itself.

---

### **3. `default` (Package-Private)**
- **Definition**: If no access modifier is specified, the member has `default` access (also called package-private). It is accessible only within the same package.
- **Scope**: Limited to the package where the class is defined.
- **Usage**: Used for members that should be shared among classes in the same package but hidden from external packages.

#### Example:
```java
package pkg1;

class MyClass {
    int value = 20; // Default access

    void print() {  // Default access
        System.out.println("Value: " + value);
    }
}

package pkg1;

class Test {
    public static void main(String[] args) {
        MyClass obj = new MyClass();
        System.out.println(obj.value); // Accessible: 20 (same package)
        obj.print();                  // Accessible (same package)
    }
}

package pkg2;

import pkg1.MyClass;

class OutsideTest {
    public static void main(String[] args) {
        MyClass obj = new MyClass();
        // obj.value and obj.print() are inaccessible here (different package)
    }
}
```

---

### **4. `private`**
- **Definition**: The member is accessible only within the same class. It is the most restrictive modifier.
- **Scope**: Limited to the enclosing class; not visible to subclasses, other classes, or packages.
- **Usage**: Used to hide implementation details and enforce encapsulation, typically with getters and setters for controlled access.

#### Example:
```java
class BankAccount {
    private double balance = 1000.0;

    private void deductFee() {
        balance -= 10;
    }

    // Public method to access private field
    public double getBalance() {
        deductFee(); // Accessible within the class
        return balance;
    }
}

class Test {
    public static void main(String[] args) {
        BankAccount account = new BankAccount();
        // System.out.println(account.balance); // Error: balance is private
        System.out.println(account.getBalance()); // Output: 990.0
    }
}
```

---

### **Comparison Table**
| Modifier    | Class Access          | Package Access         | Subclass Access (Same Package) | Subclass Access (Different Package) | Outside Access |
|-------------|-----------------------|------------------------|-------------------------------|-------------------------------------|----------------|
| `public`    | Yes                   | Yes                    | Yes                           | Yes                                 | Yes            |
| `protected` | Yes                   | Yes                    | Yes                           | Yes (via inheritance)               | No             |
| `default`   | Yes                   | Yes                    | Yes                           | No                                  | No             |
| `private`   | Yes                   | No                     | No                            | No                                  | No             |

---

### **Key Points**
1. **Class-Level Access**:
  - A top-level class can only be `public` or `default`. `private` and `protected` are not allowed for top-level classes (but can be used for nested/inner classes).
  - Example:
    ```java
    public class PublicClass {} // Allowed
    class DefaultClass {}       // Allowed
    // private class PrivateClass {} // Error
    ```

2. **Inheritance**:
  - Subclasses inherit `public` and `protected` members but not `private` members (though `private` members can be accessed indirectly via inherited public/protected methods).
  - `default` members are inherited only if the subclass is in the same package.

3. **Constructor Access**:
  - Constructors can have any access modifier (`public`, `protected`, `default`, `private`).
  - Example: `private` constructors are used in singleton patterns to prevent instantiation outside the class.

4. **Method Overriding**:
  - When overriding a method, the subclass cannot reduce the visibility of the superclass method (e.g., cannot override a `public` method as `protected`).

#### Example of Overriding Rule:
```java
class SuperClass {
    protected void method() {}
}

class SubClass extends SuperClass {
    public void method() {} // Allowed (increases visibility)
    // private void method() {} // Error (reduces visibility)
}
```

---

### **Practical Usage**
- **`public`**: For APIs or members intended for broad use (e.g., `main()` method).
- **`protected`**: For members shared with subclasses but not the wider world.
- **`default`**: For package-level collaboration, like internal utilities.
- **`private`**: For hiding implementation details and ensuring data integrity.

Access modifiers are fundamental to Java’s encapsulation principle, allowing developers to control how and where class members are accessed, thereby improving security and maintainability.

---

## 11. What is the difference between an abstract class and an interface?

In Java, **abstract classes** and **interfaces** are both mechanisms for achieving abstraction and defining contracts for subclasses, but they differ in purpose, structure, and usage. Here's a detailed comparison:

---

### **Abstract Class**
- **Definition**: An abstract class is a class declared with the `abstract` keyword that cannot be instantiated directly. It may contain both **abstract methods** (without implementation) and **concrete methods** (with implementation), along with fields and constructors.
- **Purpose**: Used to provide a common base with shared code and partial implementation for related classes, while leaving some methods to be implemented by subclasses.
- **Inheritance**: A class can extend only **one abstract class** (single inheritance in Java).

#### Key Features:
- Can have **abstract methods** (no body) and **concrete methods** (with body).
- Can have **instance variables** (fields) with any access modifier (`private`, `protected`, `public`).
- Can have **constructors** to initialize fields, called by subclass constructors via `super()`.
- Supports **partial implementation**, making it suitable for sharing code among subclasses.

#### Example:
```java
abstract class Animal {
    String name; // Instance variable

    // Constructor
    Animal(String name) {
        this.name = name;
    }

    // Abstract method
    abstract void sound();

    // Concrete method
    void eat() {
        System.out.println(name + " is eating.");
    }
}

class Dog extends Animal {
    Dog(String name) {
        super(name); // Call abstract class constructor
    }

    @Override
    void sound() {
        System.out.println(name + " says Woof");
    }
}

class Main {
    public static void main(String[] args) {
        Dog dog = new Dog("Rex");
        dog.sound(); // Output: Rex says Woof
        dog.eat();   // Output: Rex is eating.
    }
}
```

---

### **Interface**
- **Definition**: An interface is a completely abstract type declared with the `interface` keyword. Historically (before Java 8), it contained only **abstract methods** (no implementation). Since Java 8, it can also include **default methods** (with implementation) and **static methods**.
- **Purpose**: Used to define a contract or standard behavior that implementing classes must follow, without dictating how the behavior is implemented.
- **Inheritance**: A class can implement **multiple interfaces** (supports multiple inheritance of type).

#### Key Features:
- All methods were implicitly `public` and `abstract` (before Java 8); now can have `default` and `static` methods with bodies.
- Variables are implicitly `public`, `static`, and `final` (constants only, no instance fields).
- No constructors (since interfaces cannot be instantiated).
- Focuses on **what** should be done, not **how** (though `default` methods provide optional implementation).

#### Example:
```java
interface Animal {
    // Constant (implicitly public static final)
    String TYPE = "Mammal";

    // Abstract method (implicitly public)
    void sound();

    // Default method (Java 8+)
    default void eat() {
        System.out.println("Eating food.");
    }

    // Static method (Java 8+)
    static void info() {
        System.out.println("This is an animal interface.");
    }
}

class Cat implements Animal {
    @Override
    public void sound() {
        System.out.println("Meow");
    }
}

class Main {
    public static void main(String[] args) {
        Cat cat = new Cat();
        cat.sound();      // Output: Meow
        cat.eat();        // Output: Eating food.
        Animal.info();    // Output: This is an animal interface.
        System.out.println(Animal.TYPE); // Output: Mammal
    }
}
```

---

### **Key Differences**
| Feature                | Abstract Class                           | Interface                               |
|------------------------|------------------------------------------|-----------------------------------------|
| **Keyword**            | `abstract class`                        | `interface`                            |
| **Instantiation**      | Cannot be instantiated directly         | Cannot be instantiated directly        |
| **Method Types**       | Abstract + Concrete methods             | Abstract (default), Default (Java 8+), Static (Java 8+) |
| **Fields**             | Instance variables (any access modifier) | Only constants (`public static final`) |
| **Constructors**       | Yes, can have constructors              | No constructors                        |
| **Inheritance**        | Single inheritance (`extends`)          | Multiple inheritance (`implements`)    |
| **Access Modifiers**   | Can use `public`, `protected`, `private`| Methods implicitly `public` (except `static`/`default`) |
| **Purpose**            | Partial implementation + abstraction    | Pure abstraction + contract            |
| **Default Behavior**   | Concrete methods provide behavior       | `default` methods provide behavior (Java 8+) |
| **Extensibility**      | Less flexible (single inheritance)      | More flexible (multiple interfaces)    |

---

### **When to Use**
- **Abstract Class**:
  - Use when you want to share code (fields, methods) among related classes.
  - Suitable for a hierarchy where subclasses share a common base (e.g., `Animal` → `Dog`, `Cat`).
  - Example: A base class with some default behavior and abstract methods for customization.

- **Interface**:
  - Use when you want to define a contract that unrelated classes can implement.
  - Ideal for multiple inheritance or when implementation details should be left to the implementing class.
  - Example: A behavior like `Runnable` or `Serializable` that any class can adopt.

---

### **Combined Example**
```java
abstract class Vehicle {
    String brand;

    Vehicle(String brand) {
        this.brand = brand;
    }

    abstract void move(); // Abstract method

    void start() {        // Concrete method
        System.out.println(brand + " is starting.");
    }
}

interface Fuelable {
    void refuel();       // Abstract method

    default void checkFuel() { // Default method
        System.out.println("Checking fuel level.");
    }
}

class Car extends Vehicle implements Fuelable {
    Car(String brand) {
        super(brand);
    }

    @Override
    void move() {
        System.out.println(brand + " is driving.");
    }

    @Override
    public void refuel() {
        System.out.println(brand + " is refueling.");
    }
}

class Main {
    public static void main(String[] args) {
        Car car = new Car("Toyota");
        car.start();     // Output: Toyota is starting.
        car.move();      // Output: Toyota is driving.
        car.refuel();    // Output: Toyota is refueling.
        car.checkFuel(); // Output: Checking fuel level.
    }
}
```

---

### **Evolution with Java Versions**
- **Pre-Java 8**: Interfaces were purely abstract; abstract classes were the only way to share code.
- **Java 8**: Interfaces gained `default` and `static` methods, blurring the line but still differing in fields and inheritance rules.
- **Java 9+**: Interfaces can have `private` methods (for internal use by `default` methods), but they still lack instance fields or constructors.

---

### **Summary**
- **Abstract Class**: A partially implemented blueprint for related classes, with single inheritance and shared state/behavior.
- **Interface**: A fully abstract contract (with optional default behavior since Java 8), supporting multiple inheritance and defining capabilities.

Choosing between them depends on whether you need shared implementation (abstract class) or a flexible, reusable contract (interface). Both are essential tools for abstraction and polymorphism in Java.

---

## 12. Can you implement multiple interfaces in Java?

Yes, in Java, a class can implement **multiple interfaces**. This is one of the key features of interfaces and a way Java supports a form of **multiple inheritance** for behavior (but not state, as with classes). Unlike abstract classes, where a class can extend only one superclass due to Java’s single inheritance restriction, a class can implement any number of interfaces using the `implements` keyword.

---

### **How It Works**
- Use the `implements` keyword followed by a comma-separated list of interface names.
- The implementing class must provide concrete implementations for all abstract methods defined in each interface (unless the class itself is abstract).
- Since Java 8, interfaces can include `default` methods (with implementations) and `static` methods, which don’t require implementation by the class unless overridden.

---

### **Syntax**
```java
interface Interface1 {
    void method1();
}

interface Interface2 {
    void method2();
}

class MyClass implements Interface1, Interface2 {
    @Override
    public void method1() {
        System.out.println("Method1 from Interface1");
    }

    @Override
    public void method2() {
        System.out.println("Method2 from Interface2");
    }
}
```

---

### **Example: Implementing Multiple Interfaces**
Here’s a practical example combining two interfaces:

```java
interface Printable {
    void print();
}

interface Scannable {
    void scan();
    default void reset() {
        System.out.println("Resetting scanner.");
    }
}

class PrinterScanner implements Printable, Scannable {
    private String name;

    PrinterScanner(String name) {
        this.name = name;
    }

    @Override
    public void print() {
        System.out.println(name + " is printing.");
    }

    @Override
    public void scan() {
        System.out.println(name + " is scanning.");
    }
}

public class Main {
    public static void main(String[] args) {
        PrinterScanner device = new PrinterScanner("HP Device");
        device.print();  // Output: HP Device is printing.
        device.scan();   // Output: HP Device is scanning.
        device.reset();  // Output: Resetting scanner.
    }
}
```

---

### **Key Points**
1. **All Abstract Methods Must Be Implemented**:
  - If a class implements multiple interfaces, it must provide implementations for all abstract methods from all interfaces, or it must be declared `abstract` itself.
  - Example:
    ```java
    abstract class Partial implements Printable, Scannable {
        // No implementation provided, so class is abstract
    }
    ```

2. **Handling Method Name Conflicts**:
  - If two interfaces declare abstract methods with the same name and signature, the implementing class provides a single implementation that satisfies both interfaces.
  - Example:
    ```java
    interface A {
        void action();
    }

    interface B {
        void action();
    }

    class Impl implements A, B {
        @Override
        public void action() {
            System.out.println("Single implementation for A and B");
        }
    }
    ```

3. **Default Method Conflicts**:
  - If two interfaces provide `default` methods with the same name, the implementing class must override the conflicting method to resolve the ambiguity.
  - Example:
    ```java
    interface X {
        default void show() {
            System.out.println("X's show");
        }
    }

    interface Y {
        default void show() {
            System.out.println("Y's show");
        }
    }

    class Conflict implements X, Y {
        @Override
        public void show() {
            // Must override to resolve conflict
            System.out.println("Resolved show");
            // Optionally call specific interface's default method
            X.super.show(); // Calls X's default method
        }
    }
    ```

4. **Multiple Inheritance of Behavior**:
  - Interfaces allow a class to inherit multiple behaviors (method declarations), unlike extending multiple classes, which isn’t allowed in Java.
  - Example: A class can implement `Runnable`, `Serializable`, and a custom interface simultaneously.

---

### **Real-World Example**
Imagine a device that needs to support multiple functionalities:

```java
interface Logger {
    void log(String message);
}

interface Connectable {
    void connect();
    default void disconnect() {
        System.out.println("Disconnected.");
    }
}

class SmartDevice implements Logger, Connectable {
    private String deviceName;

    SmartDevice(String deviceName) {
        this.deviceName = deviceName;
    }

    @Override
    public void log(String message) {
        System.out.println(deviceName + " logged: " + message);
    }

    @Override
    public void connect() {
        System.out.println(deviceName + " is connected.");
    }
}

public class Main {
    public static void main(String[] args) {
        SmartDevice device = new SmartDevice("SmartHub");
        device.log("System started"); // Output: SmartHub logged: System started
        device.connect();            // Output: SmartHub is connected.
        device.disconnect();         // Output: Disconnected.
    }
}
```

---

### **Benefits of Multiple Interfaces**
- **Flexibility**: A class can adopt multiple roles or behaviors (e.g., `Printable` and `Scannable`).
- **Loose Coupling**: Interfaces define contracts without tying classes to a specific implementation hierarchy.
- **Workaround for Single Inheritance**: Since Java doesn’t allow multiple class inheritance, multiple interfaces provide a way to combine functionalities.

---

### **Limitations**
- **No State**: Interfaces cannot have instance fields (only `public static final` constants), so they don’t share state like abstract classes can.
- **Implementation Overhead**: The class must implement all abstract methods from all interfaces, which can increase complexity if many interfaces are involved.

---

### **Conclusion**
Yes, Java allows a class to implement multiple interfaces, making it a powerful feature for defining flexible and reusable behavior. This capability complements Java’s single inheritance model for classes, enabling developers to design systems where a single class can conform to multiple contracts or roles seamlessly.

---

## 13. What is the purpose of the `final` keyword in Java?

In Java, the `final` keyword is a versatile modifier that imposes restrictions on classes, methods, and variables to prevent modification or extension. Its purpose varies depending on where it is applied—classes, methods, or variables—but it generally ensures immutability, prevents overriding, or restricts inheritance. Here's a detailed explanation of its roles:

---

### **1. `final` with Variables**
- **Purpose**: Makes a variable **immutable**, meaning its value cannot be changed once assigned.
- **Behavior**:
  - For **primitive types**: The value (e.g., `int`, `double`) cannot be altered.
  - For **reference types**: The reference cannot be reassigned to point to a different object, though the object’s internal state can still be modified if it’s mutable (e.g., fields of an object can change unless the object itself is immutable).
- **Initialization**: A `final` variable must be initialized at declaration or in a constructor/static block (for instance/static variables), otherwise, it’s a compile-time error.
- **Common Use**: Constants, such as configuration values or fixed settings.

#### Example:
```java
class Example {
    final int NUMBER = 10; // Constant
    final StringBuilder sb; // Reference can't change, but object can

    Example() {
        sb = new StringBuilder("Hello"); // Initialized in constructor
    }

    void test() {
        // NUMBER = 20; // Error: cannot assign a value to final variable
        sb.append(" World"); // Allowed: modifying object's state
        // sb = new StringBuilder("New"); // Error: cannot reassign reference
    }
}

public class Main {
    public static void main(String[] args) {
        Example ex = new Example();
        System.out.println(ex.sb); // Output: Hello World
    }
}
```

- **Static Final**: Often used for class-level constants:
  ```java
  class Constants {
      public static final double PI = 3.14159;
  }
  ```

---

### **2. `final` with Methods**
- **Purpose**: Prevents a method from being **overridden** by subclasses.
- **Behavior**: The method’s implementation is fixed, ensuring that its behavior remains consistent across all subclasses.
- **Usage**: Used when a method’s logic should not be altered for design or security reasons (e.g., in APIs or critical functionality).

#### Example:
```java
class Parent {
    final void display() {
        System.out.println("This is a final method.");
    }
}

class Child extends Parent {
    // void display() { // Error: cannot override final method
    //     System.out.println("Trying to override");
    // }
}

public class Main {
    public static void main(String[] args) {
        Child child = new Child();
        child.display(); // Output: This is a final method.
    }
}
```

- **Note**: `final` methods can still be called by subclasses; they just can’t be redefined.

---

### **3. `final` with Classes**
- **Purpose**: Prevents a class from being **extended** (i.e., subclassed).
- **Behavior**: The class cannot have any subclasses, making it a "leaf" in the inheritance hierarchy.
- **Usage**: Used for security (e.g., preventing unintended modifications) or when a class’s design is complete and should not be altered (e.g., `String` class in Java is `final`).

#### Example:
```java
final class Immutable {
    private int value;

    Immutable(int value) {
        this.value = value;
    }

    int getValue() {
        return value;
    }
}

// class SubImmutable extends Immutable { // Error: cannot inherit from final class
// }

public class Main {
    public static void main(String[] args) {
        Immutable obj = new Immutable(42);
        System.out.println(obj.getValue()); // Output: 42
    }
}
```

- **Real-World Example**: `java.lang.String`, `java.lang.Integer`, and other wrapper classes are `final` to ensure their immutability and consistency.

---

### **Key Uses of `final`**
| Applied To      | Effect                                  | Example Use Case                          |
|-----------------|-----------------------------------------|-------------------------------------------|
| **Variable**    | Cannot be reassigned (immutable)        | Constants like `PI`, configuration values |
| **Method**      | Cannot be overridden by subclasses      | Fixed behavior in a framework or API     |
| **Class**       | Cannot be extended (no subclasses)      | Immutable classes like `String`           |

---

### **Additional Notes**
1. **Performance**: Historically, `final` was thought to enable compiler optimizations (e.g., inlining), but modern JVMs (with JIT compilation) optimize code regardless of `final`. Its primary role today is design and safety, not performance.
2. **Blank Final Variables**:
  - A `final` variable can be declared without immediate initialization (called a "blank final") but must be assigned exactly once in a constructor or static block:
    ```java
    class Test {
        final int x;

        Test(int value) {
            x = value; // Must initialize here
        }
    }
    ```
3. **Final vs. Immutability**:
  - For objects, `final` only locks the reference, not the object’s state. Full immutability requires additional design (e.g., making fields `final` and avoiding setters).
  - Example: `final List<String> list = new ArrayList<>();`—`list` can still be modified (e.g., `list.add("item")`), but it can’t be reassigned to a new `List`.

---

### **Practical Example Combining All Uses**
```java
final class Calculator {
    public static final int MAX_VALUE = 100; // Constant

    final int add(int a, int b) {        // Cannot be overridden
        return a + b;
    }
}

class Test {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println(calc.add(5, 3));      // Output: 8
        System.out.println(Calculator.MAX_VALUE); // Output: 100
        // Calculator cannot be extended, and add() cannot be overridden
    }
}
```

---

### **Summary**
The `final` keyword in Java enforces immutability and restricts modification:
- **Variables**: Locks the value or reference.
- **Methods**: Prevents overriding for consistent behavior.
- **Classes**: Stops inheritance for design integrity.

It’s a powerful tool for creating robust, predictable, and secure code, commonly used in constants, immutable objects, and API design.

---

## 14. What are default methods in interfaces (Java 8)?

In Java, **default methods** were introduced in **Java 8** as a significant enhancement to interfaces. They allow interfaces to provide method implementations (bodies) rather than requiring all methods to be abstract. This feature was added to enable backward compatibility and to extend interfaces without breaking existing code that implements them. Here's a detailed explanation:

---

### **What Are Default Methods?**
- **Definition**: A default method is a method in an interface that has a body (implementation) and is marked with the `default` keyword. Implementing classes can use this implementation as-is, override it, or ignore it without being forced to provide their own implementation.
- **Purpose**: To add new functionality to interfaces without requiring all implementing classes to update their code, solving the problem of interface evolution in large APIs.

#### Syntax:
```java
interface InterfaceName {
    // Abstract method (no body)
    void abstractMethod();

    // Default method (with body)
    default void defaultMethod() {
        System.out.println("This is a default implementation.");
    }
}
```

---

### **Why Were Default Methods Introduced?**
Before Java 8, interfaces could only declare abstract methods, and adding a new method to an existing interface would break all classes implementing it because they’d need to implement the new method. Default methods address this by:
- Providing a **default implementation** that existing classes inherit automatically.
- Allowing interfaces to evolve over time (e.g., adding methods to the `Collection` interface in the Java standard library).

#### Example Problem Without Default Methods:
```java
// Pre-Java 8 Interface
interface OldInterface {
    void doSomething();
}

// Implementing class
class OldImpl implements OldInterface {
    public void doSomething() {
        System.out.println("Doing something.");
    }
}

// If we add a new method to OldInterface...
interface OldInterface {
    void doSomething();
    void doMore(); // All implementing classes must now implement this
}
```
- `OldImpl` would fail to compile unless `doMore()` is implemented.

#### Solution with Default Methods:
```java
interface NewInterface {
    void doSomething();

    // New method with default implementation
    default void doMore() {
        System.out.println("Doing more with default behavior.");
    }
}

class NewImpl implements NewInterface {
    public void doSomething() {
        System.out.println("Doing something.");
    }
    // No need to implement doMore()
}

public class Main {
    public static void main(String[] args) {
        NewImpl obj = new NewImpl();
        obj.doSomething(); // Output: Doing something.
        obj.doMore();      // Output: Doing more with default behavior.
    }
}
```

---

### **Key Features of Default Methods**
1. **Optional Implementation**:
  - Implementing classes can use the default method as provided or override it with a custom implementation.
  - Example:
    ```java
    class CustomImpl implements NewInterface {
        public void doSomething() {
            System.out.println("Custom doSomething.");
        }

        @Override
        public void doMore() {
            System.out.println("Custom doMore.");
        }
    }
    ```

2. **Backward Compatibility**:
  - Libraries like Java’s `java.util` package added methods (e.g., `forEach` in `Iterable`) without breaking existing implementations.

3. **Multiple Inheritance Support**:
  - Since a class can implement multiple interfaces, default methods allow combining behaviors from multiple sources.
  - If two interfaces provide default methods with the same name, the implementing class must resolve the conflict explicitly.

4. **Access Modifier**:
  - Default methods are implicitly `public` (like all interface methods). You cannot make them `private` or `protected` directly (though Java 9 introduced `private` methods in interfaces for internal use).

---

### **Handling Conflicts with Multiple Interfaces**
When a class implements multiple interfaces that have default methods with the same name, a **conflict** arises. Java requires the class to override the conflicting method to resolve the ambiguity.

#### Example of Conflict:
```java
interface Interface1 {
    default void action() {
        System.out.println("Action from Interface1");
    }
}

interface Interface2 {
    default void action() {
        System.out.println("Action from Interface2");
    }
}

class ConflictClass implements Interface1, Interface2 {
    // Must override to resolve conflict
    @Override
    public void action() {
        System.out.println("Resolved action in ConflictClass");
        // Optionally call a specific interface's default method
        Interface1.super.action(); // Explicitly call Interface1's version
    }
}

public class Main {
    public static void main(String[] args) {
        ConflictClass obj = new ConflictClass();
        obj.action();
        // Output:
        // Resolved action in ConflictClass
        // Action from Interface1
    }
}
```

---

### **Default Methods vs. Abstract Classes**
| Feature                | Default Methods in Interfaces         | Abstract Class Methods               |
|------------------------|---------------------------------------|--------------------------------------|
| **Implementation**     | Provides default behavior             | Can have concrete methods            |
| **Inheritance**        | Multiple interfaces allowed           | Single inheritance only              |
| **State**              | No instance fields (only constants)   | Can have instance fields             |
| **Purpose**            | Extend interface behavior             | Share code among related classes     |
| **Override Requirement**| Optional                             | Required for abstract methods        |

---

### **Real-World Use Case**
Default methods are widely used in Java’s standard library. For example, the `Iterable` interface added a `forEach` method in Java 8:
```java
interface Iterable<T> {
    // Existing abstract method
    Iterator<T> iterator();

    // Default method added in Java 8
    default void forEach(Consumer<? super T> action) {
        Objects.requireNonNull(action);
        for (T t : this) {
            action.accept(t);
        }
    }
}
```
- Classes implementing `Iterable` (e.g., `ArrayList`) didn’t need to implement `forEach`—they inherited the default behavior.

#### Usage:
```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("A");
        list.add("B");
        list.forEach(System.out::println); // Output: A, B
    }
}
```

---

### **Limitations**
1. **No State**: Default methods cannot access instance fields (since interfaces don’t have them), limiting their ability to manage state compared to abstract classes.
2. **Conflict Resolution**: Requires manual overriding in cases of method name clashes, which can add complexity.
3. **Not Truly Private**: Before Java 9, default methods couldn’t be `private`, so they were always part of the public API (Java 9 introduced `private` interface methods to support default methods internally).

---

### **Summary**
Default methods in Java 8 allow interfaces to provide concrete implementations while maintaining their role as contracts. They:
- Enable **backward compatibility** for evolving APIs.
- Support **multiple inheritance of behavior**.
- Offer flexibility by allowing optional overriding.

This feature bridges the gap between interfaces and abstract classes, making interfaces more powerful and adaptable while preserving Java’s design principles.

---

## 15. What is the diamond problem in Java?

The **diamond problem** is a well-known issue in object-oriented programming related to **multiple inheritance**, where ambiguity arises when a class inherits from two or more classes that share a common ancestor. It’s called the "diamond problem" because the inheritance hierarchy forms a diamond shape. While Java avoids the diamond problem for **classes** by restricting multiple inheritance, it can still occur with **interfaces** that have **default methods** (introduced in Java 8). Here’s a detailed explanation:

---

### **What is the Diamond Problem?**
The diamond problem occurs when:
1. A class (or interface) `A` is inherited by two intermediate classes (or interfaces) `B` and `C`.
2. A subclass `D` then inherits from both `B` and `C`.
3. If `A` defines a method that `B` and `C` inherit (or override), and `D` doesn’t explicitly resolve it, there’s ambiguity about which version of the method `D` should use.

This creates a "diamond" shape:
```
       A
      / \
     B   C
      \ /
       D
```

---

### **Diamond Problem in Languages with Multiple Class Inheritance**
In languages like C++, which allow a class to extend multiple classes, the diamond problem is a significant issue. For example:
```cpp
class A {
public:
    void method() { cout << "A's method"; }
};

class B : public A {};
class C : public A {};
class D : public B, public C {};

int main() {
    D d;
    d.method(); // Ambiguity: B's inherited method or C's?
}
```
- In C++, this leads to ambiguity unless resolved with mechanisms like virtual inheritance.

---

### **Java’s Approach: No Multiple Class Inheritance**
Java avoids the diamond problem for **classes** by prohibiting multiple inheritance of classes. A class can extend only **one superclass**, ensuring a single inheritance chain:
```java
class A {}
class B extends A {}
class C extends A {}
// class D extends B, C {} // Error: Multiple inheritance not allowed
```
- This design eliminates ambiguity for class hierarchies, as there’s no way for a class to inherit conflicting implementations from multiple parents.

---

### **Diamond Problem with Interfaces in Java**
While Java prevents the diamond problem with classes, it can still arise with **interfaces** due to:
1. A class being able to implement **multiple interfaces**.
2. The introduction of **default methods** in Java 8, which allow interfaces to provide method implementations.

#### Scenario:
- Interface `A` defines a default method.
- Interfaces `B` and `C` extend `A` and inherit the default method.
- Class `D` implements both `B` and `C`, leading to potential ambiguity about which default method to use.

#### Example:
```java
interface A {
    default void show() {
        System.out.println("A's show");
    }
}

interface B extends A {}
interface C extends A {}

class D implements B, C {
    // No implementation provided
}

public class Main {
    public static void main(String[] args) {
        D d = new D();
        d.show(); // Output: A's show (no ambiguity here)
    }
}
```
- **Result**: In this case, there’s no real conflict because `B` and `C` don’t override `show()`, so `D` inherits the single implementation from `A`. Java resolves this implicitly by using the common ancestor’s method.

#### Real Diamond Problem with Conflicting Defaults:
If `B` or `C` overrides the default method from `A`, ambiguity can arise:
```java
interface A {
    default void show() {
        System.out.println("A's show");
    }
}

interface B extends A {
    default void show() {
        System.out.println("B's show");
    }
}

interface C extends A {
    default void show() {
        System.out.println("C's show");
    }
}

class D implements B, C {
    // Compile-time error without resolution
}

public class Main {
    public static void main(String[] args) {
        D d = new D();
        d.show(); // Which show() to call: B's or C's?
    }
}
```
- **Problem**: This code won’t compile because `D` inherits conflicting default implementations of `show()` from `B` and `C`. Java doesn’t know which one to use.

---

### **Resolving the Diamond Problem in Java**
Java requires the implementing class (`D`) to explicitly resolve the conflict by:
1. **Overriding the Conflicting Method**:
  - Provide a new implementation in `D`.
  - Optionally, call a specific interface’s default method using the `InterfaceName.super.method()` syntax.

#### Resolved Example:
```java
interface A {
    default void show() {
        System.out.println("A's show");
    }
}

interface B extends A {
    default void show() {
        System.out.println("B's show");
    }
}

interface C extends A {
    default void show() {
        System.out.println("C's show");
    }
}

class D implements B, C {
    @Override
    public void show() {
        System.out.println("D's show"); // Custom resolution
        // Optionally call B's or C's version
        B.super.show(); // Explicitly invoke B's default method
    }
}

public class Main {
    public static void main(String[] args) {
        D d = new D();
        d.show();
        // Output:
        // D's show
        // B's show
    }
}
```

---

### **How Java Mitigates the Diamond Problem**
1. **No Multiple Class Inheritance**:
  - By restricting classes to single inheritance, Java avoids the diamond problem for class hierarchies entirely.
2. **Interface Rules**:
  - If multiple interfaces provide default methods with the same name, the implementing class must override the method to resolve the conflict.
  - If the interfaces inherit a default method from a common ancestor without overriding it, Java uses the ancestor’s implementation, avoiding ambiguity.
3. **Explicit Resolution**:
  - The `InterfaceName.super` syntax allows precise control over which default method to invoke.

---

### **Key Points**
- **Classic Diamond Problem**: Doesn’t occur with Java classes due to single inheritance.
- **Interface Diamond Problem**: Can occur with default methods but is manageable.
- **Resolution**: The programmer must explicitly override conflicting methods, ensuring clarity and control.

---

### **Comparison with Other Languages**
- **C++**: Uses virtual inheritance to resolve the diamond problem, but it’s complex and error-prone.
- **Python**: Allows multiple inheritance and resolves it using the Method Resolution Order (MRO).
- **Java**: Avoids it for classes and provides a clear resolution mechanism for interfaces.

---

### **Summary**
The diamond problem in Java is relevant only in the context of interfaces with default methods. Java handles it by:
- Preventing multiple class inheritance.
- Requiring explicit overriding in cases of conflict.
- Providing tools (`super`) to invoke specific interface implementations.

This design ensures that while Java supports multiple inheritance of behavior via interfaces, it avoids the ambiguity and complexity of the diamond problem seen in other languages.

---

### 🔹 16–30: **Data Types, Variables, Operators**

16. What is the difference between primitive and reference types?
17. What is autoboxing and unboxing in Java?
18. What is type casting? Explain implicit and explicit casting.
19. What is the difference between int and Integer?
20. What are wrapper classes in Java?
21. What are the different types of variables in Java?
22. What is the scope of a local, instance, and static variable?
23. Explain the ternary operator in Java.
24. What is short-circuit evaluation in Java?
25. What is the difference between ++i and i++?
26. What are bitwise operators in Java?
27. What is the difference between & and &&?
28. What is the purpose of the `instanceof` keyword?
29. What is null in Java? Can you call a method on a null object?
30. How does Java handle memory for variables?

---

### 🔹 31–45: **Control Statements & Loops**

31. What is the difference between `break` and `continue`?
32. What are enhanced for-loops in Java?
33. How does a switch-case statement work in Java?
34. Can you use strings in switch-case statements?
35. What is a labeled break or continue?
36. What is the difference between while and do-while?
37. How do you handle infinite loops in Java?
38. What are nested loops? How does it affect performance?
39. How does Java evaluate expressions in if-else conditions?
40. Can we replace if-else ladder with switch-case?
41. What are guard clauses?
42. What is fall-through in switch-case?
43. How do loops affect memory and performance in Java?
44. What is the difference between forEach() and for loop?
45. When should you avoid using recursion?

---

### 🔹 46–60: **Exception Handling**

46. What is the difference between checked and unchecked exceptions?
47. What is the base class of all exceptions?
48. How do try-catch-finally blocks work?
49. What happens if an exception is thrown in finally block?
50. What is the purpose of the `throw` and `throws` keywords?
51. What is a custom exception and how to create one?
52. What is the difference between `Exception` and `Error`?
53. What are runtime exceptions? Give examples.
54. Can a finally block be skipped?
55. Can we catch multiple exceptions in one catch block?
56. How does try-with-resources work?
57. What are suppressed exceptions?
58. Can you rethrow an exception? How?
59. What is exception chaining?
60. Why is it bad to catch `Exception` or `Throwable`?

---

### 🔹 61–75: **Collections Framework**

61. What is the Collection framework in Java?
62. What is the difference between List, Set, and Map?
63. What is the difference between ArrayList and LinkedList?
64. What is the difference between HashSet and TreeSet?
65. What is the difference between HashMap and Hashtable?
66. What is the internal working of HashMap?
67. What is the load factor in HashMap?
68. What is the difference between fail-fast and fail-safe iterators?
69. What is the difference between Iterator and ListIterator?
70. How does ConcurrentHashMap work?
71. What is the difference between HashMap and LinkedHashMap?
72. How does TreeMap work internally?
73. What are priority queues in Java?
74. What is the use of Collections.unmodifiableList()?
75. How can you sort a list of custom objects?

---

### 🔹 76–85: **Multithreading & Concurrency**

76. What is the difference between process and thread?
77. How do you create a thread in Java?
78. What is the difference between `Runnable` and `Thread`?
79. What is synchronization? How do you use `synchronized`?
80. What is a deadlock and how can it be avoided?
81. What are thread states in Java?
82. What is the difference between `wait()`, `notify()`, and `notifyAll()`?
83. What is thread pooling and how is it implemented?
84. What is the Executor framework?
85. What is `volatile` keyword in Java?

---

### 🔹 86–90: **Memory Management & Garbage Collection**

86. How does memory management work in Java?
87. What is garbage collection in Java?
88. What are the types of garbage collectors in JVM?
89. What is the difference between heap and stack memory?
90. How can you make an object eligible for garbage collection?

---

### 🔹 91–100: **Java 8+ Features (Functional & Streams)**

91. What are lambda expressions in Java?
92. What are functional interfaces?
93. What are default and static methods in interfaces?
94. What is the Stream API in Java?
95. What are intermediate and terminal operations in streams?
96. What is Optional and how is it used?
97. What is method reference in Java?
98. What is the use of `Collectors.toList()`?
99. What are predicates and consumers in Java?
100. How does Java support functional programming?

---

### 📘 Bonus Options

Would you like:
- A **PDF version** of this list?
- Detailed **answers with code examples** for each?
- A **Java interview cheat sheet** with key concepts?
- Or a **topic-by-topic preparation plan**?

Let me know and I’ll set it up for you!