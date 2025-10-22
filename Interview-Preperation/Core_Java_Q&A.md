## ✅ Top 100 Core Java Interview Questions

---

### 🔹 1–15: **OOPs Concepts & Basics**

## 1. What are the main principles of Object-Oriented Programming?

The main principles of **Object-Oriented Programming (OOP)** are often summarized as **four core pillars**. These principles help structure code in a modular, reusable, and scalable way.

### 1. **Encapsulation**
- **Definition**: Binding data (variables) and code (methods) together as a single unit and restricting direct access to some of the object's components.
- **Purpose**: To hide internal details and only expose what is necessary (via access modifiers like `private`, `public`, `protected`).
- **Example**: Using getters and setters to access private fields in a class.

```java
public class Person {
    private String name; // encapsulated field

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

---

### 2. **Abstraction**
- **Definition**: Hiding complex implementation details and showing only the essential features of the object.
- **Purpose**: To reduce complexity and increase efficiency by exposing only what is necessary.
- **Example**: Using interfaces or abstract classes to define a contract without specifying the complete behavior.

```java
interface Vehicle {
    void start();
}
```

---

### 3. **Inheritance**
- **Definition**: A mechanism where one class (child) inherits the properties and behaviors (methods) of another class (parent).
- **Purpose**: To promote code reuse and method overriding for achieving runtime polymorphism.
- **Example**:

```java
class Animal {
    void sound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("Dog barks");
    }
}
```

---

### 4. **Polymorphism**
- **Definition**: The ability of a single function or method to work in different ways depending on the object calling it.
- **Types**:
    - **Compile-time polymorphism** (Method Overloading)
    - **Runtime polymorphism** (Method Overriding)
- **Example**:

```java
class MathUtils {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }
}
```
---

## 2. What is the difference between abstraction and encapsulation?

### 🔍 **Definition**

| Concept        | Abstraction                                           | Encapsulation                                        |
|----------------|--------------------------------------------------------|-------------------------------------------------------|
| **What it is** | Hiding **implementation details** and showing only the **essential features** | Hiding **data** (variables) by restricting access and exposing only through methods |
| **Focus**      | Focuses on **what** an object does                    | Focuses on **how** the object hides its data         |

---

### 🎯 **Purpose**

- **Abstraction**: Simplify complexity by exposing only necessary functionality.
- **Encapsulation**: Protect the internal state of the object from unintended changes.

---

### 📦 **Example in Java**

#### 🔸 *Abstraction Example:*

```java
abstract class Animal {
    abstract void sound(); // abstract method (only behavior)
}

class Dog extends Animal {
    void sound() {
        System.out.println("Dog barks");
    }
}
```
- `Animal` shows **only essential behavior** (`sound()`), without implementation.
- `Dog` gives the actual implementation — abstraction in action.

#### 🔸 *Encapsulation Example:*

```java
class Person {
    private String name; // private data - hidden

    public String getName() {  // public getter
        return name;
    }

    public void setName(String name) {  // public setter
        this.name = name;
    }
}
```
- Data (`name`) is **hidden** from outside and accessed only through **controlled methods**.

---

### 🧠 In Simple Words:
| | |
|-|--|
| **Abstraction** is like driving a car — you know how to steer and brake, but you don’t need to know how the engine works. |
| **Encapsulation** is like the engine being under the hood — it's hidden and protected from direct access or changes. |

---

## 3. What is inheritance in Java? How does it work?

### 🔁 **What is Inheritance in Java?**

**Inheritance** is the process by which one class (called **child** or **subclass**) **inherits** the fields and methods of another class (called **parent** or **superclass**).

👉 It helps in:
- **Code reuse** (write once, reuse many times),
- **Method overriding** (runtime polymorphism),
- **Creating hierarchical class structures**.

---

### 🧠 **How It Works:**

- Use the `extends` keyword to inherit a class.
- The subclass inherits **non-private** members (fields and methods) of the superclass.
- Subclass can:
    - Use inherited methods/fields directly.
    - **Override** superclass methods for custom behavior.
    - Add its **own methods and fields**.

---

### 🔧 **Example:**

```java
// Superclass (Parent)
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

// Subclass (Child)
class Dog extends Animal {
    void bark() {
        System.out.println("Dog barks.");
    }
}

public class Test {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.eat();  // inherited method
        d.bark(); // method of Dog class
    }
}
```

**Output:**
```
This animal eats food.
Dog barks.
```

---

### ✅ **Key Points:**

- Java supports **single inheritance** (one class can extend only one class).
- To achieve **multiple inheritance**, Java uses **interfaces**.
- A subclass can **override** methods of its superclass to provide custom behavior.
- Constructors are **not inherited**, but the **super()** call is used to invoke the parent constructor.

---

### 🔒 Access Modifiers & Inheritance:
| Modifier   | Inherited? | Accessible in subclass? |
|------------|------------|--------------------------|
| `public`   | ✅ Yes     | ✅ Yes                   |
| `protected`| ✅ Yes     | ✅ Yes                   |
| `default`  | ✅ Yes     | ☑️ Yes (only in same package) |
| `private`  | ❌ No      | ❌ No                   |

---

## 4. What is method overloading and method overriding?

## 🔁 **1. Method Overloading** (👉 Compile-Time Polymorphism)

### ✅ **What is it?**
When **multiple methods in the same class** have the **same name** but **different parameters** (type, number, or order).

### 🎯 **Purpose:** Increases flexibility and readability. You can call the same method in different ways.

### 🔧 **Example:**

```java
class MathUtils {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }

    int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

> 🧠 Same method name `add()`, but different parameter signatures = **method overloading**.

---

## 🔄 **2. Method Overriding** (👉 Runtime Polymorphism)

### ✅ **What is it?**
When a **subclass** provides a **specific implementation** of a method that is already defined in its **superclass**.

### 🎯 **Purpose:** To achieve dynamic method dispatch — Java decides at runtime which version of the method to call based on the object's actual type.

### 🔧 **Example:**

```java
class Animal {
    void sound() {
        System.out.println("Some animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}
```

### ▶️ **Usage:**
```java
Animal a = new Dog();
a.sound();  // Output: Dog barks
```

> 🧠 The subclass (`Dog`) overrides the `sound()` method of its superclass (`Animal`) = **method overriding**.

---

## 🆚 **Overloading vs Overriding - Key Differences:**

| Feature              | Method Overloading                        | Method Overriding                          |
|----------------------|--------------------------------------------|---------------------------------------------|
| **Where it occurs**  | Same class                                 | Subclass and superclass                     |
| **Method Signature** | Must be **different**                      | Must be **same**                            |
| **Return Type**      | Can be same or different                   | Must be same (or covariant)                 |
| **Access Modifier**  | Can change freely                          | Cannot reduce visibility                    |
| **Polymorphism**     | Compile-time                               | Runtime                                     |
| **Inheritance**      | Not required                               | Required                                    |

---

## 5. What is polymorphism? Explain with an example.

## 🔁 **What is Polymorphism?**

**Polymorphism** means **“many forms”**.  
It allows **one interface** to be used for a **general class of actions**, making the code more **flexible and reusable**.

---

### 🔥 **Types of Polymorphism in Java**

| Type                   | Also Known As        | How It's Achieved       |
|------------------------|----------------------|--------------------------|
| **Compile-time**       | Static Polymorphism  | Method Overloading       |
| **Runtime**            | Dynamic Polymorphism | Method Overriding        |

---

### ✅ **1. Compile-Time Polymorphism (Method Overloading)**

**Definition:** Same method name with **different parameter lists** within the same class.

```java
class Calculator {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }
}
```

**Usage:**

```java
Calculator calc = new Calculator();
System.out.println(calc.add(2, 3));         // Outputs 5
System.out.println(calc.add(2.5, 3.5));     // Outputs 6.0
```

---

### ✅ **2. Runtime Polymorphism (Method Overriding)**

**Definition:** When a **subclass overrides** a method from the superclass, and the method that gets called is determined **at runtime**.

```java
class Animal {
    void sound() {
        System.out.println("Animal makes sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}

class Cat extends Animal {
    @Override
    void sound() {
        System.out.println("Cat meows");
    }
}
```

**Usage:**

```java
Animal a1 = new Dog();
Animal a2 = new Cat();

a1.sound();  // Output: Dog barks
a2.sound();  // Output: Cat meows
```

> 🧠 Even though the reference type is `Animal`, the actual object type (`Dog`, `Cat`) determines the method to call at **runtime** — that’s **runtime polymorphism**.

---

### 🎯 **Why Use Polymorphism?**

- Promotes **code reuse** and **scalability**
- Makes code more **flexible** and **maintainable**
- Enables **interface-based design**

---

## 6. What is the difference between static and non-static methods?

## 🔍 **1. Static Methods**

### ✅ **Definition:**
A **static method** belongs to the **class itself**, not to any specific object.

### 🔧 **Syntax:**
```java
class MyClass {
    static void sayHello() {
        System.out.println("Hello from static method");
    }
}
```

### ▶️ **Usage:**
```java
MyClass.sayHello();  // No object needed
```

---

## 🔓 **2. Non-Static Methods (Instance Methods)**

### ✅ **Definition:**
A **non-static method** belongs to a **specific object (instance)** of the class.

### 🔧 **Syntax:**
```java
class MyClass {
    void sayHi() {
        System.out.println("Hi from non-static method");
    }
}
```

### ▶️ **Usage:**
```java
MyClass obj = new MyClass();
obj.sayHi();  // Requires an object
```

---

## 🆚 **Static vs Non-Static - Quick Comparison**

| Feature                  | Static Method                         | Non-Static Method                      |
|--------------------------|----------------------------------------|----------------------------------------|
| **Belongs to**           | Class                                  | Instance (Object)                      |
| **Called using**         | `ClassName.method()`                   | `object.method()`                      |
| **Can access**           | Only static variables/methods          | Both static and non-static members     |
| **Memory**               | Allocated once (class-level)           | Allocated for each object              |
| **Usage**                | Utility/helper methods (e.g., `Math.max()`) | Business logic or behavior per object |
| **Keyword needed?**      | Yes → `static`                         | No `static` keyword                    |

---

### ✅ **Example with Both:**

```java
class Demo {
    static void staticMethod() {
        System.out.println("Static method called.");
    }

    void nonStaticMethod() {
        System.out.println("Non-static method called.");
    }
}
```

**Calling:**
```java
Demo.staticMethod();          // No object needed
Demo d = new Demo();
d.nonStaticMethod();          // Object required
```

---

## 7. Can a constructor be final, static, or abstract?

## ❓ **Can a constructor be `final`, `static`, or `abstract`?**

### ✖️ 1. **Can a constructor be `final`?** → **No**

🔹 **Why not?**  
`final` means the method **cannot be overridden** by subclasses.  
But constructors are **not inherited**, so there's no point in marking them `final`.

> ✅ **Conclusion**: It's meaningless — constructors can’t be `final`.

---

### ✖️ 2. **Can a constructor be `static`?** → **No**

🔹 **Why not?**  
`static` means something **belongs to the class**, not an object.  
But a **constructor is used to create objects** — you can't call it without an object, and it **can't be shared like static methods**.

> ✅ **Conclusion**: Constructors are inherently non-static because they are used to **instantiate objects**.

---

### ✖️ 3. **Can a constructor be `abstract`?** → **No**

🔹 **Why not?**  
`abstract` means a method **must be overridden** in a subclass and **has no body**.  
But constructors:
- **Always have a body**
- **Can't be overridden**
- **Aren’t inherited**

> ✅ **Conclusion**: Constructors can't be `abstract` — it contradicts their purpose.

---

### ✅ **Quick Summary Table:**

| Modifier   | Allowed with Constructor? | Reason |
|------------|---------------------------|--------|
| `final`    | ❌ No                     | Constructors are not inherited |
| `static`   | ❌ No                     | Constructors are tied to object creation |
| `abstract` | ❌ No                     | Constructors can’t be abstract or inherited |

---

## 8. What is the difference between == and equals() in Java?

## 🔁 **`==` vs `.equals()` in Java**

| Feature          | `==`                                   | `.equals()`                                |
|------------------|----------------------------------------|---------------------------------------------|
| **Type**         | Operator                                | Method (defined in `Object` class)         |
| **Compares**     | **References** (memory addresses)       | **Contents/Values** (depends on class)     |
| **Used For**     | Primitive types & object reference check | Logical comparison (mainly for objects)    |
| **Can be overridden?** | ❌ No                            | ✅ Yes (e.g., in `String`, `Integer`)       |

---

### ✅ **1. Primitive Types (like int, float)**

```java
int a = 10;
int b = 10;

System.out.println(a == b);       // ✅ true
// .equals() can't be used on primitives
```

---

### ✅ **2. Object Reference Comparison (`==`)**

```java
String s1 = new String("Aditya");
String s2 = new String("Aditya");

System.out.println(s1 == s2);     // ❌ false (different objects)
```

---

### ✅ **3. Content Comparison (`.equals()`)**

```java
System.out.println(s1.equals(s2)); // ✅ true (compares values)
```

---

### 🧠 **Under the Hood:**
- `==` compares **whether both references point to the same object** in memory.
- `.equals()` checks if the **actual data** inside the objects are equal.

---

### ✅ **Example with Custom Class:**

```java
class Person {
    String name;

    Person(String name) {
        this.name = name;
    }
}

public class Test {
    public static void main(String[] args) {
        Person p1 = new Person("Adi");
        Person p2 = new Person("Adi");

        System.out.println(p1 == p2);          // ❌ false (different objects)
        System.out.println(p1.equals(p2));     // ❌ false (default equals = reference check)
    }
}
```

➡️ If you **override `.equals()`** in `Person` to compare names, the second check will return `true`.

---

### 💡 TL;DR:

| Use this... | When you want to... |
|-------------|---------------------|
| `==`        | Check if two **references** point to the **same object** |
| `.equals()` | Check if two objects have **equal values** (logical equality) |

---

## 9. What is the role of the `this` and `super` keywords?

## 🔷 **`this` Keyword in Java**

### ✅ **Purpose:**
`this` refers to the **current object** (the object on which the method or constructor is called).

---

### 🔧 **Common Uses of `this`:**

1. **To refer to current class instance variable:**
```java
class Student {
    String name;

    Student(String name) {
        this.name = name; // 'this' refers to the current object's variable
    }
}
```

2. **To invoke current class methods:**
```java
void display() {
    System.out.println("Display called");
    this.show(); // optional, can just write show();
}

void show() {
    System.out.println("Show called");
}
```

3. **To call another constructor in the same class:**
```java
class Demo {
    Demo() {
        this(10);  // calls parameterized constructor
        System.out.println("Default Constructor");
    }

    Demo(int x) {
        System.out.println("Parameterized Constructor: " + x);
    }
}
```

---

## 🔶 **`super` Keyword in Java**

### ✅ **Purpose:**
`super` refers to the **immediate parent class** of the current class.

---

### 🔧 **Common Uses of `super`:**

1. **To call parent class constructor:**
```java
class Animal {
    Animal() {
        System.out.println("Animal constructor");
    }
}

class Dog extends Animal {
    Dog() {
        super(); // optional, Java adds it implicitly
        System.out.println("Dog constructor");
    }
}
```

2. **To access parent class methods:**
```java
class Animal {
    void sound() {
        System.out.println("Animal makes sound");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("Dog barks");
        super.sound(); // call parent class method
    }
}
```

3. **To access parent class variables:**
```java
class Animal {
    String type = "Animal";
}

class Dog extends Animal {
    String type = "Dog";

    void printType() {
        System.out.println(this.type);   // Dog
        System.out.println(super.type);  // Animal
    }
}
```

---

### 🔄 **`this` vs `super` — Quick Comparison**

| Feature                | `this`                              | `super`                            |
|------------------------|--------------------------------------|------------------------------------|
| Refers to              | Current class object                 | Parent class object                |
| Used in                | Same class                          | Child class                        |
| Calls constructor/methods/variables from | Current class         | Parent class                        |
| Can be used in static context? | ❌ No                         | ❌ No                               |

---

## 10. What are access modifiers in Java?

Understanding **access modifiers** is key to writing secure, well-structured, and modular Java code. Let’s break it down with definitions, a comparison table, and practical examples.

---

## 🔐 **What are Access Modifiers in Java?**

Access modifiers define **how accessible** a **class, method, constructor, or variable** is from **other classes**.

---

### ✅ **Types of Access Modifiers:**

| Modifier     | Accessible Within | Same Package | Subclasses in Other Packages | Other Classes |
|--------------|------------------|--------------|-------------------------------|----------------|
| `public`     | ✅ Yes            | ✅ Yes       | ✅ Yes                        | ✅ Yes          |
| `protected`  | ✅ Yes            | ✅ Yes       | ✅ Yes                        | ❌ No           |
| (default)    | ✅ Yes            | ✅ Yes       | ❌ No                         | ❌ No           |
| `private`    | ✅ Yes            | ❌ No        | ❌ No                         | ❌ No           |

> 💡 **Default** means **no modifier** is specified.

---

## 🔍 **Modifier Details & Examples**

---

### 🔓 `public`

- Accessible from **anywhere** in the project (same package or different).
```java
public class Test {
    public void show() {
        System.out.println("Public method");
    }
}
```

---

### 🔒 `private`

- Accessible **only within the same class**.
- Commonly used for **data hiding**.

```java
class Demo {
    private int value = 5;

    private void display() {
        System.out.println("Private method");
    }
}
```

---

### 🛡️ `protected`

- Accessible:
    - Within the same package
    - In **subclasses**, even if they are in **different packages**
```java
class Animal {
    protected void sound() {
        System.out.println("Animal sound");
    }
}
```

---

### 🔸 Default (No modifier)

- Accessible **only within the same package**.
```java
class MyClass {
    void greet() {  // default access
        System.out.println("Hello from default method");
    }
}
```

---

## 🧠 When to Use What?

| Goal                       | Use Modifier      |
|---------------------------|-------------------|
| Use everywhere             | `public`          |
| Hide implementation details | `private`         |
| Share with child classes   | `protected`       |
| Package-level control      | **default** (no modifier) |

---

## 11. What is the difference between an abstract class and an interface?

This one comes up in almost **every Java interview**, especially when talking about **OOP design**. Let's break down the **difference between an abstract class and an interface** in Java with a full comparison and examples.

---

## 🔷 **Abstract Class vs Interface in Java**

| Feature                        | **Abstract Class**                              | **Interface**                               |
|-------------------------------|--------------------------------------------------|----------------------------------------------|
| **Purpose**                   | To provide a **base class with default behavior** | To define a **contract** for what a class can do |
| **Keyword**                   | `abstract class`                                 | `interface`                                   |
| **Methods**                   | Can have **abstract and concrete methods**        | Can have **abstract, default, static, private** methods |
| **Variables**                 | Can have **instance variables**                  | Only `public static final` constants (by default) |
| **Constructors**              | ✅ Yes                                            | ❌ No                                         |
| **Multiple Inheritance**      | ❌ Not allowed (only one superclass)              | ✅ Yes (a class can implement multiple interfaces) |
| **Access Modifiers on Methods**| Can be `public`, `protected`, `private`          | All methods are `public` (by default)         |
| **When to use**              | When some **common behavior** is shared           | When you need to define a **pure capability/contract** |

---

## ✅ **Example of Abstract Class**

```java
abstract class Animal {
    abstract void sound();  // abstract method

    void eat() {
        System.out.println("Animal eats");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("Dog barks");
    }
}
```

➡️ `Dog` must implement `sound()` but inherits `eat()` as-is.

---

## ✅ **Example of Interface**

```java
interface Vehicle {
    void drive();  // abstract by default
}

class Car implements Vehicle {
    public void drive() {
        System.out.println("Car is driving");
    }
}
```

➡️ `Car` implements `drive()` as per the contract of `Vehicle`.

---

## 🧠 Real-World Analogy:

- **Abstract Class** = A base "template" with **some code already written**.
- **Interface** = A **completely empty contract** that says "if you implement me, you must do X, Y, Z".

---

## 🔥 Java 8+ Note:

Since Java 8 and later:
- **Interfaces can have:**
    - `default` methods (with body)
    - `static` methods
    - `private` methods (Java 9+)

So interfaces have become **more powerful**, but abstract classes still have their place when:
- You need **constructors**
- You want to **maintain state** with instance variables

---

## 12. Can you implement multiple interfaces in Java?

In **Java**, a class **can implement multiple interfaces** — and this is one of the key features that makes interfaces powerful and flexible. 🔥

---

## ✅ **Why is it allowed?**
Java **doesn’t support multiple inheritance with classes** (to avoid ambiguity like the Diamond Problem),  
**but it allows multiple interface implementation** because:
- Interfaces don't have instance variables.
- Methods in interfaces are either **abstract** (no body) or **default/static**, which avoids conflict.

---

## 🔧 **Syntax Example:**

```java
interface Printable {
    void print();
}

interface Showable {
    void show();
}

class MyClass implements Printable, Showable {
    public void print() {
        System.out.println("Printing...");
    }

    public void show() {
        System.out.println("Showing...");
    }
}
```

### ▶️ **Usage:**
```java
public class Test {
    public static void main(String[] args) {
        MyClass obj = new MyClass();
        obj.print();  // Output: Printing...
        obj.show();   // Output: Showing...
    }
}
```

---

## 🧠 Key Points:

- A class can implement **as many interfaces** as needed:
  ```java
  class A implements Interface1, Interface2, Interface3 { ... }
  ```

- If **two interfaces have methods with the same signature**, there’s **no conflict** — you just provide **one implementation**.

- If **two interfaces have default methods with the same name**, you'll need to **override it** in the class to resolve ambiguity.

---

### ⚠️ **Example: Default Method Conflict**

```java
interface A {
    default void greet() {
        System.out.println("Hello from A");
    }
}

interface B {
    default void greet() {
        System.out.println("Hello from B");
    }
}

class C implements A, B {
    // Must override to resolve conflict
    public void greet() {
        A.super.greet();  // or B.super.greet()
    }
}
```

---

## ✅ Conclusion:

Yes, you can **definitely implement multiple interfaces** in Java. It's a common practice when you want to combine multiple behaviors or capabilities — like `Serializable`, `Cloneable`, `Comparable`, etc.

Want to try a mini example mixing 3 interfaces like `Flyable`, `Swimmable`, and `Runnable`? 😄

---

## 13. What is the purpose of the `final` keyword in Java?

The `final` keyword is a **multi-purpose modifier** in Java, and it can be used with **variables**, **methods**, and **classes** — each with a different but important meaning.

Let’s break it down clearly:

---

## 🔒 **Purpose of `final` in Java**

| Can be used with | Meaning |
|------------------|---------|
| `final` variable | Value **cannot be changed** (like a constant) |
| `final` method   | Method **cannot be overridden** in subclasses |
| `final` class    | Class **cannot be extended/inherited** |

---

### ✅ 1. **Final Variable** (constant)

Once assigned, the value **cannot be changed**.

```java
final int MAX_USERS = 100;
MAX_USERS = 200;  // ❌ Compile-time error
```

🔹 **Tip:** Common for constants like `PI`, `MAX_SIZE`, etc.

---

### ✅ 2. **Final Method** (no overriding)

Used to **prevent a method from being overridden** by subclasses.

```java
class Parent {
    final void show() {
        System.out.println("Parent method");
    }
}

class Child extends Parent {
    // void show() {} ❌ Error: cannot override final method
}
```

---

### ✅ 3. **Final Class** (no inheritance)

Used to **prevent a class from being subclassed**.

```java
final class Utility {
    static void help() {
        System.out.println("Helping...");
    }
}

// class MyUtil extends Utility {} ❌ Error: cannot inherit from final class
```

---

## 🔍 Bonus: Final Reference Variables (Objects)

```java
final Student s = new Student("Aditya");
s = new Student("John");  // ❌ Not allowed

// But you CAN modify internal state
s.name = "Rahul";  // ✅ Allowed
```

🔸 You can't change the **reference**, but can still modify the **object it points to**.

---

## 🔐 TL;DR

| Usage | Effect |
|-------|--------|
| `final` variable | Makes value constant |
| `final` method | Prevents method from being overridden |
| `final` class | Prevents class from being subclassed |

---

## 14. What are default methods in interfaces (Java 8)?

**Default methods in interfaces** were introduced in **Java 8**, and they significantly enhanced the power of interfaces.

Let’s break it down step by step 👇

---

## 🔧 **What are Default Methods in Interfaces (Java 8)?**

Default methods allow you to **add method implementations inside interfaces** without breaking existing implementations of that interface.

> ✅ **Keyword:** `default`

---

### ✅ **Why were they introduced?
To solve the "diamond problem" of evolving interfaces.**

Imagine adding a new method to an interface that many classes already implement — it would break all of them. Default methods provide a **default implementation** so existing classes **don’t need to implement it unless they want to override**.

---

## 🔍 **Syntax Example:**

```java
interface MyInterface {
    default void greet() {
        System.out.println("Hello from default method!");
    }
}
```

---

### ✅ **Implemented in Class:**

```java
class MyClass implements MyInterface {
    // No need to override 'greet' unless custom behavior needed
}

public class Test {
    public static void main(String[] args) {
        MyClass obj = new MyClass();
        obj.greet();  // Output: Hello from default method!
    }
}
```

---

## 🛠️ **Key Characteristics:**

| Feature                        | Default Method                           |
|-------------------------------|------------------------------------------|
| **Has method body?**          | ✅ Yes                                    |
| **Can be overridden?**        | ✅ Yes                                    |
| **Access modifier?**          | Must be `public` (implicitly)            |
| **Allowed in abstract class?**| ❌ No need — abstract classes already allow method bodies |
| **Can call private/static methods?** | ✅ Yes (Java 9+ allows private methods in interfaces too) |

---

## ⚠️ **Multiple Default Methods — Conflict**

If a class implements **two interfaces with the same default method**, it **must override** it to resolve ambiguity.

```java
interface A {
    default void greet() {
        System.out.println("Hello from A");
    }
}

interface B {
    default void greet() {
        System.out.println("Hello from B");
    }
}

class C implements A, B {
    public void greet() {
        A.super.greet(); // or B.super.greet()
    }
}
```

---

## ✅ **Real-World Example: Java 8 Collections API**

The `List` interface got new default methods:

```java
List<String> list = Arrays.asList("Java", "Python", "C++");

list.forEach(System.out::println); // 'forEach' is a default method
```

---

## 🔥 TL;DR

| Feature               | Description |
|-----------------------|-------------|
| **default method**    | A method in an interface with a **default implementation** |
| **Why needed**        | To add new functionality to interfaces **without breaking old code** |
| **Can override?**     | ✅ Yes |

---

## 15. What is the diamond problem in Java?

The **diamond problem** is a classic issue in object-oriented languages that support **multiple inheritance**, and Java handles it in a very specific way. Let’s unpack it with examples and visualizations. 🧩

---

## 💎 What is the **Diamond Problem**?

The **diamond problem** occurs when a class inherits from two classes **that both inherit from a common superclass**, and all of them have a method with the **same signature**.

➡️ This creates **ambiguity** — which version of the method should be inherited?

---

## 🔻 Diamond Problem — Visual Example (Hypothetical)

```
      A
     / \
    B   C
     \ /
      D
```

- Class `A` has a method `display()`.
- Classes `B` and `C` override `display()`.
- Class `D` extends both `B` and `C` (in **languages that allow multiple inheritance**).

> 🛑 In this case, which `display()` method should `D` inherit? `B`'s or `C`'s? This is the **diamond problem**.

---

## 🧯 How Java Avoids It

Java **does NOT allow multiple inheritance of classes** to **prevent** this ambiguity.

```java
class A {
    void display() { System.out.println("A"); }
}

class B extends A {
    void display() { System.out.println("B"); }
}

class C extends A {
    void display() { System.out.println("C"); }
}

// class D extends B, C {}  ❌ Not allowed in Java
```

You get a **compile-time error**:  
`"Class D inherits unrelated defaults for display() from types B and C"`

---

## ✅ What About Interfaces?

Java **does allow** multiple inheritance with **interfaces**.  
But since **Java 8**, interfaces can have **default methods**, and this can also cause a **diamond-like situation**.

### 🔧 Example:

```java
interface A {
    default void greet() {
        System.out.println("Hello from A");
    }
}

interface B {
    default void greet() {
        System.out.println("Hello from B");
    }
}

class C implements A, B {
    public void greet() {
        A.super.greet(); // Resolve ambiguity manually
    }
}
```

> ✅ Java forces you to **override the method and specify** which interface's version to use, solving the diamond problem.

---

## 🧠 TL;DR

| Aspect                   | Description |
|--------------------------|-------------|
| **What is it?**          | Ambiguity in multiple inheritance when the same method exists in multiple parent classes |
| **Does Java allow it?**  | ❌ For classes (prevents it entirely) |
| **Interfaces?**          | ✅ Yes — but requires **explicit resolution** if conflict occurs |
| **How to resolve?**      | Use `InterfaceName.super.methodName()` in the subclass |

---

Let me know if you'd like a visual diagram or want to explore how C++ handles it differently (with virtual inheritance)!

---

### 🔹 16–30: **Data Types, Variables, Operators**

## 16. What is the difference between primitive and reference types?

The difference between **primitive types** and **reference types** is fundamental in programming languages like Java. Here's a clear breakdown:

---

### ✅ **Primitive Types:**
- **Definition:** These are the most basic data types built into the language.
- **Examples in Java:** `int`, `byte`, `short`, `long`, `float`, `double`, `char`, `boolean`
- **Stored in:** **Stack memory**
- **Holds:** The actual value
- **Size:** Fixed (depending on type, e.g., `int` is 4 bytes)
- **Immutable:** Values are not changeable (though variables can be reassigned)

**Example:**
```java
int a = 5;
int b = a;
b = 10;
System.out.println(a); // Output: 5 (a is unaffected by changes to b)
```

---

### ✅ **Reference Types:**
- **Definition:** These refer to objects created from classes, including arrays and custom classes.
- **Examples in Java:** `String`, `Array`, `Object`, `List`, custom class like `Employee`, etc.
- **Stored in:** **Heap memory** (reference itself is on the stack)
- **Holds:** A reference (memory address) to the actual object
- **Size:** Varies (depends on object)
- **Mutable:** Objects can be changed through references

**Example:**
```java
int[] arr1 = {1, 2, 3};
int[] arr2 = arr1;
arr2[0] = 10;
System.out.println(arr1[0]); // Output: 10 (both arr1 and arr2 refer to the same object)
```

---

### 🔑 Key Differences:

| Feature              | Primitive Type      | Reference Type           |
|----------------------|---------------------|---------------------------|
| Stores               | Actual value         | Memory address (reference)|
| Memory location      | Stack                | Heap (object), Stack (reference) |
| Mutability           | Immutable            | Mutable (usually)         |
| Default value        | 0, false, etc.       | `null`                    |
| Comparison (`==`)    | Compares value       | Compares reference (memory address) |
| Performance          | Faster               | Slightly slower (object overhead) |

---

## 17. What is autoboxing and unboxing in Java?

Great question! In Java, **autoboxing** and **unboxing** are features that help bridge the gap between **primitive types** and their **wrapper classes**.

---

### ✅ **Autoboxing:**
It is the **automatic conversion** of a **primitive type** into its **corresponding wrapper class** by the compiler.

#### 🔁 Primitive → Wrapper

| Primitive | Wrapper Class |
|-----------|----------------|
| `int`     | `Integer`      |
| `char`    | `Character`    |
| `boolean` | `Boolean`      |
| `double`  | `Double`       |
| etc.      |                |

#### 🧠 Example:
```java
int num = 10;
Integer obj = num;  // Autoboxing: int → Integer
```

---

### ✅ **Unboxing:**
It is the **automatic conversion** of a **wrapper class object** back into its **corresponding primitive type**.

#### 🔁 Wrapper → Primitive

#### 🧠 Example:
```java
Integer obj = 20;
int num = obj;  // Unboxing: Integer → int
```

---

### ✅ Why are they useful?
Because Java Collections (like `ArrayList`) **only work with objects**, not primitives. So autoboxing allows seamless use of primitives in these cases.

#### 🧠 Example:
```java
List<Integer> list = new ArrayList<>();
list.add(5);     // Autoboxing: int → Integer
int x = list.get(0);  // Unboxing: Integer → int
```

---

### 🔎 Internally (What Java does):
```java
Integer obj = Integer.valueOf(num);  // Autoboxing
int num = obj.intValue();            // Unboxing
```

---

## 18. What is type casting? Explain implicit and explicit casting.

Great! Let’s break down **type casting** in Java in a simple way.

---

## ✅ What is Type Casting?
**Type casting** is the process of converting a variable from one data type to another.

Java supports two types of casting:

---

## 🔹 1. **Implicit Casting (Widening Conversion)**

- **Automatically done** by the compiler.
- Happens when you convert a **smaller** type to a **larger** type.
- **No data loss**.

### 🔁 Example:
```java
int a = 100;
long b = a;  // int → long (Implicit)
```

### ✅ Valid Widening:
| From     | To               |
|----------|------------------|
| byte     | short, int, long, float, double |
| short    | int, long, float, double        |
| char     | int, long, float, double        |
| int      | long, float, double             |
| long     | float, double                   |
| float    | double                          |

---

## 🔹 2. **Explicit Casting (Narrowing Conversion)**

- **Manually done** by the programmer using a cast operator.
- Happens when you convert a **larger** type to a **smaller** type.
- **Possible data loss** or precision loss.

### 🔁 Example:
```java
double x = 10.5;
int y = (int) x;  // double → int (Explicit)
System.out.println(y); // Output: 10
```

### ⚠️ Notes:
- Might result in **truncation** (decimal part lost).
- Can cause **overflow/underflow**.

---

### 🔁 Quick Summary:

| Feature                | Implicit Casting           | Explicit Casting             |
|------------------------|----------------------------|------------------------------|
| Also called            | Widening                   | Narrowing                    |
| Conversion direction   | Smaller → Larger type      | Larger → Smaller type        |
| Performed by compiler  | Yes                        | No (done manually)           |
| Risk of data loss      | No                         | Yes                          |
| Syntax                 | Automatic                  | `(type)` before the variable |

---

## 19. What is the difference between int and Integer?

Understanding the difference between `int` and `Integer` is key when working in Java.

---

## ✅ `int` vs `Integer`

| Feature             | `int` (Primitive)           | `Integer` (Wrapper Class)      |
|---------------------|-----------------------------|-------------------------------|
| Type                | Primitive data type         | Reference (Object) type       |
| Stored in           | Stack memory                | Heap memory (object), reference in stack |
| Holds               | Actual numeric value        | Reference to an `Integer` object |
| Default value       | `0`                         | `null`                        |
| Can be `null`?      | ❌ No                       | ✅ Yes                         |
| Part of collections?| ❌ No (not directly)        | ✅ Yes                         |
| Methods available?  | ❌ None                     | ✅ Yes (`intValue()`, `compareTo()`, etc.) |
| Autoboxing allowed? | ❌ Not needed               | ✅ Automatically from `int`   |

---

### 🔁 Example of Autoboxing:
```java
int num = 10;
Integer obj = num;  // Autoboxing: int → Integer
```

### 🔁 Example of Unboxing:
```java
Integer obj = 20;
int num = obj;  // Unboxing: Integer → int
```

---

### ✅ When to use which?

| Use `int` when...         | Use `Integer` when...                      |
|---------------------------|--------------------------------------------|
| Performance matters       | You need to use objects (like in collections) |
| You’re doing calculations | You need `null` values or object methods   |

---

## 20. What are wrapper classes in Java?

Let’s dive into **Wrapper Classes** in Java.

---

## ✅ What are Wrapper Classes?

**Wrapper classes** in Java are **object representations of primitive data types**.  
They "wrap" the primitive values in an **object** so they can be used where objects are required—like in **collections, generics, or method calls expecting objects**.

---

### 🔁 Primitive to Wrapper Mapping:

| Primitive Type | Wrapper Class   |
|----------------|-----------------|
| `byte`         | `Byte`          |
| `short`        | `Short`         |
| `int`          | `Integer`       |
| `long`         | `Long`          |
| `float`        | `Float`         |
| `double`       | `Double`        |
| `char`         | `Character`     |
| `boolean`      | `Boolean`       |

---

### ✅ Why are Wrapper Classes Needed?

1. **Collections API** – Java collections (like `ArrayList`) **can’t store primitives**, only objects.
   ```java
   List<Integer> list = new ArrayList<>();
   list.add(5);  // int gets autoboxed to Integer
   ```

2. **Object Methods** – Wrapper classes provide **useful methods**:
   ```java
   Integer num = 42;
   String str = num.toString();  // "42"
   ```

3. **Null Support** – Primitives can’t be `null`, but wrapper objects can:
   ```java
   Integer a = null; // OK
   int b = null;     // ❌ Compile-time error
   ```

4. **Autoboxing & Unboxing** – Java automatically converts between primitives and wrappers:
   ```java
   Integer obj = 10; // Autoboxing
   int val = obj;    // Unboxing
   ```

---

### 🧠 Quick Example:

```java
int a = 10;                  // primitive
Integer b = Integer.valueOf(a); // manual boxing
int c = b.intValue();        // manual unboxing
```

Or using **autoboxing/unboxing**:
```java
Integer x = 10;  // autoboxing
int y = x;       // unboxing
```

---

## 21. What are the different types of variables in Java?

Java has **three main types of variables**, each with a specific purpose and scope.

---

## ✅ Types of Variables in Java:

| Type             | Also Known As     | Scope               | Stored In         | Default Value     |
|------------------|-------------------|---------------------|-------------------|-------------------|
| **Local**        | Method variable   | Inside a method/block | Stack          | ❌ Must be initialized |
| **Instance**     | Non-static field  | Per object          | Heap              | ✅ Based on type    |
| **Static**       | Class variable    | Shared across all objects | Heap (Class area) | ✅ Based on type    |

---

### 🔹 1. **Local Variables**

- Declared inside **methods**, **constructors**, or **blocks**
- **Only accessible** within that method or block
- **Must be initialized** before use
- **Not stored in object** memory

#### 🧠 Example:
```java
void show() {
    int x = 10; // local variable
    System.out.println(x);
}
```

---

### 🔹 2. **Instance Variables**

- Declared **inside a class**, but **outside any method**
- **Each object** gets its own copy
- Can be accessed using **`this`** keyword
- **Default values**: 0, false, null (if not initialized)

#### 🧠 Example:
```java
class Person {
    String name;   // instance variable
    int age;       // instance variable
}
```

---

### 🔹 3. **Static Variables**

- Declared with the `static` keyword
- **Shared** by **all objects** of the class
- **Belongs to the class**, not the instance
- Can be accessed using **ClassName.variable**

#### 🧠 Example:
```java
class Employee {
    static String company = "Google"; // static variable
}
```

---

### 📌 Bonus: Scope + Memory Summary

| Variable     | Scope            | Memory Location |
|--------------|------------------|-----------------|
| Local        | Within method/block | Stack         |
| Instance     | Within object       | Heap          |
| Static       | Within class        | Heap (Class area) |

---

## 22. What is the scope of a local, instance, and static variable?

Let’s clearly define the **scope** of **local**, **instance**, and **static** variables in Java:

---

## ✅ 1. **Local Variable Scope**

- Declared **inside** a method, constructor, or block.
- Scope is **limited to the block** where it's defined.
- **Cannot be accessed** outside that block.
- **Must be initialized** before use.

### 🧠 Example:
```java
void display() {
    int x = 10; // local variable
    System.out.println(x); // ✅ Accessible here
}
// System.out.println(x); // ❌ Not accessible here
```

---

## ✅ 2. **Instance Variable Scope**

- Declared **inside the class**, but **outside any method**.
- Scope is **entire class**, but tied to a **specific object**.
- **Accessible by all methods** of that class using `this.variableName`.
- Each **object gets its own copy**.

### 🧠 Example:
```java
class Car {
    String color; // instance variable

    void setColor(String color) {
        this.color = color; // ✅ Accessible throughout the class
    }

    void showColor() {
        System.out.println(color); // ✅ Accessible here too
    }
}
```

---

## ✅ 3. **Static Variable Scope**

- Declared with the `static` keyword inside a class.
- Scope is the **entire class**, **shared** across all objects.
- Can be accessed:
    - **Inside the class** using `ClassName.variableName` or just `variableName` (if in the same class)
    - **Outside the class** using `ClassName.variableName`

### 🧠 Example:
```java
class Employee {
    static String company = "Google"; // static variable

    void showCompany() {
        System.out.println(company); // ✅ Accessible here
    }
}

class Test {
    public static void main(String[] args) {
        System.out.println(Employee.company); // ✅ Accessible without object
    }
}
```

---

### 🔁 Quick Summary Table:

| Variable Type | Declared In        | Scope / Accessible In                   | Memory     |
|---------------|--------------------|------------------------------------------|------------|
| Local         | Method/Block       | Only within that method/block            | Stack      |
| Instance      | Inside class        | Throughout the class (using object)       | Heap       |
| Static        | Inside class (`static`) | Entire class (shared across all objects) | Heap (Class area) |

---

## 23. Explain the ternary operator in Java.

The **ternary operator** in Java is a **short-hand way of writing if-else statements**. It’s simple, compact, and super useful for quick decisions.

---

## ✅ What is the Ternary Operator?

It's a **three-part** operator (`? :`) that acts as a mini `if-else`.

### 🧠 Syntax:
```java
condition ? expression1 : expression2;
```

- If `condition` is **true**, it returns `expression1`
- If `condition` is **false**, it returns `expression2`

---

### 🔍 Example 1: Basic Usage
```java
int a = 10, b = 20;
int max = (a > b) ? a : b;
System.out.println("Max is: " + max);  // Output: Max is: 20
```

---

### 🔍 Example 2: Even or Odd
```java
int num = 7;
String result = (num % 2 == 0) ? "Even" : "Odd";
System.out.println(result);  // Output: Odd
```

---

### ✅ Benefits:
- Shorter and cleaner than `if-else`
- Works well for assignments and return values

---

### ⚠️ Caution:
- Don’t overuse it for complex logic—it can reduce readability.
- Not meant to replace full `if-else` blocks with multiple statements.

---

### 🔁 Equivalent if-else:
```java
// Ternary
String status = (age >= 18) ? "Adult" : "Minor";

// Same using if-else
String status;
if (age >= 18) {
    status = "Adult";
} else {
    status = "Minor";
}
```

---

## 24. What is short-circuit evaluation in Java?

Let's break down **short-circuit evaluation** in Java — a very handy concept in conditional logic.

---

## ✅ What is Short-Circuit Evaluation?

Short-circuit evaluation is a behavior in Java where **logical operators stop evaluating expressions as soon as the result is determined**.

### ☑️ Applies to:
- `&&` (Logical AND)
- `||` (Logical OR)

---

## 🔹 1. **Logical AND (`&&`)**

- If the **first condition is false**, Java **won’t check the second** — because the whole condition will be false anyway.

### 🧠 Example:
```java
int a = 5;
if (a > 10 && a / 0 == 1) {
    System.out.println("Won’t reach here");
}
// No error! The second part is never evaluated
```

---

## 🔹 2. **Logical OR (`||`)**

- If the **first condition is true**, Java **won’t evaluate the second** — because the whole condition will be true.

### 🧠 Example:
```java
int b = 20;
if (b > 10 || b / 0 == 1) {
    System.out.println("Short-circuited! No error.");
}
```

---

## ✅ Why is it useful?

- **Improves performance** (skips unnecessary evaluations)
- **Prevents runtime errors** (like divide by zero or null pointer exceptions)

---

### 🔁 Example: Null Check
```java
String name = null;

if (name != null && name.length() > 3) {
    System.out.println("Name is long enough");
}
// ✅ Safe — avoids NullPointerException due to short-circuit
```

---

### ⚠️ Note:
- **Short-circuit operators**: `&&`, `||`
- **Non-short-circuit versions**: `&`, `|` (used for bitwise logic or full evaluation)

---

## 25. What is the difference between ++i and i++?

The difference between `++i` and `i++` may seem small, but it can affect how your code behaves—especially in expressions.

---

## ✅ Difference Between `++i` and `i++`

| Operation     | Name             | When the increment happens | Returns       |
|---------------|------------------|-----------------------------|----------------|
| `++i`         | **Pre-increment** | Increments **before** use  | New (updated) value |
| `i++`         | **Post-increment**| Increments **after** use   | Old (original) value |

---

### 🔍 Example:

```java
int i = 5;

int a = ++i;  // i is incremented to 6, then a = 6
int b = i++;  // b = 6 (old value), then i becomes 7
```

🧾 Final values:
- `i = 7`
- `a = 6`
- `b = 6`

---

### 🔁 More Breakdown:

#### 🔹 Pre-Increment (`++i`)
```java
int x = 3;
int y = ++x;  // x becomes 4, then y = 4
```

#### 🔹 Post-Increment (`i++`)
```java
int x = 3;
int y = x++;  // y = 3, then x becomes 4
```

---

### ✅ When to Use What?

| Use `++i` when...                       | Use `i++` when...                     |
|----------------------------------------|----------------------------------------|
| You want to **increment before use**   | You want to **use the value first**, then increment |
| You're in **loop conditions** or **pre-checks** | You're using value in an expression |

---

### 🔁 Example in Loops:
```java
for (int i = 0; i < 5; ++i) // Same effect as i++
    System.out.print(i + " ");
```

💡 In loops, both `i++` and `++i` behave similarly unless used in complex expressions.

---

## 26. What are bitwise operators in Java?

Bitwise operators in Java are **used to perform operations at the binary level** — that is, they directly manipulate the bits of numbers. They're mostly used in **low-level programming, performance tuning, and some algorithm tricks**.

---

## ✅ Bitwise Operators in Java

| Operator | Name                | Description                                            |
|----------|---------------------|--------------------------------------------------------|
| `&`      | Bitwise AND         | 1 if **both** bits are 1                              |
| `|`      | Bitwise OR          | 1 if **any one** of the bits is 1                     |
| `^`      | Bitwise XOR         | 1 if **only one** of the bits is 1                    |
| `~`      | Bitwise Complement  | Inverts all bits (1s to 0s, 0s to 1s)                 |
| `<<`     | Left Shift          | Shifts bits to the left (multiplies by 2)             |
| `>>`     | Right Shift         | Shifts bits to the right (divides by 2, keeps sign)   |
| `>>>`    | Unsigned Right Shift| Shifts bits to the right, fills 0 on the left         |

---

## 🔍 Examples:

### 🔹 1. Bitwise AND (`&`)
```java
int a = 5;     // 0101
int b = 3;     // 0011
int c = a & b; // 0001 = 1
```

### 🔹 2. Bitwise OR (`|`)
```java
int c = a | b; // 0111 = 7
```

### 🔹 3. Bitwise XOR (`^`)
```java
int c = a ^ b; // 0110 = 6
```

### 🔹 4. Bitwise Complement (`~`)
```java
int a = 5;     // 00000101
int c = ~a;    // 11111010 = -6 (in 2's complement)
```

---

### 🔹 5. Left Shift (`<<`)
```java
int a = 5;        // 00000101
int c = a << 1;   // 00001010 = 10
```

### 🔹 6. Right Shift (`>>`)
```java
int a = 10;       // 00001010
int c = a >> 1;   // 00000101 = 5
```

### 🔹 7. Unsigned Right Shift (`>>>`)
```java
int a = -10;
int c = a >>> 1;  // shifts bits and fills 0 on the left
```

---

## ✅ When Are Bitwise Operators Useful?

- **Performance optimization**
- **Low-level I/O**
- **Encryption/Decryption algorithms**
- **Working with binary data**
- **Flags, masks, and bit manipulation tricks**

---

## 27. What is the difference between & and &&?

Understanding the difference between `&` and `&&` is important, especially when working with **conditions** and **bitwise logic** in Java.

---

## ✅ Difference Between `&` and `&&` in Java

| Operator | Name                  | Type          | Evaluates Both Operands? | Use Case                       |
|----------|-----------------------|---------------|---------------------------|--------------------------------|
| `&&`     | Logical AND (short-circuit) | Boolean logic | ❌ No (if first is false)      | Conditions (if, while, etc.)   |
| `&`      | Bitwise AND / Logical AND | Bitwise & Boolean | ✅ Yes, always               | Bitwise ops or force both to eval |

---

### 🔹 1. **`&&` — Logical AND (Short-Circuit)**

- Works **only with boolean** values.
- **Stops evaluation** if the first condition is false.
- Improves performance and **avoids exceptions** (like `NullPointerException`).

#### 🧠 Example:
```java
String name = null;

if (name != null && name.length() > 3) {
    System.out.println("Valid name");
}
// ✅ Safe — second part won't run if name is null
```

---

### 🔹 2. **`&` — Bitwise AND or Full Logical AND**

- Works with:
    - **Booleans** → behaves like `&&` but **evaluates both sides always**
    - **Integers** → performs **bitwise AND**

#### 🧠 Boolean Example:
```java
String name = null;

if (name != null & name.length() > 3) {
    System.out.println("Oops?");
}
// ❌ Throws NullPointerException — both conditions evaluated
```

#### 🧠 Bitwise Example:
```java
int a = 5;     // 0101
int b = 3;     // 0011
int c = a & b; // 0001 = 1
```

---

### ✅ When to Use Which?

| Use `&&` when...                    | Use `&` when...                               |
|------------------------------------|-----------------------------------------------|
| You want **short-circuit behavior** | You’re doing **bitwise operations**           |
| You want to avoid **unnecessary checks** | You **must** evaluate both conditions        |

---

## 28. What is the purpose of the `instanceof` keyword?

The `instanceof` keyword in Java is super handy when you're dealing with **inheritance, interfaces, or polymorphism**.

---

## ✅ Purpose of the `instanceof` Keyword

The `instanceof` keyword is used to **check whether an object is an instance of a specific class or implements an interface**.

---

### 🧠 Syntax:
```java
object instanceof ClassName
```

- Returns `true` if `object` is an **instance of** `ClassName` or its subclass.
- Returns `false` if not.

---

## 🔍 Example:
```java
class Animal {}
class Dog extends Animal {}

public class Test {
    public static void main(String[] args) {
        Animal a = new Dog();

        System.out.println(a instanceof Animal); // true
        System.out.println(a instanceof Dog);    // true
        System.out.println(a instanceof Object); // true
        System.out.println(a instanceof String); // ❌ Compile-time error
    }
}
```

---

### ✅ When to Use `instanceof`?

- Before downcasting an object to **avoid `ClassCastException`**
- To implement **custom type-based logic**
- Useful in **polymorphic behavior** or generic methods

---

### 🔁 Example with Downcasting:
```java
if (a instanceof Dog) {
    Dog d = (Dog) a; // ✅ Safe cast
    d.bark();
}
```

---

### ⚠️ Things to Remember:
- It returns **`false`** if the object is `null`.
- Can only be used with **objects**, not primitives.
- It’s evaluated at **runtime**.

---

## 29. What is null in Java? Can you call a method on a null object?

Let's dive into the concept of `null` in Java — it's simple but **critical** for writing safe and bug-free code.

---

## ✅ What is `null` in Java?

- `null` is a **special literal** in Java that represents the **absence of a value** or **non-existence** of an object.
- It means the **reference variable is not pointing to any object** in memory.

---

### 🧠 Example:
```java
String name = null;  // name doesn't refer to any String object
```

---

## ❌ Can You Call a Method on a Null Object?

**No**, you **cannot** call a method on a `null` reference — doing so will throw a:

### 🚨 `NullPointerException`

---

### 🔍 Example:
```java
String str = null;
System.out.println(str.length());  // ❌ Throws NullPointerException
```

---

## ✅ How to Avoid `NullPointerException`

1. **Check for null before calling methods**
   ```java
   if (str != null) {
       System.out.println(str.length());
   }
   ```

2. **Use `Optional` (Java 8+)** for safer handling of nulls

3. **Initialize your variables** properly before use

---

## 🔁 Bonus Tip: `null instanceof Class`

```java
String str = null;
System.out.println(str instanceof String);  // Output: false
```

Even though `str` is declared as `String`, `instanceof` returns `false` because it's `null`.

---

## 30. How does Java handle memory for variables?

Understanding how **Java handles memory for variables** is key to writing efficient and bug-free code.

Java uses a **memory model** divided into **Stack** and **Heap**, along with **Method Area** and **Garbage Collection** for managing memory.

---

## 🧠 Java Memory Management Overview

### 📦 1. **Stack Memory**
- Stores:
    - **Method calls**
    - **Local variables**
    - **References to objects**
- Each thread has its own stack.
- Memory is **automatically managed** (LIFO: last in, first out).

### ✅ Example:
```java
int x = 10;       // `x` is stored in the stack
String name = "Aditya"; // reference to string object is on the stack
```

---

### 🧠 2. **Heap Memory**
- Stores:
    - **Objects** and **their instance variables**
- Shared among all threads.
- Managed by the **Garbage Collector (GC)**.

### ✅ Example:
```java
Person p = new Person(); // `p` is on stack, actual object is on heap
```

---

## 🔁 Variable Categories and Memory:

| Variable Type      | Stored In       | Lives Until                          |
|--------------------|------------------|--------------------------------------|
| **Local variable** | Stack            | End of method                        |
| **Instance variable** | Heap         | As long as the object exists         |
| **Static variable** | Method Area     | Until class is unloaded              |

---

## 🧹 Garbage Collection

- Java **automatically deallocates** heap memory for objects no longer in use.
- Objects with **no references** are marked for garbage collection.

---

### 🔍 Simple Example:
```java
public class Test {
    int id = 101;              // stored on heap (instance variable)
    
    public static void main(String[] args) {
        int a = 5;              // stack
        Test t = new Test();    // `t` on stack, object on heap
    }
}
```

---

### 📌 Quick Summary:

| Memory Type | Stores                     | Managed By           |
|-------------|----------------------------|-----------------------|
| Stack       | Local vars, method calls   | JVM automatically     |
| Heap        | Objects, instance vars     | Garbage Collector     |
| Method Area | Class-level (static) data  | JVM                   |

---

Let me know if you'd like a diagram or visual breakdown of this, or want to see how memory behaves in multithreaded programs!

---

### 🔹 31–45: **Control Statements & Loops**

## 31. What is the difference between `break` and `continue`?

The `break` and `continue` are **control flow statements** in Java used inside loops (and `switch`), but they serve very **different purposes**.

---

## ✅ Difference Between `break` and `continue`

| Keyword    | Purpose                               | Effect on Loop                          |
| ---------- | ------------------------------------- | --------------------------------------- |
| `break`    | **Exits** the loop or switch entirely | Stops the loop execution immediately    |
| `continue` | **Skips** the current iteration       | Proceeds to the **next** loop iteration |

---

### 🔍 `break` Example:

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        break;
    }
    System.out.println(i);
}
```

🧾 **Output:**

```
1
2
```

✅ The loop stops when `i == 3`.

---

### 🔍 `continue` Example:

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        continue;
    }
    System.out.println(i);
}
```

🧾 **Output:**

```
1
2
4
5
```

✅ When `i == 3`, the print is skipped, but the loop continues.

---

### ✅ Summary:

| Use `break` when...                 | Use `continue` when...                         |
| ----------------------------------- | ---------------------------------------------- |
| You want to **exit** the loop early | You want to **skip an iteration** but continue |
| Common in **searching** or `switch` | Common in **filtering** within loops           |

---

## 32. What are enhanced for-loops in Java?

The **enhanced for-loop** (also known as the **"for-each" loop**) in Java is a **simplified loop** used to iterate over arrays and collections without using an index or iterator explicitly.

---

## ✅ What Is an Enhanced For-Loop?

It is a **clean and readable way** to loop through elements of:

* Arrays
* Collections (like `List`, `Set`, etc.)

---

### 🔍 Syntax:

```java
for (type variable : collection/array) {
    // use variable
}
```

---

### 🧠 Example with Array:

```java
int[] numbers = {1, 2, 3, 4, 5};

for (int num : numbers) {
    System.out.println(num);
}
```

---

### 🧠 Example with List:

```java
List<String> names = Arrays.asList("Aditya", "Ravi", "Neha");

for (String name : names) {
    System.out.println(name);
}
```

---

## ✅ Benefits of Enhanced For-Loop:

| Feature                       | Benefit          |
| ----------------------------- | ---------------- |
| No index management           | Less error-prone |
| More readable                 | Cleaner syntax   |
| Works on arrays & collections | Versatile        |

---

## ⚠️ Limitations:

* You **cannot modify** the collection during iteration (like removing elements).
* No access to **index** (use regular `for` loop if index is needed).
* Not suitable if you need to **iterate in reverse**.

---

### 🔁 Regular `for` vs Enhanced `for`:

```java
// Regular for
for (int i = 0; i < numbers.length; i++) {
    System.out.println(numbers[i]);
}

// Enhanced for
for (int num : numbers) {
    System.out.println(num);
}
```

---

## 33. How does a switch-case statement work in Java?

The `switch-case` statement in Java is a control structure that lets you **execute different blocks of code based on the value of a variable** — it's often used as a cleaner alternative to multiple `if-else-if` statements.

---

## ✅ How `switch-case` Works in Java:

* Evaluates a **single expression**.
* Matches the result to a **case label**.
* Executes the **matching case block**.
* `break` is used to **exit the switch**.
* `default` runs when **no cases match**.

---

### 🔍 Syntax:

```java
switch (expression) {
    case value1:
        // code block
        break;
    case value2:
        // code block
        break;
    default:
        // default code block
}
```

---

### 🧠 Example:

```java
int day = 3;

switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday");
        break;
    default:
        System.out.println("Invalid day");
}
```

🧾 **Output:**

```
Wednesday
```

---

## ✅ Key Points:

| Feature               | Description                                                |
| --------------------- | ---------------------------------------------------------- |
| Supports data types   | `int`, `char`, `byte`, `short`, `enum`, `String`           |
| `break` is important  | Prevents **fall-through** to the next case                 |
| `default` is optional | Runs if no other case matches                              |
| Java 14+              | Introduced **switch expressions** with arrow (`->`) syntax |

---

### 🔁 Java 14+ Enhanced Syntax (Preview Feature):

```java
String dayType = switch (day) {
    case 1, 7 -> "Weekend";
    case 2, 3, 4, 5, 6 -> "Weekday";
    default -> "Unknown";
};
```

---

## 34. Can you use strings in switch-case statements?

**You can use `String` values in `switch-case` statements** starting from **Java 7** and onwards!

---

## ✅ Using Strings in `switch-case`

* Java allows `String` expressions in `switch` to improve **readability** and **maintainability**, especially for command-based or menu-driven programs.

---

### 🔍 Example:

```java
String role = "admin";

switch (role) {
    case "admin":
        System.out.println("Access granted: Admin panel");
        break;
    case "user":
        System.out.println("Access granted: User dashboard");
        break;
    case "guest":
        System.out.println("Access granted: Guest view");
        break;
    default:
        System.out.println("Invalid role");
}
```

🧾 **Output:**

```
Access granted: Admin panel
```

---

## ✅ Key Points:

| Feature              | Detail                                             |
| -------------------- | -------------------------------------------------- |
| Allowed since        | Java 7                                             |
| Case-sensitive       | Yes (`"Admin"` ≠ `"admin"`)                        |
| Internally converted | Java uses `.equals()` and `.hashCode()` internally |
| Best for             | Menu systems, command inputs, user roles, etc.     |

---

### ⚠️ Be careful:

* **Avoid `null`** values in `switch` expressions — if the string is `null`, it will throw a **`NullPointerException`**.

```java
String status = null;
switch (status) {     // ❌ Throws NullPointerException
    case "open": ...
}
```

➡️ Always check for `null` before using a string in a `switch`.

---

## 35. What is a labeled break or continue?

**Labeled `break` and `continue`** in Java are advanced control flow features used when working with **nested loops**. They give you **more control** over which loop to exit or continue.

---

## ✅ What Is a Label?

A **label** is an identifier placed before a loop. You can use it with `break` or `continue` to jump out of or skip a specific loop — **not just the innermost one**.

---

### 🔹 Syntax for Label:

```java
labelName:
for (...) {
    // code
}
```

---

## 🔸 Labeled `break`

It **exits the labeled loop entirely**, even if it’s nested.

### 🔍 Example:

```java
outer:
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 3; j++) {
        if (j == 2) {
            break outer;  // exits the outer loop
        }
        System.out.println("i=" + i + ", j=" + j);
    }
}
```

🧾 **Output:**

```
i=1, j=1
```

---

## 🔸 Labeled `continue`

It **skips to the next iteration** of the **labeled loop**, not just the inner one.

### 🔍 Example:

```java
outer:
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 3; j++) {
        if (j == 2) {
            continue outer;  // jumps to next iteration of outer loop
        }
        System.out.println("i=" + i + ", j=" + j);
    }
}
```

🧾 **Output:**

```
i=1, j=1
i=2, j=1
i=3, j=1
```

---

## ✅ When to Use Labeled `break`/`continue`?

| Use Case                             | Keyword           |
| ------------------------------------ | ----------------- |
| Exit a nested loop early             | `break label;`    |
| Skip to next iteration of outer loop | `continue label;` |

---

### ⚠️ Best Practice:

* Use labels **sparingly** — overusing them can make code hard to read.
* Prefer **refactoring** large loops into methods if logic is complex.

---

## 36. What is the difference between while and do-while?

The `while` and `do-while` loops in Java are both **entry-controlled** and **exit-controlled** loops, but they have a key difference in **when the condition is evaluated**.

---

## ✅ Key Difference

| Feature           | `while` Loop                  | `do-while` Loop                           |
| ----------------- | ----------------------------- | ----------------------------------------- |
| Condition check   | **Before** loop body executes | **After** loop body executes              |
| Minimum execution | May execute **zero** times    | Executes **at least once**, even if false |
| Syntax            | `while(condition)`            | `do { ... } while(condition);`            |

---

## 🔍 Syntax & Example

### ✅ `while` Loop:

```java
int i = 5;
while (i < 5) {
    System.out.println("While loop");
    i++;
}
```

🧾 **Output:** *Nothing prints* — because the condition is false before the loop starts.

---

### ✅ `do-while` Loop:

```java
int i = 5;
do {
    System.out.println("Do-while loop");
    i++;
} while (i < 5);
```

🧾 **Output:**

```
Do-while loop
```

Even though `i < 5` is false, the body runs **once**.

---

## 🧠 Use Case Summary

| Use when...                                      | Loop Type  |
| ------------------------------------------------ | ---------- |
| You want to loop **only if** a condition is true | `while`    |
| You want the loop to run **at least once**       | `do-while` |

---

## 37. How do you handle infinite loops in Java?

An **infinite loop** in Java is a loop that **never terminates** unless you explicitly break out of it. It can be **intentional** (e.g., for a server that waits for requests) or **accidental** (causing bugs or freezing programs).

---

## ✅ How to Write an Infinite Loop

### 🔁 Using `while`:

```java
while (true) {
    // loop forever
}
```

### 🔁 Using `for`:

```java
for (;;) {
    // also loops forever
}
```

---

## 🛑 How to Handle Infinite Loops

### 1. **Use a `break` statement** to exit when needed:

```java
while (true) {
    if (someCondition) {
        break; // exit the loop
    }
    // other logic
}
```

### 2. **Use flags (boolean variables):**

```java
boolean running = true;
while (running) {
    // logic
    if (shouldStop) {
        running = false;
    }
}
```

### 3. **Limit the number of iterations (in case of bugs):**

Use counters or time-based checks for safety:

```java
int count = 0;
while (true) {
    if (++count > 1000) break;
    // logic
}
```

---

## ⚠️ When Infinite Loops Are Useful

| Use Case                         | Why?                                 |
| -------------------------------- | ------------------------------------ |
| Servers or daemons               | Need to keep running continuously    |
| Event listeners or polling loops | Constantly waiting for new input     |
| Games or UI threads              | Maintain a consistent refresh/update |

---

## 🧯 Tips to Avoid Problems

* Always include a **termination condition** or `break`.
* Avoid logic that never updates the loop condition.
* Use **debugging tools** or **log statements** to monitor loops.
* Use **thread sleep** if looping continuously to avoid CPU overload:

```java
Thread.sleep(1000);  // 1-second pause
```

---

## 38. What are nested loops? How does it affect performance?

Let's break it down clearly.

---

## ✅ What Are Nested Loops?

A **nested loop** is a loop **inside another loop**. The **inner loop** runs **completely** for **each iteration** of the **outer loop**.

---

### 🔍 Example:

```java
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 2; j++) {
        System.out.println("i = " + i + ", j = " + j);
    }
}
```

🧾 **Output:**

```
i = 1, j = 1
i = 1, j = 2
i = 2, j = 1
i = 2, j = 2
i = 3, j = 1
i = 3, j = 2
```

➡️ The inner loop runs **2 times** for each outer loop iteration → total: `3 x 2 = 6` iterations.

---

## ⚠️ How Does It Affect Performance?

### ⏱ Time Complexity:

* The total number of iterations = `outer × inner`
* Example:

  ```java
  for (int i = 0; i < n; i++) {
      for (int j = 0; j < n; j++) {
          // O(n^2) work
      }
  }
  ```

    * This is **O(n²)** time — grows rapidly with input size.

---

### 🧠 Performance Impact:

| Factor                | Impact                                    |
| --------------------- | ----------------------------------------- |
| Increases CPU usage   | Especially with large datasets            |
| Slows execution       | Especially in **quadratic or cubic** time |
| More memory use       | If you're storing results in nested loops |
| Nested deeper = worse | O(n³), O(n⁴), etc. are very slow          |

---

### ✅ When to Use:

* When you’re working with **grids**, **matrices**, **combinations**, or **nested data**.
* Should be **optimized** or **refactored** for large inputs.

---

### 🔧 Tips to Improve Performance:

* **Break early** if a condition is met.
* Use **flags** or **return** to exit multiple levels.
* Consider **flattening logic** or using **algorithms with better time complexity**.

---

## 39. How does Java evaluate expressions in if-else conditions?

In Java, **expressions in `if-else` conditions** are evaluated based on their **boolean result** — meaning the condition must resolve to either `true` or `false`.

---

## ✅ Basic Evaluation Flow:

```java
if (condition) {
    // Executes if condition is true
} else {
    // Executes if condition is false
}
```

* Java first **evaluates the condition** inside the `if`.
* If the result is `true`, the `if` block runs.
* Otherwise, it skips to the `else` block (if present).

---

## 🔍 Example:

```java
int x = 10;

if (x > 5) {
    System.out.println("x is greater than 5");
} else {
    System.out.println("x is not greater than 5");
}
```

🧾 **Output:**

```
x is greater than 5
```

---

## 🔢 Expression Evaluation Order

Java uses **operator precedence and associativity** to evaluate expressions:

```java
int a = 5, b = 10, c = 15;

if (a < b && b < c) {
    System.out.println("Chained condition is true");
}
```

* `a < b` → `true`
* `b < c` → `true`
* `true && true` → `true` → condition passes

---

## 🔁 Short-Circuit Behavior

Java uses **short-circuit evaluation** for `&&` and `||`:

### 🔹 `&&` (AND):

* If **first condition is false**, second is **not evaluated**.

```java
if (false && someMethod()) { } // someMethod() is not called
```

### 🔹 `||` (OR):

* If **first condition is true**, second is **not evaluated**.

---

## 🧯 Invalid Conditions:

You **cannot** use non-boolean expressions directly in `if` conditions:

❌ This is illegal in Java:

```java
int a = 10;
if (a) {  // Compile-time error: incompatible types
    ...
}
```

✔️ Must be a **boolean** expression:

```java
if (a != 0) {
    ...
}
```

---

## 40. Can we replace if-else ladder with switch-case?

Yes, **you can sometimes replace an `if-else` ladder with a `switch-case`**, but **only under specific conditions**.

---

## ✅ When You **Can** Use `switch` Instead of `if-else`:

You can use `switch-case` if you're comparing a **single variable** against **multiple constant values** of these types:

* `int`, `byte`, `short`, `char`
* `enum`
* `String` (since Java 7)
* `Integer`, `Character`, etc. (autoboxed)
* **Pattern matching** (Java 17+ preview features)

---

### 🔍 Example: Replacing `if-else` with `switch`

#### `if-else` version:

```java
int day = 2;
if (day == 1)
    System.out.println("Monday");
else if (day == 2)
    System.out.println("Tuesday");
else
    System.out.println("Other day");
```

#### ✅ `switch` version:

```java
switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    default:
        System.out.println("Other day");
}
```

---

## ❌ When You **Cannot** Use `switch`:

You **cannot** use `switch` if:

* You're comparing **ranges** (`if (score > 90)`)
* You need **complex boolean logic** (`if (x > 10 && y < 5)`)
* You're comparing **multiple variables**
* The condition isn't a compile-time constant

---

### 🔍 Example That Needs `if-else`:

```java
int score = 85;
if (score >= 90) {
    System.out.println("Grade A");
} else if (score >= 80) {
    System.out.println("Grade B");
}
```

➡️ **This cannot be done using `switch`** unless you rewrite logic (e.g., mapping score ranges).

---

## ✅ Summary:

| Use Case                     | Use `if-else` | Use `switch-case` |
| ---------------------------- | ------------- | ----------------- |
| Range checks (`x > 5`)       | ✅             | ❌                 |
| Comparing multiple variables | ✅             | ❌                 |
| Exact value match (1, 2, 3)  | ✅             | ✅                 |
| String or enum matching      | ✅             | ✅ (Java 7+)       |

---

## 41. What are guard clauses?

A **guard clause** is a **programming technique** where you handle edge cases or conditions **early** in a function or method, allowing the main logic to be **more readable** and reducing nesting.

Instead of writing multiple `if` conditions or an `if-else` ladder, a guard clause checks for an early exit condition, which allows the function to **return early** if something is wrong (like invalid input or edge cases). This helps in avoiding deep nested structures.

---

## ✅ How Guard Clauses Work:

### **The basic idea**:

* **Check for a condition early** (e.g., invalid input).
* If the condition is true, **exit early** (typically with `return` or `throw`).
* If the condition is false, the method continues with the **normal flow**.

---

## 🔍 Example of Guard Clauses:

### Without Guard Clauses (Nested `if` statements):

```java
public void processOrder(Order order) {
    if (order != null) {
        if (order.isValid()) {
            if (order.hasItems()) {
                // Proceed with processing the order
                System.out.println("Order processed");
            } else {
                System.out.println("Order has no items");
            }
        } else {
            System.out.println("Order is invalid");
        }
    } else {
        System.out.println("Order is null");
    }
}
```

### With Guard Clauses (Early Return):

```java
public void processOrder(Order order) {
    if (order == null) {
        System.out.println("Order is null");
        return; // Guard clause for null check
    }
    if (!order.isValid()) {
        System.out.println("Order is invalid");
        return; // Guard clause for invalid order
    }
    if (!order.hasItems()) {
        System.out.println("Order has no items");
        return; // Guard clause for no items
    }
    
    // Proceed with processing the order
    System.out.println("Order processed");
}
```

---

### **Advantages of Guard Clauses**:

* **Improved readability**: Logic is flat, and there’s less indentation.
* **Faster exits**: Conditions are handled early, allowing you to return or throw exceptions quickly.
* **Reduced complexity**: Fewer nested `if-else` statements, making code easier to follow.

---

## 🧠 When to Use Guard Clauses:

* **Input validation**: Checking if the parameters are valid early on in a method.
* **Edge cases**: Handling special conditions like null, empty collections, etc.
* **Preconditions**: Ensuring prerequisites are met before proceeding with the main logic.

---

### ✅ Example of Guard Clause in a Method:

```java
public boolean isEligibleForDiscount(Customer customer) {
    if (customer == null || !customer.hasValidMembership()) {
        return false; // Guard clause: customer is not eligible
    }
    if (customer.getAge() < 18) {
        return false; // Guard clause: not eligible due to age
    }
    // All conditions are met, eligible for discount
    return true;
}
```

---

### ⚠️ Avoid Overusing Guard Clauses:

While guard clauses are useful, **don't overuse them** in complex logic, as they can lead to code being fragmented or scattered. Stick to using them when it helps **simplify flow**.

---

## 42. What is fall-through in switch-case?

**Fall-through** in a `switch-case` refers to the behavior where, after a case is matched and executed, the control **falls through** to the next case unless a `break` statement is used to exit the `switch` block.

This is the default behavior of `switch-case` statements in Java, where **if you don't include a `break` after a case, the execution will continue into the next case**, even if that case does not match the value.

---

## ✅ Fall-through Example:

### Without `break` (Fall-through occurs):

```java
int day = 3;

switch (day) {
    case 1:
        System.out.println("Monday");
        // no break here
    case 2:
        System.out.println("Tuesday");
        // no break here
    case 3:
        System.out.println("Wednesday");
        // no break here
    case 4:
        System.out.println("Thursday");
        break;
    default:
        System.out.println("Invalid day");
}
```

🧾 **Output:**

```
Wednesday
Thursday
```

### Explanation:

* `day == 3`, so it matches **case 3**.
* However, **there’s no `break`** in case 3, so it continues (falls through) into **case 4**.
* The execution stops at **case 4**, because there’s a `break` statement.

---

## ✅ Fall-through with `break` (Prevent Fall-through):

To **prevent fall-through**, add a `break` statement at the end of each case.

### Corrected Example with `break`:

```java
int day = 3;

switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday");
        break;
    case 4:
        System.out.println("Thursday");
        break;
    default:
        System.out.println("Invalid day");
}
```

🧾 **Output:**

```
Wednesday
```

### Explanation:

* **No fall-through** happens, and only the matched case (3) executes.
* Execution exits the `switch` statement after the `break` in **case 3**.

---

## ⚠️ When Is Fall-through Useful?

**Fall-through** can be useful when you want **multiple cases to execute the same code** without repeating it.

### Example of Fall-through for Common Logic:

```java
int day = 3;

switch (day) {
    case 1:
    case 2:
    case 3:
        System.out.println("Weekday");
        break;
    case 4:
    case 5:
        System.out.println("Weekend");
        break;
    default:
        System.out.println("Invalid day");
}
```

🧾 **Output:**

```
Weekday
```

### Explanation:

* **Cases 1, 2, and 3** will all print "Weekday" because there's no `break` between them, so the control "falls through."
* **Case 4 and 5** print "Weekend."

---

## ✅ How to Avoid Unintended Fall-through:

* Always ensure a `break` is added if you don’t intend for fall-through.
* You can also use a `return` statement or `throw` an exception to exit early from the `switch` block if necessary.

---

## 43. How do loops affect memory and performance in Java?

Loops in Java can have significant impacts on both **memory usage** and **performance**, depending on how they are structured and the size of the data being processed. Let’s dive into the details.

---

## 🧠 **How Loops Affect Memory**:

1. **Memory Usage Depends on Data**:

* **Primitive types** (e.g., `int`, `char`, `boolean`) in loops generally have **low memory overhead**.
* **Object references** (e.g., arrays, objects) in loops may **increase memory usage** because each object or reference requires additional space in the heap memory.

2. **Memory Leaks**:

* In **infinite loops** or **loops creating new objects**, memory consumption can increase if objects are not properly released (i.e., not garbage collected).
* If you're adding elements to a **collection** or **list** inside a loop, **unbounded growth** of the collection can occur, leading to high memory usage.

Example (Potential Memory Issue):

   ```java
   List<Integer> list = new ArrayList<>();
   while (true) {
       list.add(new Integer(1));  // Potential memory leak if the loop is infinite
   }
   ```

3. **Stack Memory in Recursive Loops**:

* Recursive functions can **consume stack memory** for each function call. If recursion depth is large (like in some algorithms), it could lead to a **stack overflow**.

---

## ⏱ **How Loops Affect Performance**:

1. **Time Complexity**:

* The performance impact of loops is closely tied to the **time complexity** of the algorithm.
* For example:

    * A **simple loop** that runs `n` times has **O(n)** complexity.
    * Nested loops (e.g., two loops inside one) can have a higher complexity, like **O(n²)** or **O(n³)**, which can drastically reduce performance for large input sizes.

Example (O(n²) Complexity):

   ```java
   for (int i = 0; i < n; i++) {
       for (int j = 0; j < n; j++) {
           // Do something
       }
   }
   ```

* For large `n`, this leads to **n \* n = n² iterations**, which can become slow.

2. **CPU Usage**:

* Each loop iteration consumes CPU cycles, and the more iterations there are, the more **CPU time** is consumed.
* **Nested loops** or **loops with heavy logic** inside them can cause significant CPU usage, leading to performance degradation, especially in multi-threaded environments.

3. **Memory Access Patterns**:

* **Cache locality**: If loops access memory in a predictable, sequential order (e.g., accessing array elements one by one), they are more likely to benefit from **cache locality**, which can improve performance.
* **Random access patterns** (e.g., accessing array elements randomly) can reduce performance due to increased **cache misses**.

Example (Optimal Cache Access):

   ```java
   int[] array = new int[1000000];
   for (int i = 0; i < array.length; i++) {
       array[i] = i;
   }
   ```

This access pattern is **cache-friendly** because memory is accessed in a sequential manner.

4. **Loop Unrolling**:

* Loop unrolling is a **compiler optimization** where the loop is "expanded" to decrease the number of iterations and increase performance. This is usually done at the compiler level but can be manually implemented in some cases.

Example (Loop Unrolling):

   ```java
   for (int i = 0; i < n; i++) {
       // Do something
   }
   ```

Can be unrolled to:

   ```java
   for (int i = 0; i < n; i += 4) {
       // Do something
       // Do something
       // Do something
       // Do something
   }
   ```

---

## 📉 **Optimizing Loops for Memory and Performance**:

1. **Avoiding Unnecessary Object Creation**:

* Avoid creating new objects in every iteration of the loop unless absolutely necessary. This can reduce memory overhead and improve performance by not continuously allocating new memory.

2. **Minimize Nested Loops**:

* If possible, avoid **nested loops**. Look for opportunities to flatten loops or use more efficient algorithms (e.g., sorting algorithms, search algorithms).

3. **Using Efficient Data Structures**:

* Choose **appropriate data structures** to store and access elements. For example, use **HashMaps** for faster lookups instead of iterating through lists.

4. **Loop Fusion**:

* Combine multiple loops that traverse the same data into one. This reduces the number of iterations and improves cache locality.

Example:

   ```java
   for (int i = 0; i < n; i++) {
       array1[i] = i;
       array2[i] = i * 2;
   }
   ```

Instead of two loops, you can **merge** them into one to reduce iteration time.

5. **Use Parallelism**:

* For **large datasets**, consider using **parallel streams** (Java 8+) or **multithreading** to split work across multiple CPU cores.
* For example, using `parallelStream()` in Java:

  ```java
  Arrays.stream(array).parallel().forEach(x -> process(x));
  ```

---

## 🧠 **Summary**:

| Factor              | Impact on Memory                                               | Impact on Performance                                                   |
| ------------------- | -------------------------------------------------------------- | ----------------------------------------------------------------------- |
| **Loop Size**       | Larger loops consume more memory                               | More iterations lead to higher CPU usage and slower performance         |
| **Nested Loops**    | More nested loops increase memory usage                        | Higher time complexity (O(n²), O(n³)) affects performance significantly |
| **Object Creation** | Creating new objects in every iteration increases memory usage | Increases memory allocation and reduces performance                     |
| **Data Access**     | Sequential memory access is more memory-efficient              | Sequential access improves CPU cache usage and performance              |
| **Recursion**       | Consumes stack memory for each call                            | Deep recursion can cause stack overflow and slower performance          |

---

## 44. What is the difference between forEach() and for loop?

The `forEach()` method and the traditional `for` loop are both used to iterate over collections or arrays in Java, but they have some key differences in terms of syntax, flexibility, and use cases. Let’s break down the main differences.

---

## ✅ **1. Syntax and Usage**:

### **`forEach()`**:

* `forEach()` is a method defined in **`Iterable`** and **`Stream`** interfaces (Java 8 and above).
* It is often used with **lambda expressions** or **method references** to process elements in a collection or stream.

#### Example (using `forEach()` with lambda):

```java
List<String> names = List.of("Alice", "Bob", "Charlie");

names.forEach(name -> System.out.println(name));
```

#### Example (using `forEach()` with method reference):

```java
names.forEach(System.out::println);
```

---

### **Traditional `for` Loop**:

* The `for` loop is more **general-purpose** and can iterate over any collection or array.
* It gives you **more control** over the iteration process, such as accessing the index or breaking the loop early.

#### Example (using `for` loop):

```java
for (int i = 0; i < names.size(); i++) {
    System.out.println(names.get(i));
}
```

---

## ✅ **2. Flexibility**:

### **`forEach()`**:

* **Less flexible** compared to a `for` loop.
* **No control over the index**: You cannot access the index of elements directly when using `forEach()`. You must rely on methods like `List.get(i)` for index-based access.
* **Can't break or continue**: You cannot use `break`, `continue`, or `return` inside a `forEach()` loop (unless using exceptions for early exit).

### **`for` Loop**:

* **Highly flexible** and gives you full control.
* You can access **element indices**, break, continue, and **exit the loop early** using `break` or `return`.

---

## ✅ **3. Performance**:

### **`forEach()`**:

* **Less performance-efficient** for some use cases because:

    * It uses **lambda expressions** or method references, which might introduce overhead compared to the direct index-based access of a traditional `for` loop.
    * It doesn't allow **parallelism** (though `Stream.forEach()` can be parallelized, that’s a different concept from `forEach()` in collections).

### **`for` Loop**:

* Generally **more performance-efficient** than `forEach()` because:

    * It has less overhead in terms of execution since it does not rely on lambda expressions.
    * Offers better performance for **primitive types** as there's no object overhead, unlike with streams.

---

## ✅ **4. Parallelism**:

### **`forEach()`** (Streams only):

* In streams, `forEach()` can be parallelized to take advantage of multi-core processors.

  Example with parallel streams:

  ```java
  List<String> names = List.of("Alice", "Bob", "Charlie");
  names.parallelStream().forEach(name -> System.out.println(name));
  ```

* **Parallelism** can improve performance in some cases when processing large data sets.

### **`for` Loop**:

* A regular `for` loop does not have **native parallelism** support.
* You would need to use external libraries like `ForkJoinPool` or create threads manually for parallel execution.

---

## ✅ **5. Readability**:

### **`forEach()`**:

* **More concise** and **functional** in style.
* It can improve readability when working with **streams** or collections because it uses lambda expressions and method references.
* Ideal when you need simple actions or transformations on elements.

### **`for` Loop**:

* **More verbose** but **clear** for beginners or situations where you need **index access**, more complex logic, or early exits.
* Offers **better readability** when your loop involves conditions such as `break`, `continue`, or nested loops.

---

## ✅ **6. Use Cases**:

### **`forEach()`**:

* Best suited for **simple operations** on elements of collections or streams (like printing or applying a transformation).
* Ideal when you don't need to manipulate the loop index or exit the loop early.

  Example:

  ```java
  List<String> names = List.of("Alice", "Bob", "Charlie");
  names.forEach(name -> System.out.println(name));
  ```

### **`for` Loop**:

* More flexible and better for **complex logic**.
* Use it when you need to **access indices**, **break the loop early**, or perform operations where functional programming style (like `forEach()`) isn't ideal.

  Example:

  ```java
  List<String> names = List.of("Alice", "Bob", "Charlie");
  for (int i = 0; i < names.size(); i++) {
      if (names.get(i).equals("Bob")) {
          System.out.println("Found Bob at index " + i);
          break;
      }
  }
  ```

---

## 🧠 **Summary Table**:

| Feature          | `forEach()`                           | `for` Loop                                  |
| ---------------- | ------------------------------------- | ------------------------------------------- |
| **Syntax**       | Lambda expressions, method references | Classic for loop with index                 |
| **Index Access** | No direct index access                | Full index access                           |
| **Control Flow** | No `break`/`continue`                 | `break`, `continue`, `return` allowed       |
| **Parallelism**  | Supported in Streams                  | Not supported                               |
| **Performance**  | Slight overhead with lambdas          | More efficient, especially with primitives  |
| **Readability**  | More concise, functional style        | More verbose, but clearer for complex logic |
| **Use Cases**    | Simple operations, functional style   | Complex logic, index manipulation           |

---

## 🔧 **When to Use**:

* **Use `forEach()`**: When you're working with collections or streams and performing simple operations like printing, modifying, or applying actions on each element.

* **Use `for` loop**: When you need more control over the iteration process, like accessing element indices, breaking or continuing the loop, or handling complex logic.

---

## 45. When should you avoid using recursion?

Recursion is a powerful programming technique, but there are situations where it might not be the best choice. Let's explore the scenarios where **you should avoid using recursion** in Java:

---

## 🚫 **1. When the Problem Can Be Solved Iteratively**:

* If a problem can be solved using a simple loop or iteration, recursion is generally **not needed**. Recursion introduces additional complexity and potential performance issues.

* **Reason**: Iterative solutions are usually **more efficient** in terms of **memory usage** and avoid the overhead of recursive function calls.

  **Example** (Summing numbers iteratively vs. recursively):

    * **Iterative Solution**:

      ```java
      int sum = 0;
      for (int i = 1; i <= 10; i++) {
          sum += i;
      }
      ```
    * **Recursive Solution**:

      ```java
      public int sum(int n) {
          if (n == 0) return 0;
          return n + sum(n - 1);
      }
      ```

  **When to avoid recursion**: When an iterative approach is simple and efficient.

---

## 🚫 **2. When There's a Risk of Stack Overflow**:

* **Recursion** involves function calls being pushed onto the **call stack**. If the recursion goes too deep, you may encounter a **stack overflow error** (e.g., for large input sizes or too many recursive calls).

* **Reason**: The call stack has a limited size, and deep recursion can quickly exhaust it, especially in languages like Java that don’t have **tail recursion optimization**.

  **Example** (Deep Recursion with large input):

  ```java
  public int factorial(int n) {
      if (n == 1) return 1;
      return n * factorial(n - 1);
  }
  ```

  If you call `factorial(10000)`, it could cause a stack overflow, especially if the **depth of recursion is large**.

  **When to avoid recursion**: When you are dealing with a problem that has a **large input size** or requires deep recursion. An **iterative approach** or using **dynamic programming** might be better suited.

---

## 🚫 **3. When Performance is Critical**:

* Recursion can introduce overhead in terms of both **time complexity** and **memory usage**, particularly when dealing with a large number of function calls.

* **Reason**: Each recursive call adds a new frame to the **call stack**, and the program has to perform additional operations (such as maintaining state) for each function call. This can be slower than an iterative solution.

  **Example**: Consider the naive recursive Fibonacci algorithm:

  ```java
  public int fibonacci(int n) {
      if (n <= 1) return n;
      return fibonacci(n - 1) + fibonacci(n - 2);
  }
  ```

  This implementation has exponential time complexity `O(2^n)` and recalculates the same values multiple times, making it very inefficient.

  **When to avoid recursion**: When **performance** is a top priority, and recursion leads to inefficient solutions (e.g., recalculating values or excessive function calls).

---

## 🚫 **4. When You Need Constant Memory Use**:

* Recursion generally uses more **memory** because each recursive call adds a new **stack frame** (the memory required for function calls). This can be a problem if the algorithm is expected to run with constant memory.

* **Reason**: Recursive calls increase memory usage due to the **call stack**. If your program needs to operate with **constant space**, recursion might not be ideal.

  **Example**:
  A recursive tree traversal might use a significant amount of memory if the tree depth is large.

  **When to avoid recursion**: When the program needs to minimize memory usage, or you're operating in an environment with limited stack space (e.g., embedded systems or real-time systems).

---

## 🚫 **5. When You Can Use Tail Recursion Optimization**:

* While Java does not support **tail recursion optimization** (unlike some other languages), some languages can optimize tail-recursive functions to use constant stack space. If you're in such a language, you may still avoid recursion if it’s not tail-recursive or if you’re facing limitations in Java.

* **Reason**: Even in languages that support tail recursion optimization, it's essential to ensure that recursion is implemented in a way that the compiler can optimize it.

  **When to avoid recursion**: When the language (like Java) does not support tail recursion optimization and you need to avoid consuming excessive stack space.

---

## 🚫 **6. When the Problem is Too Simple for Recursion**:

* Recursion is often used in more complex problems, but for problems that are simple or involve small amounts of data, using recursion can add unnecessary complexity.

* **Reason**: A simple **loop** or **conditional statements** may be more straightforward and less error-prone than recursion for trivial problems.

  **Example** (Iterating through small data):

  ```java
  List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);
  for (int i : list) {
      System.out.println(i);
  }
  ```

  **When to avoid recursion**: When the problem is trivial, and recursion would just add extra layers of complexity without any real benefit.

---

## ✅ **When Recursion is Ideal**:

* **Recursion** is a great choice for problems involving **divide and conquer** strategies, such as:

    * **Tree traversal** (pre-order, in-order, post-order)
    * **Graph traversal** (depth-first search, breadth-first search)
    * **Backtracking algorithms** (e.g., solving mazes, puzzles)
    * **Recursive mathematical problems** (e.g., calculating factorial, Fibonacci numbers)

---

## 📋 **Summary**:

| **When to Avoid Recursion**                      | **Why**                                                                                                        |
| ------------------------------------------------ | -------------------------------------------------------------------------------------------------------------- |
| **When the problem can be solved iteratively**   | Recursion introduces unnecessary complexity and performance overhead when an iterative solution is simpler.    |
| **When there's a risk of stack overflow**        | Deep recursion consumes stack space, and a stack overflow can occur if the recursion depth is too large.       |
| **When performance is critical**                 | Recursion introduces overhead, and iterative solutions might be more efficient in terms of time and space.     |
| **When you need constant memory use**            | Recursion uses memory for each function call, increasing the memory footprint.                                 |
| **When the problem is too simple for recursion** | Recursion might add unnecessary complexity for simple problems that can be solved using loops or conditionals. |

---

Would you like help with refactoring a recursive solution to an iterative one, or have any further questions on recursion in specific scenarios?

---

### 🔹 46–60: **Exception Handling**

## 46. What is the difference between checked and unchecked exceptions?

In Java, exceptions are classified into **checked exceptions** and **unchecked exceptions**. These two categories of exceptions differ in how they are handled by the Java compiler and the programmer. Let’s break down their differences:

---

## ✅ **1. Definition**:

### **Checked Exceptions**:

* **Checked exceptions** are exceptions that are **explicitly checked** by the Java compiler at **compile-time**. The compiler ensures that these exceptions are either **caught** or **declared** in the method signature.
* If a method might throw a checked exception, it must either **catch** the exception using a `try-catch` block or **declare** it using the `throws` keyword in the method signature.

  **Example**:

  ```java
  public void readFile(String fileName) throws IOException {
      // Code that might throw an IOException
      FileReader file = new FileReader(fileName);
  }
  ```

  In this example, `IOException` is a **checked exception**, and the method `readFile` must either catch it or declare it in the method signature.

---

### **Unchecked Exceptions**:

* **Unchecked exceptions** are exceptions that are **not checked** by the Java compiler at compile-time. These are **subclasses** of `RuntimeException` and do not need to be explicitly caught or declared in the method signature.
* The programmer has the option to handle these exceptions, but it’s **not mandatory**.

  **Example**:

  ```java
  public void divide(int a, int b) {
      int result = a / b; // ArithmeticException could be thrown here if b is 0
  }
  ```

  Here, `ArithmeticException` is an **unchecked exception** because it’s a subclass of `RuntimeException`. The method doesn’t need to declare or catch it, but it can if desired.

---

## ✅ **2. Inheritance**:

### **Checked Exceptions**:

* Checked exceptions are **direct subclasses of `Exception`** (excluding `RuntimeException` and its subclasses).

    * Example of checked exceptions: `IOException`, `SQLException`, `ClassNotFoundException`, etc.

### **Unchecked Exceptions**:

* Unchecked exceptions are **subclasses of `RuntimeException`**.

    * Example of unchecked exceptions: `NullPointerException`, `ArithmeticException`, `ArrayIndexOutOfBoundsException`, `ClassCastException`, etc.

---

## ✅ **3. Compilation Behavior**:

### **Checked Exceptions**:

* The compiler **forces** the programmer to handle checked exceptions either by:

    * Catching the exception in a `try-catch` block.
    * Declaring the exception with the `throws` keyword.

  If a checked exception is not properly handled or declared, the program will **not compile**.

  ```java
  public void readFile(String fileName) throws IOException {
      // Compiler checks this exception
      FileReader file = new FileReader(fileName);
  }
  ```

  If the `IOException` is not handled or declared in the method signature, the compiler will throw an error.

### **Unchecked Exceptions**:

* The compiler **does not check** for unchecked exceptions.
* **No need to catch** or **declare** unchecked exceptions in the method signature. The program can compile even if an unchecked exception is not handled.

  ```java
  public void divide(int a, int b) {
      int result = a / b; // Compiler does not require handling ArithmeticException
  }
  ```

  If `b` is 0, the `ArithmeticException` might be thrown at runtime, but it’s not required to be caught or declared.

---

## ✅ **4. Handling Strategy**:

### **Checked Exceptions**:

* Checked exceptions typically represent **recoverable conditions** where the program can handle the exception and continue execution.
* Examples of situations where checked exceptions are appropriate: working with files, networking, database operations, etc., where failure is expected but can be managed (like a missing file or a database connection error).

  **Example**:

  ```java
  try {
      readFile("data.txt");
  } catch (IOException e) {
      System.out.println("Error reading file: " + e.getMessage());
  }
  ```

### **Unchecked Exceptions**:

* Unchecked exceptions often represent **programming errors** or **unexpected conditions** that the program cannot reasonably recover from, such as division by zero, accessing a null reference, or array index out-of-bounds.
* Handling unchecked exceptions is usually optional, but it’s often good practice to fix the root cause of the issue rather than handling it in a `try-catch` block.

  **Example**:

  ```java
  try {
      divide(10, 0);
  } catch (ArithmeticException e) {
      System.out.println("Cannot divide by zero!");
  }
  ```

---

## ✅ **5. Example Classifications**:

| **Exception Type**       | **Examples**                                                                    | **When to Use**                                                                                                 |
| ------------------------ | ------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| **Checked Exceptions**   | `IOException`, `SQLException`, `ClassNotFoundException`                         | Use for situations where the problem can be **recovered** or **handled** (e.g., file handling, network issues). |
| **Unchecked Exceptions** | `NullPointerException`, `ArrayIndexOutOfBoundsException`, `ArithmeticException` | Use for **programming errors** or **unexpected conditions** (e.g., invalid array index, dividing by zero).      |

---

## ✅ **6. Pros and Cons**:

### **Checked Exceptions**:

* **Pros**:

    * Forces the programmer to handle or declare potential issues, leading to more robust code.
    * Helps ensure that error conditions are dealt with explicitly.
* **Cons**:

    * Can result in verbose code if many exceptions need to be handled or declared.
    * May cause excessive boilerplate code, making the program harder to maintain.

### **Unchecked Exceptions**:

* **Pros**:

    * More flexible and less boilerplate code.
    * Suitable for conditions that cannot be reasonably anticipated or recovered from.
* **Cons**:

    * Can lead to **runtime errors** if not carefully handled.
    * May allow programming errors to go unnoticed until execution, leading to potential issues in production.

---

## 🧠 **Summary**:

| **Aspect**         | **Checked Exceptions**                                       | **Unchecked Exceptions**                                                        |
| ------------------ | ------------------------------------------------------------ | ------------------------------------------------------------------------------- |
| **Inheritance**    | Subclass of `Exception` (excluding `RuntimeException`)       | Subclass of `RuntimeException`                                                  |
| **Compiler Check** | Must be handled or declared with `throws`                    | Not checked by the compiler                                                     |
| **Handling**       | Must be explicitly handled or declared                       | Optional to handle                                                              |
| **Examples**       | `IOException`, `SQLException`, `ClassNotFoundException`      | `NullPointerException`, `ArithmeticException`, `ArrayIndexOutOfBoundsException` |
| **When to Use**    | For recoverable errors, like file handling or network issues | For programming errors or unexpected conditions                                 |

---

## 47. What is the base class of all exceptions?

In Java, the **base class of all exceptions** is `Throwable`. It is the parent class for both **exceptions** and **errors**.

Here’s the class hierarchy:

```
Throwable
   ├── Error
   └── Exception
        ├── RuntimeException
        └── Other exceptions (e.g., IOException, SQLException)
```

---

### **Key Points:**

1. **`Throwable`**:

* The **root** class for all errors and exceptions in Java.
* It is **directly inherited** by two main subclasses: **`Error`** and **`Exception`**.

2. **`Error`**:

* Represents **serious issues** that are typically **not recoverable** (e.g., out of memory, JVM crashes).
* Common errors: `OutOfMemoryError`, `StackOverflowError`, etc.
* Errors are usually not handled by applications, as they indicate problems that are generally beyond the control of the application.

3. **`Exception`**:

* Represents **exceptional conditions** that a program can catch and handle.
* Subclasses of `Exception` include both **checked exceptions** (e.g., `IOException`, `SQLException`) and **unchecked exceptions** (e.g., `NullPointerException`, `ArithmeticException`).

---

### Example of the `Throwable` class hierarchy:

```java
try {
    // Code that may throw an exception
} catch (Exception e) {  // `Exception` is a subclass of `Throwable`
    // Handle the exception
} catch (Error e) {  // `Error` is also a subclass of `Throwable`
    // Handle errors (though usually we don't handle errors)
}
```

### **Summary**:

* `Throwable` is the superclass of all errors and exceptions in Java, and every exception or error must extend this class, either directly or indirectly.

---

## 48. How do try-catch-finally blocks work?

In Java, the **`try-catch-finally`** block is used to handle exceptions (runtime errors) gracefully without crashing the program. It allows the programmer to define blocks of code for **trying** an operation, **catching** any exceptions that occur during that operation, and **finally** performing actions (such as cleanup) regardless of whether an exception was thrown.

Let’s break down how each part works:

---

## 1. **`try` Block**:

* The `try` block is where you place the code that **may throw an exception**.
* If an exception occurs within the `try` block, the remaining code in that block is skipped, and the program moves to the appropriate `catch` block.

**Example**:

```java
try {
    int result = 10 / 0;  // This will throw ArithmeticException
}
```

---

## 2. **`catch` Block**:

* The `catch` block is used to **handle exceptions** that occur in the `try` block.
* When an exception occurs, the corresponding `catch` block is executed. The type of exception in the `catch` block determines which exception it will catch.
* Multiple `catch` blocks can be used to catch different types of exceptions.

**Example**:

```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Error: Division by zero!");
}
```

---

## 3. **`finally` Block**:

* The `finally` block is **optional** and is used to **ensure that certain code always runs** regardless of whether an exception was thrown or not.
* The `finally` block is **executed after the `try` and `catch` blocks**, even if an exception was thrown or caught, and it runs regardless of the outcome.
* It is typically used for **cleanup** activities, such as closing files, releasing resources, or closing database connections.

**Example**:

```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Error: Division by zero!");
} finally {
    System.out.println("This will always be printed.");
}
```

* In this case, even though an exception occurs and is caught, the `finally` block will still execute, printing `"This will always be printed."`.

---

### **Key Points**:

* **`try`**: The block where the exception might be thrown.
* **`catch`**: Catches the exception if it occurs and handles it.
* **`finally`**: This block is always executed after the `try` and `catch` blocks, even if no exception occurred or if an exception was caught.

---

## **Exception Flow**:

1. If **no exception occurs** in the `try` block:

* The code in the `catch` block is **skipped**.
* The `finally` block, if present, is executed.

2. If an exception **occurs** in the `try` block:

* The rest of the `try` block is skipped.
* If the exception type matches one of the `catch` blocks, the corresponding `catch` block is executed.
* After the `catch` block finishes, the `finally` block is executed.

3. **`finally` Block Execution**:

* The `finally` block is always executed, even if an exception is not thrown or caught, unless the program is terminated by a `System.exit()` call or a fatal error occurs.

---

### **Example with Multiple `catch` Blocks**:

```java
public class TryCatchExample {
    public static void main(String[] args) {
        try {
            // Trying to parse a string to integer
            String str = "abc";
            int num = Integer.parseInt(str);  // This will throw NumberFormatException
        } catch (NumberFormatException e) {
            System.out.println("Error: Invalid number format!");
        } catch (Exception e) {
            System.out.println("Generic error!");
        } finally {
            System.out.println("This will always execute.");
        }
    }
}
```

* In this example:

    * The `try` block throws a `NumberFormatException`, which is caught by the first `catch` block.
    * The `finally` block will always execute after the exception is caught.

---

### **Flow with Exception and `finally`**:

```java
public class TryCatchFinallyExample {
    public static void main(String[] args) {
        try {
            System.out.println("Trying to divide by zero...");
            int result = 10 / 0;  // This will throw ArithmeticException
        } catch (ArithmeticException e) {
            System.out.println("Error: Cannot divide by zero!");
        } finally {
            System.out.println("This will execute regardless of whether an exception occurs.");
        }
    }
}
```

**Output**:

```
Trying to divide by zero...
Error: Cannot divide by zero!
This will execute regardless of whether an exception occurs.
```

---

### **Summary**:

| **Block**     | **Purpose**                                                                          | **Execution**                                                                |
| ------------- | ------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------- |
| **`try`**     | Code that might throw an exception.                                                  | Executed first. If no exception occurs, `catch` and `finally` are skipped.   |
| **`catch`**   | Catches and handles the exception thrown in the `try` block.                         | Executed if the exception type matches the `catch` block.                    |
| **`finally`** | Code that will always execute, regardless of whether an exception was thrown or not. | Always executed after `try` and `catch`, even if an exception occurs or not. |

---

## 49. What happens if an exception is thrown in finally block?

If an exception is thrown in the **`finally`** block, it can complicate things, because the **`finally`** block is designed to run regardless of whether an exception occurs in the `try` block or whether a `catch` block handles an exception. However, if an exception is thrown in the `finally` block, it can **override** any exception that was thrown in the `try` or `catch` block, potentially causing the original exception to be lost.

Here’s what happens in different scenarios:

---

### **Scenario 1: Exception in `finally` Block and No Exception in `try` Block**

If there is **no exception** in the `try` block but an exception occurs in the `finally` block, the exception in the `finally` block will be propagated, and it will **replace any other exception** that might have occurred earlier.

**Example**:

```java
public class FinallyExceptionExample {
    public static void main(String[] args) {
        try {
            System.out.println("Inside try block");
        } finally {
            System.out.println("Inside finally block");
            // Exception thrown in the finally block
            throw new RuntimeException("Exception from finally block");
        }
    }
}
```

**Output**:

```
Inside try block
Inside finally block
Exception in thread "main" java.lang.RuntimeException: Exception from finally block
```

Here, the exception in the `finally` block is thrown, and it becomes the exception that gets propagated. The program prints the messages from both the `try` and `finally` blocks, but the exception from the `finally` block is the one that is thrown and displayed.

---

### **Scenario 2: Exception in `finally` Block and Exception in `try` Block**

If both the `try` block and the `finally` block throw an exception, the **exception thrown in the `finally` block** will **override** the exception that was thrown in the `try` block.

**Example**:

```java
public class FinallyExceptionExample {
    public static void main(String[] args) {
        try {
            System.out.println("Inside try block");
            throw new RuntimeException("Exception from try block");
        } catch (Exception e) {
            System.out.println("Caught exception in catch block");
        } finally {
            System.out.println("Inside finally block");
            // Exception thrown in the finally block
            throw new RuntimeException("Exception from finally block");
        }
    }
}
```

**Output**:

```
Inside try block
Caught exception in catch block
Inside finally block
Exception in thread "main" java.lang.RuntimeException: Exception from finally block
```

In this case:

1. The exception from the `try` block (`RuntimeException` with message `"Exception from try block"`) is caught by the `catch` block.
2. The `finally` block executes and throws its own exception (`RuntimeException` with message `"Exception from finally block"`).
3. The exception thrown in the `finally` block overrides the exception from the `try` block, and it is the one that is propagated.

---

### **Scenario 3: Returning a Value from `finally` Block**

If there is a `return` statement in the `finally` block, it will override any `return` statement in the `try` or `catch` block.

**Example**:

```java
public class FinallyReturnExample {
    public static void main(String[] args) {
        System.out.println("Returned value: " + testMethod());
    }

    public static int testMethod() {
        try {
            System.out.println("Inside try block");
            return 1;  // return from try block
        } catch (Exception e) {
            System.out.println("Caught exception in catch block");
            return 2;  // return from catch block
        } finally {
            System.out.println("Inside finally block");
            return 3;  // return from finally block, overrides others
        }
    }
}
```

**Output**:

```
Inside try block
Inside finally block
Returned value: 3
```

In this case, even though a `return` statement is present in both the `try` and `catch` blocks, the `return` from the `finally` block takes precedence. The method ultimately returns `3` because the `finally` block executes last and overrides the earlier `return` values.

---

### **Handling Exceptions in `finally` Block**

It is also possible for the exception in the `finally` block to be caught if you explicitly handle it with a `try-catch` inside the `finally` block, although this is rare and typically not recommended.

**Example**:

```java
public class FinallyExceptionHandling {
    public static void main(String[] args) {
        try {
            System.out.println("Inside try block");
            throw new RuntimeException("Exception from try block");
        } catch (Exception e) {
            System.out.println("Caught exception in catch block");
        } finally {
            try {
                System.out.println("Inside finally block");
                throw new RuntimeException("Exception from finally block");
            } catch (Exception e) {
                System.out.println("Caught exception in finally block");
            }
        }
    }
}
```

**Output**:

```
Inside try block
Caught exception in catch block
Inside finally block
Caught exception in finally block
```

In this case, the exception in the `finally` block is caught inside its own `try-catch`, so it doesn’t propagate. The program handles it gracefully and continues executing.

---

### **Important Considerations**:

* **Exception Propagation**: If an exception is thrown in the `finally` block, it can **hide or override the exception** thrown in the `try` block or the `catch` block. As a result, the original exception might not be visible to the caller.
* **Uncaught Exception**: If an exception in the `finally` block is not caught, it will propagate and cause the program to terminate.
* **Avoid Complex Logic in `finally`**: It’s generally best to keep the `finally` block simple and focused on cleanup tasks, like closing resources (files, database connections, etc.), to avoid unintended side effects.

---

### **Summary**:

* If an exception occurs in the `finally` block, it will **override** any exception that was thrown in the `try` or `catch` block.
* If there is a `return` in the `finally` block, it will **override** any return from the `try` or `catch` blocks.
* Exceptions in the `finally` block can be **caught and handled** inside the `finally` block itself, but it is generally not recommended.

---

## 50. What is the purpose of the `throw` and `throws` keywords?

In Java, the **`throw`** and **`throws`** keywords are used for exception handling, but they serve different purposes. Here’s a breakdown of each:

---

### **1. `throw` Keyword**:

The `throw` keyword is used to **explicitly throw an exception** from within a method or block of code.

#### Purpose:

* **Throwing Exceptions**: You can use `throw` to create and throw a specific exception (either a predefined one or a custom exception) at runtime.
* Typically used inside methods when you want to handle certain conditions that are considered **exceptional** (i.e., abnormal) in the program’s flow.

#### Syntax:

```java
throw new ExceptionType("Error message");
```

#### Example:

```java
public class ThrowExample {
    public static void main(String[] args) {
        try {
            checkAge(15);  // This will throw an exception
        } catch (IllegalArgumentException e) {
            System.out.println("Caught exception: " + e.getMessage());
        }
    }

    public static void checkAge(int age) {
        if (age < 18) {
            // Throwing an exception when age is less than 18
            throw new IllegalArgumentException("Age must be 18 or older.");
        }
        System.out.println("You are eligible.");
    }
}
```

**Output**:

```
Caught exception: Age must be 18 or older.
```

In this example, if the `age` is less than 18, the `throw` statement is used to explicitly throw an `IllegalArgumentException`.

---

### **2. `throws` Keyword**:

The `throws` keyword is used in a **method declaration** to indicate that the method might **throw one or more exceptions** during execution. It specifies which exceptions the method might throw, making it the responsibility of the calling code to handle them.

#### Purpose:

* **Indicating Possible Exceptions**: Used when a method can throw certain types of checked exceptions that are **not handled within the method**. The calling method must either handle these exceptions using a `try-catch` block or declare that it throws them using `throws`.
* Only **checked exceptions** (exceptions that are subclasses of `Exception`, excluding `RuntimeException` and its subclasses) must be declared with `throws`.

#### Syntax:

```java
returnType methodName() throws ExceptionType1, ExceptionType2 {
    // method implementation
}
```

#### Example:

```java
public class ThrowsExample {
    public static void main(String[] args) {
        try {
            readFile("non_existent_file.txt");
        } catch (IOException e) {
            System.out.println("Caught exception: " + e.getMessage());
        }
    }

    public static void readFile(String fileName) throws IOException {
        // Simulating a situation where an exception could occur
        if (fileName.equals("non_existent_file.txt")) {
            throw new IOException("File not found.");
        }
        System.out.println("File read successfully.");
    }
}
```

**Output**:

```
Caught exception: File not found.
```

In this example, the `readFile()` method declares that it might throw an `IOException`. The calling method (`main`) must handle this exception using a `try-catch` block.

---

### **Differences Between `throw` and `throws`**:

| **Keyword** | **Purpose**                                                                                                                              | **Where It Is Used**              | **Example**                                                   |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------- | ------------------------------------------------------------- |
| `throw`     | Used to **explicitly throw an exception** from within a method or block of code.                                                         | Inside a method or block of code. | `throw new IllegalArgumentException("Invalid age");`          |
| `throws`    | Used in a **method declaration** to indicate that the method might throw certain exceptions that need to be handled by the calling code. | In the method signature.          | `public void readFile(String fileName) throws IOException {}` |

---

### **Example of Both `throw` and `throws`**:

```java
public class ThrowThrowsExample {
    public static void main(String[] args) {
        try {
            validateAge(15);  // This will throw an exception
        } catch (IllegalArgumentException e) {
            System.out.println("Caught exception: " + e.getMessage());
        }
    }

    // Declaring that the method may throw an exception
    public static void validateAge(int age) throws IllegalArgumentException {
        if (age < 18) {
            // Throwing an exception inside the method
            throw new IllegalArgumentException("Age must be at least 18.");
        }
        System.out.println("You are eligible.");
    }
}
```

**Output**:

```
Caught exception: Age must be at least 18.
```

* Here, the method `validateAge()` declares that it may throw an `IllegalArgumentException` using `throws`, and it **explicitly throws** the exception inside the method using `throw`.

---

### **Summary**:

* **`throw`**: Used to **throw** an exception from within a method or code block. It is followed by an instance of an exception (e.g., `throw new Exception("message")`).
* **`throws`**: Used in the method signature to **declare** that the method may throw specific exceptions. The calling code must handle or declare the exception.

---

## 51. What is a custom exception and how to create one?

A **custom exception** in Java is an exception that is defined by the programmer to represent a specific error condition that is not covered by the standard Java exceptions. Custom exceptions are useful when you need to handle specific scenarios in your application that are unique to your business logic.

---

### **How to Create a Custom Exception**

To create a custom exception in Java, you need to:

1. **Extend** the `Exception` class (for checked exceptions) or `RuntimeException` class (for unchecked exceptions).
2. Optionally, provide constructors to pass error messages or other data when the exception is thrown.

### **Steps to Create a Custom Exception:**

1. **Define a class** that extends `Exception` or `RuntimeException`.
2. **Provide constructors** that pass error messages or other details to the superclass.

* A default constructor (no-argument constructor).
* A constructor that accepts an error message (usually a `String`).
* Optionally, a constructor that accepts both a message and a cause (another throwable exception).

### **Example: Custom Checked Exception**

A **checked exception** is one that must be either caught or declared in the method signature using `throws`.

#### Custom Checked Exception Example:

```java
// Define a custom checked exception
class InvalidAgeException extends Exception {
    // Default constructor
    public InvalidAgeException() {
        super("Invalid age provided");
    }

    // Constructor that accepts a custom message
    public InvalidAgeException(String message) {
        super(message);
    }

    // Constructor that accepts a message and a cause
    public InvalidAgeException(String message, Throwable cause) {
        super(message, cause);
    }
}
```

#### Using the Custom Checked Exception:

```java
public class CustomExceptionExample {
    public static void main(String[] args) {
        try {
            validateAge(15);  // This will throw the custom exception
        } catch (InvalidAgeException e) {
            System.out.println("Caught exception: " + e.getMessage());
        }
    }

    // Method that throws the custom exception if age is less than 18
    public static void validateAge(int age) throws InvalidAgeException {
        if (age < 18) {
            throw new InvalidAgeException("Age must be 18 or older.");
        }
        System.out.println("You are eligible.");
    }
}
```

**Output**:

```
Caught exception: Age must be 18 or older.
```

In this example:

* The `InvalidAgeException` class is a custom checked exception.
* The `validateAge()` method declares that it may throw this exception using `throws InvalidAgeException`.
* If the age is less than 18, the method throws an `InvalidAgeException`, and the exception is caught and handled in the `catch` block.

---

### **Example: Custom Unchecked Exception**

An **unchecked exception** is one that extends `RuntimeException`. These do not need to be explicitly declared or caught. They can be thrown and propagated freely.

#### Custom Unchecked Exception Example:

```java
// Define a custom unchecked exception
class InvalidAgeRuntimeException extends RuntimeException {
    // Default constructor
    public InvalidAgeRuntimeException() {
        super("Invalid age provided");
    }

    // Constructor that accepts a custom message
    public InvalidAgeRuntimeException(String message) {
        super(message);
    }

    // Constructor that accepts a message and a cause
    public InvalidAgeRuntimeException(String message, Throwable cause) {
        super(message, cause);
    }
}
```

#### Using the Custom Unchecked Exception:

```java
public class CustomUncheckedExceptionExample {
    public static void main(String[] args) {
        try {
            validateAge(15);  // This will throw the custom unchecked exception
        } catch (InvalidAgeRuntimeException e) {
            System.out.println("Caught exception: " + e.getMessage());
        }
    }

    // Method that throws the custom unchecked exception if age is less than 18
    public static void validateAge(int age) {
        if (age < 18) {
            throw new InvalidAgeRuntimeException("Age must be 18 or older.");
        }
        System.out.println("You are eligible.");
    }
}
```

**Output**:

```
Caught exception: Age must be 18 or older.
```

In this example:

* The `InvalidAgeRuntimeException` class is a custom unchecked exception, extending `RuntimeException`.
* The `validateAge()` method **does not** declare the exception with `throws` because it's an unchecked exception.
* If the age is less than 18, the method throws an `InvalidAgeRuntimeException`, which is caught by the `catch` block.

---

### **Best Practices for Custom Exceptions**:

1. **Use Custom Exceptions to Represent Specific Business Logic**:

* Create custom exceptions that make sense in the context of your application or domain (e.g., `UserNotFoundException`, `InvalidOrderStatusException`).

2. **Provide Meaningful Messages**:

* Always provide meaningful error messages that can help the user or developer understand the issue.

3. **Include a Cause When Appropriate**:

* If your exception is caused by another exception, pass the original exception as the cause to help trace the stack trace.

4. **Extend `RuntimeException` for Unchecked Exceptions**:

* Use `RuntimeException` if you expect the exception to be **rare** or **not recoverable**.
* Use `Exception` for checked exceptions that the caller is expected to handle.

5. **Avoid Overuse of Custom Exceptions**:

* Avoid creating custom exceptions for every minor issue; sometimes using built-in exceptions like `IllegalArgumentException` or `IllegalStateException` is sufficient.

---

### **Summary**:

* **Custom Exception**: An exception that you create to handle specific situations or business rules in your application.
* **To Create a Custom Exception**:

    1. Extend `Exception` for checked exceptions or `RuntimeException` for unchecked exceptions.
    2. Provide meaningful constructors (with messages and optional causes).
* **Checked vs Unchecked**: If you extend `Exception`, it’s a checked exception, and if you extend `RuntimeException`, it’s an unchecked exception.

---

## 52. What is the difference between `Exception` and `Error`?

In Java, both `Exception` and `Error` are subclasses of `Throwable`, which is the superclass of all errors and exceptions in Java. However, they represent different categories of problems and are used in different scenarios.

### **Key Differences Between `Exception` and `Error`**

| **Aspect**               | **`Exception`**                                                                                                                     | **`Error`**                                                                                                                              |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| **Definition**           | Represents conditions that a program can catch and handle (recover from).                                                           | Represents serious problems that a program cannot typically recover from.                                                                |
| **Subclass of**          | `Throwable` → `Exception`                                                                                                           | `Throwable` → `Error`                                                                                                                    |
| **Recoverable?**         | Yes, exceptions are usually recoverable.                                                                                            | No, errors usually represent serious issues that cannot be recovered from.                                                               |
| **Used For**             | Problems that arise due to faulty logic, incorrect input, or external conditions (e.g., file not found, invalid user input).        | Problems that are outside the program's control, such as system failures or JVM issues (e.g., `OutOfMemoryError`, `StackOverflowError`). |
| **Example**              | `IOException`, `SQLException`, `NullPointerException`, `IllegalArgumentException`                                                   | `OutOfMemoryError`, `StackOverflowError`, `VirtualMachineError`                                                                          |
| **Checked or Unchecked** | Most exceptions are **checked exceptions** (e.g., `IOException`), but some are unchecked exceptions (e.g., `NullPointerException`). | Errors are always **unchecked exceptions** (e.g., `OutOfMemoryError`).                                                                   |
| **Handling**             | Can be caught and handled using `try-catch` blocks.                                                                                 | Typically, errors are not caught and handled. They indicate severe problems that the program cannot usually recover from.                |
| **Purpose**              | To signal conditions that a program should handle gracefully (e.g., user input error, I/O errors).                                  | To signal critical system failures that are usually beyond the control of the program (e.g., hardware failures, JVM issues).             |

---

### **Detailed Explanation:**

#### **1. `Exception`:**

An `Exception` is typically used to represent a situation that can be **handled** by the program. You can **catch** an exception in a `try-catch` block, and it is expected that the program can recover from the exception and continue running.

##### **Examples of `Exception`:**

* `IOException`: Thrown when there is a problem with input/output operations (e.g., reading a file).
* `SQLException`: Thrown when there is a database access error.
* `NullPointerException`: Thrown when trying to access a method or field of a null object.

##### **Checked vs Unchecked Exceptions:**

* **Checked exceptions** (e.g., `IOException`, `SQLException`) must be either caught or declared in the method signature using `throws`.
* **Unchecked exceptions** (e.g., `NullPointerException`, `ArrayIndexOutOfBoundsException`) are not required to be caught or declared, and they typically represent programming errors.

---

#### **2. `Error`:**

An `Error` in Java represents a serious problem that the program **cannot handle**. Errors are typically related to the **environment in which the program is running**, such as JVM or system issues, and they indicate that something went wrong at a level beyond the control of the application.

##### **Examples of `Error`:**

* `OutOfMemoryError`: Thrown when the Java Virtual Machine (JVM) runs out of memory.
* `StackOverflowError`: Thrown when the stack size is exceeded, usually due to deep recursion.
* `VirtualMachineError`: Thrown when there is a failure in the JVM, like when the JVM crashes.

##### **Why `Error` is Not Handled:**

Errors usually indicate fatal conditions that cannot be recovered from within the application. Therefore, you **cannot** (and generally should not) catch them using `try-catch` blocks. They usually terminate the program immediately, and recovery from these errors is generally impossible from within the application.

---

### **Example to Illustrate the Difference:**

```java
public class ExceptionErrorExample {
    public static void main(String[] args) {
        try {
            // Uncomment one of the lines below to see how the program behaves
            // Throwing an exception (handled by the program)
            throw new Exception("This is an exception");
            
            // Throwing an error (not typically caught)
            // throw new Error("This is an error");
        } catch (Exception e) {
            System.out.println("Caught Exception: " + e.getMessage());
        }
        // Note: Errors are not caught in the same way as exceptions
    }
}
```

* If you throw an **exception** (`new Exception("This is an exception")`), it will be caught by the `catch` block, and you can handle the error.
* If you throw an **error** (`new Error("This is an error")`), the program will likely terminate abruptly. It is not typically caught and handled.

---

### **Summary of Differences:**

* **`Exception`**: Represents a problem that can usually be handled by the program. Most of the time, exceptions represent errors in the program's logic or operations that can be recovered from.
* **`Error`**: Represents a critical problem (typically system-level failures or JVM issues) that usually cannot be handled by the program.

In practice, **errors** are not meant to be caught or handled, while **exceptions** are the main way Java programs signal and recover from problems that arise during execution.

---

## 53. What are runtime exceptions? Give examples.

**Runtime exceptions** in Java are a special type of **unchecked exception**. They are exceptions that can occur during the execution of the program and are typically caused by programming errors. Unlike checked exceptions, runtime exceptions do not need to be explicitly declared or caught.

### **Key Characteristics of Runtime Exceptions**:

* **Unchecked exceptions**: These do not need to be caught or declared in the method signature. The Java compiler does not require you to handle or declare runtime exceptions.
* **Inherit from `RuntimeException`**: All runtime exceptions are subclasses of the `RuntimeException` class, which in turn inherits from `Exception`.
* **Typically caused by programming bugs**: Most runtime exceptions are caused by programming mistakes, such as accessing an array out of bounds, or trying to access a null object.

### **Common Runtime Exceptions in Java**:

Here are some common runtime exceptions in Java:

---

#### **1. `NullPointerException`**

* **Cause**: Occurs when an application attempts to use `null` where an object is required. For example, calling a method on a null object or accessing a field of a null object.

**Example**:

```java
public class NullPointerExample {
    public static void main(String[] args) {
        String str = null;
        // This will throw a NullPointerException
        System.out.println(str.length());  // Accessing a method on a null object
    }
}
```

---

#### **2. `ArrayIndexOutOfBoundsException`**

* **Cause**: Thrown when an application tries to access an array element using an invalid index (i.e., an index less than `0` or greater than or equal to the array length).

**Example**:

```java
public class ArrayIndexOutOfBoundsExample {
    public static void main(String[] args) {
        int[] arr = new int[5];
        // This will throw ArrayIndexOutOfBoundsException as the index is out of bounds
        System.out.println(arr[5]);  // Valid indices are 0 to 4
    }
}
```

---

#### **3. `ArithmeticException`**

* **Cause**: This exception is thrown when an illegal arithmetic operation occurs, such as dividing by zero.

**Example**:

```java
public class ArithmeticExceptionExample {
    public static void main(String[] args) {
        int result = 10 / 0;  // Division by zero will throw ArithmeticException
    }
}
```

---

#### **4. `ClassCastException`**

* **Cause**: Occurs when an application attempts to cast an object to a class that it is not an instance of.

**Example**:

```java
public class ClassCastExceptionExample {
    public static void main(String[] args) {
        Object obj = new String("Hello");
        // This will throw ClassCastException because obj is a String, not an Integer
        Integer num = (Integer) obj;
    }
}
```

---

#### **5. `NumberFormatException`**

* **Cause**: Thrown when an application attempts to convert a string to a numeric type (e.g., `int`, `double`) but the string does not have a valid format.

**Example**:

```java
public class NumberFormatExceptionExample {
    public static void main(String[] args) {
        String str = "abc";
        // This will throw NumberFormatException as "abc" cannot be parsed to an integer
        int num = Integer.parseInt(str);
    }
}
```

---

#### **6. `IllegalArgumentException`**

* **Cause**: Thrown when a method receives an argument that is inappropriate or illegal for the method’s intended operation.

**Example**:

```java
public class IllegalArgumentExceptionExample {
    public static void main(String[] args) {
        // This will throw IllegalArgumentException because the argument is negative
        setAge(-1);
    }

    public static void setAge(int age) {
        if (age < 0) {
            throw new IllegalArgumentException("Age cannot be negative");
        }
        System.out.println("Age is " + age);
    }
}
```

---

#### **7. `IndexOutOfBoundsException`**

* **Cause**: Similar to `ArrayIndexOutOfBoundsException`, but this exception is thrown for other types of collections such as `List`, `String`, etc.

**Example**:

```java
public class IndexOutOfBoundsExceptionExample {
    public static void main(String[] args) {
        String str = "Hello";
        // This will throw IndexOutOfBoundsException as index 10 is out of bounds
        char ch = str.charAt(10);
    }
}
```

---

### **Why Runtime Exceptions Occur**:

* **Programming Errors**: Most runtime exceptions are caused by simple bugs in the code, such as accessing a null reference, illegal array indices, or incorrect input values.
* **Can be Prevented by Code Reviews and Proper Validation**: Proper input validation and careful code review can minimize the occurrence of runtime exceptions.

### **Do Runtime Exceptions Need to Be Handled?**

* **No, they are unchecked exceptions**: You don't need to declare or handle runtime exceptions explicitly. However, it is a good practice to catch and handle them when you anticipate certain scenarios.

* **Best Practices**:

    * Although runtime exceptions do not need to be caught, it is advisable to prevent them by writing robust code, performing input validation, and using appropriate exception handling where necessary.

---

### **Example: Handling Runtime Exceptions**:

You can handle runtime exceptions using `try-catch` blocks, but it is typically unnecessary for most cases since these exceptions often point to programming mistakes that should be fixed rather than handled at runtime.

```java
public class RuntimeExceptionHandling {
    public static void main(String[] args) {
        try {
            String str = null;
            // Attempting to invoke a method on a null object
            System.out.println(str.length());  // This will throw NullPointerException
        } catch (NullPointerException e) {
            System.out.println("Caught RuntimeException: " + e.getMessage());
        }
    }
}
```

**Output**:

```
Caught RuntimeException: null
```

In this case, the `NullPointerException` is caught and handled, but in most cases, you'd want to avoid such runtime exceptions rather than catch them.

---

### **Summary:**

* **Runtime exceptions** are exceptions that occur during program execution and typically represent programming bugs (e.g., null pointer, array index out of bounds, etc.).
* **Unchecked exceptions**: Runtime exceptions don't need to be explicitly declared or caught.
* **Examples**: `NullPointerException`, `ArrayIndexOutOfBoundsException`, `ArithmeticException`, `ClassCastException`, `NumberFormatException`, etc.
* **Handling**: While you can handle runtime exceptions, it's usually better to fix the underlying issue in the code rather than catching them at runtime.

---

## 54. Can a finally block be skipped?

In Java, the `finally` block is generally guaranteed to execute, whether or not an exception occurs in the `try` block. However, there are a few scenarios in which the `finally` block **may not execute**, but these are rare and exceptional circumstances.

### **1. If the JVM crashes or the program terminates abnormally**

* If the Java Virtual Machine (JVM) crashes or the program is terminated forcibly (e.g., using `System.exit()` or by a fatal error such as a `Segmentation Fault`), the `finally` block may not execute.

  **Example**:

  ```java
  public class FinallyExample {
      public static void main(String[] args) {
          try {
              System.out.println("In try block");
              System.exit(0);  // JVM terminates the program before finally block
          } finally {
              System.out.println("In finally block");  // This will not be executed
          }
      }
  }
  ```

  In the example above, the `System.exit(0)` terminates the program, preventing the `finally` block from executing.

---

### **2. If the thread executing the `finally` block is interrupted or killed**

* If the thread that is executing the `finally` block is interrupted or terminated (e.g., using `Thread.stop()` or an external signal), the `finally` block may not execute completely.

  **Example**:

  ```java
  public class FinallyThreadExample {
      public static void main(String[] args) throws InterruptedException {
          Thread thread = new Thread(() -> {
              try {
                  System.out.println("In try block");
              } finally {
                  System.out.println("In finally block");
              }
          });
          thread.start();
          thread.interrupt();  // Interrupting the thread
          thread.join();
      }
  }
  ```

  In this example, if the thread is interrupted while executing the `finally` block, the `finally` block may be prematurely stopped, and some actions within the block may not be executed.

---

### **3. If a `ThreadDeath` error occurs**

* If the program throws a `ThreadDeath` error (which typically occurs when a thread is stopped forcibly), the `finally` block might not be executed. This is because `ThreadDeath` is a subclass of `Error`, which can be fatal to the thread.

  **Example**:

  ```java
  public class ThreadDeathExample {
      public static void main(String[] args) {
          Thread currentThread = Thread.currentThread();
          currentThread.stop();  // Stop the current thread, causing a ThreadDeath
          try {
              System.out.println("This will not print in finally block");
          } finally {
              System.out.println("Finally block - might not execute in case of ThreadDeath");
          }
      }
  }
  ```

  In this case, `Thread.stop()` throws a `ThreadDeath` error, and the `finally` block might be skipped.

---

### **4. If the program is forcibly terminated (e.g., by an external kill signal)**

* If the program is terminated by an external source, like a kill signal from the operating system (e.g., using `kill` command in Unix/Linux), the `finally` block might not execute.

---

### **Summary**:

* In general, the `finally` block is guaranteed to execute, regardless of whether an exception occurs or not.
* The `finally` block may **not execute** in the following scenarios:

    * The JVM crashes or the program is terminated using `System.exit()`.
    * The thread executing the `finally` block is interrupted or killed.
    * A `ThreadDeath` error occurs.
    * The program is forcibly terminated (e.g., using external tools).

However, in regular, well-behaved programs, you can rely on the `finally` block to execute, making it a useful place to put cleanup code (e.g., closing file streams, releasing resources).

---

## 55. Can we catch multiple exceptions in one catch block?

Yes, in Java **you can catch multiple exceptions in one `catch` block**. This feature was introduced in **Java 7** and is called **multi-catch**.

### **Syntax of Multi-Catch**:

The syntax allows you to specify multiple exceptions by separating them with a pipe (`|`) symbol. These exceptions are caught in the same `catch` block, and you can handle them together.

```java
try {
    // Code that might throw multiple exceptions
} catch (ExceptionType1 | ExceptionType2 | ExceptionType3 e) {
    // Handle the exceptions
}
```

### **Key Points**:

1. **Exceptions are separated by `|`**: Use the pipe (`|`) symbol to separate different exception types.
2. **Cannot use the same exception type multiple times**: If the exception types are the same, you can't catch them in a multi-catch block.
3. **The exception variable (`e`) is effectively `final`**: The exception object cannot be modified within the `catch` block since the variable is implicitly declared as `final`.
4. **No multiple `catch` blocks for the same exception**: You can't catch the same exception type in multiple `catch` blocks within a single `try-catch` statement.

---

### **Example of Multi-Catch**:

```java
public class MultiCatchExample {
    public static void main(String[] args) {
        try {
            String str = null;
            int[] arr = new int[5];

            // This will throw a NullPointerException
            System.out.println(str.length());
            
            // This will throw an ArrayIndexOutOfBoundsException
            System.out.println(arr[10]);
        } catch (NullPointerException | ArrayIndexOutOfBoundsException e) {
            System.out.println("Caught exception: " + e);
        }
    }
}
```

### **Explanation**:

* In the above example, both `NullPointerException` and `ArrayIndexOutOfBoundsException` are caught by the same `catch` block.
* You can add more exceptions separated by `|` if needed.

### **Why Use Multi-Catch?**

* **Cleaner code**: When the handling logic for different exceptions is the same, using multi-catch helps you avoid redundancy in your code.
* **Better readability**: It's easier to understand and maintain the code when multiple exceptions can be handled together.

---

### **Example with Multiple Exceptions and Handling Logic**:

```java
public class MultiCatchExample {
    public static void main(String[] args) {
        try {
            String str = "123a";  // Invalid number format
            
            // This will throw NumberFormatException
            int number = Integer.parseInt(str);

            // This will throw ArithmeticException (divide by zero)
            int result = 10 / 0;
        } catch (NumberFormatException | ArithmeticException e) {
            System.out.println("Caught exception: " + e.getClass().getName() + " - " + e.getMessage());
        }
    }
}
```

**Output**:

```
Caught exception: java.lang.ArithmeticException - / by zero
```

In this case, the `catch` block handles both `NumberFormatException` and `ArithmeticException` in the same way.

---

### **Things to Avoid**:

* You **cannot catch `Exception` and its subclasses together** in a multi-catch block if the subclasses are listed. For example:

  ```java
  catch (Exception | RuntimeException e)  // This will not compile
  ```

  Since `RuntimeException` is already a subclass of `Exception`, it leads to redundancy.

---

### **Summary**:

* **Yes**, you can catch multiple exceptions in a single `catch` block using multi-catch (available since Java 7).
* You separate exceptions using `|` (pipe symbol).
* The exception variable is implicitly `final`, meaning it cannot be modified inside the `catch` block.

This feature simplifies exception handling and makes the code more concise when you need to handle multiple types of exceptions similarly.

---

## 56. How does try-with-resources work?

The **try-with-resources** statement, introduced in **Java 7**, is a feature that simplifies the management of resources like files, sockets, database connections, etc. It automatically **closes** resources when they are no longer needed, without the need for explicit `finally` blocks. This feature ensures that resources are closed even if an exception occurs.

### **How It Works:**

* **Try-with-resources** works by using the **`AutoCloseable`** interface.
* Any class that implements `AutoCloseable` (or its more specific subclass `Closeable`) can be used in the try-with-resources statement.
* The **`close()`** method of these resources is automatically called when the `try` block finishes executing, whether it completes successfully or an exception is thrown.

### **Syntax of try-with-resources**:

```java
try (ResourceType resource = new ResourceType()) {
    // Code that uses the resource
} catch (Exception e) {
    // Handle exceptions
} finally {
    // The resource will automatically be closed after the try block is executed
}
```

### **Key Points**:

1. **Automatic Resource Management**: Resources (like `FileInputStream`, `BufferedReader`, etc.) are **automatically closed** when the `try` block completes.
2. **Requires `AutoCloseable` Interface**: Resources must implement `AutoCloseable` (or `Closeable` for IO resources).
3. **No Need for `finally` Block**: You don’t need to explicitly write code to close resources in the `finally` block.
4. **Multiple Resources**: You can handle multiple resources in the same `try` statement, and all of them will be closed automatically.

---

### **Example: Using try-with-resources**:

```java
import java.io.*;

public class TryWithResourcesExample {
    public static void main(String[] args) {
        // Using try-with-resources for reading a file
        try (BufferedReader reader = new BufferedReader(new FileReader("testfile.txt"))) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            System.out.println("Exception: " + e.getMessage());
        }
    }
}
```

### **Explanation**:

* In the above example, `BufferedReader` is a resource that implements `AutoCloseable`, so it can be used in the try-with-resources statement.
* After the `try` block finishes (whether an exception is thrown or not), the `BufferedReader` is automatically closed, and the `close()` method is called.

---

### **Multiple Resources in try-with-resources**:

You can use multiple resources in the same `try-with-resources` block by separating them with a semicolon (`;`).

```java
import java.io.*;

public class MultipleResourcesExample {
    public static void main(String[] args) {
        // Using multiple resources in try-with-resources
        try (BufferedReader reader = new BufferedReader(new FileReader("testfile.txt"));
             PrintWriter writer = new PrintWriter(new FileWriter("outputfile.txt"))) {

            String line;
            while ((line = reader.readLine()) != null) {
                writer.println(line);  // Write to another file
            }

        } catch (IOException e) {
            System.out.println("Exception: " + e.getMessage());
        }
    }
}
```

In this example, both the `BufferedReader` and `PrintWriter` are automatically closed at the end of the `try` block, even if an exception is thrown.

---

### **How the `close()` Method Works**:

* Each resource that is used in a try-with-resources block must implement the `AutoCloseable` interface, which has a `close()` method.
* When the `try` block finishes, whether normally or due to an exception, the **`close()`** method is invoked automatically on each resource.

### **Exceptions and the `close()` Method**:

* If an exception is thrown during the execution of the `try` block, the `close()` method is still invoked.
* If an exception is thrown while closing a resource (in the `close()` method), the exception is suppressed and can be accessed through the `getSuppressed()` method of the original exception.

Example:

```java
public class SuppressedExceptionsExample {
    public static void main(String[] args) {
        try (BufferedReader reader = new BufferedReader(new FileReader("testfile.txt"))) {
            String line = reader.readLine();  // May throw IOException
        } catch (IOException e) {
            System.out.println("Main exception: " + e.getMessage());
            // Access suppressed exceptions if any
            Throwable[] suppressedExceptions = e.getSuppressed();
            for (Throwable t : suppressedExceptions) {
                System.out.println("Suppressed: " + t);
            }
        }
    }
}
```

In this case, if an exception occurs when trying to close the `BufferedReader`, it is stored as a suppressed exception and can be accessed later.

---

### **Advantages of try-with-resources**:

1. **Simplifies code**: It reduces boilerplate code needed to manage resource cleanup.
2. **Automatic resource management**: Resources are closed automatically, making the code cleaner and less error-prone.
3. **Prevents resource leaks**: By ensuring resources are always closed, it helps avoid issues like memory leaks or file handle exhaustion.

---

### **Summary**:

* **Try-with-resources** is a feature in Java 7 and later that simplifies resource management by automatically closing resources (like files, streams, database connections) when they are no longer needed.
* It works with classes that implement `AutoCloseable` or `Closeable`.
* You can handle multiple resources in the same `try` block, and all resources will be closed automatically.
* It's an efficient and error-free way to manage resources, especially in situations where manual resource cleanup in a `finally` block could be cumbersome or prone to errors.

---

## 57. What are suppressed exceptions?

**Suppressed exceptions** in Java refer to exceptions that are **not thrown directly**, but are instead **stored** and reported by the JVM in case of multiple exceptions, particularly in the context of a `try-with-resources` block. These exceptions occur when an exception is thrown during the **closing of resources** (in the `close()` method of an `AutoCloseable` or `Closeable` resource), and the JVM needs to track both the original exception and the one that occurred during the resource cleanup.

### **How Suppressed Exceptions Work:**

1. **Multiple Exceptions**: When an exception is thrown inside the `try` block, and another exception is thrown during the closing of resources in the `finally` block (or automatically during the try-with-resources mechanism), the first exception is considered the **primary exception**.

2. **Suppressed Exception**: The exception that occurs while closing the resource is stored as a **suppressed exception**. It is associated with the primary exception, so both can be reported to the programmer. This ensures that all exceptions are not lost, even if one exception has already been thrown.

3. **Accessing Suppressed Exceptions**: The suppressed exceptions can be accessed via the `getSuppressed()` method on the primary exception.

### **Key Points About Suppressed Exceptions**:

* **Primary vs. Suppressed**: The exception that caused the control flow to enter the `catch` block is the primary exception, and the exception that occurs while closing the resource is the suppressed exception.
* **getSuppressed() Method**: The `getSuppressed()` method of `Throwable` returns an array of `Throwable` objects that were suppressed during the handling of the primary exception.
* **Automatic Handling**: Suppressed exceptions are typically handled by the JVM and don't need to be manually tracked by the programmer. However, if you're logging or rethrowing exceptions, you can access them using `getSuppressed()`.

---

### **Example of Suppressed Exceptions**:

```java
import java.io.*;

public class SuppressedExceptionExample {
    public static void main(String[] args) {
        try (BufferedReader reader = new BufferedReader(new FileReader("testfile.txt"))) {
            String line = reader.readLine();  // May throw IOException
            System.out.println(line);
        } catch (IOException e) {
            System.out.println("Primary exception: " + e.getMessage());
            
            // Get and print any suppressed exceptions
            for (Throwable t : e.getSuppressed()) {
                System.out.println("Suppressed: " + t.getMessage());
            }
        }
    }
}
```

### **Explanation**:

* In this example, the `BufferedReader` is opened using a try-with-resources block.
* If an exception is thrown while reading the file (e.g., `IOException`), it is the **primary exception**.
* If an exception occurs when closing the `BufferedReader` (e.g., another `IOException`), it is considered a **suppressed exception**.
* The suppressed exceptions can be accessed using `e.getSuppressed()` and can be logged or further analyzed.

---

### **How Suppressed Exceptions Occur**:

Suppressed exceptions commonly occur when a resource that implements `AutoCloseable` or `Closeable` (like a `BufferedReader`, `FileOutputStream`, or database connection) throws an exception during its `close()` method, after the primary exception has already been thrown. These suppressed exceptions don't interrupt the flow of the program, but they are **logged** and **accessible** through the primary exception.

---

### **Example with Multiple Exceptions**:

```java
import java.io.*;

public class MultipleExceptionsExample {
    public static void main(String[] args) {
        try (BufferedReader reader = new BufferedReader(new FileReader("testfile.txt"))) {
            // Simulating an exception during resource reading
            String line = reader.readLine();  
            int result = 10 / 0;  // Simulate ArithmeticException

        } catch (IOException | ArithmeticException e) {
            System.out.println("Primary exception: " + e.getMessage());

            // Access and print suppressed exceptions
            for (Throwable t : e.getSuppressed()) {
                System.out.println("Suppressed: " + t.getMessage());
            }
        }
    }
}
```

### **Explanation**:

1. An `IOException` might occur when reading the file.
2. Simultaneously, an `ArithmeticException` is thrown (division by zero).
3. If an exception happens when closing the `BufferedReader`, that exception will be suppressed and stored in the `getSuppressed()` array.
4. Both the primary exception (e.g., `ArithmeticException`) and any suppressed exceptions (e.g., `IOException` when closing the reader) can be accessed.

---

### **What Happens Under the Hood**:

* When the `try` block finishes (successfully or via an exception), the `finally` block (or the resource closing in the try-with-resources) attempts to clean up the resources.
* If an exception occurs during resource cleanup, the JVM associates that exception as a suppressed exception with the original exception (if one exists).
* The primary exception is thrown first, and if it’s caught, you can examine the suppressed exceptions.

### **Accessing Suppressed Exceptions**:

To access suppressed exceptions, you can use the `getSuppressed()` method on the caught exception (the primary exception). The method returns an array of `Throwable` objects that represent the suppressed exceptions.

```java
Throwable[] suppressedExceptions = exception.getSuppressed();
for (Throwable suppressed : suppressedExceptions) {
    System.out.println("Suppressed: " + suppressed);
}
```

### **Why Suppressed Exceptions Matter**:

* **Prevents loss of exception details**: Without suppressed exceptions, you might lose important exception details that happen during resource cleanup (e.g., closing a file stream).
* **Helps in debugging**: By providing both the primary and suppressed exceptions, developers have more context and can investigate all issues, not just the one that directly caused the failure.

---

### **Summary**:

* **Suppressed exceptions** occur when an exception is thrown during the automatic closing of resources (in `try-with-resources`).
* These exceptions are **not thrown directly** but are instead stored and reported alongside the primary exception.
* You can access suppressed exceptions through the `getSuppressed()` method on the primary exception.
* This mechanism helps ensure that no exception details are lost during cleanup, especially in cases where resource management could cause additional errors.

---

## 58. Can you rethrow an exception? How?

Yes, you can **rethrow an exception** in Java. Rethrowing an exception means **throwing an exception that has been caught** in a `catch` block so that it can be handled further up the call stack or logged.

### **Why Rethrow an Exception?**

* **Allowing Higher Layers to Handle It**: Sometimes, a lower-level method might catch an exception but decide that it cannot fully handle it, so it rethrows it to be handled by a higher-level method.
* **Log and Re-throw**: You might want to log an exception at one level, then rethrow it for a higher-level handler to take further action.
* **Preserving Stack Trace**: Rethrowing the exception ensures that the original stack trace is preserved, allowing for better debugging.

### **How to Rethrow an Exception**:

There are two common ways to rethrow an exception:

1. **Rethrow the caught exception as-is**.
2. **Rethrow the caught exception as a different exception**.

---

### **1. Rethrow the Caught Exception As-Is**:

If you catch an exception and want to rethrow it without modifying it, you simply use the `throw` statement.

#### Example:

```java
public class RethrowExample {
    public static void main(String[] args) {
        try {
            someMethod();
        } catch (Exception e) {
            System.out.println("Caught exception: " + e.getMessage());
            // Rethrow the exception
            throw e;  // Rethrowing the caught exception
        }
    }

    public static void someMethod() throws Exception {
        throw new Exception("An exception occurred!");
    }
}
```

### **Explanation**:

* In this example, `someMethod()` throws an exception.
* The exception is caught in the `catch` block, and the same exception is rethrown using `throw e;`.

---

### **2. Rethrow the Caught Exception as a Different Exception**:

You can also catch one exception type and **throw another type** of exception (this is known as "wrapping" an exception). This can be useful if you want to provide more specific information or wrap a lower-level exception in a more meaningful custom exception.

#### Example:

```java
public class RethrowAsDifferentException {
    public static void main(String[] args) {
        try {
            someMethod();
        } catch (IOException e) {
            System.out.println("Caught IOException: " + e.getMessage());
            // Wrap the IOException in a custom exception and rethrow it
            throw new CustomException("Custom exception occurred", e);
        }
    }

    public static void someMethod() throws IOException {
        throw new IOException("File not found");
    }
}

// Custom exception
class CustomException extends RuntimeException {
    public CustomException(String message, Throwable cause) {
        super(message, cause);
    }
}
```

### **Explanation**:

* In this case, `someMethod()` throws an `IOException`.
* The `IOException` is caught and wrapped in a custom `CustomException` and then rethrown.
* The custom exception retains the original exception (`IOException`) as its cause, which helps in preserving the original stack trace.

---

### **When to Rethrow an Exception**:

* **When a method cannot fully handle the exception**: If the current method cannot properly handle the exception, it can rethrow it so that a higher-level method can take care of it.
* **To add more context**: Rethrowing exceptions can be useful to provide more context or to wrap lower-level exceptions into more meaningful exceptions for the higher layers of the application.
* **Preserving original exception details**: By rethrowing the original exception or wrapping it in another exception, you preserve the original exception's stack trace.

---

### **Rethrowing and Exception Types**:

* **Checked Exceptions**: If you're rethrowing a checked exception, it must either be caught or declared in the method signature using `throws`. For example, if a method throws an `IOException`, you must either handle it with a `catch` block or declare it using `throws IOException` in the method signature.

* **Unchecked Exceptions**: For unchecked exceptions (like `RuntimeException` and its subclasses), you can rethrow them without declaring them in the method signature or having to catch them explicitly.

---

### **Example with Declaring Exceptions**:

```java
public class RethrowCheckedException {
    public static void main(String[] args) {
        try {
            someMethod();
        } catch (IOException e) {
            System.out.println("Caught IOException: " + e.getMessage());
            // Rethrow IOException
            try {
                throw e;  // Rethrowing the caught exception
            } catch (IOException e2) {
                System.out.println("Caught and rethrown: " + e2.getMessage());
            }
        }
    }

    public static void someMethod() throws IOException {
        throw new IOException("An IO exception occurred!");
    }
}
```

In this case, the exception is both caught and then rethrown.

---

### **Summary**:

* **Yes, you can rethrow an exception** in Java using the `throw` statement.
* **Rethrow as-is**: Simply throw the caught exception again.
* **Wrap and rethrow**: Catch one exception and throw a new exception (e.g., a custom exception).
* **Why rethrow?**: To allow higher levels to handle the exception, preserve the stack trace, or provide more meaningful context by wrapping the original exception.
* **Rethrowing checked exceptions**: If the exception is a checked exception, you must declare it in the method signature (`throws`).

---

## 59. What is exception chaining?

**Exception chaining** in Java refers to the practice of **throwing a new exception while preserving the original exception** that caused the error. This allows developers to provide more context or meaning when an exception is propagated, while also retaining the stack trace and other details of the original exception.

### **How Does Exception Chaining Work?**

When an exception occurs in a method, it can be caught and then rethrown or wrapped in another exception (often a custom exception). This **original exception** is passed as the **cause** of the new exception. This mechanism is supported by the `Throwable` class through the `initCause(Throwable cause)` method, and the `Throwable.getCause()` method, which allows access to the original exception.

### **Why Use Exception Chaining?**

* **Contextual Information**: When an exception occurs in a lower-level method, rethrowing it as a higher-level exception allows you to provide more context and help the calling method understand what went wrong in a clearer way.
* **Preserving the Original Stack Trace**: Exception chaining ensures that the original exception's stack trace is preserved, so the full context of the failure can be analyzed.

---

### **Example of Exception Chaining**:

```java
public class ExceptionChainingExample {
    public static void main(String[] args) {
        try {
            methodA();
        } catch (CustomException e) {
            e.printStackTrace();
        }
    }

    public static void methodA() throws CustomException {
        try {
            methodB();
        } catch (IOException e) {
            // Exception chaining: Wrap IOException in a CustomException and pass it as the cause
            throw new CustomException("Exception occurred in methodA", e);
        }
    }

    public static void methodB() throws IOException {
        // Simulate an IOException
        throw new IOException("File not found");
    }
}

// Custom exception
class CustomException extends Exception {
    public CustomException(String message, Throwable cause) {
        super(message, cause);
    }
}
```

### **Explanation**:

1. **`methodB()`** throws an `IOException` (simulating a file-related issue).
2. **`methodA()`** catches the `IOException` and then throws a `CustomException`, passing the original `IOException` as the cause of the new exception.
3. The exception is then caught in the `main` method and printed using `e.printStackTrace()`, which will show both the `CustomException` and the original `IOException` in the output.

The output of this program would look like this:

```
CustomException: Exception occurred in methodA
    at ExceptionChainingExample.methodA(ExceptionChainingExample.java:10)
    at ExceptionChainingExample.main(ExceptionChainingExample.java:5)
Caused by: java.io.IOException: File not found
    at ExceptionChainingExample.methodB(ExceptionChainingExample.java:15)
    at ExceptionChainingExample.methodA(ExceptionChainingExample.java:8)
    ... 1 more
```

As shown above:

* The `CustomException` provides a new message (`Exception occurred in methodA`).
* The **original exception** (`IOException: File not found`) is chained and shown as the cause of the `CustomException`, preserving the original stack trace.

---

### **How Exception Chaining Works**:

1. **Using `initCause()`**: If you want to set a cause for an exception, you can use the `initCause()` method after the exception object is created. However, this is mostly done in the constructor of custom exceptions.

   ```java
   public class CustomException extends Exception {
       public CustomException(String message) {
           super(message);
       }
       
       public CustomException(String message, Throwable cause) {
           super(message);
           this.initCause(cause); // Initialize cause
       }
   }
   ```

2. **Using Constructors to Pass the Cause**: Most custom exception classes extend `Exception` or `RuntimeException` and provide constructors that allow passing the cause directly.

   ```java
   public CustomException(String message, Throwable cause) {
       super(message, cause);
   }
   ```

3. **`getCause()` Method**: To access the original exception, you can use the `getCause()` method on the exception object, which returns the original exception (the cause).

   ```java
   try {
       // some code
   } catch (CustomException e) {
       Throwable cause = e.getCause();
       System.out.println("Original exception: " + cause);
   }
   ```

---

### **Advantages of Exception Chaining**:

* **Better Debugging**: By retaining the original exception, you provide more context for debugging, as the complete stack trace and the cause of the error are available.
* **Improved Exception Handling**: It allows a lower-level method to throw a higher-level exception that makes sense in the context of the application without losing information about the underlying issue.
* **Clearer Error Messages**: By chaining exceptions, you can provide more meaningful messages in the new exception that describe the problem more clearly, while still capturing the details of the original exception.

---

### **Example of Exception Chaining with Unchecked Exceptions**:

You can also chain unchecked exceptions (i.e., subclasses of `RuntimeException`), just like checked exceptions.

```java
public class UncheckedExceptionChaining {
    public static void main(String[] args) {
        try {
            methodA();
        } catch (RuntimeException e) {
            e.printStackTrace();
        }
    }

    public static void methodA() {
        try {
            methodB();
        } catch (ArithmeticException e) {
            // Rethrow as a different unchecked exception
            throw new CustomRuntimeException("Custom runtime exception", e);
        }
    }

    public static void methodB() {
        // Simulating an ArithmeticException
        int result = 10 / 0;  // This will throw ArithmeticException
    }
}

// Custom unchecked exception
class CustomRuntimeException extends RuntimeException {
    public CustomRuntimeException(String message, Throwable cause) {
        super(message, cause);
    }
}
```

This will output:

```
CustomRuntimeException: Custom runtime exception
    at UncheckedExceptionChaining.methodA(UncheckedExceptionChaining.java:10)
    at UncheckedExceptionChaining.main(UncheckedExceptionChaining.java:5)
Caused by: java.lang.ArithmeticException: / by zero
    at UncheckedExceptionChaining.methodB(UncheckedExceptionChaining.java:15)
    at UncheckedExceptionChaining.methodA(UncheckedExceptionChaining.java:8)
    ... 1 more
```

---

### **Conclusion**:

* **Exception chaining** allows you to throw a new exception while preserving the original exception (the cause), providing more context and making it easier to debug errors.
* It is useful when you want to wrap lower-level exceptions into higher-level exceptions, add more context, and still keep the original exception's details for troubleshooting.
* Exception chaining is supported by the `Throwable` class via constructors and the `initCause()` method, and you can access the cause using the `getCause()` method.

---

## 60. Why is it bad to catch `Exception` or `Throwable`?

Catching `Exception` or `Throwable` in Java is generally considered bad practice for several important reasons. While it may seem convenient to catch all types of exceptions, doing so can lead to serious issues in your code, including making it harder to debug and maintain. Here’s why catching these general exceptions is usually discouraged:

### **1. Hides Specific Exceptions**

When you catch `Exception` or `Throwable`, you are catching all exceptions, including those that are **not intended** to be caught in that context. This can **hide specific exceptions** that would otherwise be handled more appropriately by catching them individually. Catching a general exception prevents you from identifying and handling specific issues properly.

For example:

```java
try {
    // Some code that might throw various exceptions
} catch (Exception e) {
    // Catch all exceptions (good or bad)
    e.printStackTrace();
}
```

In this case, the developer cannot distinguish between an **IOException**, **NullPointerException**, or other exceptions that might require different handling logic.

### **2. Makes Debugging Harder**

By catching general exceptions, you lose valuable debugging information. The original exception’s stack trace is often crucial in diagnosing the cause of a problem. When you catch `Exception` or `Throwable`, you may miss out on **critical information** about what exactly went wrong.

For example:

```java
try {
    // Some risky code
} catch (Exception e) {
    // Printing the error, but losing the context of the actual problem
    System.out.println("Something went wrong");
}
```

If you caught only specific exceptions, you would have seen the exact error that occurred, making it easier to fix the problem.

### **3. Captures Errors That Shouldn’t Be Handled**

`Throwable` is the superclass of both `Exception` and `Error`. `Error` represents serious issues that your program **cannot** handle, such as **OutOfMemoryError**, **StackOverflowError**, or **VirtualMachineError**. These are typically unrecoverable errors and should not be caught or handled by the application. Catching these errors can **lead to unpredictable behavior** and **suppress critical problems** that should cause the program to fail fast.

Example:

```java
try {
    // Code that might run into an OutOfMemoryError
} catch (Throwable t) {
    // Catching Error types like OutOfMemoryError is dangerous
    t.printStackTrace();
}
```

Catching `Throwable` would let the program continue running despite an **OutOfMemoryError**, which is potentially catastrophic and should cause the program to stop.

### **4. Makes Code Harder to Maintain**

Catching `Exception` or `Throwable` indiscriminately can make your code **unclear** and **difficult to maintain**. It can mask potential bugs and lead to unhandled exceptions that aren't properly addressed. Future developers may be unsure of why exceptions are being caught so broadly and may not be aware of specific error-handling requirements.

For example:

```java
try {
    // Risky code
} catch (Exception e) {
    // Logging or swallowing the exception but not addressing the underlying issue
    e.printStackTrace();
}
```

This type of generic handling makes it unclear what exceptions are expected and how they should be handled.

### **5. Can Lead to Unintended Consequences**

Catching all exceptions can lead to unintended consequences, especially if you decide to swallow exceptions (i.e., catch them without taking any corrective action). This can lead to **silent failures**, where the program continues to run despite encountering an error. The problem might go unnoticed until it causes a much larger issue.

For example:

```java
try {
    // Some operation
} catch (Exception e) {
    // Swallowing the exception without any recovery logic
}
```

In this case, even though the exception occurs, nothing is done to handle it, leading to potentially severe consequences down the road.

---

### **Best Practices for Exception Handling:**

1. **Catch Specific Exceptions**: Always catch specific exceptions that you expect might happen, and handle them appropriately. This allows you to respond to errors in a meaningful way.

   ```java
   try {
       // Code that might throw specific exceptions
   } catch (IOException e) {
       // Handle IO exception
   } catch (SQLException e) {
       // Handle SQL exception
   }
   ```

2. **Avoid Catching `Throwable`**: Never catch `Throwable` unless you have a very specific use case (like for a top-level exception handler), as it can also capture `Error` types that should not be caught.

3. **Handle Errors Properly**: If you must catch exceptions, **catch only the exceptions you can handle**. Let the program fail fast for critical errors (like `OutOfMemoryError`).

4. **Use Multiple Catch Blocks**: Use separate `catch` blocks for different types of exceptions, so you can handle each case appropriately.

   ```java
   try {
       // Code
   } catch (IOException e) {
       // Handle IO exception
   } catch (SQLException e) {
       // Handle SQL exception
   }
   ```

5. **Re-throw Exceptions When Appropriate**: If you cannot handle an exception properly, **rethrow it** to let the caller handle it, ensuring that the exception doesn't get swallowed or lost.

---

### **Summary:**

* Catching `Exception` or `Throwable` is bad practice because it hides specific exceptions, makes debugging difficult, captures errors that should not be handled, and makes the code harder to maintain.
* Always try to catch specific exceptions and handle them meaningfully.
* Avoid catching `Throwable` or generic `Exception` unless absolutely necessary (such as for logging or top-level exception handling).
* Handle only the exceptions you can address and let the program fail fast in case of serious issues.

By following these guidelines, you'll write more robust, maintainable, and predictable code.

Let me know if you need further clarification!

---

### 🔹 61–75: **Collections Framework**

## 61. What is the Collection framework in Java?

The **Collection Framework in Java** is a unified architecture that provides **interfaces**, **classes**, and **algorithms** to store, retrieve, and manipulate groups of objects efficiently.

---

### 🔹 Key Points:

* It is part of the `java.util` package.
* Supports **data structures** like lists, sets, queues, and maps.
* Enables **polymorphism**, **code reusability**, and **performance optimization**.
* Most collections support **generics** for type safety.

---

### 🔹 Core Interfaces:

| Interface    | Description                                                                            |
| ------------ | -------------------------------------------------------------------------------------- |
| `Collection` | Root of the hierarchy. Represents a group of objects.                                  |
| `List`       | Ordered collection. Allows duplicates. (e.g., `ArrayList`, `LinkedList`)               |
| `Set`        | No duplicates. (e.g., `HashSet`, `TreeSet`)                                            |
| `Queue`      | FIFO structure for holding elements before processing. (e.g., `PriorityQueue`)         |
| `Deque`      | Double-ended queue. (e.g., `ArrayDeque`)                                               |
| `Map`        | Stores key-value pairs. Not a subinterface of Collection. (e.g., `HashMap`, `TreeMap`) |

---

### 🔹 Advantages of Collection Framework:

* **Reduces development time** through reusable components.
* **Consistent API**: All collections implement standard interfaces.
* **Interoperability**: Can switch implementations easily.
* **Efficiency**: High-performance algorithms and data structures.

---

### 🔹 Example:

```java
import java.util.*;

public class CollectionDemo {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Java");
        list.add("Python");
        list.add("Java"); // Duplicates allowed
        System.out.println("List: " + list);

        Set<String> set = new HashSet<>(list);
        System.out.println("Set: " + set); // No duplicates

        Map<Integer, String> map = new HashMap<>();
        map.put(1, "One");
        map.put(2, "Two");
        System.out.println("Map: " + map);
    }
}
```

---

## 62. What is the difference between List, Set, and Map?

The main differences between **List**, **Set**, and **Map** in Java lie in how they store elements, whether they allow duplicates, and how they maintain order.

---

### 🔸 1. **List**

* **Definition**: An ordered collection (also known as a sequence).
* **Duplicates**: ✅ **Allows duplicates**
* **Order**: ✅ **Maintains insertion order**
* **Index-based access**: ✅ Yes
* **Common Implementations**:

    * `ArrayList`
    * `LinkedList`
    * `Vector`
    * `Stack`

**Example**:

```java
List<String> list = new ArrayList<>();
list.add("A");
list.add("B");
list.add("A");  // Duplicate allowed
System.out.println(list);  // [A, B, A]
```

---

### 🔸 2. **Set**

* **Definition**: A collection that **does not allow duplicate elements**.

* **Duplicates**: ❌ **No duplicates**

* **Order**:

    * `HashSet`: ❌ Unordered
    * `LinkedHashSet`: ✅ Maintains insertion order
    * `TreeSet`: ✅ Sorted order

* **Common Implementations**:

    * `HashSet`
    * `LinkedHashSet`
    * `TreeSet`

**Example**:

```java
Set<String> set = new HashSet<>();
set.add("A");
set.add("B");
set.add("A");  // Ignored
System.out.println(set);  // [A, B] or [B, A] (unordered)
```

---

### 🔸 3. **Map**

* **Definition**: Stores **key-value pairs**. Each key is unique.

* **Duplicates**:

    * **Keys**: ❌ No duplicates
    * **Values**: ✅ Duplicates allowed

* **Order**:

    * `HashMap`: ❌ Unordered
    * `LinkedHashMap`: ✅ Insertion order
    * `TreeMap`: ✅ Sorted by keys

* **Common Implementations**:

    * `HashMap`
    * `LinkedHashMap`
    * `TreeMap`
    * `Hashtable`

**Example**:

```java
Map<Integer, String> map = new HashMap<>();
map.put(1, "Apple");
map.put(2, "Banana");
map.put(1, "Grape");  // Key 1 is overwritten
System.out.println(map);  // {1=Grape, 2=Banana}
```

---

### 🔹 Summary Table:

| Feature      | **List**        | **Set**         | **Map**                   |
| ------------ | --------------- | --------------- | ------------------------- |
| Duplicates   | Allowed         | Not allowed     | Keys: No, Values: Allowed |
| Order        | Maintains order | Depends on type | Depends on type           |
| Key-Value    | No              | No              | Yes                       |
| Index Access | Yes             | No              | No                        |

---

## 63. What is the difference between ArrayList and LinkedList?

The main difference between **ArrayList** and **LinkedList** in Java lies in their **internal data structures** and **performance characteristics** for common operations like insertion, deletion, and access.

---

### 🔸 1. **ArrayList**

* **Backed by**: Dynamic **array**
* **Access Time**: ✅ **Fast (O(1))** for random access
* **Insertion/Deletion**:

    * ❌ **Slow (O(n))** in the middle (shifting needed)
    * ✅ Fast at the end (usually)
* **Memory Overhead**: Less (no extra object for links)

```java
List<String> arrayList = new ArrayList<>();
arrayList.add("A");
arrayList.get(0);  // Fast access
```

---

### 🔸 2. **LinkedList**

* **Backed by**: **Doubly linked list**
* **Access Time**: ❌ **Slower (O(n))** for random access
* **Insertion/Deletion**:

    * ✅ **Fast (O(1))** at head/tail/middle if position is known
* **Memory Overhead**: More (each node stores two pointers)

```java
List<String> linkedList = new LinkedList<>();
linkedList.add("A");
linkedList.addFirst("B");  // Efficient insertion at head
```

---

### 🔹 Summary Table:

| Feature                | **ArrayList**   | **LinkedList**                     |
| ---------------------- | --------------- | ---------------------------------- |
| Data Structure         | Dynamic array   | Doubly linked list                 |
| Access (get/set)       | ✅ Fast (O(1))   | ❌ Slow (O(n))                      |
| Insert/Delete (middle) | ❌ Slow (O(n))   | ✅ Fast (O(1)) if node is known     |
| Memory                 | Efficient       | More overhead (next/prev pointers) |
| Use Case               | Frequent access | Frequent insertions/deletions      |

---

### 🔹 When to Use Which?

* Use **ArrayList** when you need **fast access** and don't modify the list much.
* Use **LinkedList** when you need **frequent additions/removals** at the beginning or middle.

---

## 64. What is the difference between HashSet and TreeSet?

The **difference between `HashSet` and `TreeSet`** in Java mainly lies in how they store data, maintain order, and their performance characteristics.

---

### 🔸 1. **HashSet**

* **Underlying structure**: Hash table
* **Ordering**: ❌ No ordering — elements are stored in **unpredictable** order
* **Performance**: ✅ **Fast (O(1))** for add, remove, contains (on average)
* **Null elements**: ✅ Allows **one null element**
* **Requirements**: Elements must implement `hashCode()` and `equals()`

```java
Set<String> hashSet = new HashSet<>();
hashSet.add("Banana");
hashSet.add("Apple");
hashSet.add("Cherry");
System.out.println(hashSet); // Order is not guaranteed
```

---

### 🔸 2. **TreeSet**

* **Underlying structure**: Red-Black Tree (self-balancing BST)
* **Ordering**: ✅ Elements are stored in **sorted (natural or custom) order**
* **Performance**: ❌ Slower than HashSet — **O(log n)** for add, remove, contains
* **Null elements**: ❌ **Does not allow null** (throws `NullPointerException`)
* **Requirements**: Elements must be **comparable** (`Comparable` or `Comparator`)

```java
Set<String> treeSet = new TreeSet<>();
treeSet.add("Banana");
treeSet.add("Apple");
treeSet.add("Cherry");
System.out.println(treeSet); // [Apple, Banana, Cherry]
```

---

### 🔹 Summary Table:

| Feature       | **HashSet**                             | **TreeSet**                                       |
| ------------- | --------------------------------------- | ------------------------------------------------- |
| Underlying DS | Hash Table                              | Red-Black Tree (BST)                              |
| Order         | No order                                | Sorted order                                      |
| Performance   | Faster (O(1) for ops)                   | Slower (O(log n)) for ops                         |
| Null Support  | ✅ Allows one null                       | ❌ Does not allow null                             |
| Element Type  | Must override `hashCode()` & `equals()` | Must be comparable (`Comparable` or `Comparator`) |
| Use Case      | Fast access, no order needed            | Need sorted data                                  |

---

### 🔹 When to Use Which?

* Use **HashSet** when you just need **uniqueness** and **performance**.
* Use **TreeSet** when you need **sorted** unique elements.

---

## 65. What is the difference between HashMap and Hashtable?

The **difference between `HashMap` and `Hashtable`** in Java primarily lies in **synchronization**, **performance**, and **null support**. Though both store key-value pairs, they are used in different scenarios.

---

### 🔹 1. **HashMap**

* **Introduced in**: Java 1.2
* **Thread Safety**: ❌ Not synchronized (not thread-safe by default)
* **Performance**: ✅ **Faster** (no synchronization overhead)
* **Null Support**:

    * ✅ Allows **one null key**
    * ✅ Allows **multiple null values**
* **Inheritance**: Extends `AbstractMap`
* **Usage**: Best suited for **non-threaded applications** or where external synchronization is used (e.g., with `Collections.synchronizedMap()`)

```java
Map<String, String> hashMap = new HashMap<>();
hashMap.put(null, "value");     // Allowed
hashMap.put("key", null);       // Allowed
```

---

### 🔹 2. **Hashtable**

* **Introduced in**: Java 1.0
* **Thread Safety**: ✅ **Synchronized** (thread-safe)
* **Performance**: ❌ Slower due to synchronization overhead
* **Null Support**:

    * ❌ Does **not allow** null keys or values (throws `NullPointerException`)
* **Inheritance**: Extends `Dictionary` (legacy class)
* **Usage**: Considered **obsolete**, but still used in legacy systems

```java
Map<String, String> hashtable = new Hashtable<>();
hashtable.put("key", "value");
// hashtable.put(null, "value"); // Throws NullPointerException
```

---

### 🔹 Summary Table:

| Feature         | **HashMap**                    | **Hashtable**                             |
| --------------- | ------------------------------ | ----------------------------------------- |
| Thread-safe     | ❌ No                           | ✅ Yes (synchronized)                      |
| Performance     | ✅ Faster                       | ❌ Slower                                  |
| Null key/value  | ✅ 1 null key, many null values | ❌ No null key or value                    |
| Introduced in   | Java 1.2                       | Java 1.0                                  |
| Parent Class    | `AbstractMap`                  | `Dictionary` (legacy)                     |
| Use in new code | ✅ Recommended                  | ❌ Avoid (use `ConcurrentHashMap` instead) |

---

### 🔹 Best Practice:

If you need a **thread-safe map**, prefer using **`ConcurrentHashMap`** over `Hashtable`.

---

## 66. What is the internal working of HashMap?

The **internal working of `HashMap`** in Java is based on a **hashing mechanism** that uses an **array of buckets**, where each bucket can hold a **linked list (or a red-black tree in Java 8+)** of entries to handle collisions.

---

### 🔹 Key Components:

1. **Array**: Main data structure (`Node<K, V>[] table`) to store key-value pairs.
2. **Hash Function**: Computes hash code for the key, then compresses it to a valid array index using `index = hash % array.length`.
3. **Buckets**: Each index in the array refers to a "bucket" that stores a list/tree of nodes in case of hash collisions.
4. **Collision Handling**:

* **Chaining** (Linked List): Multiple entries in one bucket.
* **Treeification**: Converts a bucket to a red-black tree when collisions become too many (threshold = 8 entries).

---

### 🔹 Internal Flow (Put Operation):

```java
map.put("John", 25);
```

1. **Hashing**: Java calls `hashCode()` on `"John"` and applies hashing (using `hash()` method internally).
2. **Index Calculation**: Index = `(n - 1) & hash` (efficient modulo using bitwise AND).
3. **Check Bucket**:

* If empty: place a new `Node`.
* If not empty:

    * Traverse the list or tree.
    * If key exists: replace value.
    * If not: append to list or insert in tree.
4. **Resize (Rehashing)**: If load factor (`size/capacity`) exceeds `0.75`, the array size is **doubled** and all existing entries are **rehashed**.

---

### 🔹 Internal Node Structure (Simplified):

```java
static class Node<K, V> {
    final int hash;
    final K key;
    V value;
    Node<K, V> next;
}
```

---

### 🔹 Java 8 Optimization:

* Uses a **linked list** in each bucket by default.
* If a bucket gets **more than 8 entries**, it **converts** to a **red-black tree** for faster lookups (O(log n)).

---

### 🔹 Get Operation:

1. Compute hash and index.
2. Go to bucket at that index.
3. Traverse list/tree and compare keys using `equals()`.
4. Return the associated value if found.

---

### 🔹 Visual Summary:

```
hash("John") → index 5
table[5] → Node(key="John", value=25, next) → ...
```

---

### 🔹 Time Complexity:

| Operation | Average Case | Worst Case (many collisions) |
| --------- | ------------ | ---------------------------- |
| put/get   | O(1)         | O(n) (or O(log n) with tree) |

---

## 67. What is the load factor in HashMap?

The **load factor** in a `HashMap` is a measure that determines **when to resize** (rehash) the internal array to maintain performance.

---

### 🔹 Definition:

> **Load Factor** = **(Number of entries)** / **(Capacity of the HashMap)**

It tells Java **how full the HashMap can get** before it needs to **increase the capacity** (i.e., resize the internal array).

---

### 🔹 Default Value:

* The **default load factor** in Java is **`0.75`**
* It provides a good balance between **time and space complexity**

---

### 🔹 How It Works:

If the **initial capacity** is `16` and **load factor** is `0.75`:

* Resize will happen when the number of entries exceeds `16 × 0.75 = 12`

So, when you add the 13th entry, the HashMap will **resize** — doubling the capacity to 32, and **rehash** all existing keys.

---

### 🔹 Why is it Important?

* A **lower load factor** (e.g., `0.5`) → **less chance of collisions**, but uses more memory
* A **higher load factor** (e.g., `0.9`) → **better space usage**, but increases collision chances and slows down performance

---

### 🔹 Setting Load Factor (Custom):

```java
Map<String, String> map = new HashMap<>(16, 0.5f);
```

---

### 🔹 Summary:

| Load Factor        | Pros                             | Cons                        |
| ------------------ | -------------------------------- | --------------------------- |
| Lower (e.g., 0.5)  | Faster access (less collisions)  | Uses more memory            |
| Higher (e.g., 0.9) | Uses less memory                 | Slower (more collisions)    |
| Default (0.75)     | Good balance of speed and memory | Suitable for most use cases |

---

## 68. What is the difference between fail-fast and fail-safe iterators?

The **difference between fail-fast and fail-safe iterators** in Java lies in how they behave when a collection is **modified during iteration**.

---

### 🔹 Fail-Fast Iterator

* **Definition**: Immediately throws a `ConcurrentModificationException` if the collection is **structurally modified** (e.g., add/remove) during iteration.
* **Examples**: Iterators from `ArrayList`, `HashSet`, `HashMap` (keySet/entrySet)
* **Mechanism**: Uses an internal **modCount** to track modifications.
* **Not Thread-Safe**.

```java
List<String> list = new ArrayList<>();
list.add("A");
list.add("B");

for (String s : list) {
    list.add("C"); // ⚠️ Throws ConcurrentModificationException
}
```

---

### 🔹 Fail-Safe Iterator

* **Definition**: Doesn’t throw exceptions if the collection is modified during iteration.
* **How**: Iterates over a **copy** of the collection, not the original.
* **Examples**: `ConcurrentHashMap`, `CopyOnWriteArrayList`
* **Thread-Safe** but with performance trade-offs.

```java
CopyOnWriteArrayList<String> list = new CopyOnWriteArrayList<>();
list.add("A");
list.add("B");

for (String s : list) {
    list.add("C"); // ✅ No exception
}
```

---

### 🔹 Comparison Table:

| Feature                  | **Fail-Fast Iterator**                   | **Fail-Safe Iterator**                      |
| ------------------------ | ---------------------------------------- | ------------------------------------------- |
| Behavior on modification | Throws `ConcurrentModificationException` | No exception thrown                         |
| Iterates over            | Original collection                      | A **copy** of the collection                |
| Thread-safety            | ❌ Not thread-safe                        | ✅ Thread-safe                               |
| Performance              | ✅ Fast                                   | ❌ Slower (copies collection)                |
| Examples                 | `ArrayList`, `HashSet`, `HashMap`        | `ConcurrentHashMap`, `CopyOnWriteArrayList` |

---

### 🔹 When to Use:

* Use **fail-fast** in single-threaded or read-only loops.
* Use **fail-safe** for **concurrent modifications** or multi-threaded access.

---

## 69. What is the difference between Iterator and ListIterator?

The **difference between `Iterator` and `ListIterator`** in Java lies in their capabilities and the types of collections they support.

---

### 🔹 1. `Iterator`

* **Available in**: All **Collection** types (e.g., `Set`, `List`, `Queue`)
* **Traversal**: ✅ **Forward-only**
* **Modification**: ✅ Can **remove** elements during iteration (`remove()` method)
* **Limitations**:

    * ❌ No **backward traversal**
    * ❌ No access to **index**
    * ❌ No ability to **add or replace** elements

```java
Iterator<String> iterator = list.iterator();
while (iterator.hasNext()) {
    String s = iterator.next();
    if (s.equals("B")) {
        iterator.remove(); // ✅ Allowed
    }
}
```

---

### 🔹 2. `ListIterator`

* **Available in**: Only for **List** types (e.g., `ArrayList`, `LinkedList`)
* **Traversal**: ✅ **Forward and backward**
* **Modification**:

    * ✅ `remove()`
    * ✅ `add(E element)`
    * ✅ `set(E element)` (to replace current element)
* **Provides Index Info**: ✅ `nextIndex()` and `previousIndex()`

```java
ListIterator<String> listIterator = list.listIterator();
while (listIterator.hasNext()) {
    String s = listIterator.next();
    if (s.equals("B")) {
        listIterator.set("Beta"); // ✅ Replace "B" with "Beta"
    }
}
```

---

### 🔹 Summary Table:

| Feature                | `Iterator`         | `ListIterator`                           |
| ---------------------- | ------------------ | ---------------------------------------- |
| Applicable to          | All collections    | Only Lists                               |
| Direction of traversal | Forward only       | Forward and backward                     |
| Can remove elements    | ✅ Yes (`remove()`) | ✅ Yes (`remove()`)                       |
| Can add elements       | ❌ No               | ✅ Yes (`add(E)`)                         |
| Can replace elements   | ❌ No               | ✅ Yes (`set(E)`)                         |
| Can get index          | ❌ No               | ✅ Yes (`nextIndex()`, `previousIndex()`) |
| Introduced in          | Java 1.2           | Java 1.2                                 |

---

### 🔹 Use Cases:

* Use **`Iterator`** when you only need to **read and remove** while going forward.
* Use **`ListIterator`** when you need to **modify**, **reverse**, or **navigate by index**.

---

## 70. How does ConcurrentHashMap work?

The **`ConcurrentHashMap`** in Java is a thread-safe, high-performance map designed for concurrent access. It allows multiple threads to read and write to the map simultaneously without causing data corruption or requiring the entire map to be locked. This is achieved through **segmentation** and **fine-grained locking**.

Here's how it works:

---

### 🔹 **Key Features of ConcurrentHashMap:**

1. **Thread Safety**:

* It ensures **thread safety** for read and write operations without locking the entire map. This allows for high concurrency.

2. **Segments**:

* The map is divided into **segments**. Each segment acts like a separate **bucket** for entries and is independently locked.
* This division allows multiple threads to work on different segments concurrently, significantly reducing the contention compared to traditional synchronized maps (like `Hashtable`).

3. **Locking Mechanism**:

* **Fine-Grained Locking**: `ConcurrentHashMap` uses **segment-level locks** (introduced in Java 7) rather than a single lock for the whole map. This means that different threads can operate on different segments simultaneously.
* For example, if one thread is modifying the entries in one segment, other threads can still work on entries in other segments without blocking.

4. **No Global Lock**:

* Unlike `Hashtable` or synchronized `HashMap`, which lock the entire map during any operation, `ConcurrentHashMap` only locks a small portion of the data structure at a time (usually a segment or bucket), so concurrent operations on different parts of the map are allowed.

5. **Size and Read Operations**:

* **Reads**: Read operations are generally lock-free. Multiple threads can read the map simultaneously without locking.
* **Writes**: Writes are synchronized at the segment level. If a thread wants to update a value, it locks only the affected segment.

6. **Atomic Operations**:

* `ConcurrentHashMap` provides several **atomic operations** like `putIfAbsent()`, `remove()`, and `replace()` to ensure thread-safe operations on single elements without needing additional synchronization.

7. **Iterator**:

* Iterators in `ConcurrentHashMap` are **fail-safe**. They do not throw `ConcurrentModificationException` if the map is modified during iteration. However, the values may not be consistent if the map is modified while iterating.

---

### 🔹 **Structure of ConcurrentHashMap:**

1. **Buckets**:

* It internally uses an **array of segments**. Each segment contains an array of **buckets** (or bins).
* The bucket is responsible for storing the key-value pairs and resolving collisions using **chaining** or **bucket-level locking**.

2. **Locking at the Segment Level**:

* The map is divided into **segments**, and each segment is a **separate hash table**. Each segment can be independently locked.
* In earlier versions of Java (pre-Java 8), each segment had its own lock.
* In **Java 8**, it uses **bin-level locking** inside each segment.

3. **Concurrency**:

* The default number of **segments** is typically 16 (can be adjusted at map creation), allowing for a good level of concurrency.

---

### 🔹 **How ConcurrentHashMap Works in Practice:**

1. **Put Operation**:

* When a thread performs a `put` operation, it computes the hash of the key and determines the segment and bucket.
* If the segment is not locked by another thread, it will acquire a lock on that segment (using fine-grained locks) and perform the insertion.
* If the key already exists, it will perform an atomic update based on the operation (e.g., `putIfAbsent()`).

2. **Get Operation**:

* The `get` operation is **lock-free** because it doesn't need to modify the map. Threads can concurrently read values without any blocking.

3. **Resize Operation (Rehashing)**:

* When the map becomes too large or the segment exceeds a certain threshold, the map will **resize**. This resizing is **done incrementally** on each segment to avoid locking the entire map.
* In Java 8, it uses a more sophisticated strategy to avoid global locks during rehashing by locking individual bins within a segment.

4. **Atomic Operations**:

* Methods like `putIfAbsent()`, `remove()`, and `replace()` allow operations on individual elements to be performed atomically, ensuring consistency in concurrent scenarios.

---

### 🔹 **Code Example of ConcurrentHashMap**:

```java
import java.util.concurrent.ConcurrentHashMap;

public class Example {
    public static void main(String[] args) {
        // Create a ConcurrentHashMap with default concurrency level (16 segments)
        ConcurrentHashMap<String, Integer> map = new ConcurrentHashMap<>();
        
        // Adding elements
        map.put("A", 1);
        map.put("B", 2);
        map.put("C", 3);
        
        // Atomic replace operation
        map.replace("A", 1, 100); // Only replaces if current value is 1
        
        // Thread-safe get operation
        System.out.println(map.get("A")); // Output: 100

        // Atomic put if absent
        map.putIfAbsent("D", 4); // Only inserts if key "D" doesn't exist
        
        // Concurrent read and update without blocking
        map.forEach((key, value) -> {
            System.out.println(key + ": " + value);
        });
    }
}
```

---

### 🔹 **Advantages of ConcurrentHashMap**:

* **High Concurrency**: Multiple threads can access different segments of the map concurrently.
* **Efficient Read Operations**: Reads are generally lock-free, making them fast even in multi-threaded environments.
* **Atomicity**: Supports atomic operations for common use cases.
* **Resilience**: It's highly scalable with low contention for common operations.

### 🔹 **Disadvantages**:

* **Not a Full Replacement for Synchronized Map**: If you need to perform multiple operations atomically across the entire map, `ConcurrentHashMap` may not be sufficient.
* **Complexity**: The internal implementation can be complex, especially when it comes to handling concurrency at the segment level.

---

### 🔹 **When to Use ConcurrentHashMap**:

* **When you have high concurrency requirements** and you want to allow multiple threads to **read and write** to the map simultaneously without locking the entire structure.
* Ideal for scenarios where **many threads** need to access the map and you want to avoid the bottleneck of synchronized blocks.

---

## 71. What is the difference between HashMap and LinkedHashMap?

The **difference between `HashMap` and `LinkedHashMap`** in Java lies in the way they store the entries and their order of iteration.

---

### 🔹 **1. Order of Elements**

* **`HashMap`**:

    * Does **not maintain any order** for its entries. The order of key-value pairs in a `HashMap` is dependent on the hash of the keys and may change over time as the map is modified.
    * The iteration order is not predictable and could appear random.
* **`LinkedHashMap`**:

    * **Maintains insertion order** by default. This means that the elements will be iterated in the same order in which they were added to the map.
    * Can also be configured to maintain **access order**. When configured for access order, the order of entries will be based on the last access time (i.e., most recently accessed entries are moved to the end).

---

### 🔹 **2. Performance**

* **`HashMap`**:

    * **Faster** for operations like `put()`, `get()`, and `remove()` because it only uses the hash table for storage and does not need to maintain any order of elements.
* **`LinkedHashMap`**:

    * Slightly **slower** than `HashMap` due to the overhead of maintaining a doubly-linked list (to maintain insertion or access order). However, the performance difference is generally minor unless you have a large number of operations.

---

### 🔹 **3. Internal Data Structure**

* **`HashMap`**:

    * Uses a **hash table** for storage.
    * Stores key-value pairs without any specific order.
* **`LinkedHashMap`**:

    * Uses a **hash table** for storage (like `HashMap`), but also maintains a **doubly linked list** to track the order of insertion or access.

---

### 🔹 **4. Use Cases**

* **`HashMap`**:

    * Use when **order of elements** is **not important**, and you want **fast lookups** and minimal overhead.

* **`LinkedHashMap`**:

    * Use when you need to maintain the **insertion order** of entries (e.g., displaying results in the order they were added).
    * Also useful when you need **access order** (e.g., for implementing **LRU (Least Recently Used) cache**).

---

### 🔹 **5. Constructor Differences**

* **`HashMap`**:

    * No special constructor for controlling order.
* **`LinkedHashMap`**:

    * Provides an additional constructor to control whether the map maintains **insertion order** or **access order**:

  ```java
  LinkedHashMap<K, V> map = new LinkedHashMap<>(initialCapacity, loadFactor, accessOrder);
  ```

  Where `accessOrder` is a boolean flag:

    * `true`: Maintain **access order** (useful for LRU cache).
    * `false`: Maintain **insertion order** (default).

---

### 🔹 **6. Example Code**

#### `HashMap` Example:

```java
import java.util.HashMap;
import java.util.Map;

public class HashMapExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("One", 1);
        map.put("Two", 2);
        map.put("Three", 3);
        
        for (Map.Entry<String, Integer> entry : map.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
    }
}
```

**Output** (The order of iteration is unpredictable):

```
One: 1
Three: 3
Two: 2
```

#### `LinkedHashMap` Example:

```java
import java.util.LinkedHashMap;
import java.util.Map;

public class LinkedHashMapExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new LinkedHashMap<>();
        map.put("One", 1);
        map.put("Two", 2);
        map.put("Three", 3);
        
        for (Map.Entry<String, Integer> entry : map.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
    }
}
```

**Output** (The order of iteration is predictable and maintains insertion order):

```
One: 1
Two: 2
Three: 3
```

---

### 🔹 **Summary Table**:

| Feature                     | **`HashMap`**               | **`LinkedHashMap`**                                 |
| --------------------------- | --------------------------- | --------------------------------------------------- |
| **Order of Elements**       | No specific order           | Maintains insertion order (default)                 |
| **Internal Data Structure** | Hash table                  | Hash table + doubly linked list                     |
| **Performance**             | Faster                      | Slightly slower (due to linked list)                |
| **Use Case**                | When order is not important | When order is important (insertion or access order) |
| **Access Order**            | ❌ Not supported             | ✅ Can be maintained (via constructor)               |
| **Constructor**             | Standard constructor        | Additional constructor for access order             |

---

### 🔹 **When to Use Each**:

* **Use `HashMap`**: When you just need a fast, unordered map and don’t care about the order of the elements.
* **Use `LinkedHashMap`**: When you need to preserve the **order** of insertion or access, for example, when implementing caching mechanisms or displaying results in the order they were inserted.

Would you like an example where `LinkedHashMap` is used with access order (like an LRU cache)?
The **difference between `HashMap` and `LinkedHashMap`** in Java lies in the way they store the entries and their order of iteration.

---

### 🔹 **1. Order of Elements**

* **`HashMap`**:

    * Does **not maintain any order** for its entries. The order of key-value pairs in a `HashMap` is dependent on the hash of the keys and may change over time as the map is modified.
    * The iteration order is not predictable and could appear random.
* **`LinkedHashMap`**:

    * **Maintains insertion order** by default. This means that the elements will be iterated in the same order in which they were added to the map.
    * Can also be configured to maintain **access order**. When configured for access order, the order of entries will be based on the last access time (i.e., most recently accessed entries are moved to the end).

---

### 🔹 **2. Performance**

* **`HashMap`**:

    * **Faster** for operations like `put()`, `get()`, and `remove()` because it only uses the hash table for storage and does not need to maintain any order of elements.
* **`LinkedHashMap`**:

    * Slightly **slower** than `HashMap` due to the overhead of maintaining a doubly-linked list (to maintain insertion or access order). However, the performance difference is generally minor unless you have a large number of operations.

---

### 🔹 **3. Internal Data Structure**

* **`HashMap`**:

    * Uses a **hash table** for storage.
    * Stores key-value pairs without any specific order.
* **`LinkedHashMap`**:

    * Uses a **hash table** for storage (like `HashMap`), but also maintains a **doubly linked list** to track the order of insertion or access.

---

### 🔹 **4. Use Cases**

* **`HashMap`**:

    * Use when **order of elements** is **not important**, and you want **fast lookups** and minimal overhead.

* **`LinkedHashMap`**:

    * Use when you need to maintain the **insertion order** of entries (e.g., displaying results in the order they were added).
    * Also useful when you need **access order** (e.g., for implementing **LRU (Least Recently Used) cache**).

---

### 🔹 **5. Constructor Differences**

* **`HashMap`**:

    * No special constructor for controlling order.
* **`LinkedHashMap`**:

    * Provides an additional constructor to control whether the map maintains **insertion order** or **access order**:

  ```java
  LinkedHashMap<K, V> map = new LinkedHashMap<>(initialCapacity, loadFactor, accessOrder);
  ```

  Where `accessOrder` is a boolean flag:

    * `true`: Maintain **access order** (useful for LRU cache).
    * `false`: Maintain **insertion order** (default).

---

### 🔹 **6. Example Code**

#### `HashMap` Example:

```java
import java.util.HashMap;
import java.util.Map;

public class HashMapExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("One", 1);
        map.put("Two", 2);
        map.put("Three", 3);
        
        for (Map.Entry<String, Integer> entry : map.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
    }
}
```

**Output** (The order of iteration is unpredictable):

```
One: 1
Three: 3
Two: 2
```

#### `LinkedHashMap` Example:

```java
import java.util.LinkedHashMap;
import java.util.Map;

public class LinkedHashMapExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new LinkedHashMap<>();
        map.put("One", 1);
        map.put("Two", 2);
        map.put("Three", 3);
        
        for (Map.Entry<String, Integer> entry : map.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
    }
}
```

**Output** (The order of iteration is predictable and maintains insertion order):

```
One: 1
Two: 2
Three: 3
```

---

### 🔹 **Summary Table**:

| Feature                     | **`HashMap`**               | **`LinkedHashMap`**                                 |
| --------------------------- | --------------------------- | --------------------------------------------------- |
| **Order of Elements**       | No specific order           | Maintains insertion order (default)                 |
| **Internal Data Structure** | Hash table                  | Hash table + doubly linked list                     |
| **Performance**             | Faster                      | Slightly slower (due to linked list)                |
| **Use Case**                | When order is not important | When order is important (insertion or access order) |
| **Access Order**            | ❌ Not supported             | ✅ Can be maintained (via constructor)               |
| **Constructor**             | Standard constructor        | Additional constructor for access order             |

---

### 🔹 **When to Use Each**:

* **Use `HashMap`**: When you just need a fast, unordered map and don’t care about the order of the elements.
* **Use `LinkedHashMap`**: When you need to preserve the **order** of insertion or access, for example, when implementing caching mechanisms or displaying results in the order they were inserted.

---

## 72. How does TreeMap work internally?

The **`TreeMap`** in Java is a **SortedMap** implementation that is backed by a **Red-Black Tree**, which is a self-balancing binary search tree. It provides a **natural ordering** of keys or a custom order specified by a **Comparator**. The elements in a `TreeMap` are always sorted according to the key, and it maintains **key-value pairs** in ascending order of the keys.

### 🔹 **Key Characteristics of TreeMap:**

1. **Sorted Order**:

* The keys in a `TreeMap` are automatically sorted either in **natural order** (if the keys implement `Comparable`) or by a **custom comparator** provided during map creation.

2. **Red-Black Tree**:

* The internal data structure used by `TreeMap` is a **Red-Black Tree**, which ensures the map remains balanced, thus maintaining **log(n)** time complexity for most operations like `put()`, `get()`, `remove()`, etc.

3. **Performance**:

* **`get()`, `put()`, and `remove()` operations** all run in **O(log n)** time, where `n` is the number of elements in the map, due to the properties of the Red-Black Tree.
* This is different from `HashMap`, where these operations are **O(1)** on average but can degrade to **O(n)** in the worst case when there are hash collisions.

4. **No Null Keys**:

* `TreeMap` does not allow `null` keys, since `null` cannot be compared. However, it allows `null` values, as values are not compared during the sorting process.

5. **NavigableMap Interface**:

* `TreeMap` implements the **`NavigableMap`** interface, providing additional features such as `firstEntry()`, `lastEntry()`, `lowerEntry()`, `higherEntry()`, and methods to retrieve ranges of keys (e.g., `subMap()`, `headMap()`, `tailMap()`).

---

### 🔹 **Internal Structure of TreeMap (Red-Black Tree)**:

A **Red-Black Tree** is a type of self-balancing binary search tree with the following properties:

1. **Each node** is either **red** or **black**.
2. **The root node** is always **black**.
3. **Red nodes** cannot have **red children** (no two red nodes can be adjacent).
4. Every **path** from a node to its descendant `null` nodes has the same number of **black nodes** (this ensures balance).
5. The **leaf nodes** (i.e., `null` nodes) are considered black.

Due to these properties, a Red-Black Tree ensures that the height of the tree is always balanced, leading to **O(log n)** time complexity for operations like search, insert, and delete.

---

### 🔹 **How TreeMap Operations Work**:

1. **Insert Operation (`put()`)**:

* When a new key-value pair is added, the key is inserted into the tree according to its value. The insertion follows the binary search tree rules.
* If the tree becomes unbalanced after insertion, **re-balancing** occurs through **rotations** (left and right rotations), which are part of the Red-Black Tree balancing rules.
* **Time Complexity**: O(log n).

2. **Search Operation (`get()`)**:

* To retrieve a value associated with a key, the tree is traversed from the root following the binary search path. The traversal is based on the key's natural order or the custom comparator.
* **Time Complexity**: O(log n).

3. **Delete Operation (`remove()`)**:

* When a key-value pair is removed, the Red-Black Tree is updated by removing the node and re-balancing the tree to maintain its properties.
* **Time Complexity**: O(log n).

4. **Iterating over TreeMap**:

* Since the keys are sorted, iteration over the `TreeMap` will always happen in **ascending order** of the keys.
* You can also iterate over the map using **`entrySet()`**, **`keySet()`**, or **`values()`** methods, all of which return the entries in the natural sorted order of keys.

---

### 🔹 **Example Code**:

```java
import java.util.TreeMap;

public class TreeMapExample {
    public static void main(String[] args) {
        // Create a TreeMap with default natural order
        TreeMap<String, Integer> map = new TreeMap<>();
        
        // Adding entries to TreeMap
        map.put("Apple", 5);
        map.put("Banana", 3);
        map.put("Orange", 7);
        map.put("Grapes", 2);
        
        // Iterating over the TreeMap
        for (String key : map.keySet()) {
            System.out.println(key + ": " + map.get(key));
        }

        // Get a specific value
        System.out.println("Value for 'Banana': " + map.get("Banana"));
        
        // Remove a specific entry
        map.remove("Apple");

        // Iterating again after removal
        System.out.println("\nAfter removing 'Apple':");
        for (String key : map.keySet()) {
            System.out.println(key + ": " + map.get(key));
        }
    }
}
```

**Output**:

```
Apple: 5
Banana: 3
Grapes: 2
Orange: 7

Value for 'Banana': 3

After removing 'Apple':
Banana: 3
Grapes: 2
Orange: 7
```

**Explanation**:

* The keys are automatically sorted in **ascending** order when iterated: `"Apple"`, `"Banana"`, `"Grapes"`, `"Orange"`.
* After removing `"Apple"`, the iteration order is updated accordingly.

---

### 🔹 **NavigableMap Methods in TreeMap**:

As `TreeMap` implements the **`NavigableMap`** interface, it provides additional methods like:

1. **`firstEntry()`**: Returns the first (lowest) entry.
2. **`lastEntry()`**: Returns the last (highest) entry.
3. **`lowerEntry(K key)`**: Returns the entry before the specified key.
4. **`higherEntry(K key)`**: Returns the entry after the specified key.
5. **`subMap(K fromKey, boolean fromInclusive, K toKey, boolean toInclusive)`**: Returns a view of a portion of the map.

```java
TreeMap<Integer, String> map = new TreeMap<>();
map.put(1, "One");
map.put(3, "Three");
map.put(5, "Five");
map.put(7, "Seven");

System.out.println("First Entry: " + map.firstEntry());  // (1, One)
System.out.println("Last Entry: " + map.lastEntry());    // (7, Seven)
System.out.println("Lower Entry than 5: " + map.lowerEntry(5)); // (3, Three)
```

**Output**:

```
First Entry: 1=One
Last Entry: 7=Seven
Lower Entry than 5: 3=Three
```

---

### 🔹 **Advantages of TreeMap**:

1. **Sorted Map**: Ensures elements are always sorted by the keys.
2. **Navigable Operations**: Provides various range and navigation operations (e.g., `subMap()`, `higherEntry()`).
3. **Balanced Tree**: Red-Black Tree ensures that the map is always balanced, offering **log(n)** time complexity for key operations.

### 🔹 **Disadvantages of TreeMap**:

1. **Slower than HashMap**: Operations like `put()`, `get()`, and `remove()` are slower (O(log n)) compared to `HashMap` (O(1) on average).
2. **No Null Keys**: Unlike `HashMap`, `TreeMap` does not allow `null` keys, which may limit its usage in some scenarios.

---

### 🔹 **When to Use TreeMap**:

* When you need the keys in a **sorted order**.
* When you need to perform operations that rely on **range queries** or **navigation** through keys (e.g., finding the smallest/largest key).
* For **custom sorting** via a `Comparator`.

---

## 73. What are priority queues in Java?

### **Priority Queues in Java**

In Java, a **Priority Queue** is a data structure that is similar to a regular queue, but with a slight difference: **elements are dequeued based on their priority** rather than the order in which they were enqueued.

* The **highest priority element** is dequeued first.
* The **lowest priority element** is dequeued last.
* **Priority queues** do not guarantee the order in which elements of the same priority are processed, except when using a **natural ordering** or a **custom comparator**.

Java provides the `PriorityQueue` class, which is part of the **`java.util`** package. It is implemented using a **heap** data structure, which allows for efficient retrieval of the highest (or lowest) priority element.

---

### 🔹 **Key Features of PriorityQueue**:

1. **Heap-based**: Internally, a priority queue is implemented as a **binary heap** (either min-heap or max-heap).

* By default, the `PriorityQueue` is a **min-heap**, meaning the element with the **smallest value** (or highest priority) is dequeued first.

2. **Ordering**: The elements are ordered based on their **natural ordering** (if they implement `Comparable`) or a **custom comparator** (if one is provided at the time of queue creation).

3. **Unbounded**: A `PriorityQueue` can grow dynamically to accommodate new elements. It does not have a fixed size.

4. **Null elements**: **Cannot** be inserted into a `PriorityQueue`. It does not allow `null` elements.

5. **Time Complexity**:

* **Insertion (`offer()`)**: O(log n) — Each insertion requires adjusting the heap.
* **Removal (`poll()` or `remove()`)**: O(log n) — The root element (highest priority) is removed, and the heap is adjusted.
* **Peek (`peek()`)**: O(1) — The highest priority element is at the root of the heap.

6. **Thread Safety**: It is **not thread-safe**. If you need thread safety, you can use alternatives like `PriorityBlockingQueue` or wrap it using `Collections.synchronizedQueue()`.

---

### 🔹 **Creating a PriorityQueue**:

You can create a `PriorityQueue` using its default constructor or by passing a comparator.

#### **1. Default Constructor (Min-Heap)**:

```java
import java.util.PriorityQueue;

public class PriorityQueueExample {
    public static void main(String[] args) {
        // Create a priority queue (min-heap by default)
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        
        // Add elements to the queue
        pq.add(10);
        pq.add(20);
        pq.add(5);
        pq.add(15);
        
        // Print and remove elements
        while (!pq.isEmpty()) {
            System.out.println(pq.poll());  // Elements are dequeued in order of priority (smallest first)
        }
    }
}
```

**Output**:

```
5
10
15
20
```

#### **2. Using a Custom Comparator (Max-Heap)**:

You can customize the order by passing a comparator to the `PriorityQueue` constructor.

```java
import java.util.PriorityQueue;
import java.util.Comparator;

public class MaxHeapExample {
    public static void main(String[] args) {
        // Create a priority queue with a custom comparator (max-heap)
        PriorityQueue<Integer> pq = new PriorityQueue<>(Comparator.reverseOrder());
        
        // Add elements to the queue
        pq.add(10);
        pq.add(20);
        pq.add(5);
        pq.add(15);
        
        // Print and remove elements
        while (!pq.isEmpty()) {
            System.out.println(pq.poll());  // Elements are dequeued in order of priority (largest first)
        }
    }
}
```

**Output**:

```
20
15
10
5
```

#### **3. Using Objects in PriorityQueue**:

If you want to store objects in the priority queue, the objects must either:

* Implement the `Comparable` interface, or
* A comparator should be provided at the time of queue creation.

For example, let's use a custom class `Student` that implements `Comparable`:

```java
import java.util.PriorityQueue;

class Student implements Comparable<Student> {
    String name;
    int priority;

    Student(String name, int priority) {
        this.name = name;
        this.priority = priority;
    }

    @Override
    public int compareTo(Student other) {
        // Lower priority number means higher priority in the queue
        return Integer.compare(this.priority, other.priority);
    }

    @Override
    public String toString() {
        return name + " (Priority: " + priority + ")";
    }
}

public class StudentPriorityQueue {
    public static void main(String[] args) {
        // Create a priority queue for Students
        PriorityQueue<Student> pq = new PriorityQueue<>();
        
        pq.add(new Student("John", 2));
        pq.add(new Student("Alice", 1));
        pq.add(new Student("Bob", 3));

        // Print and remove elements
        while (!pq.isEmpty()) {
            System.out.println(pq.poll());
        }
    }
}
```

**Output**:

```
Alice (Priority: 1)
John (Priority: 2)
Bob (Priority: 3)
```

---

### 🔹 **Common Operations in PriorityQueue**:

1. **`offer(E e)`**: Inserts the specified element into the priority queue.

   ```java
   pq.offer(30);  // Adds 30 to the queue
   ```

2. **`poll()`**: Retrieves and removes the highest-priority element (the root).

   ```java
   pq.poll();  // Removes the element with the highest priority (min or max)
   ```

3. **`peek()`**: Retrieves, but does not remove, the highest-priority element.

   ```java
   pq.peek();  // Returns the element with the highest priority without removing it
   ```

4. **`isEmpty()`**: Checks if the queue is empty.

   ```java
   pq.isEmpty();  // Returns true if the queue is empty, false otherwise
   ```

5. **`size()`**: Returns the number of elements in the queue.

   ```java
   pq.size();  // Returns the size of the priority queue
   ```

---

### 🔹 **Applications of PriorityQueue**:

* **Task Scheduling**: Useful in scenarios where you need to process tasks based on their priority, such as job scheduling.
* **Dijkstra’s Algorithm**: Used in graph algorithms like **Dijkstra’s Shortest Path** where the priority queue helps in selecting the next vertex to visit based on the shortest distance.
* **Huffman Encoding**: In data compression algorithms like **Huffman coding**, a priority queue is used to build a tree based on the frequency of characters.

---

### 🔹 **Advantages**:

1. **Efficient Priority Handling**: Provides efficient access to the element with the highest or lowest priority in O(log n) time.
2. **Automatic Sorting**: Automatically sorts the elements based on their priority, removing the need for manual sorting.
3. **Flexible**: Can use a custom comparator for different priority orderings (min-heap or max-heap).

---

### 🔹 **Disadvantages**:

1. **Not Thread-Safe**: The `PriorityQueue` is not synchronized, so for multi-threaded applications, you need to use a **synchronized wrapper** or an alternative like **`PriorityBlockingQueue`**.
2. **No Capacity Limitation**: The `PriorityQueue` is unbounded. If you need a fixed-size priority queue, you may have to manually manage it.

---

### 🔹 **Conclusion**:

The `PriorityQueue` is a useful data structure for managing elements where the order of processing depends on their priority, and it is widely used in algorithmic applications such as scheduling, shortest path algorithms, and event-driven simulations.

---

## 74. What is the use of Collections.unmodifiableList()?

### **`Collections.unmodifiableList()` in Java**

The `Collections.unmodifiableList()` method is used to create an **immutable** version of a `List` in Java. This means that once the list is created, its contents cannot be changed (i.e., no elements can be added, removed, or modified).

### **Key Points**:

* **Immutable List**: The list returned by `Collections.unmodifiableList()` is **unmodifiable**, meaning any attempt to modify the list (such as adding or removing elements) will throw an `UnsupportedOperationException`.
* **Wrapper**: The `unmodifiableList()` method does not create a new list with copied elements; rather, it wraps the original list in an unmodifiable view. The original list is still mutable, but the unmodifiable view prevents modification through the returned reference.

### **Syntax**:

```java
Collections.unmodifiableList(List<? extends T> list)
```

* **Parameters**: It takes a list as an argument, which will be the base for creating the unmodifiable list.
* **Returns**: An unmodifiable view of the provided list.

### **Example Usage**:

```java
import java.util.*;

public class UnmodifiableListExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Banana");
        list.add("Orange");

        // Create an unmodifiable view of the list
        List<String> unmodifiableList = Collections.unmodifiableList(list);

        // Try to modify the list
        try {
            unmodifiableList.add("Grapes"); // This will throw UnsupportedOperationException
        } catch (UnsupportedOperationException e) {
            System.out.println("Cannot modify the list: " + e);
        }

        // Print the list
        System.out.println("Unmodifiable List: " + unmodifiableList);

        // Modifying the original list will still affect the unmodifiable view
        list.add("Mango");
        System.out.println("Original List: " + list);
        System.out.println("Unmodifiable List after modifying original: " + unmodifiableList);
    }
}
```

**Output**:

```
Cannot modify the list: java.lang.UnsupportedOperationException
Unmodifiable List: [Apple, Banana, Orange]
Original List: [Apple, Banana, Orange, Mango]
Unmodifiable List after modifying original: [Apple, Banana, Orange, Mango]
```

### **Explanation**:

* The `unmodifiableList()` method creates a read-only view of the original list.
* Any modification attempt on the returned list (`unmodifiableList`) results in an `UnsupportedOperationException`.
* However, if you modify the **original list** (`list`), the change will reflect in the unmodifiable list because it's just a view of the original.

### **Common Use Cases**:

1. **Protecting Collections from Modification**: When you want to return a collection that cannot be modified, you can use `unmodifiableList()`. This is commonly used in libraries or APIs to ensure that callers cannot alter internal data structures.

2. **Safe Sharing of Collections**: When you need to share a list across different parts of your program but don’t want the list to be modified, `unmodifiableList()` provides a safe way to pass the list around without allowing modifications.

3. **Immutable Data Structures**: It's used in scenarios where you need to create read-only views of data structures to ensure that no unintended changes happen to the collection.

### **Limitations**:

* **Doesn't make the original list immutable**: The original list can still be modified directly. The unmodifiable view only prevents changes through the view, not the original list.
* **No deep immutability**: The `unmodifiableList()` method does not ensure that the elements inside the list are themselves immutable. For example, if the list contains mutable objects, those objects can still be modified.

### **Conclusion**:

`Collections.unmodifiableList()` is a useful method when you need to ensure that a `List` cannot be modified after it's created. It is commonly used to expose immutable lists while preserving the original list's ability to change, if necessary.

---

## 75. How can you sort a list of custom objects?

In Java, sorting a list of custom objects can be done in a few ways, primarily by implementing the `Comparable` interface or by using a `Comparator`. Here’s a breakdown of both approaches:

### **1. Sorting Using `Comparable` Interface**

The `Comparable` interface allows you to define a natural ordering for your custom objects. This is useful when you want to sort your objects based on a single field or property (such as age, name, etc.).

#### **Steps**:

1. Implement the `Comparable<T>` interface in your class.
2. Override the `compareTo(T other)` method to define how two objects should be compared.
3. Use `Collections.sort()` or `List.sort()` to sort the list.

#### **Example**:

Let's say you have a `Student` class with `name` and `age` fields. You can sort a list of students by `age` using `Comparable`.

```java
import java.util.*;

class Student implements Comparable<Student> {
    String name;
    int age;

    // Constructor
    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Implement the compareTo method to compare by age
    @Override
    public int compareTo(Student other) {
        return Integer.compare(this.age, other.age);  // Sorting by age in ascending order
    }

    @Override
    public String toString() {
        return name + " (" + age + ")";
    }
}

public class Main {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("John", 20));
        students.add(new Student("Alice", 22));
        students.add(new Student("Bob", 18));

        // Sort using Comparable (natural order by age)
        Collections.sort(students);

        // Print sorted list
        System.out.println(students);  // [Bob (18), John (20), Alice (22)]
    }
}
```

### **Explanation**:

* The `Student` class implements `Comparable<Student>`, and we override the `compareTo()` method to sort students by their `age` field.
* The `Collections.sort()` method sorts the list according to the `compareTo()` implementation.

---

### **2. Sorting Using `Comparator` Interface**

A `Comparator` allows you to define different sorting criteria, especially when you don't want to modify the natural ordering of the class. You can define multiple `Comparator` implementations for different fields (e.g., by name, by age, etc.).

#### **Steps**:

1. Implement the `Comparator<T>` interface.
2. Override the `compare(T o1, T o2)` method to define the comparison logic.
3. Use `Collections.sort()` or `List.sort()` and pass the comparator as an argument.

#### **Example**:

Using the same `Student` class, let's say you want to sort the students by `name` and `age` using a `Comparator`.

```java
import java.util.*;

class Student {
    String name;
    int age;

    // Constructor
    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return name + " (" + age + ")";
    }
}

public class Main {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("John", 20));
        students.add(new Student("Alice", 22));
        students.add(new Student("Bob", 18));

        // Comparator to sort by age
        Comparator<Student> byAge = (s1, s2) -> Integer.compare(s1.age, s2.age);
        
        // Sort using Comparator (by age)
        Collections.sort(students, byAge);
        System.out.println("Sorted by age: " + students);

        // Comparator to sort by name
        Comparator<Student> byName = (s1, s2) -> s1.name.compareTo(s2.name);

        // Sort using Comparator (by name)
        Collections.sort(students, byName);
        System.out.println("Sorted by name: " + students);
    }
}
```

**Output**:

```
Sorted by age: [Bob (18), John (20), Alice (22)]
Sorted by name: [Alice (22), Bob (18), John (20)]
```

### **Explanation**:

* The `Comparator<Student>` is used to create custom sorting logic.
* We created two comparators: one for sorting by `age` and one for sorting by `name`.
* We then use `Collections.sort()` and pass the appropriate comparator to sort the list.

---

### **3. Using `Comparator` with Lambda Expressions**:

In Java 8 and above, you can use lambda expressions to define the `Comparator` in a more concise way.

#### **Example**:

```java
import java.util.*;

class Student {
    String name;
    int age;

    // Constructor
    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return name + " (" + age + ")";
    }
}

public class Main {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("John", 20));
        students.add(new Student("Alice", 22));
        students.add(new Student("Bob", 18));

        // Sort by age using lambda expression
        students.sort((s1, s2) -> Integer.compare(s1.age, s2.age));
        System.out.println("Sorted by age: " + students);

        // Sort by name using lambda expression
        students.sort((s1, s2) -> s1.name.compareTo(s2.name));
        System.out.println("Sorted by name: " + students);
    }
}
```

**Output**:

```
Sorted by age: [Bob (18), John (20), Alice (22)]
Sorted by name: [Alice (22), Bob (18), John (20)]
```

### **4. Using `List.sort()` with Comparator**:

If you're using Java 8 or above, you can use the `List.sort()` method directly instead of `Collections.sort()`.

#### **Example**:

```java
students.sort(Comparator.comparingInt(Student::getAge));  // Sorting by age
```

---

### **Conclusion**:

* **`Comparable`** is used when you want to define a **natural ordering** for the objects (one criteria).
* **`Comparator`** is used when you want to define multiple sorting criteria or don't want to modify the natural ordering.
* Both approaches allow you to sort a list of custom objects in Java, either by a single field or multiple fields using custom logic.

Would you like to explore more examples or need help with anything else related to sorting?

---

### 🔹 76–85: **Multithreading & Concurrency**

## 76. What is the difference between process and thread?

The terms **process** and **thread** refer to two fundamental concepts in operating systems and concurrent programming. Though they are related, they differ in several key aspects, such as their execution models, resource allocation, and the way they manage tasks. Here's a detailed comparison:

### **1. Process**

A **process** is an independent program in execution, which has its own address space and memory. Each process is a container for one or more threads and is isolated from other processes, meaning one process cannot directly access the memory or resources of another process.

#### **Key Characteristics of a Process**:

* **Memory Isolation**: Each process has its own memory space (virtual memory), which means the memory of one process is not accessible to others.
* **Independent Execution**: Processes are independent and do not share data or state unless specifically communicated (via inter-process communication mechanisms like pipes, shared memory, or message passing).
* **Overhead**: Since processes are independent, they require more overhead in terms of memory and context switching because they need to load and manage separate address spaces.
* **Creation**: Creating a new process is generally more resource-intensive and time-consuming than creating a thread because it involves allocating a separate memory space.
* **Inter-Process Communication (IPC)**: Communication between processes is more complex and typically slower than between threads.

#### **Example**:

* Running a web browser and a text editor are two separate processes. Each runs independently with its own memory space.

### **2. Thread**

A **thread** is the smallest unit of execution within a process. Multiple threads can exist within a single process, sharing the same memory space and resources. Threads within the same process can communicate with each other directly, which makes multithreading more efficient for certain tasks.

#### **Key Characteristics of a Thread**:

* **Shared Memory**: Threads within the same process share the same address space (i.e., they have access to the same memory and resources), making communication between threads easier and faster.
* **Lightweight**: Threads are considered lightweight because they do not require their own memory space. Creating a thread is faster and requires fewer resources compared to creating a new process.
* **Execution within Process**: All threads of a process run in the same context and share the same process resources like open files, variables, and memory.
* **Context Switching**: Switching between threads within the same process is less expensive in terms of CPU time and memory compared to context switching between processes.
* **Concurrency**: Multiple threads in the same process can execute concurrently, making it possible to perform multiple tasks simultaneously (e.g., UI update and background data processing).

#### **Example**:

* In a web browser, one thread may be responsible for rendering the page, while another thread handles user input (like clicks and keypresses), and another handles network requests.

---

### **Key Differences Between Process and Thread**

| Feature               | Process                                                                                      | Thread                                                                                  |
| --------------------- | -------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| **Definition**        | A process is an independent program in execution with its own memory space.                  | A thread is a single execution unit within a process that shares the same memory space. |
| **Memory Allocation** | Processes have separate memory spaces (isolation).                                           | Threads within a process share the same memory space.                                   |
| **Execution**         | Processes execute independently.                                                             | Threads execute concurrently within the same process.                                   |
| **Overhead**          | Creating a process involves significant overhead (due to memory space allocation).           | Threads are lightweight and involve less overhead compared to processes.                |
| **Communication**     | Communication between processes requires Inter-Process Communication (IPC), which is slower. | Communication between threads is faster since they share the same memory space.         |
| **Creation**          | Creating a process is resource-intensive and slow.                                           | Creating a thread is relatively fast and requires fewer resources.                      |
| **Context Switching** | Context switching between processes is expensive.                                            | Context switching between threads is relatively cheap.                                  |
| **Isolation**         | Processes are isolated from each other, preventing direct access to each other's memory.     | Threads are not isolated; they can directly access each other's memory and resources.   |
| **Failure Impact**    | If a process crashes, it does not affect other processes.                                    | If a thread crashes, it can potentially bring down the entire process.                  |

---

### **When to Use Processes vs. Threads**

* **Use Processes**:

    * When tasks are completely independent and require isolation.
    * When tasks need to run independently, with their own memory and resources.
    * When tasks involve separate applications that should not interfere with each other (e.g., running a database and a web server).
* **Use Threads**:

    * When tasks need to perform concurrently within the same application and share the same resources (e.g., background tasks, UI handling).
    * When you want better performance with lower overhead for tasks that need to access shared data (e.g., multithreading in games or simulations).

---

### **Conclusion**:

* **Processes** are isolated, independent units of execution with their own memory, while **threads** are lightweight execution units within a process that share memory.
* **Processes** are used when isolation and independence are required, while **threads** are used when concurrency and resource sharing within a single application are necessary.

---

## 77. How do you create a thread in Java?

In Java, you can create and run a thread in two main ways:

1. **By implementing the `Runnable` interface**
2. **By extending the `Thread` class**

### **1. Creating a Thread by Implementing the `Runnable` Interface**

The `Runnable` interface represents a task that can be executed by a thread. You implement the `run()` method in this interface, and the thread is created using the `Thread` class, which takes the `Runnable` object as a parameter.

#### **Steps:**

* Implement the `Runnable` interface.
* Define the `run()` method that contains the code to be executed by the thread.
* Create a `Thread` object, passing the `Runnable` object to its constructor.
* Start the thread by calling the `start()` method on the `Thread` object.

#### **Example**:

```java
class MyRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("Thread is running using Runnable!");
    }
}

public class Main {
    public static void main(String[] args) {
        // Create an instance of MyRunnable
        MyRunnable myRunnable = new MyRunnable();

        // Create a thread and pass the Runnable instance to it
        Thread thread = new Thread(myRunnable);

        // Start the thread
        thread.start();
    }
}
```

**Explanation**:

* The `MyRunnable` class implements the `Runnable` interface and overrides the `run()` method with the logic you want to execute in the thread.
* A `Thread` is created with `myRunnable` as its target, and the `start()` method is called to begin the execution of the thread.

---

### **2. Creating a Thread by Extending the `Thread` Class**

In this approach, you extend the `Thread` class and override its `run()` method to define the task that the thread will execute. After defining the `run()` method, you create an instance of the `Thread` subclass and call the `start()` method to run the thread.

#### **Steps:**

* Extend the `Thread` class.
* Override the `run()` method to define the code to be executed by the thread.
* Create an instance of the subclass and call the `start()` method.

#### **Example**:

```java
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Thread is running using Thread class!");
    }
}

public class Main {
    public static void main(String[] args) {
        // Create an instance of MyThread
        MyThread myThread = new MyThread();

        // Start the thread
        myThread.start();
    }
}
```

**Explanation**:

* The `MyThread` class extends `Thread` and overrides the `run()` method to provide the thread's task.
* By calling `myThread.start()`, the `run()` method is invoked in a new thread of execution.

---

### **Key Points**:

* **Using `Runnable`**: This is the preferred way to create a thread when you need to implement the task independently from the `Thread` class. It allows you to implement the task in a separate class and also enables the possibility of using the same `Runnable` object with multiple threads.

* **Using `Thread`**: Extending the `Thread` class can be simpler when you don't need to implement the task separately. However, Java doesn't allow multiple inheritance, so if your class needs to extend another class, you cannot extend `Thread`. In such cases, it's better to implement `Runnable` instead.

---

### **Starting a Thread**:

To start a thread, you call the `start()` method on the `Thread` object. This internally calls the `run()` method in a new thread of execution.

```java
Thread thread = new Thread(new MyRunnable());
thread.start();
```

* **Important**: You should **never** call the `run()` method directly. Calling `run()` directly will execute it in the current thread (just like a normal method call), instead of starting a new thread.

---

### **Thread Lifecycle**:

A thread in Java goes through several states during its lifecycle:

1. **New**: When a thread is created but has not yet started.
2. **Runnable**: When the thread is ready to run and waiting for the CPU to schedule it.
3. **Blocked/Waiting**: When the thread is waiting for a resource or is in a blocking operation (e.g., I/O operations).
4. **Terminated**: When the thread has completed its execution or has been manually stopped.

---

### **Conclusion**:

* Use **`Runnable`** when you want to decouple the task from the thread itself and possibly share the task across multiple threads.
* Use **`Thread`** when you don't need to separate the task into a different class or if it's a simpler design.

---

## 78. What is the difference between `Runnable` and `Thread`?

The main difference between **`Runnable`** and **`Thread`** in Java lies in their design and usage when working with threads. Both are used to represent tasks that can be executed by a thread, but they serve different purposes. Here's a detailed breakdown:

### **1. `Runnable` Interface**

* **Purpose**: The `Runnable` interface is designed to represent a task that can be executed by a thread. It defines a single method, `run()`, that contains the code to be executed when the thread runs.

* **Definition**:

    * **`Runnable`** is an interface, meaning it does not directly provide functionality for thread management. Instead, it allows a task to be executed by any thread.

* **Usage**:

    * When you implement the `Runnable` interface, you can pass the `Runnable` object to a `Thread` object, which will execute the task in a separate thread.

* **Advantages**:

    * **Separation of Concerns**: By using `Runnable`, the task is separated from the thread. This allows the task to be reused by multiple threads, making the code more modular and flexible.
    * **Multiple Inheritance**: Since `Runnable` is an interface, a class can implement `Runnable` while also extending another class, providing more flexibility.
    * **Resource Sharing**: Multiple threads can share the same `Runnable` object and execute the same task.

* **Example**:

  ```java
  class MyRunnable implements Runnable {
      @Override
      public void run() {
          System.out.println("Runnable thread is running");
      }
  }

  public class Main {
      public static void main(String[] args) {
          MyRunnable myRunnable = new MyRunnable();
          Thread thread = new Thread(myRunnable);
          thread.start();  // Starting the thread
      }
  }
  ```

### **2. `Thread` Class**

* **Purpose**: The `Thread` class represents a thread of execution in a Java program. It provides both the task (via the `run()` method) and the ability to start, manage, and control the thread's lifecycle.

* **Definition**:

    * **`Thread`** is a concrete class that directly extends the `Object` class and provides functionality for thread management. You can either subclass `Thread` and override its `run()` method or instantiate a `Thread` object and pass a `Runnable` object to it.

* **Usage**:

    * When you extend the `Thread` class, you can define the task within the `run()` method and directly create and start the thread by calling the `start()` method.

* **Advantages**:

    * **Simplicity**: It's easier to use when you only need one thread and don't need to share the task between multiple threads.
    * **Direct Thread Control**: Since `Thread` is a concrete class, you can call `start()` directly on an instance of the `Thread` class.

* **Disadvantages**:

    * **Single Inheritance Limitation**: Since `Thread` is a class and Java does not support multiple inheritance, if your class already extends another class, you cannot extend `Thread`.
    * **Less Flexibility**: Unlike `Runnable`, you cannot easily reuse the task in multiple threads unless you explicitly pass it into each `Thread`.

* **Example**:

  ```java
  class MyThread extends Thread {
      @Override
      public void run() {
          System.out.println("Thread class is running");
      }
  }

  public class Main {
      public static void main(String[] args) {
          MyThread myThread = new MyThread();
          myThread.start();  // Starting the thread
      }
  }
  ```

---

### **Key Differences Between `Runnable` and `Thread`**

| Feature               | `Runnable`                                                                                                  | `Thread`                                                                                                |
| --------------------- | ----------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| **Type**              | Interface                                                                                                   | Class                                                                                                   |
| **Purpose**           | Represents a task that can be executed by a thread                                                          | Represents a thread of execution itself                                                                 |
| **Inheritance**       | Can be implemented by any class (no restrictions)                                                           | Must extend the `Thread` class, which limits inheritance to one class                                   |
| **Usage**             | Used to define a task that can be executed by a thread (passed to `Thread` constructor)                     | Can directly be used to create and manage a thread (either by extending `Thread` or passing `Runnable`) |
| **Multiple Threads**  | Multiple threads can share a single `Runnable` instance                                                     | Each `Thread` instance represents a separate thread                                                     |
| **Thread Management** | Cannot directly manage threads (must use `Thread` to manage execution)                                      | Directly manages thread execution (via `start()`, `sleep()`, etc.)                                      |
| **Flexibility**       | More flexible, as it can be used with any class (supports multiple inheritance)                             | Less flexible, as it limits inheritance (since Java supports only single inheritance)                   |
| **Use Case**          | Preferred when you need to define a task separately from the thread or share a task across multiple threads | Useful when thread control is required within the same class, or no task sharing is necessary           |

---

### **When to Use `Runnable` vs. `Thread`**

* **Use `Runnable`**:

    * When you need to define a task that can be executed by multiple threads (for example, if the task is to be reused across multiple threads).
    * When you want more flexibility by allowing the class to extend another class while also implementing `Runnable`.
    * When you want to separate the task from the thread itself, making the code cleaner and more modular.

* **Use `Thread`**:

    * When you don't need to reuse the task in other threads.
    * When you want to directly control thread creation and execution within the same class.
    * If you don't need to implement other interfaces and simply need a straightforward thread implementation.

---

### **Summary**:

* **`Runnable`** is an interface that defines a task to be executed by a thread.
* **`Thread`** is a concrete class that represents a thread and allows for direct thread management.
* **`Runnable`** provides flexibility and is more suitable for scenarios where multiple threads need to execute the same task.
* **`Thread`** is simpler but less flexible because it limits inheritance and directly handles thread management.

---

## 79. What is synchronization? How do you use `synchronized`?

### **Synchronization in Java**

**Synchronization** in Java is a mechanism used to control access to shared resources (like variables, data structures, files, etc.) in a concurrent environment (i.e., when multiple threads are running). It ensures that only one thread at a time can access a shared resource, preventing **race conditions** and ensuring thread safety.

### **Why Synchronization?**

In a multithreaded environment, multiple threads may try to modify or read shared data at the same time. This can lead to **data inconsistency** or **incorrect results**. For example, two threads updating the same variable simultaneously can cause unpredictable results. Synchronization helps ensure that only one thread can access the critical section (the block of code that accesses shared resources) at a time, making sure the data remains consistent.

---

### **How Synchronization Works**

Java provides the `synchronized` keyword to control access to critical sections. When a method or block of code is marked as synchronized, only one thread can execute that section at any given time. Other threads that attempt to enter the synchronized block or method will be blocked until the first thread finishes.

### **Ways to Use `synchronized`**

1. **Synchronized Methods**
2. **Synchronized Blocks**

---

### **1. Synchronized Methods**

A method can be declared as synchronized by adding the `synchronized` keyword to its declaration. This ensures that only one thread can execute the method at a time for each instance of the object.

#### **Instance-Level Synchronization**

When you declare a method as synchronized, it locks on the object instance (i.e., `this` object). Only one thread at a time can execute any synchronized instance method on the same object.

```java
class Counter {
    private int count = 0;

    // Synchronized method to ensure thread-safe access
    public synchronized void increment() {
        count++;
    }

    public synchronized int getCount() {
        return count;
    }
}

public class Main {
    public static void main(String[] args) {
        Counter counter = new Counter();

        // Thread 1
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        });

        // Thread 2
        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        });

        t1.start();
        t2.start();

        // Wait for both threads to finish
        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Final Count: " + counter.getCount());
    }
}
```

**Explanation**:

* The `increment()` and `getCount()` methods are synchronized, which means only one thread can execute these methods on the same object at a time.
* Both threads (t1 and t2) attempt to increment the counter simultaneously, but synchronization ensures the threads update the `count` variable in a thread-safe manner.

#### **Class-Level Synchronization (Static Methods)**

If the method is **static**, it locks on the class object (`ClassName.class`) rather than the instance of the object. This ensures that only one thread can execute any synchronized static method of the class at a time, regardless of the instance.

```java
class Counter {
    private static int count = 0;

    // Synchronized static method
    public synchronized static void increment() {
        count++;
    }

    public synchronized static int getCount() {
        return count;
    }
}

public class Main {
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                Counter.increment();
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                Counter.increment();
            }
        });

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Final Count: " + Counter.getCount());
    }
}
```

**Explanation**:

* The `increment()` and `getCount()` methods are synchronized on the class level (because they are static), meaning only one thread can execute any synchronized static method at any time.

---

### **2. Synchronized Blocks**

In some cases, synchronizing an entire method might be inefficient. If only part of a method needs synchronization, you can use a **synchronized block** to lock only that section of the code.

#### **Example**:

```java
class Counter {
    private int count = 0;

    public void increment() {
        synchronized (this) {  // Synchronizing only this block
            count++;
        }
    }

    public int getCount() {
        return count;
    }
}

public class Main {
    public static void main(String[] args) {
        Counter counter = new Counter();

        // Thread 1
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        });

        // Thread 2
        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        });

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Final Count: " + counter.getCount());
    }
}
```

**Explanation**:

* In this example, the `synchronized` block ensures that only one thread can execute the `count++` operation at a time. This is more efficient than synchronizing the entire method, as other parts of the method can be executed concurrently.

#### **Locking on Objects Other Than `this`**

You can synchronize on any object (not just `this`) by passing the object reference to the `synchronized` block. For example, you can use a lock object to control synchronization.

```java
class Counter {
    private int count = 0;
    private final Object lock = new Object();  // Lock object

    public void increment() {
        synchronized (lock) {  // Synchronize on the lock object
            count++;
        }
    }

    public int getCount() {
        return count;
    }
}
```

---

### **When to Use `synchronized`**

* **When you have shared resources** (e.g., variables, data structures) that multiple threads need to access.
* **When you need to prevent race conditions** where multiple threads are updating the same resource at the same time.
* **When you want to ensure thread safety** in operations like reading, updating, or deleting shared resources.

---

### **Performance Considerations**

* **Blocking**: When a thread is executing a synchronized block, other threads that need the same lock will be blocked until the first thread finishes.
* **Deadlock**: Be careful of deadlocks, which can occur if two threads wait for each other to release locks, leading to an infinite wait.

---

### **Conclusion**

* **Synchronization** in Java ensures that only one thread at a time can access a shared resource, preventing **race conditions**.
* You can synchronize **methods** or **blocks** of code using the `synchronized` keyword.
* Use synchronization when you have shared data that can be modified by multiple threads to ensure thread safety.

---

## 80. What is a deadlock and how can it be avoided?

### **Deadlock in Java**

A **deadlock** is a situation in multithreading programming where two or more threads are blocked forever, waiting for each other to release resources that they hold. This occurs when each thread holds a lock on one resource and is waiting to acquire a lock on another resource held by another thread, forming a cycle of dependencies. Since none of the threads can proceed, they all end up in a **deadlock state**.

### **Conditions for Deadlock**

For a deadlock to occur, the following four conditions must be true simultaneously:

1. **Mutual Exclusion**: At least one resource is in a non-shareable mode. This means only one thread can use a resource at a time.
2. **Hold and Wait**: A thread holding at least one resource is waiting to acquire additional resources held by other threads.
3. **No Preemption**: Resources cannot be preempted (taken back) from a thread holding them. They can only be released voluntarily by the thread.
4. **Circular Wait**: A set of threads are waiting for each other in a circular chain, where each thread holds at least one resource that the next thread in the chain is waiting for.

### **Example of Deadlock**

Here’s a simple example of a deadlock in Java:

```java
class A {
    synchronized void methodA(B b) {
        System.out.println("Thread 1: Holding lock on A...");
        try { Thread.sleep(100); } catch (InterruptedException e) {}
        System.out.println("Thread 1: Waiting for lock on B...");
        b.last();
    }

    synchronized void last() {
        System.out.println("Inside A's last method");
    }
}

class B {
    synchronized void methodB(A a) {
        System.out.println("Thread 2: Holding lock on B...");
        try { Thread.sleep(100); } catch (InterruptedException e) {}
        System.out.println("Thread 2: Waiting for lock on A...");
        a.last();
    }

    synchronized void last() {
        System.out.println("Inside B's last method");
    }
}

public class DeadlockExample {
    public static void main(String[] args) {
        final A a = new A();
        final B b = new B();

        Thread t1 = new Thread(() -> a.methodA(b));
        Thread t2 = new Thread(() -> b.methodB(a));

        t1.start();
        t2.start();
    }
}
```

**Explanation**:

* In this example, Thread 1 holds a lock on object `A` and tries to acquire a lock on object `B`, while Thread 2 holds a lock on object `B` and tries to acquire a lock on object `A`. Neither thread can proceed, leading to a **deadlock**.

### **How to Avoid Deadlock**

Deadlock can be avoided by careful design and by following specific techniques to ensure that the necessary conditions for a deadlock are not met. Here are some strategies:

---

### **1. Lock Ordering**

One common way to avoid deadlock is to ensure that all threads acquire locks in the same order. This eliminates circular dependencies, which is a necessary condition for a deadlock.

**Example**:
If both threads must acquire locks on `A` and `B`, always acquire the lock on `A` first, then on `B`.

```java
class A {
    synchronized void methodA(B b) {
        synchronized (b) { // Locking B after A
            System.out.println("Thread 1: Holding lock on A...");
            try { Thread.sleep(100); } catch (InterruptedException e) {}
            System.out.println("Thread 1: Waiting for lock on B...");
            b.last();
        }
    }

    synchronized void last() {
        System.out.println("Inside A's last method");
    }
}

class B {
    synchronized void methodB(A a) {
        synchronized (a) { // Locking A after B
            System.out.println("Thread 2: Holding lock on B...");
            try { Thread.sleep(100); } catch (InterruptedException e) {}
            System.out.println("Thread 2: Waiting for lock on A...");
            a.last();
        }
    }

    synchronized void last() {
        System.out.println("Inside B's last method");
    }
}
```

By acquiring locks in the same order (A -> B), we can avoid deadlock.

---

### **2. Timeout Mechanism (Deadlock Detection)**

In some cases, it is possible to use a **timeout mechanism** when acquiring a lock. If a thread is unable to acquire the lock within a certain period, it can back off and try again, thus avoiding getting stuck indefinitely.

**Example**:

```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

class A {
    Lock lockA = new ReentrantLock();
    Lock lockB = new ReentrantLock();

    void methodA(B b) {
        try {
            if (lockA.tryLock() && b.lockB.tryLock()) {
                // Do some work here
            }
        } finally {
            lockA.unlock();
            b.lockB.unlock();
        }
    }
}

class B {
    Lock lockA = new ReentrantLock();
    Lock lockB = new ReentrantLock();

    void methodB(A a) {
        try {
            if (lockB.tryLock() && a.lockA.tryLock()) {
                // Do some work here
            }
        } finally {
            lockB.unlock();
            a.lockA.unlock();
        }
    }
}
```

By using `tryLock()` with a timeout, the thread can decide not to wait indefinitely if it cannot acquire the lock.

---

### **3. Using a Single Lock**

If possible, use a **single lock** for all related resources instead of locking on multiple objects. This way, you don't have to worry about the order in which locks are acquired, since there's only one lock.

```java
class Counter {
    private int count = 0;
    private final Object lock = new Object();

    public void increment() {
        synchronized (lock) {
            count++;
        }
    }

    public int getCount() {
        synchronized (lock) {
            return count;
        }
    }
}
```

By using a single lock for both operations, you ensure that no other thread can access the critical section while one thread is executing it.

---

### **4. Use Higher-Level Concurrency Utilities**

Java's **`java.util.concurrent`** package offers higher-level utilities (like `ExecutorService`, `CountDownLatch`, `Semaphore`, `CyclicBarrier`, etc.) to handle concurrency more effectively. These utilities are designed to minimize the chance of deadlocks by abstracting the low-level lock management.

---

### **5. Deadlock Detection Tools**

For debugging and detecting deadlocks, you can use Java’s built-in tools such as the `jstack` utility, which prints a thread dump that shows the state of all threads, including threads that are in a deadlock state. Many IDEs like IntelliJ IDEA and Eclipse also provide tools for detecting deadlocks during development.

---

### **Summary**

* **Deadlock** occurs when two or more threads are blocked forever, each waiting for the other to release a resource they need.
* **Deadlock conditions** are: mutual exclusion, hold and wait, no preemption, and circular wait.
* **Avoiding deadlock** can be done by using techniques such as:

    * Lock ordering
    * Using timeout mechanisms (e.g., `tryLock()` with a timeout)
    * Using a single lock for all shared resources
    * Leveraging higher-level concurrency utilities like `ExecutorService`
* Deadlock detection tools such as `jstack` can help identify and debug deadlocks during runtime.

By carefully managing thread synchronization and lock acquisition, you can significantly reduce the risk of deadlocks in your Java applications.

---

## 81. What are thread states in Java?

In Java, a **thread** can exist in one of several states during its lifecycle. These states are part of the **thread state model** in the Java **Thread** class, which is defined by the `Thread.State` enum. Each state represents a different phase of a thread’s life cycle, and threads move between these states as they progress from being created to finishing execution.

### **Thread States in Java**

Here are the **7 main thread states** in Java:

1. **New** (also called **Born** or **Newborn**)

* The thread is in the "New" state when it is created but not yet started. It has been instantiated, but the `start()` method has not been called.
* **Example**: `Thread t = new Thread();` creates a thread, but it is in the **New** state until `t.start()` is called.

2. **Runnable**

* A thread is in the **Runnable** state when it is ready to run and is waiting for the CPU to be allocated to it by the thread scheduler. The thread may not be running right now, but it is in the queue, waiting for its turn to execute.
* **Note**: A thread is in the **Runnable** state whether it is actually running or just ready to run.
* **Example**: After calling `start()` on a thread, it moves into the **Runnable** state.

3. **Blocked**

* A thread is in the **Blocked** state when it is blocked and waiting to acquire a lock (monitor) that another thread is holding. In other words, if a thread is trying to access a synchronized block of code that is already being accessed by another thread, it will be moved to the **Blocked** state.
* Once the thread gets the required lock, it moves to the **Runnable** state.
* **Example**: Two threads trying to access a synchronized method, one thread will be blocked until the other finishes.

4. **Waiting**

* A thread is in the **Waiting** state when it is waiting indefinitely for another thread to perform a particular action (like notifying the thread that it can proceed). A thread in the **Waiting** state will not consume CPU time.
* Threads can enter this state via the following methods:

    * `Object.wait()`
    * `Thread.join()`
    * `LockSupport.park()`
* A thread in this state can only be awakened by another thread through methods like `notify()`, `notifyAll()`, or `interrupt()`.
* **Example**: A thread that is waiting for another thread to finish using `join()` or calling `wait()` in synchronized blocks.

5. **Timed Waiting**

* A thread is in the **Timed Waiting** state when it is waiting for a specific amount of time. After the specified time expires, the thread will return to the **Runnable** state.
* The following methods put a thread into the **Timed Waiting** state:

    * `Thread.sleep(long milliseconds)`
    * `Thread.join(long milliseconds)`
    * `Object.wait(long milliseconds)`
    * `LockSupport.parkNanos(long nanos)`
    * `LockSupport.parkUntil(long deadline)`
* **Example**: If a thread calls `Thread.sleep(1000)`, it will be in the **Timed Waiting** state for 1 second before resuming.

6. **Terminated** (also called **Dead**)

* A thread is in the **Terminated** state when it has completed its execution or when it has been stopped by an exception. A thread moves into this state after it has successfully finished or encountered an exception or has been manually stopped.
* Once a thread is in the **Terminated** state, it cannot be restarted.
* **Example**: Once the `run()` method completes execution or throws an uncaught exception, the thread transitions to the **Terminated** state.

7. **Blocked and Waiting (or Suspended)**

* This is a combination of **Blocked** and **Waiting** states, but it is rarely explicitly used in Java as a separate state. Threads waiting for a lock or condition go through various stages during synchronization or when using a `synchronized` block/method.

---

### **Thread Lifecycle (Flow)**

* **New** → The thread is created, but the `start()` method has not been called.
* **Runnable** → The `start()` method is called, and the thread is ready to run or is currently running.
* **Blocked** → The thread is waiting for a resource (lock).
* **Waiting** → The thread is waiting for another thread to notify it.
* **Timed Waiting** → The thread is waiting for a specific period (e.g., `sleep` or `join` with timeout).
* **Terminated** → The thread has completed execution or has been terminated.

---

### **Thread State Transitions**

1. **New → Runnable**: When the thread's `start()` method is called.
2. **Runnable → Blocked**: When the thread tries to acquire a lock (monitor) and the lock is not available.
3. **Runnable → Waiting**: When the thread calls `wait()`, `join()`, or `LockSupport.park()`.
4. **Runnable → Timed Waiting**: When the thread calls `sleep()`, `join()` with a timeout, or `wait()` with a timeout.
5. **Blocked → Runnable**: When the thread successfully acquires the lock.
6. **Waiting → Runnable**: When the thread is notified by another thread (via `notify()` or `notifyAll()`), or the timeout expires.
7. **Terminated**: Once the thread has completed execution or has been stopped (either normally or with an exception).

---

### **Example of Thread States:**

```java
class ExampleThread extends Thread {
    public void run() {
        System.out.println("Thread is running...");
        try {
            Thread.sleep(1000);  // Timed Waiting state
            System.out.println("Thread is awake...");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

public class ThreadStateExample {
    public static void main(String[] args) throws InterruptedException {
        ExampleThread t1 = new ExampleThread();
        
        System.out.println("Thread state after creation: " + t1.getState()); // NEW state
        t1.start();  // The thread enters the RUNNABLE state
        System.out.println("Thread state after calling start: " + t1.getState()); // RUNNABLE state

        Thread.sleep(500);  // Allow some time for thread to move into Timed Waiting
        System.out.println("Thread state after sleep: " + t1.getState()); // TIMED_WAITING state
        
        t1.join(); // Wait for thread to finish
        System.out.println("Thread state after completion: " + t1.getState()); // TERMINATED state
    }
}
```

### **Summary of Thread States**

* **New**: Thread is created but not started.
* **Runnable**: Thread is ready to run or is running.
* **Blocked**: Thread is waiting for a lock.
* **Waiting**: Thread is waiting indefinitely for a condition.
* **Timed Waiting**: Thread is waiting for a specific amount of time.
* **Terminated**: Thread has finished execution.

---

## 82. What is the difference between `wait()`, `notify()`, and `notifyAll()`?

In Java, the methods `wait()`, `notify()`, and `notifyAll()` are used for inter-thread communication, specifically for synchronization purposes when multiple threads are involved in accessing shared resources. These methods are defined in the `Object` class, meaning every object in Java can be used as a monitor or lock for synchronization. They are mainly used for communication between threads that are working together, often in producer-consumer problems.

### **1. `wait()` Method**

* **Purpose**: The `wait()` method causes the current thread to release the monitor (lock) and enter the **waiting** state. The thread remains in this state until another thread sends a signal to wake it up (usually via `notify()` or `notifyAll()`).
* **Usage**: This method is typically called within a synchronized block or method, which means the calling thread must hold the lock for the object it's calling `wait()` on.
* **Behavior**:

    * The thread gives up its lock and moves into the **waiting** state.
    * The thread remains in the **waiting** state until it's notified or interrupted.

**Example:**

```java
synchronized (sharedResource) {
    while (conditionIsNotMet) {
        sharedResource.wait();  // Thread waits until notified
    }
}
```

* **Condition**: The `wait()` method should be used inside a synchronized block or method because it requires the current thread to hold the lock of the object on which `wait()` is called.

---

### **2. `notify()` Method**

* **Purpose**: The `notify()` method wakes up one thread that is currently waiting on the object’s monitor (lock). The thread is moved from the **waiting** state to the **runnable** state, but it will only proceed when it re-acquires the lock.
* **Usage**: This method is called within a synchronized block or method, just like `wait()`. It only wakes up **one** thread.
* **Behavior**: When a thread calls `notify()`, only one of the threads in the **waiting** state will be notified (if multiple threads are waiting).

**Example:**

```java
synchronized (sharedResource) {
    sharedResource.notify();  // Wake up one thread that is waiting
}
```

* **Note**: Calling `notify()` doesn't immediately release the lock. The notified thread must wait until the current thread releases the lock.

---

### **3. `notifyAll()` Method**

* **Purpose**: The `notifyAll()` method wakes up all threads that are currently waiting on the object's monitor (lock). All the threads that are in the **waiting** state will be moved to the **runnable** state, but like `notify()`, they will only proceed once they re-acquire the lock.
* **Usage**: This method is also called within a synchronized block or method. It wakes up **all** threads that are waiting on the object’s monitor.
* **Behavior**: Calling `notifyAll()` wakes up all threads waiting on the object's lock, but they will be scheduled to run based on the thread scheduler's policy.

**Example:**

```java
synchronized (sharedResource) {
    sharedResource.notifyAll();  // Wake up all waiting threads
}
```

* **Note**: `notifyAll()` is useful when there are multiple threads waiting on the same resource, and you want all of them to be notified and potentially continue their work.

---

### **Key Differences Between `wait()`, `notify()`, and `notifyAll()`**

| **Method**        | **Behavior**                                                                                                        | **Wakes Up**                                      | **Number of Threads Woken Up**       |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------- | ------------------------------------ |
| **`wait()`**      | The current thread releases the lock and enters the **waiting** state. It waits until notified.                     | The thread that calls `notify()` or `notifyAll()` | 1 (only the thread that is notified) |
| **`notify()`**    | Wakes up one thread that is waiting for the lock. The awakened thread will proceed when it re-acquires the lock.    | A thread that is waiting on the object's monitor  | 1                                    |
| **`notifyAll()`** | Wakes up all threads that are waiting for the lock. All waiting threads will proceed when they re-acquire the lock. | All threads waiting on the object's monitor       | All waiting threads                  |

---

### **When to Use Each Method**

* **`wait()`**: Used when a thread is waiting for a certain condition to be true before it can continue its execution. It’s often used in conjunction with a **while loop** to recheck the condition after being notified.

* **`notify()`**: Used when you want to wake up a single thread that is waiting for a condition. It is used in scenarios where only one thread should continue at a time after a certain condition is met.

* **`notifyAll()`**: Used when multiple threads are waiting on the same condition, and you want all of them to be notified and re-check the condition. This is useful when there are multiple threads and you want all of them to have a chance to proceed, such as in **producer-consumer** scenarios.

---

### **Example: Producer-Consumer Problem**

Let's take a **producer-consumer** example where a producer thread produces data and a consumer thread consumes it. The producer and consumer threads communicate using `wait()`, `notify()`, and `notifyAll()`.

```java
class SharedResource {
    private int value = 0;
    
    // Method for the producer to produce data
    public synchronized void produce() throws InterruptedException {
        while (value != 0) {
            wait();  // Wait if value is already produced
        }
        value++;
        System.out.println("Produced: " + value);
        notify();  // Notify consumer
    }

    // Method for the consumer to consume data
    public synchronized void consume() throws InterruptedException {
        while (value == 0) {
            wait();  // Wait if there's no value to consume
        }
        value--;
        System.out.println("Consumed: " + value);
        notify();  // Notify producer
    }
}

public class ProducerConsumerExample {
    public static void main(String[] args) {
        SharedResource sharedResource = new SharedResource();
        
        // Producer thread
        Thread producer = new Thread(() -> {
            try {
                while (true) {
                    sharedResource.produce();
                    Thread.sleep(1000); // Simulating production time
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });

        // Consumer thread
        Thread consumer = new Thread(() -> {
            try {
                while (true) {
                    sharedResource.consume();
                    Thread.sleep(1500); // Simulating consumption time
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });

        producer.start();
        consumer.start();
    }
}
```

**Explanation**:

* The **producer** calls `wait()` when it has produced a value and is waiting for the consumer to consume it.
* The **consumer** calls `wait()` when there’s no value to consume and is waiting for the producer to produce it.
* When either the producer or consumer finishes an action, it calls `notify()` to wake up the other thread.

### **Summary**

* **`wait()`**: Makes the current thread release the lock and wait until notified.
* **`notify()`**: Wakes up one thread waiting on the lock.
* **`notifyAll()`**: Wakes up all threads waiting on the lock.

---

## 83. What is thread pooling and how is it implemented?

**Thread pooling** is a technique in Java where a pool of worker threads is created in advance, and tasks are submitted to the pool for execution, instead of creating new threads every time a task needs to be executed. This helps improve performance, especially in applications with a large number of tasks to be processed concurrently.

When you use a **thread pool**, the threads are already available in the pool, so the system does not need to create a new thread for each task, which reduces the overhead of thread creation and destruction. This can also lead to better resource management and allows controlling the maximum number of concurrent threads.

### **Benefits of Thread Pooling**

* **Performance**: Reusing threads reduces the overhead of thread creation and destruction, which can be expensive.
* **Resource Management**: Limits the number of concurrent threads, which can help prevent resource exhaustion.
* **Improved Responsiveness**: Threads are pre-created and available, so tasks can be processed quickly.
* **Load Balancing**: Thread pools help in load balancing by managing the distribution of tasks across threads.

### **How Thread Pooling Works**

1. **Pool Creation**: A pool of worker threads is created in advance (fixed or dynamic).
2. **Task Submission**: Tasks (typically runnable tasks) are submitted to the thread pool.
3. **Task Execution**: The thread pool assigns an available worker thread to execute each task.
4. **Completion**: Once the task is completed, the worker thread returns to the pool and waits for the next task.
5. **Termination**: The thread pool can be gracefully shut down once all tasks are completed.

### **Thread Pool Executor in Java**

Java provides a robust and flexible **thread pooling mechanism** through the `ExecutorService` interface, which is part of the `java.util.concurrent` package. The most commonly used implementation of `ExecutorService` is the **ThreadPoolExecutor**.

The `ExecutorService` provides methods like:

* `submit()`: To submit a task for execution.
* `invokeAll()`: To submit a collection of tasks and wait for their completion.
* `shutdown()`: To initiate an orderly shutdown in which previously submitted tasks are executed, but no new tasks will be accepted.
* `shutdownNow()`: Attempts to stop all actively executing tasks and halts the processing of waiting tasks.

### **Basic Example of Thread Pooling in Java**

```java
import java.util.concurrent.*;

class Task implements Runnable {
    private final String taskName;

    public Task(String taskName) {
        this.taskName = taskName;
    }

    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName() + " executing " + taskName);
    }
}

public class ThreadPoolExample {
    public static void main(String[] args) {
        // Creating a thread pool with a fixed number of threads
        ExecutorService executor = Executors.newFixedThreadPool(3);

        // Submitting 5 tasks to the executor
        for (int i = 1; i <= 5; i++) {
            executor.submit(new Task("Task " + i));
        }

        // Shutting down the executor after the tasks are completed
        executor.shutdown();
    }
}
```

### **Explanation of the Code:**

1. **Creating a Thread Pool**: `Executors.newFixedThreadPool(3)` creates a thread pool with 3 worker threads.
2. **Submitting Tasks**: The `submit()` method submits each `Task` to the thread pool for execution.
3. **Shutting Down**: After all tasks are submitted, `executor.shutdown()` is called to shut down the pool gracefully.

### **Types of Thread Pools in Java**

Java provides several types of thread pool implementations through the `Executors` factory class:

1. **Fixed Thread Pool** (`newFixedThreadPool(int nThreads)`):

* A fixed-size pool that reuses a fixed number of threads.
* If all threads are busy, additional tasks will be queued until a thread becomes available.

   ```java
   ExecutorService executor = Executors.newFixedThreadPool(5); // Pool with 5 threads
   ```

2. **Cached Thread Pool** (`newCachedThreadPool()`):

* A pool that creates new threads as needed but will reuse previously constructed threads when they are available.
* It can grow the pool size dynamically as needed but has no upper limit.
* This is ideal for handling many short-lived asynchronous tasks.

   ```java
   ExecutorService executor = Executors.newCachedThreadPool();
   ```

3. **Single Thread Executor** (`newSingleThreadExecutor()`):

* A pool with only one thread to execute all tasks sequentially.
* This is useful when you need to ensure that tasks are executed in a single, ordered sequence.

   ```java
   ExecutorService executor = Executors.newSingleThreadExecutor();
   ```

4. **Scheduled Thread Pool** (`newScheduledThreadPool(int corePoolSize)`):

* A pool that can schedule commands to run after a delay or to execute periodically.
* Useful for tasks that need to be executed periodically, like scheduled jobs.

   ```java
   ScheduledExecutorService executor = Executors.newScheduledThreadPool(5);
   executor.scheduleAtFixedRate(() -> System.out.println("Task executed"), 0, 10, TimeUnit.SECONDS);
   ```

### **Advanced Thread Pool (ThreadPoolExecutor)**

You can also create a **custom thread pool** using the `ThreadPoolExecutor` class, which gives more control over the pool's behavior:

```java
import java.util.concurrent.*;

public class CustomThreadPoolExample {
    public static void main(String[] args) {
        // Creating a custom ThreadPoolExecutor
        int corePoolSize = 2;
        int maximumPoolSize = 4;
        long keepAliveTime = 60;
        
        ThreadPoolExecutor executor = new ThreadPoolExecutor(
            corePoolSize, maximumPoolSize, keepAliveTime, TimeUnit.SECONDS,
            new LinkedBlockingQueue<Runnable>()
        );

        // Submit tasks to the executor
        for (int i = 1; i <= 5; i++) {
            executor.submit(new Task("Task " + i));
        }

        executor.shutdown();
    }
}
```

### **Key Parameters for `ThreadPoolExecutor`**:

* `corePoolSize`: The number of threads to keep in the pool, even if they are idle.
* `maximumPoolSize`: The maximum number of threads allowed in the pool.
* `keepAliveTime`: The maximum time that excess idle threads will wait before being terminated.
* `TimeUnit`: The time unit for `keepAliveTime`.
* `BlockingQueue`: A queue that holds tasks before they are executed. It can be an unbounded or bounded queue, depending on your need.

---

### **Shutdown Behavior**

* **`shutdown()`**: Initiates an orderly shutdown in which previously submitted tasks are executed, but no new tasks will be accepted.
* **`shutdownNow()`**: Attempts to stop all actively executing tasks and halts the processing of waiting tasks.
* **`awaitTermination(long timeout, TimeUnit unit)`**: This method can be used to wait for all tasks to complete or for the specified timeout to elapse.

```java
executor.shutdown();
if (!executor.awaitTermination(60, TimeUnit.SECONDS)) {
    executor.shutdownNow();
}
```

### **Summary**

Thread pooling in Java is an efficient way to manage and reuse threads for concurrent tasks. Using an `ExecutorService` to manage threads simplifies concurrency and improves performance. There are various thread pool types, including fixed thread pools, cached thread pools, single thread executors, and scheduled thread pools, all available through the `Executors` class.

For more advanced configurations, you can use `ThreadPoolExecutor` to customize the pool size, task queue, and other properties. Thread pooling is essential for high-performance multithreaded applications to prevent excessive thread creation and resource contention.

---

## 84. What is the Executor framework?

The **Executor framework** in Java is a high-level replacement for managing threads manually. It provides a set of interfaces and classes that simplify thread management and task execution, abstracting away the complexities of thread creation, scheduling, and management. The main goal of the Executor framework is to decouple task submission from the details of how each task will be executed.

### **Core Interfaces of the Executor Framework**

The Executor framework consists of a few key interfaces and classes that help manage thread pools and task execution:

1. **Executor Interface**:

* The `Executor` interface provides a simple method, `execute()`, to submit tasks for execution. It does not provide any mechanism for managing the result of the task.
* **Method**:

    * `void execute(Runnable command)`: Executes the given task (a `Runnable`) at some point in the future.

Example:

   ```java
   Executor executor = Executors.newFixedThreadPool(10);
   executor.execute(() -> System.out.println("Task executed"));
   ```

2. **ExecutorService Interface**:

* Extends the `Executor` interface and adds methods for managing the lifecycle of the task execution (like shutting down the executor).
* Provides methods for submitting tasks and obtaining results via `Future`.
* **Methods**:

    * `submit()`: Accepts a `Callable` or `Runnable` task and returns a `Future` object to monitor task completion.
    * `invokeAll()`: Accepts a collection of tasks and blocks until all are completed.
    * `invokeAny()`: Accepts a collection of tasks and blocks until at least one completes.
    * `shutdown()`: Initiates an orderly shutdown of the executor.
    * `shutdownNow()`: Attempts to stop all actively executing tasks.

Example:

   ```java
   ExecutorService executorService = Executors.newFixedThreadPool(10);
   executorService.submit(() -> System.out.println("Task executed"));
   executorService.shutdown();
   ```

3. **ScheduledExecutorService Interface**:

* A subinterface of `ExecutorService` that supports scheduling of tasks with fixed-rate or fixed-delay executions. It is ideal for tasks that need to be run periodically or after a delay.
* **Methods**:

    * `schedule()`: Schedules a task for one-time execution after a specified delay.
    * `scheduleAtFixedRate()`: Schedules a task to execute at a fixed-rate (i.e., periodically at a specified interval).
    * `scheduleWithFixedDelay()`: Schedules a task to execute with a fixed delay between executions.

Example:

   ```java
   ScheduledExecutorService scheduledExecutorService = Executors.newScheduledThreadPool(5);
   scheduledExecutorService.scheduleAtFixedRate(() -> System.out.println("Scheduled Task"), 0, 5, TimeUnit.SECONDS);
   ```

4. **ThreadPoolExecutor Class**:

* This class is a concrete implementation of `ExecutorService` and allows more granular control over the thread pool's behavior, such as the number of threads, the task queue, the rejection policy, etc.
* **Methods**:

    * `setCorePoolSize()`, `setMaximumPoolSize()`, `setKeepAliveTime()`, etc., to customize thread pool settings.
    * `submit()`, `shutdown()`, `shutdownNow()` for task management.

Example:

   ```java
   ThreadPoolExecutor threadPoolExecutor = new ThreadPoolExecutor(2, 4, 60, TimeUnit.SECONDS, new LinkedBlockingQueue<>());
   threadPoolExecutor.submit(() -> System.out.println("Task executed"));
   threadPoolExecutor.shutdown();
   ```

### **Executor Framework Benefits**

* **Decoupling Task Submission from Execution**: It separates the logic of submitting tasks from the underlying details of task execution (such as creating threads).
* **Thread Pooling**: Automatically manages a pool of threads, allowing tasks to reuse existing threads rather than creating new ones, reducing resource consumption.
* **Task Scheduling**: With `ScheduledExecutorService`, tasks can be scheduled to run periodically, with fixed-rate or fixed-delay execution strategies.
* **Graceful Shutdown**: Executor services provide methods to shut down the executor gracefully and manage the termination of tasks.
* **Better Resource Management**: Provides better control over the number of threads, which helps in optimizing CPU and memory usage, especially in large, multithreaded applications.
* **Improved Performance**: Reusing threads improves performance by avoiding the cost of creating new threads frequently.

### **Executor Framework in Action**

Here’s an example that demonstrates the usage of different types of Executors:

```java
import java.util.concurrent.*;

public class ExecutorExample {
    public static void main(String[] args) {
        // Fixed thread pool example
        ExecutorService fixedThreadPool = Executors.newFixedThreadPool(3);
        fixedThreadPool.submit(() -> System.out.println("Task 1 executed in fixed thread pool"));

        // Cached thread pool example
        ExecutorService cachedThreadPool = Executors.newCachedThreadPool();
        cachedThreadPool.submit(() -> System.out.println("Task 2 executed in cached thread pool"));

        // Scheduled thread pool example
        ScheduledExecutorService scheduledExecutorService = Executors.newScheduledThreadPool(2);
        scheduledExecutorService.scheduleAtFixedRate(() -> System.out.println("Scheduled task executed"), 0, 2, TimeUnit.SECONDS);

        // Thread pool executor example with customized settings
        ThreadPoolExecutor customExecutor = new ThreadPoolExecutor(2, 4, 60, TimeUnit.SECONDS, new LinkedBlockingQueue<>());
        customExecutor.submit(() -> System.out.println("Task 3 executed in custom thread pool"));

        // Shutdown all executors
        fixedThreadPool.shutdown();
        cachedThreadPool.shutdown();
        scheduledExecutorService.shutdown();
        customExecutor.shutdown();
    }
}
```

### **Types of Executors Provided by the Executors Class**

The `Executors` class provides static factory methods to create various types of executor services:

1. **newFixedThreadPool(int nThreads)**: Creates a fixed-size thread pool with a specified number of threads.
2. **newCachedThreadPool()**: Creates a thread pool that creates new threads as needed but reuses previously created threads when available.
3. **newSingleThreadExecutor()**: Creates a single-threaded executor to run tasks sequentially.
4. **newScheduledThreadPool(int corePoolSize)**: Creates a thread pool for scheduling tasks with a fixed number of threads.

### **ExecutorService Lifecycle**

1. **Submitting Tasks**: You submit tasks (usually `Runnable` or `Callable` objects) to the executor.
2. **Executing Tasks**: The executor will execute the tasks using worker threads from its pool.
3. **Shutting Down**: You shut down the executor with `shutdown()` or `shutdownNow()`. The first will allow already-submitted tasks to finish, while the latter tries to stop them immediately.
4. **Awaiting Termination**: If you want to wait until all tasks are completed before proceeding, you can call `awaitTermination()`.

### **Summary**

The **Executor framework** simplifies concurrency in Java by providing a high-level API for managing thread execution. It decouples task submission from execution and offers various types of executors (fixed thread pool, cached thread pool, scheduled thread pool) to handle different concurrency scenarios. It abstracts the complexities of thread management, ensuring efficient use of system resources and allowing for graceful shutdown of task execution.

---

## 85. What is `volatile` keyword in Java?

The **`volatile`** keyword in Java is used to indicate that a variable's value will be modified by multiple threads. It tells the Java Virtual Machine (JVM) that the value of the variable can be changed asynchronously by different threads and that the value must be read directly from the main memory, rather than from the local thread's cache.

### **Key Characteristics of `volatile`**

1. **Visibility**:

* When a variable is declared as `volatile`, any change to the variable is immediately visible to all other threads. This ensures that when one thread updates the value of a `volatile` variable, other threads will see the updated value instantly.

2. **No Caching**:

* Normally, each thread might cache the values of variables locally to improve performance. With `volatile`, it tells the JVM to always read the value from the main memory and not from the local cache, ensuring that threads see the most up-to-date value.

3. **Atomicity for Reads and Writes**:

* Reads and writes to a `volatile` variable are atomic for variables of types that are not `long` or `double`. This means that any read or write to a `volatile` variable happens as a single, indivisible operation, preventing partial updates.
* However, note that `volatile` does not make compound actions like incrementing (`++`) atomic, as it does not provide locking, just visibility.

4. **Does Not Ensure Atomicity for Compound Operations**:

* For compound actions like incrementing or checking-and-updating a value (`i++` or `i = i + 1`), the `volatile` keyword does **not** ensure atomicity. These operations still need additional synchronization mechanisms like `synchronized` or `java.util.concurrent.atomic.AtomicInteger` to guarantee atomicity.

5. **Ordering (Happens-Before Guarantee)**:

* The `volatile` keyword provides a **happens-before** relationship, meaning that all reads and writes to a `volatile` variable will happen in the order in which they appear in the program (for the same thread). For example, if one thread writes to a `volatile` variable and another thread reads it afterward, the write will happen-before the read.

### **How Does `volatile` Work?**

* **Main Memory and Local Cache**: Without `volatile`, threads can keep copies of variables in their local cache, and changes to these variables may not be visible across threads. The `volatile` keyword tells the JVM to not use the thread-local cache for that variable and always access it directly from the main memory.
* **Visibility Guarantee**: When a thread modifies a `volatile` variable, it ensures that the change is propagated to the main memory immediately. Similarly, when a thread reads a `volatile` variable, it guarantees that it reads the latest value from the main memory, not a cached copy.

### **Example:**

```java
class SharedData {
    private volatile boolean flag = false;

    public void setFlag() {
        flag = true;  // Writing to a volatile variable
    }

    public boolean getFlag() {
        return flag;  // Reading a volatile variable
    }
}

public class VolatileExample {
    public static void main(String[] args) {
        SharedData sharedData = new SharedData();

        // Thread 1: Setting the flag to true
        Thread writer = new Thread(() -> {
            sharedData.setFlag();
            System.out.println("Flag set to true by Writer thread.");
        });

        // Thread 2: Waiting until flag is set to true
        Thread reader = new Thread(() -> {
            while (!sharedData.getFlag()) {
                // Busy-waiting until flag becomes true
            }
            System.out.println("Flag is true, Reader thread detected.");
        });

        writer.start();
        reader.start();
    }
}
```

### **Explanation of the Code:**

* In this example, we have two threads: one writing to the `flag` variable and the other reading it.
* The `flag` variable is declared `volatile`, which ensures that any change made by the writer thread is immediately visible to the reader thread.
* The reader thread will wait in a loop (`busy-waiting`) until it sees the `flag` value as `true`.

### **Use Cases for `volatile`:**

* **Flags or State Variables**: When you need to implement a simple flag or state variable that can be changed by one thread and read by others, `volatile` is a great way to ensure visibility without the overhead of synchronization.

* **Simple Communication Between Threads**: If a thread needs to signal other threads about a certain condition (like stopping a thread, or indicating that some work has been completed), you can use a `volatile` variable.

### **Limitations of `volatile`**:

1. **Does Not Provide Mutual Exclusion (Locks)**:

* `volatile` only ensures visibility, not atomicity or mutual exclusion. If multiple threads are modifying a variable (especially compound operations), you may need additional synchronization mechanisms like `synchronized` or `ReentrantLock`.

2. **Does Not Work for Complex Synchronization**:

* `volatile` is not suitable for complex synchronization problems where multiple variables or actions need to be synchronized together (e.g., transferring money between two accounts).

3. **No Guarantee for Compound Actions**:

* Operations such as increment (`i++`), or checking-and-modifying a value, need additional synchronization to be performed atomically, even if the variable itself is marked `volatile`.

### **When to Use `volatile`**:

* When a variable will be **modified** by one thread and **read** by multiple threads.
* When you need to **avoid synchronization overhead** for simple variables that are not part of complex state changes.
* For flags, state variables, or signals between threads, where only the latest value needs to be visible to all threads.

### **Example of a Non-Atomic Operation**:

```java
class Counter {
    private volatile int count = 0;

    public void increment() {
        count++;  // NOT atomic, may cause inconsistent results
    }

    public int getCount() {
        return count;
    }
}
```

In this example, even though `count` is `volatile`, the `increment()` method is **not atomic** because `count++` is a read-modify-write operation. To fix this, you would need to use `synchronized` or `AtomicInteger`.

---

### **Summary**

* The `volatile` keyword ensures that the most up-to-date value of a variable is visible to all threads.
* It provides a **visibility guarantee** but does not provide **atomicity** or **mutual exclusion** for complex operations.
* It is suitable for flags or simple state variables but not for operations that require compound updates.

---

### 🔹 86–90: **Memory Management & Garbage Collection**

## 86. How does memory management work in Java?

Memory management in Java is handled by the **Java Virtual Machine (JVM)**, which manages the allocation and deallocation of memory for Java applications. The JVM uses a combination of garbage collection, heap management, and stack management to efficiently handle memory. Here's an overview of how memory management works in Java:

### **Key Areas of Memory in Java**

Java memory is divided into several regions, each with a specific purpose:

1. **Heap Memory**:

* This is where **objects** are stored in Java. When you create an object using the `new` keyword, memory is allocated from the heap.
* The heap is further divided into two main parts:

    * **Young Generation**: Where newly created objects are stored. This generation is further divided into three sub-regions:

        * **Eden Space**: New objects are initially allocated here.
        * **Survivor Spaces (S0 and S1)**: Objects that have survived one or more garbage collection cycles in the young generation are moved to survivor spaces.
    * **Old Generation (Tenured Generation)**: Objects that have lived long enough in the young generation are promoted to the old generation. The old generation is typically larger and stores long-lived objects.
* The heap is the area where **Garbage Collection (GC)** happens, which we'll discuss below.

2. **Stack Memory**:

* The stack is used for **method calls** and **local variables**. Each thread in Java gets its own stack, and the stack stores the method execution frames, which include method arguments, local variables, and return addresses.
* The stack follows the **Last In, First Out (LIFO)** order, where method calls are pushed onto the stack and popped off when the method execution completes.
* Stack memory is automatically managed by the JVM, and once a method execution finishes, the memory used by the local variables is reclaimed.

3. **Method Area (Metaspace)**:

* This is where the **class definitions** (metadata) are stored. It holds the data for loaded classes, methods, static variables, and the constant pool.
* In older versions of Java (pre-Java 8), this was called the **PermGen (Permanent Generation)** space, but in Java 8 and beyond, the **Metaspace** replaced the PermGen space, which dynamically grows depending on the needs of the application.

4. **Program Counter (PC) Register**:

* Each thread has its own **PC register**, which keeps track of the current instruction being executed for that thread. This is used for controlling the flow of the program.

5. **Native Method Stack**:

* This is used for **native methods** (methods written in languages like C or C++) that are not executed in the Java environment. This is specific to the platform and the JVM implementation.

### **Garbage Collection (GC)**

Garbage collection is a crucial feature of Java’s memory management, which automatically reclaims memory by identifying and removing **unused objects** that are no longer referenced by any part of the program. The JVM performs **automatic garbage collection** to avoid memory leaks and ensure efficient memory usage.

**GC Phases**:

* **Mark**: The garbage collector identifies all the live objects (objects that are reachable or still referenced).
* **Sweep**: The garbage collector removes objects that are no longer referenced and reclaims their memory.
* **Compact**: The garbage collector may also compact the remaining live objects to eliminate memory fragmentation.

Java uses different garbage collection algorithms, and the JVM allows tuning the GC to optimize performance for specific use cases.

**Common GC Algorithms**:

1. **Serial GC**: Uses a single thread to manage garbage collection, best for single-threaded environments or small applications.
2. **Parallel GC**: Uses multiple threads to perform garbage collection, which is beneficial for applications with multiple threads.
3. **Concurrent Mark Sweep (CMS)**: Minimizes application pauses by performing garbage collection concurrently with the application threads. It is ideal for applications with low pause-time requirements.
4. **G1 Garbage Collector**: A more advanced garbage collection algorithm introduced in Java 7 that is designed to provide high performance with low pause times, suitable for large heaps.

### **Garbage Collection and Memory Management**

The heap memory is the primary region where objects are stored and collected by the garbage collector. The basic process of garbage collection works as follows:

* **Object Creation**: When an object is created using `new`, it is placed in the **young generation** (Eden space) of the heap.
* **Minor GC**: When the young generation is full, a **minor garbage collection** is triggered to remove unreachable objects. Surviving objects are moved to the survivor spaces or promoted to the old generation.
* **Major GC (Full GC)**: If the old generation is full, a **major garbage collection** occurs, which cleans up the old generation and may involve moving some objects back to the young generation. This can be more expensive in terms of time.

### **Java Memory Management and Object Lifecycle**

1. **Object Creation**:

* Objects are created using the `new` keyword, and memory for the object is allocated on the heap.
2. **References**:

* Variables (such as instance variables, local variables, or array elements) hold **references** to objects, not the actual objects themselves.
* When there are no more references to an object, it becomes eligible for garbage collection.
3. **Reachability**:

* An object is considered **reachable** if it can be accessed by the program through any chain of references. If an object is no longer reachable from any active part of the program, it is marked for garbage collection.
4. **Finalization**:

* Before an object is garbage collected, it can have its `finalize()` method called, allowing for resource cleanup (e.g., closing files or network connections). However, this method is generally discouraged because the timing of its invocation is not guaranteed.

### **Memory Leaks in Java**

Memory leaks in Java occur when objects are no longer needed but are still referenced, preventing the garbage collector from reclaiming the memory. Common causes of memory leaks in Java include:

* Holding onto references unnecessarily.
* Caching objects without proper eviction mechanisms.
* Static fields that reference objects and are never cleared.

### **Tuning JVM Memory**

You can control the JVM's memory management behavior by specifying the heap size and garbage collection parameters via command-line options, such as:

* `-Xms`: Initial heap size.
* `-Xmx`: Maximum heap size.
* `-XX:+UseG1GC`: Specify G1 garbage collector.
* `-XX:+PrintGCDetails`: Print details about garbage collection events.

### **Summary of Memory Management in Java**

1. **Heap Memory**: Where objects are created, divided into the young and old generations.
2. **Stack Memory**: Holds method call frames and local variables.
3. **Garbage Collection**: Automatically reclaims memory for objects that are no longer referenced.
4. **Method Area**: Stores class definitions, static variables, and constants.
5. **JVM Memory Regions**: Stack, heap, method area, program counter, and native method stacks are key regions managed by the JVM.
6. **Object Lifecycle**: Objects are created in the heap, and garbage collection reclaims unused memory.

Java's automatic memory management and garbage collection make it easier to write efficient and robust applications without manually managing memory. However, developers still need to be mindful of proper object reference management to avoid memory leaks.

---

## 87. What is garbage collection in Java?

**Garbage Collection (GC)** in Java is the process of automatically identifying and reclaiming memory occupied by objects that are no longer reachable or in use by the program. This process is managed by the **Java Virtual Machine (JVM)** and helps prevent memory leaks by freeing up memory, so developers don't have to manually manage memory.

In Java, garbage collection eliminates the need for explicit memory management, like in languages such as C or C++ where developers need to manually allocate and deallocate memory using `malloc` and `free`. The **JVM** handles the memory cleanup automatically through garbage collection.

### **Key Concepts of Garbage Collection:**

1. **Reachability**:

* An object is considered **reachable** if it can be accessed by any active thread or part of the program through a chain of references. If there are no references to an object, it is considered **unreachable** and eligible for garbage collection.

2. **Garbage Collector (GC)**:

* The **garbage collector** is the component of the JVM responsible for identifying unreachable objects and reclaiming their memory. It runs in the background, performing memory management tasks.

3. **Heap Memory**:

* Objects in Java are stored in the **heap**. The heap is where memory is dynamically allocated for objects at runtime. The garbage collector frees up memory from the heap by removing objects that are no longer reachable.

4. **Finalization**:

* Before an object is garbage collected, the JVM gives it a chance to release system resources (such as file handles, network connections, etc.) via the object's `finalize()` method. However, it's important to note that relying on `finalize()` is discouraged, as its execution time is not guaranteed.

### **How Garbage Collection Works:**

1. **Marking**:

* The garbage collector identifies **reachable objects** starting from **root objects** (such as active threads, static fields, or local variables) and marks them as **alive**. Any object that cannot be reached from the root objects is considered **unreachable**.

2. **Sweeping**:

* The garbage collector then **sweeps** through the heap and **removes** the unreachable objects, freeing up the memory they occupied.

3. **Compaction**:

* After sweeping, the JVM may also **compact** the heap to reclaim the memory occupied by the deleted objects. This step helps prevent memory fragmentation.

### **Generations in Garbage Collection:**

Java's heap is divided into different **generations** to optimize garbage collection. These generations are:

1. **Young Generation**:

* This is where newly created objects are placed. The young generation is split into:

    * **Eden Space**: New objects are initially allocated here.
    * **Survivor Spaces** (S0 and S1): Objects that survive one or more garbage collection cycles are moved to these spaces.
2. **Old Generation (Tenured Generation)**:

* Objects that have lived long enough in the young generation are promoted to the old generation. This space is used for long-lived objects.
3. **Permanent Generation / Metaspace**:

* This area stores **class metadata** and **static variables**. In Java 8 and beyond, the **Metaspace** replaced the **PermGen** (Permanent Generation) space.

### **Types of Garbage Collection Algorithms**:

1. **Serial Garbage Collection**:

* The **Serial GC** uses a single thread for garbage collection. It is the simplest GC algorithm and is suitable for small applications or single-threaded environments. The entire heap is paused while garbage collection happens.

2. **Parallel Garbage Collection**:

* The **Parallel GC** (also known as throughput collector) uses multiple threads to perform garbage collection. It is suitable for multi-threaded applications and is often used for systems with multiple processors to speed up the process.

3. **Concurrent Mark Sweep (CMS) Garbage Collection**:

* The **CMS GC** aims to minimize pause times by performing some phases of garbage collection concurrently with the application threads. It is suitable for applications that require low pause times, such as web servers or real-time applications.

4. **G1 (Garbage First) Garbage Collection**:

* The **G1 GC** was introduced in Java 7 and aims to provide low pause times and high throughput for large heaps. It divides the heap into regions and collects garbage in a way that minimizes pause times. It's a good choice for applications that need both high throughput and low-latency garbage collection.

### **Garbage Collection Phases**:

1. **Minor GC (Young Generation GC)**:

* This occurs when the **young generation** is full. It collects garbage from the **Eden space** and promotes surviving objects to the **survivor spaces** or the **old generation**.
2. **Major GC (Full GC)**:

* This occurs when the **old generation** is full. It collects garbage from the **old generation** and performs memory compaction. Major GC is more expensive and can cause longer pause times compared to minor GC.

### **Example of Garbage Collection**:

```java
public class GarbageCollectionExample {
    public static void main(String[] args) {
        // Creating an object
        MyClass obj1 = new MyClass();

        // Set obj1 to null, making it eligible for GC
        obj1 = null;

        // Manually suggest garbage collection (not guaranteed to run immediately)
        System.gc();  // This invokes the garbage collector, but it's not guaranteed.

        // Creating another object
        MyClass obj2 = new MyClass();
    }

    static class MyClass {
        @Override
        protected void finalize() throws Throwable {
            System.out.println("Object is being garbage collected");
        }
    }
}
```

In this example:

* When `obj1` is set to `null`, it becomes eligible for garbage collection.
* Calling `System.gc()` suggests that the JVM should run the garbage collector, but it is not guaranteed to happen immediately.
* When the `MyClass` object is garbage collected, the `finalize()` method is called (if defined) before the object is removed.

### **Finalization and `finalize()` Method**:

* **`finalize()`** is a method in `Object` that can be overridden to clean up resources (like closing files or releasing network connections) before the object is garbage collected.
* However, relying on `finalize()` for resource management is discouraged because the JVM does not guarantee when or if `finalize()` will be called. Additionally, it can delay garbage collection, leading to inefficient resource management.

### **Memory Leaks and Garbage Collection**:

* **Memory leaks** in Java occur when objects are still referenced but are no longer needed, preventing them from being garbage collected.
* Common causes of memory leaks include holding unnecessary references in collections, static fields, or unintended references from long-lived objects.

### **JVM Garbage Collection Tuning**:

You can tune the garbage collection process to optimize memory management using JVM flags:

* `-Xms`: Specifies the initial heap size.
* `-Xmx`: Specifies the maximum heap size.
* `-XX:+UseG1GC`: Enables G1 garbage collector.
* `-XX:+PrintGCDetails`: Prints details about garbage collection events.

### **Summary of Garbage Collection in Java**:

* Garbage collection in Java is an automatic memory management process that reclaims memory used by unreachable objects.
* The heap is divided into generations (young and old) to optimize the process.
* Different garbage collection algorithms are available to suit different needs, such as Serial GC, Parallel GC, CMS GC, and G1 GC.
* Although garbage collection minimizes memory management overhead, developers must still manage object references properly to avoid memory leaks.

---

## 88. What are the types of garbage collectors in JVM?

In the JVM (Java Virtual Machine), there are several types of garbage collectors (GC) that are designed to manage memory and optimize the garbage collection process. Each garbage collector has its own strengths and is suitable for different types of applications. Below are the primary types of garbage collectors available in the JVM:

### 1. **Serial Garbage Collector**

* **Description**: The Serial Garbage Collector is the simplest garbage collection algorithm. It uses a single thread to perform garbage collection. It's suitable for single-threaded environments or smaller applications with limited memory.
* **Key Characteristics**:

    * Uses only one thread for both minor and major garbage collection.
    * Performs all garbage collection actions (mark, sweep, compact) sequentially.
    * Introduces pause times that can be relatively long since everything runs on a single thread.
* **Best Used For**: Applications with small heaps and when minimizing complexity is preferred (e.g., single-threaded applications or environments with limited resources).
* **JVM Flag**: `-XX:+UseSerialGC`

### 2. **Parallel Garbage Collector (Throughput Collector)**

* **Description**: The Parallel Garbage Collector uses multiple threads to perform garbage collection tasks. It is designed to maximize throughput and perform garbage collection faster by using parallel threads for both minor and major garbage collection.
* **Key Characteristics**:

    * Multiple threads are used for minor garbage collection in the young generation.
    * Also performs major garbage collection (full GC) in parallel.
    * It reduces pause times by parallelizing the work of GC but still causes noticeable pauses for major collections.
* **Best Used For**: Multi-threaded applications where throughput is more important than pause times (e.g., server-side applications).
* **JVM Flag**: `-XX:+UseParallelGC`

### 3. **Concurrent Mark-Sweep (CMS) Garbage Collector**

* **Description**: The CMS Garbage Collector is designed to minimize application pause times by doing most of its work concurrently with the application threads. It tries to collect garbage with minimal disruption to application performance.
* **Key Characteristics**:

    * **Concurrent Marking**: The marking of live objects happens concurrently with the application threads.
    * **Shorter Pauses**: The goal is to avoid long pause times by doing most of the work concurrently.
    * **Phases**:

        1. **Initial Mark**: Marks reachable objects in the young generation.
        2. **Concurrent Mark**: Marks reachable objects in the old generation.
        3. **Concurrent Preclean**: Prepares the old generation for the next cycle.
        4. **Final Remark**: Finalizes the marking phase before sweeping the dead objects.
        5. **Concurrent Sweep**: Reclaims memory by sweeping through the old generation.
    * **Weakness**: It may still cause longer pause times during the "remark" phase, and if the heap becomes too fragmented, it can lead to Full GCs.
* **Best Used For**: Applications that require low pause times but can tolerate some complexity in GC phases.
* **JVM Flag**: `-XX:+UseConcMarkSweepGC`

### 4. **G1 (Garbage First) Garbage Collector**

* **Description**: The G1 garbage collector is designed for large heaps with a focus on reducing pause times while maintaining good throughput. It divides the heap into regions, allowing the garbage collector to focus on the regions with the most garbage.
* **Key Characteristics**:

    * Divides the heap into small **regions** (instead of generations like other GCs).
    * Focuses on minimizing pause times by collecting garbage in the regions with the most garbage.
    * Performs both **young generation** and **old generation** collection in parallel with application threads.
    * **Predictable Pause Times**: G1 allows the user to specify a target pause time for garbage collection, and the GC will attempt to meet this target.
    * Works well with large heaps (multiple gigabytes).
* **Best Used For**: Applications that require a balance between low pause times and good throughput, especially for applications with large heaps.
* **JVM Flag**: `-XX:+UseG1GC`

### 5. **Z Garbage Collector (ZGC)**

* **Description**: The ZGC is a low-latency garbage collector designed to minimize pause times. It was introduced in JDK 11 and is capable of handling very large heaps (multiple terabytes) while providing consistent, low-latency performance.
* **Key Characteristics**:

    * **Low-Latency**: Designed for applications that require very low pause times (usually in the range of a few milliseconds).
    * **Concurrent and Parallel**: Most GC phases are concurrent, and work is spread across multiple threads.
    * **Region-Based**: Like G1, it divides the heap into regions.
    * **Handles Large Heaps**: It can handle large heaps, including those with terabytes of memory, with minimal impact on application performance.
* **Best Used For**: Applications that need very low pause times and can operate with large heaps (e.g., real-time or latency-sensitive applications).
* **JVM Flag**: `-XX:+UseZGC`

### 6. **Shenandoah Garbage Collector**

* **Description**: The Shenandoah Garbage Collector is another low-latency garbage collector designed to reduce pause times, similar to ZGC. It was introduced in JDK 12 and focuses on minimizing GC pause times regardless of the heap size.
* **Key Characteristics**:

    * **Low-Latency**: Aims for very low pause times (sub-millisecond).
    * **Concurrent**: It performs most of its work concurrently with the application threads.
    * It was developed to meet the requirements of applications that require consistent response times (like high-frequency trading systems or real-time applications).
* **Best Used For**: Applications that require consistent low pause times with large heaps.
* **JVM Flag**: `-XX:+UseShenandoahGC`

### Summary of JVM Garbage Collectors:

| **Garbage Collector** | **Key Features**                                      | **Best For**                                                |
| --------------------- | ----------------------------------------------------- | ----------------------------------------------------------- |
| **Serial GC**         | Single-threaded, simple, minimal overhead             | Small applications, single-threaded environments            |
| **Parallel GC**       | Multi-threaded, good throughput, pause time control   | Multi-threaded applications, server-side apps               |
| **CMS GC**            | Minimizes pause times with concurrent collection      | Applications needing low pause times                        |
| **G1 GC**             | Region-based, aims for low pause times, predictable   | Large heaps, low pause time and throughput balance          |
| **ZGC**               | Low-latency, handles large heaps with minimal pauses  | Real-time or low-latency applications                       |
| **Shenandoah GC**     | Low-latency, handles large heaps, minimal pause times | Low-latency, high-frequency trading systems, real-time apps |

### How to Choose a Garbage Collector:

* **For Low Latency**: Use **ZGC** or **Shenandoah GC**.
* **For High Throughput**: Use **Parallel GC**.
* **For Large Heaps with Predictable Pause Times**: Use **G1 GC**.
* **For Low Pause Times with Concurrent Marking**: Use **CMS GC** (though CMS is deprecated in newer versions of Java, it is still used in some older applications).

### Conclusion:

Each garbage collector is designed for different use cases, and selecting the right one depends on your application's requirements for throughput, latency, heap size, and pause time. By choosing the appropriate garbage collector, you can significantly improve the performance and efficiency of memory management in Java applications.

---

## 89. What is the difference between heap and stack memory?

In Java, **heap** and **stack** are two types of memory areas used to store data, but they have different purposes, structures, and lifetimes. Here’s a detailed comparison of **heap** and **stack** memory:

### 1. **Heap Memory**

* **Purpose**: The heap is used for dynamic memory allocation. It stores **objects** and **arrays** created during the execution of the program.
* **Memory Allocation**: Objects are allocated memory from the heap when they are created using the `new` keyword.
* **Size**: The heap is generally larger in size compared to the stack. It can grow or shrink during program execution based on the system’s requirements.
* **Lifetime**: Objects in the heap have a longer lifetime and are **garbage collected** by the JVM when they are no longer referenced (i.e., they are no longer reachable).
* **Management**: Memory management in the heap is done by the **garbage collector**. The JVM automatically reclaims memory for unused objects.
* **Access Speed**: Access to heap memory is slower compared to stack memory because heap memory involves more complex management.
* **Thread Safety**: The heap is **shared** among all threads in the application, so it requires synchronization to avoid thread interference.

**Example**:

```java
public class HeapExample {
    public static void main(String[] args) {
        MyClass obj = new MyClass();  // obj is allocated in the heap
    }
}

class MyClass {
    int value = 10;
}
```

In this example, the `obj` is stored in the heap.

---

### 2. **Stack Memory**

* **Purpose**: The stack is used for static memory allocation, and it stores **method call frames**, **local variables**, and **method parameters**. It’s where primitive data types and references to objects are stored.
* **Memory Allocation**: Memory for primitive types (like `int`, `float`, etc.) and references to objects (but not the objects themselves) is allocated in the stack.
* **Size**: The stack is generally smaller than the heap and has a fixed size that is typically defined by the JVM or operating system.
* **Lifetime**: Variables in the stack have a **short lifetime**. They are created when a method is called and destroyed when the method finishes execution.
* **Management**: The stack operates in a **Last In, First Out (LIFO)** manner. When a method is called, a new frame is pushed onto the stack, and it is popped when the method finishes.
* **Access Speed**: Access to stack memory is faster compared to heap memory because the stack follows a simple and deterministic structure.
* **Thread Safety**: Each thread in Java has its own **stack**, so there is no need for synchronization when accessing stack memory (it is **thread-local**).

**Example**:

```java
public class StackExample {
    public static void main(String[] args) {
        int x = 10;  // x is allocated in the stack
        MyClass obj = new MyClass();  // Reference obj is allocated in the stack
        obj.value = 20;  // The object itself is in the heap
    }
}

class MyClass {
    int value;
}
```

In this example, `x` and the reference `obj` are stored in the stack, while the `MyClass` object itself is stored in the heap.

---

### Key Differences Between Heap and Stack Memory

| **Feature**           | **Heap Memory**                                                   | **Stack Memory**                              |
| --------------------- | ----------------------------------------------------------------- | --------------------------------------------- |
| **Purpose**           | Stores objects and arrays                                         | Stores local variables, method calls          |
| **Allocation**        | Dynamic allocation at runtime                                     | Static allocation at compile time             |
| **Size**              | Larger, can grow or shrink                                        | Smaller, fixed size                           |
| **Lifetime**          | Objects can have long lifetimes, managed by the garbage collector | Variables exist only during method execution  |
| **Memory Management** | Managed by the garbage collector                                  | Managed by the JVM automatically (via LIFO)   |
| **Access Speed**      | Slower access due to more complex management                      | Faster access (LIFO structure)                |
| **Thread Safety**     | Shared among all threads, requires synchronization                | Thread-local, no synchronization needed       |
| **Data Stored**       | Objects, arrays                                                   | Primitives, method references, function calls |
| **Growth**            | Can grow dynamically (up to system limits)                        | Fixed, cannot grow or shrink dynamically      |

---

### When to Use Heap and Stack:

* **Use Stack Memory** when you need fast, temporary storage for method calls and local variables (e.g., primitive data types and references to objects).
* **Use Heap Memory** for dynamically created objects whose lifetime is controlled by the garbage collector.

### Example to Visualize:

Consider the following Java program:

```java
class Example {
    int x;   // Instance variable in the heap

    public void method() {
        int local = 5;  // Local variable in the stack
        Example obj = new Example();  // obj reference is in the stack, object in the heap
    }
}
```

* The object `obj` and its data (instance variables like `x`) are stored in the **heap**.
* The reference variable `obj` and the local variable `local` are stored in the **stack** during the method execution.

In summary, **stack memory** is fast, thread-local, and stores method-related information like local variables and references, while **heap memory** is used for objects and arrays that have a longer lifetime and need garbage collection.

---

## 90. How can you make an object eligible for garbage collection?

In Java, an object becomes eligible for **garbage collection** when it is no longer reachable or referenced by any active part of the program. This means that there are no more **live references** pointing to the object in memory, and it cannot be accessed or used anymore. The **garbage collector** is responsible for reclaiming the memory occupied by these unreachable objects.

Here are the steps and scenarios in which an object becomes eligible for garbage collection:

### 1. **Remove All References to the Object**

If an object no longer has any references pointing to it, it becomes eligible for garbage collection. This can happen in various ways:

* **Setting the reference to `null`**: When the reference variable pointing to an object is set to `null`, it removes the reference to the object.
* **Reassigning the reference**: If a reference variable is reassigned to another object, the original object that the variable pointed to may become unreachable.
* **Going out of scope**: When a reference variable goes out of scope (e.g., when a method finishes execution and the local variable is destroyed), the object it referenced becomes eligible for GC if no other references point to it.

**Example**:

```java
class MyClass {
    int value;
}

public class GarbageCollectionExample {
    public static void main(String[] args) {
        MyClass obj = new MyClass();  // obj refers to a new MyClass object
        obj = null;  // The object becomes eligible for GC
    }
}
```

In this example, after `obj = null;`, the object that `obj` originally pointed to becomes eligible for garbage collection because there are no references pointing to it anymore.

### 2. **Objects Going Out of Scope**

When a method finishes executing, its local variables are removed from the stack. If these local variables were references to objects, and if no other active references to the objects remain, those objects become eligible for garbage collection.

**Example**:

```java
public class GarbageCollectionExample {
    public static void main(String[] args) {
        MyClass obj1 = new MyClass();  // obj1 is created
        someMethod();  // After this method ends, obj2 is eligible for GC
    }
    
    public static void someMethod() {
        MyClass obj2 = new MyClass();  // obj2 is created inside the method
        // obj2 is only accessible within this method, so it's eligible for GC once the method finishes execution
    }
}
```

### 3. **Nullifying References in Collections**

If an object is in a **collection** (like a `List`, `Set`, `Map`, etc.) and the reference to it is removed from the collection, it becomes eligible for garbage collection if there are no other references to it.

**Example**:

```java
import java.util.ArrayList;

public class GarbageCollectionExample {
    public static void main(String[] args) {
        ArrayList<MyClass> list = new ArrayList<>();
        MyClass obj = new MyClass();  // obj is created and added to the list
        list.add(obj);
        list.remove(obj);  // obj is removed from the list, now eligible for GC
    }
}
```

After `list.remove(obj);`, if there are no other references to `obj`, it becomes eligible for garbage collection.

### 4. **Circular References**

Even if two objects reference each other, if there are no external references to the circularly-referenced objects, they will still become eligible for garbage collection. The garbage collector can detect and reclaim memory occupied by circularly referenced objects as long as they are not reachable from any active thread.

**Example**:

```java
class A {
    B b;
}

class B {
    A a;
}

public class GarbageCollectionExample {
    public static void main(String[] args) {
        A objA = new A();
        B objB = new B();
        objA.b = objB;
        objB.a = objA;
        
        objA = null;  // Both objA and objB become eligible for GC
        objB = null;
    }
}
```

In this example, `objA` and `objB` are referring to each other, but once both references are set to `null`, they become eligible for garbage collection.

### 5. **Strong References vs. Weak References**

* **Strong References**: Objects that are referenced by strong references are not eligible for garbage collection.
* **Weak References**: Objects referenced only by weak references become eligible for garbage collection once there are no strong references to them.
* **Soft References**: Objects referenced by soft references are only garbage collected when the JVM is running low on memory.
* **Phantom References**: Used for more advanced garbage collection control, objects referenced by phantom references are not immediately collected, but they are queued for final cleanup before they are actually collected.

**Example with WeakReference**:

```java
import java.lang.ref.WeakReference;

public class GarbageCollectionExample {
    public static void main(String[] args) {
        MyClass obj = new MyClass();
        WeakReference<MyClass> weakRef = new WeakReference<>(obj);  // Weak reference to obj
        
        obj = null;  // obj becomes eligible for GC, weak reference doesn't prevent GC
    }
}
```

### 6. **Explicit Garbage Collection**

Although Java's garbage collection is automatic, you can request the garbage collector to run using `System.gc()`. However, it’s just a **suggestion**, and the JVM may choose to ignore it. It's generally not recommended to rely on `System.gc()` for explicit memory management.

```java
public class GarbageCollectionExample {
    public static void main(String[] args) {
        MyClass obj = new MyClass();
        obj = null;  // Object is eligible for GC
        System.gc();  // Request garbage collection (not guaranteed)
    }
}
```

---

### Conclusion:

An object becomes eligible for garbage collection when:

1. There are **no references** pointing to it.
2. It goes out of scope.
3. Circular references are present, but no active references to the objects exist.
4. It is only referenced by weak or soft references.

The **garbage collector** will eventually reclaim the memory occupied by unreachable objects, but this is not guaranteed to happen immediately.

---

### 🔹 91–100: **Java 8+ Features (Functional & Streams)**

## 91. What are lambda expressions in Java?

In Java, **lambda expressions** are a feature introduced in **Java 8** that allow you to provide a clear and concise way to express instances of single-method interfaces (functional interfaces). Lambda expressions enable you to write more compact and readable code, especially when working with functional-style operations, such as those used with the **Streams API** or **Collection API**.

### Syntax of Lambda Expression:

The general syntax of a lambda expression is as follows:

```java
(parameters) -> expression
```

* **Parameters**: The input parameters (can be zero or more) for the lambda function.
* **Arrow (`->`)**: Separates the parameter list and the body of the lambda expression.
* **Expression**: A single statement or block of code that defines what the lambda will do.

### Basic Structure:

```java
(parameter1, parameter2, ...) -> { body of the lambda expression }
```

* If the body is a single expression, you can omit the curly braces `{}` and the return statement (if applicable).
* If there are no parameters, you can leave the parentheses empty.

### Examples of Lambda Expressions:

1. **No parameters**:

   ```java
   () -> System.out.println("Hello, World!");
   ```

   This lambda expression takes no parameters and prints "Hello, World!" when executed.

2. **Single parameter**:

   ```java
   (x) -> System.out.println(x);
   ```

   This lambda expression takes a single parameter `x` and prints it.

3. **Multiple parameters**:

   ```java
   (x, y) -> x + y;
   ```

   This lambda expression takes two parameters `x` and `y` and returns their sum.

4. **With a block of code**:

   ```java
   (x, y) -> {
       int sum = x + y;
       return sum;
   }
   ```

   This lambda expression takes two parameters and calculates the sum in a block of code.

### Example Use Case:

A common use case for lambda expressions is with the **Java Collections framework**, particularly with methods like `forEach()`, `map()`, and `filter()`. For example:

```java
import java.util.List;
import java.util.Arrays;

public class LambdaExample {
    public static void main(String[] args) {
        List<String> list = Arrays.asList("apple", "banana", "cherry");

        // Using lambda expression with forEach
        list.forEach(item -> System.out.println(item));
    }
}
```

In this example, `list.forEach(item -> System.out.println(item))` uses a lambda expression to print each item in the list.

### Functional Interfaces:

A **functional interface** is an interface with just one abstract method. Lambda expressions can be used to provide implementations for functional interfaces. Java provides several built-in functional interfaces in the `java.util.function` package, such as `Predicate`, `Function`, `Consumer`, `Supplier`, etc.

For example:

```java
@FunctionalInterface
interface MyFunctionalInterface {
    void myMethod();
}

public class LambdaExample {
    public static void main(String[] args) {
        MyFunctionalInterface myFunc = () -> System.out.println("Lambda expression is working!");
        myFunc.myMethod();
    }
}
```

### Key Points about Lambda Expressions:

1. **Concise Syntax**: Lambdas allow you to express instances of single-method interfaces (functional interfaces) in a concise and readable manner.

2. **No Need for Boilerplate Code**: You don't need to create a separate class or use an anonymous inner class to implement functional interfaces.

3. **Target Type**: Lambda expressions are used primarily with **functional interfaces**, which are interfaces that contain a single abstract method.

4. **Behavior Parameterization**: Lambdas allow you to pass behavior (like a function) as arguments to methods or return it from methods, which is useful in functional programming.

5. **Higher-Order Functions**: You can pass functions as arguments to other functions or return them from functions.

### Common Use Cases:

1. **Functional Interfaces**: Lambda expressions are typically used for implementing functional interfaces, such as those in the `java.util.function` package (e.g., `Predicate`, `Consumer`, `Function`).

2. **Streams API**: Lambdas are commonly used in conjunction with the **Streams API** to operate on collections and perform operations like filtering, mapping, and reducing.

   Example with Streams:

   ```java
   import java.util.List;
   import java.util.Arrays;

   public class LambdaWithStreams {
       public static void main(String[] args) {
           List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

           // Use lambda expression to filter even numbers and print them
           numbers.stream()
                  .filter(n -> n % 2 == 0)
                  .forEach(n -> System.out.println(n));
       }
   }
   ```

   Output:

   ```
   2
   4
   ```

3. **Event Handling**: Lambdas simplify event-handling code, especially in graphical user interfaces (GUIs), where you can directly implement listeners using lambdas.

   Example:

   ```java
   JButton button = new JButton("Click Me");
   button.addActionListener(e -> System.out.println("Button clicked!"));
   ```

### Advantages of Lambda Expressions:

* **Readability**: They make your code more concise and easier to understand, especially when performing operations on collections or passing behavior as arguments.
* **Reduction of Boilerplate Code**: Lambdas eliminate the need for writing anonymous classes.
* **Enabling Functional Programming**: They enable a functional programming style in Java, making it easier to manipulate and process data using functions as first-class citizens.
* **Improved Parallelism**: When used with the Streams API, lambdas facilitate parallel processing of collections, improving performance in certain cases.

### Limitations of Lambda Expressions:

* **No `this` keyword**: In a lambda expression, the `this` keyword refers to the enclosing instance, not the lambda itself. This behavior is different from that of anonymous classes.
* **Not suitable for all situations**: Lambda expressions are designed for simple, short implementations of functional interfaces. For complex behaviors, traditional classes or anonymous classes might still be better.

In conclusion, **lambda expressions** simplify code, improve readability, and allow you to use functional programming features in Java, making them a powerful tool for developers working with modern Java features.

---

## 92. What are functional interfaces?

In Java, a **functional interface** is an interface that contains exactly **one abstract method**. These interfaces are used to represent a single functionality or action that can be implemented by a **lambda expression** or a **method reference**. Functional interfaces can have multiple **default methods** or **static methods**, but they can only have one abstract method. They form the basis for lambda expressions and functional programming features in Java, especially after the introduction of **Java 8**.

### Key Characteristics of Functional Interfaces:

1. **One Abstract Method**: A functional interface must contain exactly one abstract method.
2. **Can Contain Multiple Default or Static Methods**: A functional interface can have multiple default or static methods, but only one abstract method.
3. **Can Be Implemented by Lambda Expressions**: Functional interfaces are primarily used with lambda expressions or method references to implement the single abstract method.

### Example of a Functional Interface:

```java
@FunctionalInterface
interface MyFunctionalInterface {
    // Single abstract method
    void myMethod();

    // Default method (not abstract)
    default void defaultMethod() {
        System.out.println("This is a default method.");
    }

    // Static method (not abstract)
    static void staticMethod() {
        System.out.println("This is a static method.");
    }
}
```

In this example:

* `myMethod()` is the **abstract method**, making this interface a **functional interface**.
* `defaultMethod()` and `staticMethod()` are non-abstract methods and do not violate the requirement of having only one abstract method.

### Common Functional Interfaces in Java:

Java provides several built-in functional interfaces in the `java.util.function` package, which you can use with lambda expressions. Here are some commonly used functional interfaces:

1. **`Runnable`**: Represents a task that can be executed asynchronously or in a separate thread.

   ```java
   @FunctionalInterface
   interface Runnable {
       void run();
   }
   ```

2. **`Predicate<T>`**: Represents a boolean-valued function that accepts an argument of type `T`.

   ```java
   @FunctionalInterface
   interface Predicate<T> {
       boolean test(T t);
   }
   ```

   Example usage:

   ```java
   Predicate<Integer> isEven = n -> n % 2 == 0;
   System.out.println(isEven.test(4));  // true
   ```

3. **`Consumer<T>`**: Represents an operation that accepts a single input argument and returns no result.

   ```java
   @FunctionalInterface
   interface Consumer<T> {
       void accept(T t);
   }
   ```

   Example usage:

   ```java
   Consumer<String> printString = s -> System.out.println(s);
   printString.accept("Hello, World!");
   ```

4. **`Function<T, R>`**: Represents a function that accepts an argument of type `T` and returns a result of type `R`.

   ```java
   @FunctionalInterface
   interface Function<T, R> {
       R apply(T t);
   }
   ```

   Example usage:

   ```java
   Function<Integer, String> intToString = n -> "Number: " + n;
   System.out.println(intToString.apply(5));  // Number: 5
   ```

5. **`Supplier<T>`**: Represents a function that takes no arguments and returns a result of type `T`.

   ```java
   @FunctionalInterface
   interface Supplier<T> {
       T get();
   }
   ```

   Example usage:

   ```java
   Supplier<Double> randomValue = () -> Math.random();
   System.out.println(randomValue.get());  // Random number
   ```

6. **`UnaryOperator<T>`**: Represents a function that takes a single argument of type `T` and returns a result of the same type `T`.

   ```java
   @FunctionalInterface
   interface UnaryOperator<T> extends Function<T, T> {
   }
   ```

   Example usage:

   ```java
   UnaryOperator<Integer> square = n -> n * n;
   System.out.println(square.apply(4));  // 16
   ```

7. **`BinaryOperator<T>`**: Represents a function that takes two arguments of type `T` and returns a result of the same type `T`.

   ```java
   @FunctionalInterface
   interface BinaryOperator<T> extends BiFunction<T, T, T> {
   }
   ```

   Example usage:

   ```java
   BinaryOperator<Integer> add = (a, b) -> a + b;
   System.out.println(add.apply(5, 3));  // 8
   ```

### Why Use Functional Interfaces?

1. **Simplify Code with Lambda Expressions**: Functional interfaces allow you to pass behavior as arguments to methods or return them from methods, which simplifies the code using **lambda expressions**.

   ```java
   @FunctionalInterface
   interface Calculator {
       int add(int a, int b);
   }

   public class LambdaExample {
       public static void main(String[] args) {
           Calculator calc = (a, b) -> a + b;
           System.out.println(calc.add(5, 3));  // 8
       }
   }
   ```

2. **Functional Programming**: Java 8 introduced features like the **Streams API** and **higher-order functions**, which heavily use functional interfaces to allow functional-style programming. These interfaces help in writing more expressive, declarative, and concise code.

3. **Reusability and Flexibility**: Functional interfaces allow code to be reused and provide flexibility by enabling you to define small, reusable units of work that can be passed around, rather than having to write verbose, boilerplate code.

4. **Method References and Default Methods**: In addition to lambda expressions, functional interfaces are compatible with **method references** and **default methods**, making them even more powerful in modern Java.

### How to Create a Functional Interface:

To create a custom functional interface, you simply need to ensure that the interface contains exactly one abstract method. It's also a good practice (but not mandatory) to annotate the interface with the `@FunctionalInterface` annotation, which tells the compiler to check if the interface adheres to the functional interface contract.

```java
@FunctionalInterface
public interface MyFunctionalInterface {
    void execute();

    // Optional default method
    default void defaultMethod() {
        System.out.println("Default method");
    }
}
```

If the interface contains more than one abstract method, the compiler will throw an error, as it no longer qualifies as a functional interface.

### Conclusion:

Functional interfaces are a key feature of functional programming in Java, enabling **lambda expressions** and **method references** to be used effectively. They simplify the code by reducing boilerplate, increase code readability, and allow for more flexible and reusable components. Many of the core functional features in Java 8 and beyond, such as the Streams API, rely heavily on functional interfaces.

---

## 93. What are default and static methods in interfaces?

In Java, interfaces can contain **default methods** and **static methods**, which were introduced in **Java 8**. These methods help enhance the functionality of interfaces and allow developers to write cleaner and more flexible code without breaking backward compatibility. Let’s break down each type of method:

### 1. **Default Methods in Interfaces**:

A **default method** is a method that is defined inside an interface with the `default` keyword. Default methods provide a way to add new functionality to interfaces while maintaining backward compatibility with classes that implement the interface.

#### Key Characteristics of Default Methods:

* **Defined in the Interface**: A default method is defined inside an interface using the `default` keyword.
* **Has a Body**: Unlike regular abstract methods in interfaces (which do not have a body), default methods can have an implementation.
* **Can Be Overridden**: Classes implementing the interface can override default methods to provide their own implementation if needed.
* **Backward Compatibility**: Default methods allow new methods to be added to an interface without breaking existing implementations. If an interface is updated to include a new default method, classes that implement the interface do not need to modify their code (unless they wish to override the default implementation).

#### Example of a Default Method:

```java
interface MyInterface {
    // Abstract method (no body)
    void abstractMethod();

    // Default method (with a body)
    default void defaultMethod() {
        System.out.println("This is the default implementation.");
    }
}

class MyClass implements MyInterface {
    // Provide implementation for the abstract method
    public void abstractMethod() {
        System.out.println("Implementing abstract method.");
    }

    // Optional: override the default method
    @Override
    public void defaultMethod() {
        System.out.println("Overridden default method.");
    }
}

public class DefaultMethodExample {
    public static void main(String[] args) {
        MyClass obj = new MyClass();
        obj.abstractMethod(); // Output: Implementing abstract method.
        obj.defaultMethod();  // Output: Overridden default method.
    }
}
```

In the example above:

* `defaultMethod()` is a default method in `MyInterface`.
* `MyClass` implements `MyInterface` and provides an implementation for the abstract method.
* The default method is overridden in `MyClass` to provide a custom implementation.

If the default method is not overridden in the implementing class, the default implementation from the interface is used.

### 2. **Static Methods in Interfaces**:

A **static method** in an interface is a method that belongs to the interface itself, rather than to instances of classes that implement the interface. Static methods in interfaces are defined in the same way as static methods in classes, but they can only be invoked using the interface name.

#### Key Characteristics of Static Methods:

* **Defined in the Interface**: Static methods are defined inside an interface using the `static` keyword.
* **Cannot Be Overridden**: Unlike default methods, static methods cannot be overridden in implementing classes. They are associated with the interface itself, not instances of classes.
* **Can Be Invoked Using the Interface Name**: Static methods in interfaces must be invoked using the interface name, not the instance of the class.

#### Example of a Static Method:

```java
interface MyInterface {
    // Static method in the interface
    static void staticMethod() {
        System.out.println("This is a static method in the interface.");
    }
}

public class StaticMethodExample {
    public static void main(String[] args) {
        // Calling static method using the interface name
        MyInterface.staticMethod(); // Output: This is a static method in the interface.
    }
}
```

In the example above:

* `staticMethod()` is a static method in the `MyInterface` interface.
* The static method is called using the interface name (`MyInterface.staticMethod()`), not an instance of any implementing class.

### Comparison of Default and Static Methods:

| Feature                    | Default Method                                                              | Static Method                                  |
| -------------------------- | --------------------------------------------------------------------------- | ---------------------------------------------- |
| **Keyword**                | `default`                                                                   | `static`                                       |
| **Belongs to**             | Instance of the class implementing the interface                            | The interface itself                           |
| **Can Be Overridden?**     | Yes, in implementing classes                                                | No, it cannot be overridden                    |
| **Invocation**             | Called on an instance of a class implementing the interface                 | Called using the interface name                |
| **Use Case**               | Provide default behavior or functionality                                   | Utility methods related to the interface       |
| **Backward Compatibility** | Helps add new functionality to the interface without breaking existing code | Doesn't affect backward compatibility directly |

### Use Cases:

1. **Default Methods**:

* Default methods are used to add new methods to interfaces without breaking existing implementations. This is particularly useful in libraries or APIs where you might want to extend the interface functionality without forcing changes in all the classes that implement the interface.
* They can provide shared behavior that can be reused by all implementing classes or optionally overridden by them.

2. **Static Methods**:

* Static methods in interfaces are used for utility methods that are related to the interface but are not dependent on instance-level behavior. They can be used for common functionality related to the interface or for factory methods.

### Conclusion:

* **Default Methods** allow interfaces to evolve by adding new methods with implementations, providing backward compatibility for implementing classes.
* **Static Methods** in interfaces are used to provide utility methods related to the interface, but they cannot be overridden and are invoked using the interface name.

These two features help Java developers write more flexible and maintainable code, especially when dealing with large and evolving codebases.

---

## 94. What is the Stream API in Java?

The **Stream API** in Java, introduced in **Java 8**, provides a powerful and expressive way to process collections of objects in a functional programming style. It allows developers to perform complex data processing operations like filtering, mapping, sorting, and reducing in a declarative and concise way.

The Stream API provides a high-level abstraction for working with sequences of elements (like collections or arrays) and enables parallel processing, making it easier to work with large datasets.

### Key Concepts of the Stream API:

1. **Stream**:

* A **Stream** is a sequence of elements that supports various methods that can be used to perform operations on the data in a functional style.
* It doesn’t store data; instead, it operates on data from a **source** (such as a collection or array) lazily (i.e., only when needed).
* Streams can be **sequential** or **parallel** (for parallel processing).

2. **Pipeline**:

* Streams support the concept of a **pipeline**, which is a chain of operations applied to a stream.
* A pipeline consists of two types of operations:

    * **Intermediate Operations**: These are operations that return a new stream and are **lazy** (they do not execute until a terminal operation is invoked).
    * **Terminal Operations**: These operations trigger the processing of the stream and produce a result or a side-effect.

3. **Laziness**:

* Streams are **lazy** in nature. Intermediate operations are not executed until a terminal operation is invoked. This allows for optimized execution and can improve performance.

4. **Parallelism**:

* The Stream API allows you to parallelize your operations with minimal effort, making it easier to process large data sets concurrently using multiple threads.

### Key Operations in the Stream API:

#### 1. **Creating Streams**:

You can create streams from various data sources, such as collections, arrays, or generating elements.

Example:

* From a Collection (e.g., List):

  ```java
  List<String> list = Arrays.asList("apple", "banana", "cherry");
  Stream<String> stream = list.stream();
  ```

* From an Array:

  ```java
  String[] array = {"apple", "banana", "cherry"};
  Stream<String> streamFromArray = Arrays.stream(array);
  ```

* From a Range of Integers:

  ```java
  IntStream rangeStream = IntStream.range(1, 5); // produces 1, 2, 3, 4
  ```

#### 2. **Intermediate Operations**:

These operations transform a stream into another stream and are **lazy**. Some common intermediate operations include:

* **filter()**: Filters elements based on a condition.

  ```java
  List<String> filteredList = list.stream()
                                  .filter(s -> s.startsWith("b"))
                                  .collect(Collectors.toList()); // ["banana"]
  ```

* **map()**: Transforms each element in the stream by applying a function.

  ```java
  List<String> upperCaseList = list.stream()
                                   .map(String::toUpperCase)
                                   .collect(Collectors.toList()); // ["APPLE", "BANANA", "CHERRY"]
  ```

* **distinct()**: Removes duplicates from the stream.

  ```java
  List<String> distinctList = list.stream()
                                  .distinct()
                                  .collect(Collectors.toList());
  ```

* **sorted()**: Sorts the elements in the stream.

  ```java
  List<String> sortedList = list.stream()
                               .sorted()
                               .collect(Collectors.toList()); // ["apple", "banana", "cherry"]
  ```

* **flatMap()**: Flattens nested collections into a single stream.

  ```java
  List<List<String>> listOfLists = Arrays.asList(Arrays.asList("a", "b"), Arrays.asList("c", "d"));
  List<String> flatList = listOfLists.stream()
                                     .flatMap(Collection::stream)
                                     .collect(Collectors.toList()); // ["a", "b", "c", "d"]
  ```

#### 3. **Terminal Operations**:

Terminal operations are operations that produce a result or a side-effect. Some common terminal operations include:

* **collect()**: Collects the stream elements into a collection or other data structure.

  ```java
  List<String> collectedList = list.stream()
                                   .collect(Collectors.toList()); // Collects into a List
  ```

* **forEach()**: Performs an action for each element in the stream.

  ```java
  list.stream()
      .forEach(s -> System.out.println(s));  // prints each element
  ```

* **reduce()**: Reduces the stream elements into a single value (e.g., summing, concatenating).

  ```java
  int sum = list.stream()
                .mapToInt(String::length)
                .reduce(0, Integer::sum); // Sum of lengths of all strings
  ```

* **anyMatch()**, **allMatch()**, **noneMatch()**: Check whether any, all, or none of the elements satisfy a given condition.

  ```java
  boolean anyStartsWithB = list.stream()
                               .anyMatch(s -> s.startsWith("b")); // true
  ```

* **count()**: Counts the number of elements in the stream.

  ```java
  long count = list.stream().count(); // 3
  ```

* **findFirst()**, **findAny()**: Returns the first element or any element from the stream.

  ```java
  Optional<String> first = list.stream()
                               .findFirst(); // Optional[apple]
  ```

#### 4. **Working with Parallel Streams**:

You can easily process streams in parallel by using the `parallelStream()` method.

Example:

```java
List<String> largeList = Arrays.asList("apple", "banana", "cherry", "date", "elderberry");
largeList.parallelStream()
         .filter(s -> s.startsWith("b"))
         .forEach(System.out::println); // "banana"
```

* Parallel streams divide the work into multiple threads, potentially improving performance when working with large datasets.
* However, parallelism might introduce overhead, and for small datasets, sequential streams might be faster.

#### 5. **Optional**:

Streams can work with the `Optional` class to handle missing or null values safely, which is especially useful when performing operations like `findFirst()`, `findAny()`, etc.

Example:

```java
Optional<String> first = list.stream()
                             .filter(s -> s.startsWith("z"))
                             .findFirst();
first.ifPresent(System.out::println); // No output (optional is empty)
```

### Example of Stream Operations:

Here is an example of how the Stream API can be used to process data:

```java
import java.util.*;
import java.util.stream.*;

public class StreamExample {
    public static void main(String[] args) {
        List<String> fruits = Arrays.asList("apple", "banana", "cherry", "date", "elderberry");

        List<String> result = fruits.stream()
                                    .filter(s -> s.length() > 5)  // filter strings with length > 5
                                    .map(String::toUpperCase)     // convert to uppercase
                                    .sorted()                     // sort alphabetically
                                    .collect(Collectors.toList());  // collect as a list

        result.forEach(System.out::println); // Output: BANANA, CHERRY, ELDERBERRY
    }
}
```

### Benefits of the Stream API:

1. **Declarative Style**: The Stream API allows you to write code in a more declarative manner, focusing on what to do with data instead of how to do it. This leads to more readable and maintainable code.
2. **Parallel Processing**: The Stream API provides easy-to-use methods to process data in parallel, which can lead to performance improvements in certain cases, especially for large datasets.
3. **Lazy Evaluation**: Stream operations are lazy, meaning they are only evaluated when a terminal operation is invoked. This helps to improve performance and allows for optimizations like short-circuiting operations.
4. **Functional Programming Support**: The Stream API encourages a functional programming style, making it easier to compose operations, pass behavior as arguments (using lambda expressions), and handle immutable data.

### Conclusion:

The **Stream API** in Java provides a modern, functional-style approach to processing sequences of elements. It simplifies complex operations, such as filtering, mapping, and reducing, in a more declarative way, while also enabling parallel execution and laziness. The Stream API helps make your Java code more expressive, efficient, and easier to read.

---

## 95. What are intermediate and terminal operations in streams?

In the **Stream API** in Java, operations on streams are divided into two categories: **intermediate operations** and **terminal operations**. These operations are used to manipulate and process the elements of a stream in different ways.

### 1. **Intermediate Operations**:

* **Definition**: Intermediate operations are operations that transform a stream into another stream. These operations are **lazy**, meaning they are not executed until a terminal operation is invoked. They only define the transformation logic but do not trigger the computation themselves.
* **Characteristics**:

    * **Lazy evaluation**: Intermediate operations are not executed immediately; they are deferred until a terminal operation is executed.
    * They return a new stream, allowing them to be chained together (resulting in a pipeline of operations).
    * Intermediate operations are **non-interfering**, meaning they do not modify the original stream but instead return a new stream with modified content.

**Common Intermediate Operations**:

* **filter()**: Filters elements based on a predicate (condition).

  ```java
  Stream<String> filteredStream = stream.filter(s -> s.startsWith("a"));
  ```
* **map()**: Transforms each element in the stream by applying a function.

  ```java
  Stream<Integer> lengthStream = stream.map(String::length);
  ```
* **distinct()**: Returns a stream with duplicate elements removed.

  ```java
  Stream<String> distinctStream = stream.distinct();
  ```
* **sorted()**: Sorts the elements in the stream.

  ```java
  Stream<String> sortedStream = stream.sorted();
  ```
* **flatMap()**: Flattens nested collections into a single stream.

  ```java
  Stream<String> flatStream = nestedList.stream().flatMap(Collection::stream);
  ```
* **peek()**: Performs an action on each element of the stream without modifying the stream. It’s useful for debugging.

  ```java
  stream.peek(System.out::println).map(String::toUpperCase);
  ```

**Example**:

```java
List<String> fruits = Arrays.asList("apple", "banana", "cherry", "date");
List<String> result = fruits.stream()
                            .filter(fruit -> fruit.length() > 5)  // intermediate
                            .map(String::toUpperCase)             // intermediate
                            .collect(Collectors.toList());        // terminal
```

### 2. **Terminal Operations**:

* **Definition**: Terminal operations are operations that produce a result or a side-effect. Once a terminal operation is invoked, the stream is **consumed** and cannot be reused. Terminal operations trigger the processing of the stream and produce a result, such as a collection or a boolean value.
* **Characteristics**:

    * **Eager evaluation**: Terminal operations trigger the actual computation and cause the stream to be processed.
    * They typically result in a **non-stream result**, such as a collection, a primitive value, or a side effect.
    * After a terminal operation is invoked, the stream is considered closed and can no longer be used.

**Common Terminal Operations**:

* **collect()**: Collects the stream elements into a collection (e.g., List, Set).

  ```java
  List<String> list = stream.collect(Collectors.toList());
  ```
* **forEach()**: Performs an action for each element in the stream.

  ```java
  stream.forEach(System.out::println);
  ```
* **reduce()**: Reduces the elements in the stream to a single value using an associative accumulation function.

  ```java
  int sum = stream.mapToInt(Integer::parseInt).reduce(0, Integer::sum);
  ```
* **count()**: Returns the number of elements in the stream.

  ```java
  long count = stream.count();
  ```
* **anyMatch()**, **allMatch()**, **noneMatch()**: Checks whether any, all, or none of the elements match a given predicate.

  ```java
  boolean anyStartsWithA = stream.anyMatch(s -> s.startsWith("a"));
  ```
* **findFirst()**: Returns the first element of the stream.

  ```java
  Optional<String> first = stream.findFirst();
  ```
* **findAny()**: Returns any element from the stream (often used in parallel streams).

  ```java
  Optional<String> any = stream.findAny();
  ```

**Example**:

```java
List<String> fruits = Arrays.asList("apple", "banana", "cherry", "date");
long count = fruits.stream()
                   .filter(fruit -> fruit.length() > 5)  // intermediate
                   .count();                             // terminal
```

### **Key Differences**:

| **Intermediate Operations**                             | **Terminal Operations**                             |
| ------------------------------------------------------- | --------------------------------------------------- |
| Return a new stream                                     | Return a non-stream result                          |
| Lazy evaluation (not executed until terminal operation) | Eager evaluation (triggers stream processing)       |
| Can be chained together                                 | Consumes the stream (cannot be reused)              |
| Do not modify the source data                           | May modify the source data or produce a side-effect |

### **Example of Intermediate and Terminal Operations**:

```java
import java.util.*;
import java.util.stream.*;

public class StreamOperationsExample {
    public static void main(String[] args) {
        List<String> fruits = Arrays.asList("apple", "banana", "cherry", "date", "elderberry");

        // Intermediate operations
        List<String> result = fruits.stream()
                                    .filter(fruit -> fruit.length() > 5) // filter: intermediate
                                    .map(String::toUpperCase)            // map: intermediate
                                    .sorted()                            // sorted: intermediate
                                    .collect(Collectors.toList());       // collect: terminal

        // Output the result
        result.forEach(System.out::println);  // Output: BANANA, CHERRY, ELDERBERRY
    }
}
```

### Conclusion:

* **Intermediate operations** modify the stream lazily and return a new stream that can be chained.
* **Terminal operations** trigger the actual computation of the stream and return a final result (such as a collection, count, or side-effect).

By understanding the distinction between these two types of operations, you can effectively process and transform data using Java’s Stream API.

---

## 96. What is Optional and how is it used?

In Java, the `Optional` class is a container that may or may not contain a non-null value. It is used to represent the presence or absence of a value and is part of the `java.util` package, introduced in **Java 8**. The main purpose of `Optional` is to reduce the use of `null` references, which can lead to `NullPointerException` and to make the code more readable and expressive.

### Why use `Optional`?

1. **Avoiding NullPointerException**: By using `Optional`, you explicitly indicate the possibility of a value being absent, which makes it easier to handle cases where values are missing (e.g., empty results from a method).
2. **Improved Readability**: The use of `Optional` in method signatures clearly expresses that a method might not return a value. This improves the readability and clarity of the code.

### **Creating Optional**

There are several ways to create an `Optional` instance:

1. **Optional.of(T value)**: Returns an `Optional` containing the given non-null value. If the value is `null`, it throws a `NullPointerException`.

   ```java
   Optional<String> name = Optional.of("John");
   ```

2. **Optional.ofNullable(T value)**: Returns an `Optional` containing the given value, or an empty `Optional` if the value is `null`.

   ```java
   Optional<String> name = Optional.ofNullable("John");
   Optional<String> emptyName = Optional.ofNullable(null);  // Empty Optional
   ```

3. **Optional.empty()**: Returns an empty `Optional`, which represents the absence of a value.

   ```java
   Optional<String> empty = Optional.empty();
   ```

### **Methods in Optional**

`Optional` provides several useful methods to work with values safely.

1. **isPresent()**: Checks if the value is present.

   ```java
   Optional<String> name = Optional.of("John");
   if (name.isPresent()) {
       System.out.println(name.get());  // Prints: John
   }
   ```

2. **ifPresent(Consumer\<? super T> action)**: If the value is present, it performs the given action. This eliminates the need for `if` statements to check for null values.

   ```java
   Optional<String> name = Optional.of("John");
   name.ifPresent(n -> System.out.println(n));  // Prints: John
   ```

3. **get()**: Returns the value if present, otherwise throws `NoSuchElementException`. It is recommended to avoid using `get()` unless you are sure the value is present.

   ```java
   Optional<String> name = Optional.of("John");
   System.out.println(name.get());  // Prints: John
   ```

4. **orElse(T other)**: Returns the value if present, otherwise returns the specified default value.

   ```java
   Optional<String> name = Optional.ofNullable(null);
   String defaultName = name.orElse("Default Name");
   System.out.println(defaultName);  // Prints: Default Name
   ```

5. **orElseGet(Supplier\<? extends T> other)**: Returns the value if present, otherwise returns the result of the provided supplier function. This is useful if the default value is expensive to compute.

   ```java
   Optional<String> name = Optional.ofNullable(null);
   String defaultName = name.orElseGet(() -> "Computed Default Name");
   System.out.println(defaultName);  // Prints: Computed Default Name
   ```

6. **orElseThrow(Supplier\<? extends X> exceptionSupplier)**: Returns the value if present, otherwise throws the exception provided by the supplier.

   ```java
   Optional<String> name = Optional.ofNullable(null);
   String nameValue = name.orElseThrow(() -> new IllegalArgumentException("Name is required"));
   ```

7. **map(Function\<? super T, ? extends U> mapper)**: If the value is present, applies the provided mapping function and returns an `Optional` of the result. If the value is not present, it returns an empty `Optional`.

   ```java
   Optional<String> name = Optional.of("John");
   Optional<Integer> nameLength = name.map(String::length);
   System.out.println(nameLength.get());  // Prints: 4
   ```

8. **flatMap(Function\<? super T, Optional<U>> mapper)**: Similar to `map()`, but the mapping function must return an `Optional`. It avoids nested `Optional`s.

   ```java
   Optional<String> name = Optional.of("John");
   Optional<String> upperCaseName = name.flatMap(n -> Optional.of(n.toUpperCase()));
   System.out.println(upperCaseName.get());  // Prints: JOHN
   ```

9. **filter(Predicate\<? super T> predicate)**: If the value is present and satisfies the given predicate, it returns the `Optional` with the value; otherwise, it returns an empty `Optional`.

   ```java
   Optional<String> name = Optional.of("John");
   Optional<String> filteredName = name.filter(n -> n.startsWith("J"));
   System.out.println(filteredName.get());  // Prints: John
   ```

### **Example of Using `Optional`**

Here’s a simple example demonstrating how to use `Optional` in a Java method:

```java
import java.util.Optional;

public class OptionalExample {

    public static void main(String[] args) {
        // Create Optional instances
        Optional<String> name = Optional.of("John");
        Optional<String> emptyName = Optional.ofNullable(null);

        // Example with isPresent() and get()
        if (name.isPresent()) {
            System.out.println(name.get());  // Prints: John
        }

        // Example with ifPresent()
        emptyName.ifPresent(n -> System.out.println(n));  // No output

        // Using orElse() for default value
        String defaultName = emptyName.orElse("Default Name");
        System.out.println(defaultName);  // Prints: Default Name

        // Using map() to transform the value
        Optional<Integer> length = name.map(String::length);
        length.ifPresent(System.out::println);  // Prints: 4

        // Using filter() to filter based on a condition
        Optional<String> filteredName = name.filter(n -> n.startsWith("J"));
        filteredName.ifPresent(System.out::println);  // Prints: John
    }
}
```

### **When to Use `Optional`?**

* **Return Type**: It is best to use `Optional` as the return type for methods that might not have a value to return (e.g., methods returning `null` if a value is not found).
* **Avoiding Null Checks**: Use `Optional` to avoid having to check for `null` explicitly and to make your code more readable.
* **Avoiding NPE (NullPointerException)**: By providing an explicit alternative (such as `orElse()` or `orElseGet()`), you can prevent potential null pointer exceptions.

### **When Not to Use `Optional`?**

* **Avoid in fields or method parameters**: `Optional` should not be used as fields or parameters in most cases. It's meant for return types where you need to express the possibility of "no value." Using `Optional` as a field type can lead to unnecessary overhead.
* **In Performance-Critical Code**: `Optional` introduces additional abstraction and overhead. In highly performance-sensitive applications, using `Optional` for every null check might introduce some overhead.

### **Conclusion**:

`Optional` is a powerful feature of Java that helps in handling the absence of values in a cleaner way, avoiding null checks and reducing `NullPointerExceptions`. It provides a variety of methods like `isPresent()`, `ifPresent()`, `orElse()`, `map()`, and `flatMap()` to handle values in a more functional and declarative style.

---

## 97. What is method reference in Java?

In Java, **method reference** is a shorthand notation to call a method directly using the method's name. It is used to refer to a method of a class or an instance of a class without invoking it. Method references are primarily used to simplify the syntax when using **lambda expressions**. They provide a clear and concise way to pass methods as arguments to higher-order functions.

Method references are a more readable and compact alternative to lambda expressions. They were introduced in **Java 8** as part of the functional programming features, and they allow you to use existing methods in place of lambda expressions.

### **Syntax of Method References**

Method references have the following syntax:

```java
ClassName::methodName
```

There are four types of method references in Java:

### 1. **Reference to a Static Method**

A static method reference refers to a static method of a class. The syntax for this is:

```java
ClassName::staticMethodName
```

**Example**:

```java
class MathOperations {
    public static int square(int number) {
        return number * number;
    }
}

public class MethodReferenceExample {
    public static void main(String[] args) {
        // Using method reference for static method
        Function<Integer, Integer> squareFunction = MathOperations::square;
        System.out.println(squareFunction.apply(5));  // Output: 25
    }
}
```

### 2. **Reference to an Instance Method of an Object**

This type of method reference refers to an instance method of an object. The syntax is:

```java
instanceObject::instanceMethodName
```

**Example**:

```java
class StringOperations {
    public String toUpperCase(String str) {
        return str.toUpperCase();
    }
}

public class MethodReferenceExample {
    public static void main(String[] args) {
        StringOperations operations = new StringOperations();
        // Using method reference for instance method
        Function<String, String> upperCaseFunction = operations::toUpperCase;
        System.out.println(upperCaseFunction.apply("hello"));  // Output: HELLO
    }
}
```

### 3. **Reference to an Instance Method of an Arbitrary Object**

This method reference refers to an instance method of an arbitrary object of a particular type. This is often used in **streams** and other collection operations, where a method is applied to each element of a collection. The syntax is:

```java
ClassName::instanceMethodName
```

**Example**:

```java
import java.util.Arrays;
import java.util.List;

public class MethodReferenceExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
        // Using method reference to refer to instance method of String
        names.forEach(System.out::println);
    }
}
```

Here, `System.out::println` is a method reference to the `println` method of `System.out`.

### 4. **Reference to a Constructor**

A constructor reference refers to a constructor of a class. The syntax is:

```java
ClassName::new
```

Constructor references are used to create new instances of a class. This is useful in situations like when you need to create objects for a stream or a collection.

**Example**:

```java
import java.util.function.Supplier;

class Person {
    private String name;

    public Person(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}

public class MethodReferenceExample {
    public static void main(String[] args) {
        // Using method reference for constructor
        Supplier<Person> personSupplier = Person::new;
        Person person = personSupplier.get();  // Calls the default constructor
        System.out.println(person.getName());  // Output: null (since name is not initialized)
    }
}
```

You can also use constructor references when working with collection frameworks like `List`, `Stream`, etc.

**Example with Streams**:

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class MethodReferenceExample {
    public static void main(String[] args) {
        // Using method reference for constructor
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
        List<Person> people = names.stream()
                                    .map(Person::new)  // Calls the constructor Person(String name)
                                    .collect(Collectors.toList());
        people.forEach(person -> System.out.println(person.getName()));
    }
}
```

### **Key Points to Remember:**

* **Method references** are a shorthand way to invoke methods and can be used in place of lambda expressions.
* They are used to improve the readability and clarity of the code by eliminating boilerplate code.
* They are often used in functional interfaces, especially in methods like `map()`, `filter()`, `forEach()`, etc., commonly used with Java Streams.
* There are four types of method references: static methods, instance methods of a particular object, instance methods of arbitrary objects, and constructor references.

### **Comparison: Method Reference vs Lambda Expression**

Here is how a method reference compares to a lambda expression:

1. **Lambda Expression**:

   ```java
   Function<String, Integer> stringLength = s -> s.length();
   ```

2. **Method Reference**:

   ```java
   Function<String, Integer> stringLength = String::length;
   ```

In the above example, both the lambda expression and the method reference do the same thing: return the length of a string. The method reference is more concise and can be preferred when it enhances code readability.

---

## 98. What is the use of `Collectors.toList()`?

In Java, `Collectors.toList()` is a **Collector** implementation that collects the elements of a stream into a **List**. It is part of the **Java Stream API** and is used in combination with the `collect()` method to accumulate the elements of a stream into a collection.

### **Usage of `Collectors.toList()`**

`Collectors.toList()` is typically used when you want to collect the elements of a stream into a `List`. The `collect()` method in a stream allows you to transform the elements of the stream into a different form, such as a collection, a single value, or a map. `Collectors.toList()` specifically collects the elements into a new **ArrayList**.

### **Syntax**

```java
List<T> list = stream.collect(Collectors.toList());
```

Where:

* `stream` is the Stream from which you want to collect the elements.
* `Collectors.toList()` returns a **Collector** that accumulates the stream's elements into a **List**.

### **Example**

Here is a simple example that demonstrates how `Collectors.toList()` is used:

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class CollectorsExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("John", "Alice", "Bob", "Charlie");

        // Using Collectors.toList() to collect stream elements into a List
        List<String> filteredNames = names.stream()
                                          .filter(name -> name.length() > 3) // Filter names with length > 3
                                          .collect(Collectors.toList());

        // Output the collected list
        System.out.println(filteredNames);  // Output: [John, Alice, Charlie]
    }
}
```

### **Explanation:**

1. `names.stream()` creates a stream from the list of names.
2. `.filter(name -> name.length() > 3)` filters out names that have fewer than 4 characters.
3. `.collect(Collectors.toList())` collects the filtered names into a new `List` and returns it.

In this case, the result is a new `List<String>` containing the names `"John"`, `"Alice"`, and `"Charlie"`.

### **Benefits of Using `Collectors.toList()`**

* **Simplicity**: It allows you to collect elements from a stream into a `List` with minimal code.
* **Convenience**: It works well with other stream operations like `map()`, `filter()`, `reduce()`, etc.
* **Immutability**: It is useful when you want to return a list from a stream processing pipeline.

### **Internals**

Internally, `Collectors.toList()` uses a **Supplier** (an ArrayList) to collect the stream elements into a list. It’s a very efficient and common use case when you want to transform a stream into a collection of elements.

```java
Collector<T, ?, List<T>> toList = Collectors.toList();
```

### **Other Collectors**

While `Collectors.toList()` is used to collect elements into a `List`, the Stream API provides other collectors for different purposes, such as:

* `Collectors.toSet()` to collect elements into a `Set`.
* `Collectors.toMap()` to collect elements into a `Map`.
* `Collectors.joining()` to concatenate elements into a single String.

### **Conclusion**

`Collectors.toList()` is a powerful and convenient utility that helps in transforming streams into `List` objects. It's commonly used in functional-style programming with streams, simplifying the collection of stream elements into a list.

---

## 99. What are predicates and consumers in Java?

In Java, **Predicates** and **Consumers** are functional interfaces that are commonly used in the **Stream API** and **Lambda expressions**. They represent specific kinds of functions that are used to operate on data in a functional programming style.

### 1. **Predicate**

A **Predicate** is a functional interface that represents a boolean-valued function (a function that returns `true` or `false`). It is typically used to test conditions, such as checking if a given element satisfies a certain condition. It is used in situations where you want to evaluate a condition on an object.

#### **Syntax of Predicate**

```java
@FunctionalInterface
public interface Predicate<T> {
    boolean test(T t);
}
```

Where:

* `T` is the type of the input to the predicate.
* `test(T t)` is the method that takes an object of type `T` and returns a boolean value.

### **Example: Predicate**

```java
import java.util.function.Predicate;

public class PredicateExample {
    public static void main(String[] args) {
        // Predicate to check if a number is even
        Predicate<Integer> isEven = n -> n % 2 == 0;

        System.out.println(isEven.test(4));  // Output: true
        System.out.println(isEven.test(5));  // Output: false
    }
}
```

### **Common Methods in Predicate:**

* `test(T t)`: Tests if the predicate holds true for the given input.
* `and(Predicate<? super T> other)`: Combines two predicates using a logical AND.
* `or(Predicate<? super T> other)`: Combines two predicates using a logical OR.
* `negate()`: Returns a predicate that negates the result of the current predicate.

### **Example: Chaining Predicates**

```java
import java.util.function.Predicate;

public class PredicateExample {
    public static void main(String[] args) {
        Predicate<Integer> isEven = n -> n % 2 == 0;
        Predicate<Integer> isGreaterThan10 = n -> n > 10;

        // Using and() to combine conditions
        Predicate<Integer> isEvenAndGreaterThan10 = isEven.and(isGreaterThan10);

        System.out.println(isEvenAndGreaterThan10.test(12));  // Output: true
        System.out.println(isEvenAndGreaterThan10.test(8));   // Output: false
    }
}
```

### 2. **Consumer**

A **Consumer** is a functional interface that represents an operation that takes a single input argument and returns no result. It is used when you want to perform some action on an object but don't need to return any result.

#### **Syntax of Consumer**

```java
@FunctionalInterface
public interface Consumer<T> {
    void accept(T t);
}
```

Where:

* `T` is the type of the input to the consumer.
* `accept(T t)` is the method that takes an object of type `T` and performs an operation on it (does not return anything).

### **Example: Consumer**

```java
import java.util.function.Consumer;

public class ConsumerExample {
    public static void main(String[] args) {
        // Consumer to print a string
        Consumer<String> printMessage = message -> System.out.println(message);

        printMessage.accept("Hello, World!");  // Output: Hello, World!
    }
}
```

### **Common Methods in Consumer:**

* `accept(T t)`: Performs the operation on the given input.
* `andThen(Consumer<? super T> after)`: Returns a composed Consumer that first applies the current operation and then the `after` operation.

### **Example: Chaining Consumers**

```java
import java.util.function.Consumer;

public class ConsumerExample {
    public static void main(String[] args) {
        Consumer<String> printUpperCase = str -> System.out.println(str.toUpperCase());
        Consumer<String> printLowerCase = str -> System.out.println(str.toLowerCase());

        // Chaining two consumers
        printUpperCase.andThen(printLowerCase).accept("Hello");
        // Output: 
        // HELLO
        // hello
    }
}
```

### **Differences Between Predicate and Consumer:**

| Aspect           | Predicate                               | Consumer                                         |
| ---------------- | --------------------------------------- | ------------------------------------------------ |
| **Purpose**      | Tests a condition and returns `boolean` | Performs an action, no return value              |
| **Return Value** | Returns `boolean` (true or false)       | Returns `void` (no return value)                 |
| **Usage**        | Used in filtering, matching, conditions | Used for side-effects (e.g., printing, updating) |
| **Method Name**  | `test()`                                | `accept()`                                       |

### **Summary:**

* **Predicate** is used when you want to evaluate a condition or check if something is true or false for a given object. It returns a boolean value and is useful in filtering or checking conditions (like with the `filter()` method in streams).
* **Consumer** is used when you want to perform an action on an object without returning any result. It is often used in scenarios like applying actions to each element of a collection (e.g., with the `forEach()` method in streams).

Both of these functional interfaces are part of the `java.util.function` package and play a significant role in functional programming features in Java.

---

## 100. How does Java support functional programming?

Java supports **functional programming** (FP) through several features that were introduced starting from **Java 8**. These features allow developers to write code in a more declarative style, focusing on **what** to do rather than **how** to do it. Java's support for FP is mostly centered around the **Stream API**, **lambda expressions**, **functional interfaces**, and related features.

Here are the main ways Java supports functional programming:

### 1. **Lambda Expressions**

Lambda expressions allow you to write anonymous functions (i.e., functions without a name) in a concise way. They enable functional programming by treating behavior as a parameter, enabling **higher-order functions**.

#### **Syntax of Lambda Expression:**

```java
(parameters) -> expression
```

Example:

```java
// A lambda expression that adds two numbers
(int a, int b) -> a + b;
```

Lambda expressions are often used to pass behavior as arguments to methods or to define behavior in functional interfaces.

### 2. **Functional Interfaces**

A **functional interface** is an interface with just one abstract method. These interfaces are the foundation of lambda expressions. Java provides several built-in functional interfaces in the `java.util.function` package, such as:

* `Predicate<T>`
* `Function<T, R>`
* `Consumer<T>`
* `Supplier<T>`
* `UnaryOperator<T>`
* `BinaryOperator<T>`

These functional interfaces can be used with lambda expressions and method references.

#### **Example:**

```java
import java.util.function.Function;

public class FunctionalInterfaceExample {
    public static void main(String[] args) {
        // A lambda expression that implements the Function interface
        Function<Integer, String> intToString = (Integer i) -> "Number: " + i;

        // Using the lambda
        System.out.println(intToString.apply(5));  // Output: Number: 5
    }
}
```

### 3. **Stream API**

The **Stream API** allows you to process sequences of elements (like collections) in a declarative manner, enabling functional-style operations like filtering, mapping, and reducing.

With the Stream API, you can write code that expresses **what to do** with the data (e.g., filter, map, reduce) instead of how to do it (e.g., using loops).

#### **Common Stream Operations:**

* **Intermediate operations** (e.g., `map()`, `filter()`, `distinct()`) are lazy and return a new stream.
* **Terminal operations** (e.g., `collect()`, `forEach()`, `reduce()`) trigger the processing of the stream.

#### **Example: Stream API**

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class StreamExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        // Using stream operations (filter, map, collect)
        List<Integer> squaredNumbers = numbers.stream()
                                               .filter(n -> n % 2 == 0) // Filtering even numbers
                                               .map(n -> n * n)          // Squaring the numbers
                                               .collect(Collectors.toList()); // Collecting results into a list

        System.out.println(squaredNumbers);  // Output: [4, 16]
    }
}
```

### 4. **Method References**

Method references provide a way to refer to methods (either static or instance) directly without using a lambda expression. They make code more concise and readable.

#### **Syntax of Method Reference:**

```java
ClassName::methodName
```

Example:

```java
import java.util.Arrays;
import java.util.List;

public class MethodReferenceExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        // Using method reference to print each name
        names.forEach(System.out::println);
    }
}
```

### 5. **Optional Class**

The `Optional<T>` class is a container for a value that may or may not be present. It is used to avoid **NullPointerExceptions** by providing a way to handle optional values without explicitly checking for `null`.

#### **Example:**

```java
import java.util.Optional;

public class OptionalExample {
    public static void main(String[] args) {
        Optional<String> optionalName = Optional.ofNullable("John");

        // Using map and ifPresent
        optionalName.map(String::toUpperCase)
                    .ifPresent(System.out::println);  // Output: JOHN
    }
}
```

### 6. **Default and Static Methods in Interfaces**

Java 8 introduced **default methods** and **static methods** in interfaces, enabling you to add behavior to interfaces without breaking backward compatibility.

* **Default Methods**: Can have method implementations in interfaces. These are useful for providing common functionality.
* **Static Methods**: Can be used to define utility methods that are tied to the interface itself.

#### **Example:**

```java
interface MyInterface {
    // Default method
    default void greet() {
        System.out.println("Hello!");
    }

    // Static method
    static void sayGoodbye() {
        System.out.println("Goodbye!");
    }
}

public class DefaultMethodExample {
    public static void main(String[] args) {
        MyInterface.sayGoodbye();  // Calling static method
        MyInterface obj = new MyInterface() {};  // Anonymous class
        obj.greet();  // Calling default method
    }
}
```

### 7. **Functional Programming in Collections**

Java collections (e.g., `List`, `Set`, `Map`) can be processed in a functional way using the **Stream API**, and operations like `filter()`, `map()`, `reduce()`, `forEach()`, and others allow for functional-style processing on collections.

#### **Example:**

```java
import java.util.List;
import java.util.Arrays;

public class FunctionalCollectionsExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("John", "Alice", "Bob", "Charlie");

        // Using Stream API to process collections
        names.stream()
             .filter(name -> name.startsWith("A"))  // Filter names that start with "A"
             .map(String::toUpperCase)              // Convert to uppercase
             .forEach(System.out::println);         // Print the names
    }
}
```

### 8. **Immutability**

In functional programming, immutability is key. Java provides **`final`** variables to prevent reassignment and has immutable collections (like `List.of()`, `Set.of()`, and `Map.of()` introduced in Java 9). These are commonly used in FP-style programming to avoid state changes.

### 9. **Recursion**

Functional programming often makes use of recursion, as it is an alternative to iteration. Java allows recursion in methods, though it should be used carefully, as excessive recursion can lead to a **stack overflow** error. Java also has **tail recursion optimization** in some cases (though not as built-in as some functional programming languages).

---

### **Summary of Functional Programming Features in Java**

* **Lambda Expressions**: Concise way to represent anonymous functions.
* **Functional Interfaces**: Interfaces with a single abstract method, essential for lambda expressions.
* **Stream API**: Allows for functional-style operations on collections.
* **Method References**: Provides shorthand for referring to methods.
* **Optional**: Avoids null checks and prevents `NullPointerException`.
* **Default and Static Methods in Interfaces**: Allows adding functionality to interfaces.
* **Immutability**: Encourages working with immutable data structures.
* **Higher-Order Functions**: Functions that accept other functions as parameters or return them.

By combining these features, Java allows developers to write code in a more functional style, promoting **declarative** programming, **side-effect-free** operations, and **clearer** data processing pipelines.

---