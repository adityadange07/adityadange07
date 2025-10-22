# LEVEL 1: BEGINNER (0-2 Years Experience)

# Core Java Fundamental

# Basic Concepts

---

## 1. What is the difference between JDK, JVM and JRE

---

### **1️⃣ JDK (Java Development Kit)**

**Purpose:** It’s used to **develop and compile Java applications**.

* **Includes:**
  ✅ JRE (Java Runtime Environment)
  ✅ Development tools like `javac` (compiler), `javadoc`, `jar`, `debugger`, etc.
* **Who uses it:** Developers who write Java code.

**Example:**
When you write a `.java` file, JDK compiles it into a `.class` file using the **Java Compiler (javac)**.

**In short:**

> JDK = JRE + Development Tools

---

### **2️⃣ JRE (Java Runtime Environment)**

**Purpose:** It provides the **environment to run Java applications**.

* **Includes:**
  ✅ JVM (Java Virtual Machine)
  ✅ Core libraries (like `java.lang`, `java.util`, etc.)
  ✅ Other runtime components

**Who uses it:** End users who want to **run** a Java program but not develop it.

**In short:**

> JRE = JVM + Libraries (for runtime)

---

### **3️⃣ JVM (Java Virtual Machine)**

**Purpose:** It’s the **engine that actually runs your Java bytecode**.

* **Responsibilities:**

  * Converts bytecode to machine code (Just-In-Time compilation)
  * Provides **platform independence**
  * Handles memory management (Heap, Stack)
  * Performs garbage collection
  * Ensures security and portability

**In short:**

> JVM = The heart of Java — it executes `.class` (bytecode) files.

---

### ⚙️ **Relationship Diagram**

```
JDK
 ├── JRE
 │    ├── JVM
 │    └── Core Libraries
 └── Development Tools (javac, jar, etc.)
```

---

### **🧠 Summary Table**

| Component | Full Form                | Contains         | Used For             | Used By    |
| --------- | ------------------------ | ---------------- | -------------------- | ---------- |
| **JDK**   | Java Development Kit     | JRE + dev tools  | Developing Java apps | Developers |
| **JRE**   | Java Runtime Environment | JVM + libraries  | Running Java apps    | Users      |
| **JVM**   | Java Virtual Machine     | Execution engine | Executing bytecode   | System     |

---


## 2. What are the main features of JAVA (OOP Principles)?

---

## 🧠 **Main Features of Java (OOP Principles)**

Java is an **Object-Oriented Programming (OOP)** language — it’s built around the concept of **objects and classes**.

The **four main OOP principles** (often remembered as **A PIE**) are:

> **A → Abstraction**
> **P → Polymorphism**
> **I → Inheritance**
> **E → Encapsulation**

---

### 🔹 1. **Abstraction**

**Definition:**
Hiding complex implementation details and showing only the essential features of an object.

**Example:**
When you call `car.start()`, you don’t know what happens inside the engine — you just use the method.

**In Java:**

* Achieved using **Abstract classes** (`abstract`) and **Interfaces**.

**Example Code:**

```java
abstract class Vehicle {
    abstract void start();
}

class Car extends Vehicle {
    void start() {
        System.out.println("Car starts with a key");
    }
}
```

---

### 🔹 2. **Encapsulation**

**Definition:**
Wrapping data (variables) and code (methods) together into a single unit — a **class**, and restricting direct access to data.

**In Java:**

* Achieved using **private variables** and **public getters/setters**.

**Benefits:**
✅ Data hiding
✅ Better control over data
✅ Maintainability

**Example Code:**

```java
class Employee {
    private int salary;

    public void setSalary(int salary) {
        this.salary = salary;
    }

    public int getSalary() {
        return salary;
    }
}
```

---

### 🔹 3. **Inheritance**

**Definition:**
Allows one class (child/subclass) to **inherit** the fields and methods of another class (parent/superclass).

**In Java:**

* Achieved using the **`extends`** keyword.
* Promotes **code reusability**.

**Example Code:**

```java
class Animal {
    void eat() { System.out.println("Eating"); }
}

class Dog extends Animal {
    void bark() { System.out.println("Barking"); }
}
```

✅ `Dog` inherits `eat()` method from `Animal`.

---

### 🔹 4. **Polymorphism**

**Definition:**
The ability of an object to take **many forms** — same method name behaves differently depending on the object.

**Types:**

1. **Compile-time Polymorphism** → Method Overloading
2. **Runtime Polymorphism** → Method Overriding

**Example Code:**

```java
// Compile-time (Overloading)
class MathUtil {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
}

// Runtime (Overriding)
class Animal {
    void sound() { System.out.println("Animal sound"); }
}
class Dog extends Animal {
    void sound() { System.out.println("Bark"); }
}
```

---

## 🧩 **Bonus: Other Key Features of Java**

Besides OOP, Java also offers several other core features:

| Feature                  | Description                              |
| ------------------------ | ---------------------------------------- |
| **Platform Independent** | Write Once, Run Anywhere (thanks to JVM) |
| **Simple & Secure**      | No pointers, strong memory management    |
| **Robust**               | Exception handling & memory management   |
| **Multithreaded**        | Supports concurrent execution            |
| **Portable**             | Bytecode can run on any platform         |
| **Distributed**          | Supports RMI and web-based applications  |
| **High Performance**     | Uses Just-In-Time (JIT) compiler         |
| **Dynamic**              | Loads classes dynamically at runtime     |

---

### 🧠 **Summary Tip for Interviews**

> Java’s OOP principles are: **Abstraction, Encapsulation, Inheritance, Polymorphism**.
> They help achieve **modularity, reusability, and maintainability** in object-oriented software.

---

## 3. What are primitive data types in Java?

---

## 🧠 **Primitive Data Types in Java**

Java has **8 primitive data types** — these are **predefined by the language** and **store simple values directly in memory** (not objects).

They are grouped into **4 categories:**

| Category                     | Data Type | Size              | Default Value | Example                  |
| ---------------------------- | --------- | ----------------- | ------------- | ------------------------ |
| **1️⃣ Integer Types**        | byte      | 1 byte (8 bits)   | 0             | `byte b = 100;`          |
|                              | short     | 2 bytes (16 bits) | 0             | `short s = 1000;`        |
|                              | int       | 4 bytes (32 bits) | 0             | `int i = 100000;`        |
|                              | long      | 8 bytes (64 bits) | 0L            | `long l = 10000000000L;` |
| **2️⃣ Floating-Point Types** | float     | 4 bytes           | 0.0f          | `float f = 10.5f;`       |
|                              | double    | 8 bytes           | 0.0d          | `double d = 99.99;`      |
| **3️⃣ Character Type**       | char      | 2 bytes (Unicode) | '\u0000'      | `char c = 'A';`          |
| **4️⃣ Boolean Type**         | boolean   | 1 bit (logical)   | false         | `boolean flag = true;`   |

---

### 🔹 **Explanation of Each:**

#### 1. **byte**

* Smallest integer type
* Useful for saving memory (like arrays in large data sets)
* Range: **-128 to 127**

#### 2. **short**

* Larger than byte but smaller than int
* Range: **-32,768 to 32,767**

#### 3. **int**

* Default integer type in Java
* Range: **-2³¹ to 2³¹-1**

#### 4. **long**

* Used when int is not enough for large numbers
* Must add `L` at the end → `long l = 123456789L;`

#### 5. **float**

* Single precision decimal number
* Must add `f` at the end → `float f = 12.34f;`

#### 6. **double**

* Double precision decimal number (default for decimals)

#### 7. **char**

* Used to store **a single character or Unicode value**
* Example: `'A'`, `'9'`, or `'\u0041'` (Unicode for A)

#### 8. **boolean**

* Represents **true or false**
* Used in conditions and control statements

---

### 🧩 **Primitive vs Non-Primitive**

| Primitive                     | Non-Primitive                   |
| ----------------------------- | ------------------------------- |
| Predefined by Java            | Created by programmer           |
| Stores simple values          | Stores objects or references    |
| Example: `int, char, boolean` | Example: `String, Array, Class` |

---

### 🧠 **Memory Tip**

* **Primitive types → stored in Stack memory**
* **Objects (Non-primitive) → stored in Heap memory**

---

✅ **Summary:**

> Java has **8 primitive data types** — `byte, short, int, long, float, double, char, boolean`.

---

## 4. What is autoboxing and unboxing?

---

## 🧠 **Autoboxing and Unboxing in Java**

Java provides **wrapper classes** for all primitive data types to treat them as **objects**.
Sometimes you need to convert **primitive types** to **objects** (and vice versa).
This automatic conversion is what we call:

---

### 🔹 **1️⃣ Autoboxing**

**Definition:**
Automatic **conversion of a primitive type → corresponding wrapper class object**.

**Example:**

```java
int num = 10;              // primitive type
Integer obj = num;         // autoboxing
```

✅ Here, Java automatically converts `int` → `Integer`.

**Equivalent Manual Conversion (Before Java 5):**

```java
Integer obj = Integer.valueOf(num);
```

---

### 🔹 **2️⃣ Unboxing**

**Definition:**
Automatic **conversion of a wrapper class object → corresponding primitive type**.

**Example:**

```java
Integer obj = 20;          // wrapper object
int num = obj;             // unboxing
```

✅ Here, Java automatically converts `Integer` → `int`.

**Equivalent Manual Conversion (Before Java 5):**

```java
int num = obj.intValue();
```

---

### 🧩 **Wrapper Classes for Primitives**

| Primitive Type | Wrapper Class |
| -------------- | ------------- |
| `byte`         | `Byte`        |
| `short`        | `Short`       |
| `int`          | `Integer`     |
| `long`         | `Long`        |
| `float`        | `Float`       |
| `double`       | `Double`      |
| `char`         | `Character`   |
| `boolean`      | `Boolean`     |

---

### ⚙️ **Example: Autoboxing & Unboxing Together**

```java
public class AutoUnboxingDemo {
    public static void main(String[] args) {
        // Autoboxing: int -> Integer
        Integer obj = 100;

        // Unboxing: Integer -> int
        int num = obj;

        System.out.println(obj + " " + num);
    }
}
```

**Output:**

```
100 100
```

---

### 🔸 **Where It’s Commonly Used**

✅ In **Collections Framework**, which can only store objects (not primitives):

```java
List<Integer> list = new ArrayList<>();
list.add(5);          // autoboxing (int → Integer)
int x = list.get(0);  // unboxing (Integer → int)
```

---

### 🧠 **Key Points to Remember**

| Concept       | Description                            |
| ------------- | -------------------------------------- |
| Autoboxing    | Primitive → Wrapper Object             |
| Unboxing      | Wrapper Object → Primitive             |
| Introduced in | Java 5                                 |
| Common Usage  | Collections, Generics, Streams         |
| Performance   | Slight overhead due to object creation |

---

### ⚠️ **Performance Note**

Autoboxing can cause **extra memory allocation** and **slower performance** in large loops or high-frequency code because objects are created on the heap.

Example:

```java
Long sum = 0L;
for (long i = 0; i < 1000000; i++) {
    sum += i; // Causes repeated boxing/unboxing
}
```

👉 It’s better to use primitives when performance is critical.

---

✅ **In Short:**

> * **Autoboxing** = primitive → wrapper
> * **Unboxing** = wrapper → primitive
> * Introduced in **Java 5** to simplify code and improve readability.

---

## 5. What are access modifires in Java (private, protected, public, default)?

---

## 🧠 **Access Modifiers in Java**

Access Modifiers are **keywords** that **control the visibility (accessibility)** of **classes, methods, variables, and constructors** in Java.

Java provides **four** access modifiers:

> **1️⃣ private**
> **2️⃣ default (no modifier)**
> **3️⃣ protected**
> **4️⃣ public**

---

### ⚙️ **1. private**

**Definition:**
Members declared as `private` are **accessible only within the same class**.

**Use:**
To achieve **encapsulation** (data hiding).

**Example:**

```java
class Employee {
    private int salary = 50000;

    private void showSalary() {
        System.out.println(salary);
    }
}
```

✅ `salary` and `showSalary()` are **not accessible** outside the `Employee` class.

---

### ⚙️ **2. default** *(no modifier specified)*

**Definition:**
If no access modifier is specified, it is **default** (also called **package-private**).
Accessible **only within the same package**.

**Example:**

```java
class Employee {  // default class
    int id;       // default variable
    void display() {  // default method
        System.out.println("Employee ID: " + id);
    }
}
```

✅ Can be accessed by **other classes in the same package**,
❌ Not accessible from **outside the package**.

---

### ⚙️ **3. protected**

**Definition:**
Accessible:

* **Within the same package**, and
* **In subclasses (even if in different packages)** using inheritance.

**Example:**

```java
package com.company;

public class Employee {
    protected String department = "HR";
}

package com.test;

import com.company.Employee;

class Manager extends Employee {
    void showDept() {
        System.out.println(department); // ✅ accessible through inheritance
    }
}
```

✅ Access allowed in subclass (even in another package).
❌ Access not allowed by non-subclass in another package.

---

### ⚙️ **4. public**

**Definition:**
Accessible **from anywhere**, across all packages and projects.

**Example:**

```java
public class Employee {
    public void display() {
        System.out.println("Public Method");
    }
}
```

✅ Can be accessed from **any class**, **any package**, **any project**.

---

## 🧩 **Access Modifier Summary Table**

| Modifier      | Same Class | Same Package | Subclass (Different Package) | Other Packages |
| ------------- | ---------- | ------------ | ---------------------------- | -------------- |
| **private**   | ✅ Yes      | ❌ No         | ❌ No                         | ❌ No           |
| **default**   | ✅ Yes      | ✅ Yes        | ❌ No                         | ❌ No           |
| **protected** | ✅ Yes      | ✅ Yes        | ✅ Yes (via inheritance)      | ❌ No           |
| **public**    | ✅ Yes      | ✅ Yes        | ✅ Yes                        | ✅ Yes          |

---

### 🧠 **Access Modifiers for Classes**

| Class Modifier | Allowed? | Description                                   |
| -------------- | -------- | --------------------------------------------- |
| `public`       | ✅        | Class accessible from anywhere                |
| `default`      | ✅        | Class accessible only within the same package |
| `private`      | ❌        | Not allowed for top-level classes             |
| `protected`    | ❌        | Not allowed for top-level classes             |

---

### ✅ **Quick Interview Tip**

> * Use **private** for encapsulation
> * Use **protected** for inheritance
> * Use **default** for package-level design
> * Use **public** for global access

---

### 💡 **Example Recap**

```java
public class TestAccess {
    private int a = 10;       // only inside this class
    int b = 20;               // same package
    protected int c = 30;     // package + subclass
    public int d = 40;        // everywhere

    public void show() {
        System.out.println(a + b + c + d);
    }
}
```

---

## 6. What is a package in Java?

---

## 🧠 **What is a Package in Java?**

### **Definition:**

A **package** in Java is a **namespace** (or folder-like structure) that organizes related **classes, interfaces, and sub-packages** together.

Think of it as a **directory** on your computer used to group similar files.

---

### 🔹 **Why Packages Are Used**

✅ To **organize code** and avoid name conflicts.
✅ To make code **modular, maintainable, and reusable**.
✅ To **control access** (via access modifiers).
✅ To **locate classes easily** using import statements.

---

### ⚙️ **Types of Packages**

Java has **two main types** of packages:

#### 1️⃣ **Built-in Packages** (Predefined by Java)

These are part of the **Java API** — you just import them.

| Package     | Purpose                     | Example Class              |
| ----------- | --------------------------- | -------------------------- |
| `java.lang` | Core language classes       | `String`, `Math`, `Object` |
| `java.util` | Data structures & utilities | `ArrayList`, `HashMap`     |
| `java.io`   | Input/Output                | `File`, `BufferedReader`   |
| `java.net`  | Networking                  | `Socket`, `URL`            |
| `java.sql`  | Database                    | `Connection`, `ResultSet`  |
| `java.time` | Date & time API             | `LocalDate`, `Duration`    |

📌 These are imported automatically:

```java
import java.lang.*;  // done implicitly
```

---

#### 2️⃣ **User-defined Packages**

These are created by the **developer** to organize project classes.

**Example:**

```java
package com.company.project;   // declares package

public class Employee {
    public void display() {
        System.out.println("Inside Employee class");
    }
}
```

Now, to use this class elsewhere:

```java
import com.company.project.Employee;

class Test {
    public static void main(String[] args) {
        Employee emp = new Employee();
        emp.display();
    }
}
```

---

### 📂 **Real-World Example of Package Structure**

```
src/
 └── com/
      └── hospital/
           ├── model/
           │    ├── Patient.java
           │    └── Doctor.java
           ├── service/
           │    └── AppointmentService.java
           └── controller/
                └── PatientController.java
```

✅ Here, `com.hospital` is the **base package**,
and `model`, `service`, `controller` are **sub-packages**.

---

### 🧩 **Using `import` Keyword**

To use a class from another package:

```java
import com.hospital.model.Patient;      // import single class
import com.hospital.service.*;          // import all classes in package
```

---

### ⚠️ **Access Control with Packages**

| Modifier    | Same Package     | Different Package            |
| ----------- | ---------------- | ---------------------------- |
| `public`    | ✅ Accessible     | ✅ Accessible                 |
| `protected` | ✅ Accessible     | ✅ Accessible via inheritance |
| `default`   | ✅ Accessible     | ❌ Not Accessible             |
| `private`   | ❌ Not Accessible | ❌ Not Accessible             |

---

### 🧠 **Key Notes**

* Each `.java` file can have **only one package statement**, and it must be the **first line** (before imports).
* Packages follow **reverse domain naming** (e.g., `com.company.project`).
* Packages help in **encapsulation and modular design**.

---

✅ **In Short:**

> A **package** in Java is a way to **group related classes and interfaces** together to organize code, avoid naming conflicts, and control access.

---

## 7. What is a static keyword? Static variables and methods?

---

## 🧠 **What is the `static` keyword in Java?**

### **Definition:**

In Java, the **`static`** keyword means —

> The member (variable, method, block, or nested class) **belongs to the class**, not to any specific object.

So you can access it **without creating an object**.

---

### 🔹 **1️⃣ Static Variables (Class Variables)**

**Definition:**
A `static` variable is **shared among all objects** of the class — only **one copy** exists in memory.

**When to use:**
When you want to store **common data** shared by all objects (like a counter, constant, or configuration).

**Example:**

```java
class Employee {
    int id;                      // instance variable
    static String company = "TCS"; // static variable

    Employee(int id) {
        this.id = id;
    }

    void show() {
        System.out.println(id + " works at " + company);
    }
}

public class Test {
    public static void main(String[] args) {
        Employee e1 = new Employee(101);
        Employee e2 = new Employee(102);

        e1.show();
        e2.show();

        // Access without object
        System.out.println(Employee.company);
    }
}
```

**Output:**

```
101 works at TCS
102 works at TCS
TCS
```

✅ Only one `company` variable shared by both employees.

---

### 🔹 **2️⃣ Static Methods**

**Definition:**
Methods declared with `static` belong to the class and can be called **without creating an object**.

**Rules:**

* Can **access only static variables** and **call other static methods** directly.
* **Cannot access instance variables** or **instance methods** directly (because they belong to an object).

**Example:**

```java
class MathUtil {
    static int add(int a, int b) {
        return a + b;
    }
}

public class Test {
    public static void main(String[] args) {
        int sum = MathUtil.add(10, 20); // called without object
        System.out.println("Sum = " + sum);
    }
}
```

✅ Static methods are often used for **utility or helper methods** (like `Math.max()`, `Collections.sort()`).

---

### 🔹 **3️⃣ Static Block**

**Definition:**
A `static` block is used for **static initialization** — executed **only once** when the class is **loaded into memory**.

**Example:**

```java
class Demo {
    static int count;

    static {
        count = 10;
        System.out.println("Static block executed!");
    }

    public static void main(String[] args) {
        System.out.println("Main method executed!");
        System.out.println("Count = " + count);
    }
}
```

**Output:**

```
Static block executed!
Main method executed!
Count = 10
```

✅ Used to initialize **static variables** or perform **one-time setup**.

---

### 🔹 **4️⃣ Static Nested Class**

A class declared **inside another class** with the `static` keyword is a **static nested class**.
It can be created **without an instance** of the outer class.

**Example:**

```java
class Outer {
    static class Inner {
        void show() {
            System.out.println("Inside static nested class");
        }
    }
}

public class Test {
    public static void main(String[] args) {
        Outer.Inner obj = new Outer.Inner(); // no Outer object needed
        obj.show();
    }
}
```

---

### 🧩 **Memory Management**

| Type                 | Stored In         | Shared?                 |
| -------------------- | ----------------- | ----------------------- |
| **Static Members**   | Method Area       | ✅ Shared by all objects |
| **Instance Members** | Heap (per object) | ❌ Not shared            |

---

### ⚙️ **Common Interview Points**

| Concept           | Explanation                                    |
| ----------------- | ---------------------------------------------- |
| `static` variable | Shared by all instances                        |
| `static` method   | Belongs to class, can be called without object |
| `static` block    | Runs once when class is loaded                 |
| `static` class    | Nested class not tied to an instance           |
| Cannot use `this` | Because no instance is associated              |

---

### ✅ **Quick Summary**

| Member Type       | Belongs To | Accessed By           | Can Access             |
| ----------------- | ---------- | --------------------- | ---------------------- |
| Static Variable   | Class      | Class name or object  | Static members         |
| Static Method     | Class      | Class name            | Static members         |
| Instance Variable | Object     | Object reference      | Both static & instance |
| Static Block      | Class      | Auto-executes on load | Static members         |

---

💡 **Example from Real-World Java:**

```java
System.out.println(Math.PI);        // static variable
System.out.println(Math.max(3, 7)); // static method
```

→ `Math` class methods and constants are **static**, so we don’t need to create a `Math` object.

---

✅ **In short:**

> `static` means *“belongs to the class, not to an instance.”*
> Used for **shared variables**, **utility methods**, and **class-level initialization**.

---

## 8. What is Constructor in Java? Types of Constructor?

---

### **What is a Constructor in Java?**

A **constructor** in Java is a **special method** that is used to **initialize objects**.
It is **called automatically** when an object is created using the `new` keyword.

---

### 🧩 **Key Points About Constructors:**

* The **constructor name must be the same as the class name**.
* It **does not have a return type**, not even `void`.
* It is **automatically invoked** when an object is created.
* It is mainly used to **initialize object variables**.

---

### 🧱 **Syntax Example:**

```java
class Student {
    String name;
    int age;

    // Constructor
    Student(String n, int a) {
        name = n;
        age = a;
    }

    void display() {
        System.out.println(name + " " + age);
    }

    public static void main(String[] args) {
        Student s1 = new Student("Aditya", 25);  // Constructor called
        s1.display();
    }
}
```

---

### ⚙️ **Types of Constructors in Java:**

#### 1. **Default Constructor**

* A **no-argument constructor** that Java **creates automatically** if no constructor is defined.
* It initializes variables with **default values**.

```java
class Demo {
    int x;

    // Default constructor created by compiler
    Demo() {
        System.out.println("Default constructor called");
    }

    public static void main(String[] args) {
        Demo d = new Demo(); // Default constructor invoked
    }
}
```

---

#### 2. **Parameterized Constructor**

* Constructor that **accepts parameters** to initialize object variables with specific values.

```java
class Employee {
    String name;
    int id;

    Employee(String n, int i) {
        name = n;
        id = i;
    }

    void display() {
        System.out.println(name + " " + id);
    }

    public static void main(String[] args) {
        Employee e1 = new Employee("Aditya", 101);
        e1.display();
    }
}
```

---

#### 3. **Copy Constructor (User-defined)**

* Java doesn’t provide a built-in copy constructor, but we can **create one manually** to copy values from another object.

```java
class Student {
    String name;
    int age;

    Student(String n, int a) {
        name = n;
        age = a;
    }

    // Copy Constructor
    Student(Student s) {
        name = s.name;
        age = s.age;
    }

    public static void main(String[] args) {
        Student s1 = new Student("Aditya", 25);
        Student s2 = new Student(s1); // Copy constructor called

        System.out.println(s2.name + " " + s2.age);
    }
}
```

---

### 🔍 **Constructor Overloading**

Just like methods, constructors can also be **overloaded** (same name, different parameters).

```java
class Example {
    Example() {
        System.out.println("Default constructor");
    }

    Example(int a) {
        System.out.println("Parameterized constructor: " + a);
    }

    public static void main(String[] args) {
        new Example();
        new Example(10);
    }
}
```

---

### ✅ **Summary Table**

| Type          | Description                        | Example                     |
| ------------- | ---------------------------------- | --------------------------- |
| Default       | No arguments, provided by compiler | `Demo()`                    |
| Parameterized | Takes parameters to initialize     | `Employee(String n, int i)` |
| Copy          | Copies data from another object    | `Student(Student s)`        |

---

## 9. Can we use static methods in a Constructor?

---

### **Can We Use Static Methods in a Constructor?**

✅ **Yes, we can use static methods inside a constructor in Java.**

However, let’s break this down carefully 👇

---

### ⚙️ **Explanation:**

A **constructor** is used to initialize an **object**, while a **static method** belongs to the **class itself**, not to any specific object.

So, although constructors deal with **instance-level initialization**, they **can still call static methods** because static methods exist **independently of objects**.

---

### 🧱 **Example:**

```java
class Test {
    // Static method
    static void displayMessage() {
        System.out.println("Static method called!");
    }

    // Constructor
    Test() {
        System.out.println("Constructor called!");
        displayMessage(); // Calling static method inside constructor
    }

    public static void main(String[] args) {
        Test t1 = new Test();  // Constructor invokes static method
    }
}
```

**🧾 Output:**

```
Constructor called!
Static method called!
```

✅ Works perfectly fine.

---

### ⚠️ **Key Points to Remember:**

1. **You can call static methods inside a constructor**, directly or using the class name:

   ```java
   Test.displayMessage();
   ```

2. **You cannot use instance variables or instance methods** inside a static method —
   but the reverse (using static methods inside constructors) is allowed.

3. Static methods are often used in constructors for:

   * Logging
   * Utility checks
   * Configuration loading
   * Counting object creations, etc.

---

### 🚫 **However, Avoid Doing This:**

If the static method you call **depends on the object’s state**, it might cause inconsistent results — because the object might **not be fully initialized yet** when the constructor runs.

Example (❌ not recommended):

```java
class Example {
    int value;

    Example() {
        value = 10;
        printValue(); // risky if static method uses uninitialized fields
    }

    static void printValue() {
        // can't access instance variable 'value' here
        // System.out.println(value); // ❌ compile-time error
    }
}
```

---

### ✅ **Conclusion:**

| Question                                        | Answer                                                 |
| ----------------------------------------------- | ------------------------------------------------------ |
| Can we use static methods inside a constructor? | ✅ Yes                                                  |
| Is it recommended?                              | ✅ Yes, if used for general (non-object-specific) logic |
| Can static methods access instance variables?   | ❌ No                                                   |
| Typical use cases                               | Logging, counters, configuration, utility calls        |

---

# OOP Concepts

## 10. What is inheritance? Types of inheritance in Java?

---

## **What is Inheritance in Java?**

### **Definition:**

> **Inheritance** is a mechanism in Java by which **one class acquires the properties (fields) and behaviors (methods) of another class**.

* The **existing class** is called the **superclass (parent class)**.
* The **new class** that inherits is called the **subclass (child class)**.
* **Purpose:** Reuse code, improve maintainability, and establish a relationship between classes.

---

### **Example:**

```java
class Animal {          // Superclass
    void eat() {
        System.out.println("Animal is eating");
    }
}

class Dog extends Animal {   // Subclass
    void bark() {
        System.out.println("Dog is barking");
    }
}

public class Test {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.eat();   // inherited from Animal
        d.bark();  // own method
    }
}
```

**Output:**

```
Animal is eating
Dog is barking
```

✅ Here, `Dog` **inherits** the method `eat()` from `Animal`.

---

## **Types of Inheritance in Java**

### 1️⃣ **Single Inheritance**

* A class inherits from **one superclass**.
* Example: `class Dog extends Animal`

---

### 2️⃣ **Multilevel Inheritance**

* A class acts as a **superclass for another subclass**, forming a chain.
* Example:

```java
class Animal {
    void eat() { System.out.println("Animal eats"); }
}

class Dog extends Animal {
    void bark() { System.out.println("Dog barks"); }
}

class BabyDog extends Dog {
    void weep() { System.out.println("Baby dog weeps"); }
}

public class Test {
    public static void main(String[] args) {
        BabyDog bd = new BabyDog();
        bd.eat();
        bd.bark();
        bd.weep();
    }
}
```

**Output:**

```
Animal eats
Dog barks
Baby dog weeps
```

---

### 3️⃣ **Hierarchical Inheritance**

* **Multiple subclasses** inherit from **one superclass**.
* Example:

```java
class Animal {
    void eat() { System.out.println("Animal eats"); }
}

class Dog extends Animal {
    void bark() { System.out.println("Dog barks"); }
}

class Cat extends Animal {
    void meow() { System.out.println("Cat meows"); }
}

public class Test {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.eat();
        d.bark();

        Cat c = new Cat();
        c.eat();
        c.meow();
    }
}
```

---

### 4️⃣ **Multiple Inheritance (Through Interfaces)**

* **Java doesn’t support multiple inheritance with classes** (to avoid ambiguity).
* But it **supports multiple inheritance via interfaces**.

```java
interface Animal {
    void eat();
}

interface Pet {
    void play();
}

class Dog implements Animal, Pet {
    public void eat() { System.out.println("Dog eats"); }
    public void play() { System.out.println("Dog plays"); }
}

public class Test {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.eat();
        d.play();
    }
}
```

---

### 🔹 **Quick Summary Table**

| Type                     | Description                              | Example                      |
| ------------------------ | ---------------------------------------- | ---------------------------- |
| Single                   | One subclass inherits one superclass     | `Dog extends Animal`         |
| Multilevel               | Chain of inheritance                     | `BabyDog → Dog → Animal`     |
| Hierarchical             | Multiple subclasses from one superclass  | `Dog & Cat → Animal`         |
| Multiple (via interface) | One class implements multiple interfaces | `Dog implements Animal, Pet` |

---

### ✅ **Key Points About Inheritance**

1. Promotes **code reuse**.
2. Supports **polymorphism**.
3. **Private members** of superclass are **not inherited**, but **protected and public members are**.
4. **Constructor of superclass** is called first (via `super()`), then subclass constructor.
5. Avoid **diamond problem** in multiple inheritance by using **interfaces**.

---

## 11. What is polymorphism? Give examples.

---

## **What is Polymorphism in Java?**

### **Definition:**

> **Polymorphism** means “**many forms**.”
> In Java, it is the ability of an object, method, or operator to **take multiple forms**.

Polymorphism allows **one interface or method to behave differently** based on the context.

---

### **Types of Polymorphism in Java**

Java supports **two types of polymorphism**:

1️⃣ **Compile-time (Static) Polymorphism**
2️⃣ **Runtime (Dynamic) Polymorphism**

---

## **1️⃣ Compile-time Polymorphism (Method Overloading)**

**Definition:**

* Achieved by **method overloading** or **operator overloading**.
* The method to be executed is **decided at compile time**.

**Rules for Method Overloading:**

* Same method name
* Different parameters (type, number, or order)
* Can have different return types

**Example:**

```java
class MathUtil {
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

public class Test {
    public static void main(String[] args) {
        MathUtil m = new MathUtil();
        System.out.println(m.add(2, 3));       // calls int add(int, int)
        System.out.println(m.add(2.5, 3.5));   // calls double add(double, double)
        System.out.println(m.add(1, 2, 3));    // calls int add(int, int, int)
    }
}
```

✅ **Compile-time polymorphism** = method selected at **compile time**.

---

## **2️⃣ Runtime Polymorphism (Method Overriding)**

**Definition:**

* Achieved by **method overriding** in **inheritance**.
* The method to be executed is **decided at runtime** based on the **object type**.

**Rules for Method Overriding:**

* Same method name
* Same parameters
* Same or covariant return type
* Subclass method **cannot reduce visibility**

**Example:**

```java
class Animal {
    void sound() {
        System.out.println("Animal makes sound");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("Dog barks");
    }
}

public class Test {
    public static void main(String[] args) {
        Animal a = new Dog(); // reference type Animal, object type Dog
        a.sound();            // runtime polymorphism → calls Dog's sound()
    }
}
```

**Output:**

```
Dog barks
```

✅ **Runtime polymorphism** = method executed depends on **object type at runtime**.

---

### **Other Forms of Polymorphism**

* **Operator Overloading (Compile-time):**
  Java supports **`+` operator** for both **numbers and strings**:

  ```java
  int sum = 2 + 3; 
  String msg = "Hello " + "World";
  ```
* **Interface Polymorphism:**
  A class can implement multiple interfaces → behave differently.

---

### **Quick Summary Table**

| Type                  | Achieved By        | When Decided | Example                                  |
| --------------------- | ------------------ | ------------ | ---------------------------------------- |
| Compile-time (Static) | Method Overloading | Compile-time | `add(int, int)` vs `add(double, double)` |
| Runtime (Dynamic)     | Method Overriding  | Runtime      | `Animal a = new Dog(); a.sound()`        |

---

### ✅ **Key Points to Remember**

1. **Polymorphism = “many forms”** → same method behaves differently.
2. Compile-time → Overloading, checked by compiler.
3. Runtime → Overriding, checked by JVM at runtime.
4. Helps in **code flexibility, reusability, and maintainability**.

---

## 12. What is encapsulation and abstraction?

---

## **Encapsulation vs Abstraction in Java**

Although both are used to **hide data**, they are **different concepts**.

---

### **1️⃣ Encapsulation**

**Definition:**

> Encapsulation is the **process of wrapping data (variables) and code (methods) together into a single unit**, i.e., a **class**, and **restricting access** to the inner details.

**Key Points:**

* Achieved using **private variables** and **public getter/setter methods**.
* Protects **data from unauthorized access**.
* Improves **code maintainability and security**.

**Example:**

```java
class Employee {
    private int salary;  // private variable

    // Getter
    public int getSalary() {
        return salary;
    }

    // Setter
    public void setSalary(int salary) {
        if(salary > 0) {
            this.salary = salary;
        }
    }
}

public class Test {
    public static void main(String[] args) {
        Employee e = new Employee();
        e.setSalary(50000);
        System.out.println("Salary: " + e.getSalary());
    }
}
```

✅ Here, `salary` is **hidden** from outside, but accessed safely via methods.

---

### **2️⃣ Abstraction**

**Definition:**

> Abstraction is the **process of hiding implementation details** and **showing only essential features** to the user.

**Key Points:**

* Achieved using **abstract classes** and **interfaces**.
* Focuses on **what an object does**, not **how it does it**.
* Helps in **reducing complexity**.

**Example:**

```java
abstract class Vehicle {
    abstract void start();  // abstract method → implementation hidden
}

class Car extends Vehicle {
    void start() {           // implementation provided in subclass
        System.out.println("Car starts with key");
    }
}

public class Test {
    public static void main(String[] args) {
        Vehicle v = new Car();
        v.start();  // only shows what it does, not how
    }
}
```

✅ Here, the **user only knows** that `Vehicle` can `start()`, not the implementation details.

---

### **3️⃣ Key Differences**

| Feature     | Encapsulation               | Abstraction                             |
| ----------- | --------------------------- | --------------------------------------- |
| Purpose     | Hide **data** (variables)   | Hide **implementation** (details)       |
| Achieved By | `private` + getters/setters | `abstract class` / `interface`          |
| Focus       | Protect data                | Expose functionality                    |
| Example     | Employee salary (private)   | Vehicle start() method (abstract)       |
| Access      | Can access via methods      | Only via abstract methods or interfaces |

---

### ✅ **Quick Tip for Interviews**

> * **Encapsulation = Data hiding**
> * **Abstraction = Implementation hiding**

> **Mnemonic:** Encapsulation = “wrap your data”, Abstraction = “hide the details”.

---

## 13. What is method overloading vs method overriding?

---

## **Method Overloading vs Method Overriding**

| Feature               | Method Overloading                                               | Method Overriding                                                    |
| --------------------- | ---------------------------------------------------------------- | -------------------------------------------------------------------- |
| **Definition**        | Same method name, **different parameters** in the **same class** | Same method name, **same parameters** in **superclass and subclass** |
| **Parameters**        | Must differ (type, number, or order)                             | Must be same                                                         |
| **Return Type**       | Can be same or different (if types compatible)                   | Must be same (or covariant)                                          |
| **Inheritance**       | Not required                                                     | Required (in superclass & subclass)                                  |
| **Access Modifier**   | Can have any access modifier                                     | Subclass cannot reduce visibility (can increase)                     |
| **Polymorphism Type** | Compile-time (Static Polymorphism)                               | Runtime (Dynamic Polymorphism)                                       |
| **`super` keyword**   | Not used                                                         | Can use `super` to call parent method                                |
| **Example**           | Overloaded methods in same class                                 | Overridden method in subclass                                        |

---

### **1️⃣ Method Overloading (Compile-time Polymorphism)**

**Example:**

```java
class MathUtil {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }
}

public class Test {
    public static void main(String[] args) {
        MathUtil m = new MathUtil();
        System.out.println(m.add(2, 3));     // calls int add(int, int)
        System.out.println(m.add(2.5, 3.5)); // calls double add(double, double)
    }
}
```

✅ Method chosen **at compile time** based on parameters.

---

### **2️⃣ Method Overriding (Runtime Polymorphism)**

**Example:**

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

public class Test {
    public static void main(String[] args) {
        Animal a = new Dog(); // reference type Animal, object type Dog
        a.sound();            // calls Dog's sound() at runtime
    }
}
```

✅ Method chosen **at runtime** based on **object type**.

---

### **Key Points for Interviews**

1. **Overloading = same class, different signature, compile-time**.
2. **Overriding = inheritance, same signature, runtime**.
3. Overridden method can use `super.methodName()` to call parent’s method.
4. Overloaded methods can differ by number/type/order of parameters.

---

## 14. When to use Interface vs Abstract Class?

---

## **Interface vs Abstract Class in Java**

### **Definition:**

* **Abstract Class:**
  A class that **cannot be instantiated** and can have **abstract methods (without body)** as well as **concrete methods (with body)**. Used for **common base behavior**.

* **Interface:**
  A completely **abstract type** (before Java 8) that **defines a contract**. Classes **implement interfaces** to provide behavior.
  (From Java 8 onwards, interfaces can have **default and static methods**.)

---

### **Comparison Table**

| Feature                  | Abstract Class                                                | Interface                                                                                                     |
| ------------------------ | ------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| **Purpose**              | Share **common behavior** among related classes               | Define a **contract** for unrelated classes                                                                   |
| **Methods**              | Can have **abstract and concrete** methods                    | Java 8+: abstract, default, static methods                                                                    |
| **Multiple Inheritance** | Not allowed (Java doesn’t support multiple class inheritance) | Allowed (a class can implement **multiple interfaces**)                                                       |
| **Constructors**         | Yes, can have constructors                                    | No constructors                                                                                               |
| **Access Modifiers**     | Can have **private, protected, public**                       | All variables are **public static final** by default; methods are **public abstract** (except default/static) |
| **Fields/Variables**     | Can have instance variables                                   | Only **constants (static final)**                                                                             |
| **When to Use**          | Use when classes are **closely related** and share behavior   | Use when classes are **unrelated** but share **common contract**                                              |

---

### **Example: Abstract Class**

```java
abstract class Vehicle {
    abstract void start(); // abstract method

    void stop() {          // concrete method
        System.out.println("Vehicle stopped");
    }
}

class Car extends Vehicle {
    void start() {
        System.out.println("Car starts with key");
    }
}

public class Test {
    public static void main(String[] args) {
        Vehicle v = new Car();
        v.start();
        v.stop();
    }
}
```

✅ Abstract class allows **both shared behavior** (`stop()`) and **mandatory implementation** (`start()`).

---

### **Example: Interface**

```java
interface Vehicle {
    void start();   // abstract by default
    void stop();
}

class Bike implements Vehicle {
    public void start() {
        System.out.println("Bike starts with kick");
    }

    public void stop() {
        System.out.println("Bike stopped");
    }
}

public class Test {
    public static void main(String[] args) {
        Vehicle v = new Bike();
        v.start();
        v.stop();
    }
}
```

✅ Interface defines **what a class should do**, not how. Multiple classes can implement the **same interface** differently.

---

### **Quick Tips for Interviews**

* Use **Abstract Class**:

  * When classes are **closely related**.
  * When you need **shared code**.
  * When you want **fields, constructors, or access modifiers**.

* Use **Interface**:

  * When classes are **unrelated**.
  * When you want **multiple inheritance**.
  * When you want to define a **contract or capability** (`Runnable`, `Serializable`).

---

## 15. What is Marker Interface? Why use it?

---

## **What is a Marker Interface?**

### **Definition:**

> A **Marker Interface** is an **interface with no methods or fields** — it’s empty.
> Its purpose is to **mark or tag a class** to convey metadata to the JVM or frameworks.

**Also called:** Tagging interface.

---

### **Key Points:**

* **No methods** are defined inside a marker interface.
* Used to **signal the JVM or compiler** that the class possesses some property or behavior.
* Provides a way to **group classes logically** or enable certain functionality without modifying code.

---

### **Why Use Marker Interfaces?**

1. To **signal a class has a property** (like serializable, cloneable).
2. To allow **runtime checking** using `instanceof`.
3. To **enable certain behaviors** without changing the class code.

---

### **Common Examples in Java**

| Marker Interface | Purpose                                                             |
| ---------------- | ------------------------------------------------------------------- |
| `Serializable`   | Indicates that a class can be serialized (converted to byte stream) |
| `Cloneable`      | Indicates that a class supports `Object.clone()`                    |
| `Remote`         | Used in RMI (Remote Method Invocation) to mark remote objects       |

---

### **Example of Marker Interface**

```java
import java.io.*;

// Marker interface example: Serializable
class Employee implements Serializable { // no methods, just marks it
    int id;
    String name;

    Employee(int id, String name) {
        this.id = id;
        this.name = name;
    }
}

public class Test {
    public static void main(String[] args) throws Exception {
        Employee e = new Employee(101, "Aditya");

        // Serialize object to file
        FileOutputStream fos = new FileOutputStream("employee.ser");
        ObjectOutputStream oos = new ObjectOutputStream(fos);
        oos.writeObject(e);  // JVM checks if class implements Serializable
        oos.close();
        System.out.println("Employee object serialized successfully");
    }
}
```

✅ Here, `Serializable` **marks** that `Employee` objects can be serialized.

Without the marker, JVM throws:

```
java.io.NotSerializableException
```

---

### **Key Notes for Interviews**

1. Marker interface **does not contain methods**.
2. Provides **metadata or tagging** for a class.
3. Useful in **Java APIs** for functionality like Serialization, Cloning, or RMI.
4. **Alternative in modern Java:** Annotations (e.g., `@Override`, `@FunctionalInterface`) can serve a similar purpose.

---

💡 **Quick Tip:**

> Marker interface = **“tag a class to tell JVM or frameworks how to treat it.”**

---

# String Handling

## 16. What is the difference between String, StringBuilder and StringBuffer?

---

## **Difference between String, StringBuilder, and StringBuffer**

### **1️⃣ String**

**Definition:**

* `String` is **immutable**, meaning once created, its **value cannot be changed**.
* Any modification creates a **new String object** in the heap.

**Example:**

```java
String str = "Hello";
str = str + " World";  // creates new object
```

**Key Points:**

* Immutable → thread-safe naturally.
* Slower for **frequent modifications** because each change creates a new object.
* Stored in **String pool** if literal is used.

---

### **2️⃣ StringBuilder**

**Definition:**

* `StringBuilder` is **mutable**, meaning the **content can be changed** without creating a new object.
* Introduced in Java 5.
* **Not synchronized** → **faster** than StringBuffer.

**Example:**

```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");  // modifies the same object
System.out.println(sb);  // Hello World
```

**Key Points:**

* Mutable → efficient for **frequent modifications**.
* Not thread-safe (use in single-threaded environment).
* Methods: `append()`, `insert()`, `delete()`, `reverse()`, `replace()`.

---

### **3️⃣ StringBuffer**

**Definition:**

* `StringBuffer` is **mutable**, like StringBuilder, but **thread-safe** because methods are synchronized.
* Introduced in Java 1.0.

**Example:**

```java
StringBuffer sbf = new StringBuffer("Hello");
sbf.append(" World");  // modifies the same object
System.out.println(sbf);  // Hello World
```

**Key Points:**

* Thread-safe → suitable for **multi-threaded environments**.
* Slower than StringBuilder due to **synchronization overhead**.

---

### **Comparison Table**

| Feature           | String                          | StringBuilder                       | StringBuffer                       |
| ----------------- | ------------------------------- | ----------------------------------- | ---------------------------------- |
| **Mutability**    | Immutable                       | Mutable                             | Mutable                            |
| **Thread Safety** | Thread-safe (immutable)         | Not thread-safe                     | Thread-safe (synchronized)         |
| **Performance**   | Slow for modifications          | Fast                                | Slower than StringBuilder          |
| **Introduced in** | Java 1.0                        | Java 5                              | Java 1.0                           |
| **Use Case**      | Fixed text or few modifications | Single-threaded string manipulation | Multi-threaded string manipulation |
| **Memory**        | Each change creates new object  | Modifies existing object            | Modifies existing object           |

---

### **Example Comparing All Three:**

```java
// String
String str = "Hello";
str += " World";  // new object created
System.out.println(str);

// StringBuilder
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");  // same object
System.out.println(sb);

// StringBuffer
StringBuffer sbf = new StringBuffer("Hello");
sbf.append(" World");  // same object, thread-safe
System.out.println(sbf);
```

**Output:**

```
Hello World
Hello World
Hello World
```

✅ Behavior looks similar, but memory and performance differ.

---

💡 **Quick Tip for Interviews:**

* If **thread safety is needed → StringBuffer**
* If **single-threaded and frequent modification → StringBuilder**
* If **value won’t change → String**

---

## 17. Difference between creating String with literal and new Operator.

---

## **Difference Between Creating String with Literal and `new` Operator**

In Java, there are **two ways to create a String**:

1. Using **String literal**
2. Using **`new` keyword**

---

### **1️⃣ Using String Literal**

```java
String str1 = "Hello";
String str2 = "Hello";
```

**Key Points:**

* Stored in the **String Pool** (special area in heap).
* **Reuses existing objects** if the same literal already exists in the pool.
* **Memory efficient** because it avoids duplicate objects.
* **Immutable**, so cannot be changed.

**Example:**

```java
System.out.println(str1 == str2); // true, both reference same object
```

✅ Here, `str1` and `str2` point to **the same object in the string pool**.

---

### **2️⃣ Using `new` Operator**

```java
String str3 = new String("Hello");
String str4 = new String("Hello");
```

**Key Points:**

* Creates a **new object in heap memory**, not in string pool.
* Even if the same value exists, a **new object is created**.
* Slower and less memory efficient.

**Example:**

```java
System.out.println(str3 == str4); // false, different objects
System.out.println(str3.equals(str4)); // true, content is same
```

✅ Here, `str3` and `str4` are **different objects**, but their **values are the same**.

---

### **Comparison Table**

| Feature           | String Literal        | `new` Operator                    |
| ----------------- | --------------------- | --------------------------------- |
| Memory Location   | String Pool           | Heap                              |
| Object Reuse      | Yes, reuses if exists | No, creates new object every time |
| Performance       | Faster                | Slower                            |
| `==` Check        | True if same value    | False (different objects)         |
| `.equals()` Check | True if content same  | True if content same              |
| Syntax            | `"Hello"`             | `new String("Hello")`             |

---

### **Quick Tips for Interviews:**

1. Use **String literal** for efficiency and performance.
2. Use **`new` operator** if you explicitly want a **different object** in heap.
3. **Always use `.equals()`** to compare string content, not `==`.

---

💡 **Example Combining Both:**

```java
String a = "Java";
String b = "Java";
String c = new String("Java");

System.out.println(a == b); // true, same object in pool
System.out.println(a == c); // false, different objects
System.out.println(a.equals(c)); // true, same content
```

---

## 18. What is String pool and how does it work?

---

## **What is String Pool in Java?**

### **Definition:**

> **String Pool** (also called String Constant Pool) is a **special memory area in the heap** where **Java stores all string literals**.
> It ensures **reusability of immutable string objects** to save memory and improve performance.

---

### **How String Pool Works:**

1. **String literal creation**:

   ```java
   String s1 = "Hello";
   String s2 = "Hello";
   ```

   * JVM checks the **String Pool** first.
   * If `"Hello"` exists, `s2` **reuses the same object**.
   * No new object is created in heap.

2. **String creation with `new`**:

   ```java
   String s3 = new String("Hello");
   ```

   * A **new object** is created in heap **even if the string exists in the pool**.
   * Can still be added to the pool using `intern()` method.

3. **`intern()` method**:

   * Returns **the reference from the String Pool** if it exists.

   ```java
   String s4 = s3.intern(); // returns reference to "Hello" in pool
   System.out.println(s1 == s4); // true
   ```

---

### **Example:**

```java
String s1 = "Java";
String s2 = "Java";
String s3 = new String("Java");
String s4 = s3.intern();

System.out.println(s1 == s2); // true, same object in pool
System.out.println(s1 == s3); // false, s3 is a new object in heap
System.out.println(s1 == s4); // true, intern() returns pool reference
```

**Output:**

```
true
false
true
```

---

### **Key Points:**

1. **Memory efficiency:** Reduces duplicate string objects.
2. **Immutable Strings:** Only immutable strings can be pooled.
3. **Created by JVM at compile time** for string literals.
4. `intern()` can **manually add** heap strings to the pool.
5. **Performance:** Comparing pooled strings with `==` is faster.

---

### **Quick Tips for Interviews:**

* **String literals → stored in String Pool.**
* **`new String()` → stored in heap, not pool.**
* Use **`intern()`** to add heap strings to the pool.
* **Immutable property of String** allows reuse in the pool safely.

---

## 19. What are the advantages of String pool?

---

## **Advantages of String Pool in Java**

1️⃣ **Memory Efficiency**

* **String Pool stores only one copy of each literal**.
* Prevents **duplicate objects** for identical strings.
* Saves heap memory when the same string is used multiple times.

```java
String s1 = "Java";
String s2 = "Java";  // s2 reuses the same object
```

✅ Only **one `"Java"` object** is created in the pool.

---

2️⃣ **Faster String Comparison**

* **Strings in the pool can be compared using `==`** instead of `.equals()` because identical literals share the **same memory reference**.

```java
System.out.println(s1 == s2); // true, faster than .equals()
```

---

3️⃣ **Improved Performance**

* Reduces **object creation overhead** for frequently used strings.
* Less **garbage collection** since fewer objects are created.

---

4️⃣ **Thread-Safety**

* Strings in the pool are **immutable**, so they can be safely shared across threads without synchronization.

---

5️⃣ **Supports Interning**

* You can use the `.intern()` method to **reuse heap strings in the pool**, further improving memory usage.

```java
String s3 = new String("Java");
String s4 = s3.intern();  // returns reference to pool object
System.out.println(s1 == s4); // true
```

---

### **Summary Table**

| Advantage          | Explanation                                   |
| ------------------ | --------------------------------------------- |
| Memory Efficient   | Only one copy of each literal is stored       |
| Faster Comparison  | `==` can be used for pooled strings           |
| Better Performance | Less object creation → less GC                |
| Thread-Safe        | Immutable strings can be shared safely        |
| Supports Interning | Heap strings can join the pool to save memory |

---

💡 **Quick Tip for Interviews:**

> **String pool = memory optimization + faster comparison + safe sharing**

---

## 20. Why String is immutable?

---

## **Why is `String` immutable in Java?**

### **Definition:**

A **String is immutable** in Java, meaning **once a String object is created, its value cannot be changed**.
If you try to modify it, **a new String object is created** in memory.

Example:

```java
String s = "Java";
s.concat(" Developer");
System.out.println(s); // Output: Java (not modified)
```

✅ A new `"Java Developer"` object is created, but `s` still points to `"Java"`.

---

## **Reasons Why String Is Immutable**

### **1️⃣ Security**

* Strings are widely used in **security-sensitive areas** like:

  * File paths
  * Network connections (e.g., URLs, IPs)
  * Database usernames & passwords
* If Strings were mutable, a malicious code could **change the content** of a String used in these operations.

Example:

```java
String dbUrl = "jdbc:mysql://localhost:3306/db";
// if mutable, it could be changed to another host at runtime
```

✅ Immutability ensures **security and reliability**.

---

### **2️⃣ String Pool Optimization**

* The **String Pool** stores one copy of each literal.
* Immutability ensures that **strings can be safely shared** across multiple references.
* If Strings were mutable, changing one reference would **affect all others**, breaking pooling.

Example:

```java
String s1 = "Java";
String s2 = "Java";
```

✅ Both point to the same object safely — because it can’t change.

---

### **3️⃣ Thread-Safety**

* Since String objects cannot change, they are **automatically thread-safe**.
* Multiple threads can share and read the same String **without synchronization**.

---

### **4️⃣ Caching and HashCode Consistency**

* Strings are often used as **keys in hash-based collections** (`HashMap`, `HashSet`).
* If String values could change, their **hashCode()** would change too — breaking the map structure.

Example:

```java
Map<String, String> map = new HashMap<>();
map.put("user", "Aditya");
```

✅ Immutability ensures the **hash code remains constant**.

---

### **5️⃣ Performance (Interning)**

* Since immutable strings can be **shared (pooled)**, they reduce **memory overhead** and improve **performance**.

---

## **Summary Table**

| Reason                   | Explanation                                             |
| ------------------------ | ------------------------------------------------------- |
| **Security**             | Prevents unauthorized modification of sensitive strings |
| **String Pooling**       | Safe sharing of literals in memory                      |
| **Thread Safety**        | Multiple threads can use same string safely             |
| **HashCode Consistency** | Stable keys for maps and sets                           |
| **Performance**          | Reuse via interning saves memory                        |

---

💡 **In short:**

> “Strings are immutable in Java to ensure **security, consistency, and performance** — especially because they are used so frequently and stored in a shared pool.”

---


# Basic Collections

## 21. What is a Collection in Java?

---

## **What is a Collection in Java?**

### **Definition:**

> A **Collection** in Java is a **group of objects** (called *elements*) that can be **stored, retrieved, manipulated, and iterated** efficiently.

It is part of the **Java Collections Framework (JCF)**, located in the package:

```java
java.util
```

---

### **Purpose of Collection:**

Before Collections, Java used **arrays**, which have limitations:

* Fixed size
* Cannot grow dynamically
* No built-in methods to search, sort, or manipulate elements

✅ Collections solve these problems by providing **ready-made data structures** like **List, Set, Queue, Map**, etc.

---

### **Hierarchy of Java Collections Framework**

```
                Iterable (Interface)
                     |
                Collection (Interface)
          /             |               \
        List           Set             Queue
        ↓               ↓                ↓
   ArrayList,      HashSet,         PriorityQueue,
   LinkedList,     TreeSet,         ArrayDeque
   Vector          LinkedHashSet
```

🔹 **Map** is not part of the Collection hierarchy but is part of the **Collections Framework**:

```
Map (Interface)
  ↳ HashMap
  ↳ LinkedHashMap
  ↳ TreeMap
  ↳ Hashtable
```

---

### **Key Interfaces in Collection Framework**

| Interface | Description                           | Common Implementations                             |
| --------- | ------------------------------------- | -------------------------------------------------- |
| **List**  | Ordered collection, allows duplicates | `ArrayList`, `LinkedList`, `Vector`, `Stack`       |
| **Set**   | Unordered collection, no duplicates   | `HashSet`, `LinkedHashSet`, `TreeSet`              |
| **Queue** | Follows FIFO, can order elements      | `PriorityQueue`, `ArrayDeque`                      |
| **Map**   | Key-value pairs (unique keys)         | `HashMap`, `LinkedHashMap`, `TreeMap`, `Hashtable` |

---

### **Common Methods of Collection Interface**

| Method               | Description                    |
| -------------------- | ------------------------------ |
| `add(E e)`           | Adds an element                |
| `remove(Object o)`   | Removes an element             |
| `size()`             | Returns number of elements     |
| `isEmpty()`          | Checks if collection is empty  |
| `contains(Object o)` | Checks if element exists       |
| `iterator()`         | Returns iterator for traversal |
| `clear()`            | Removes all elements           |

---

### **Example:**

```java
import java.util.*;

public class CollectionExample {
    public static void main(String[] args) {
        Collection<String> names = new ArrayList<>();
        names.add("Aditya");
        names.add("Ram");
        names.add("Dange");

        for (String name : names) {
            System.out.println(name);
        }
    }
}
```

**Output:**

```
Aditya
Ram
Dange
```

---

### **Advantages of Collections:**

1. **Dynamic Size** – Automatically resizes.
2. **Ready-made Methods** – Add, remove, search, sort, etc.
3. **Better Performance** – Optimized data structures.
4. **Polymorphic Usage** – You can use interfaces (`List`, `Set`) for flexibility.
5. **Thread-Safe Options** – e.g., `Vector`, `ConcurrentHashMap`.

---

### **Summary:**

| Feature                      | Description                                              |
| ---------------------------- | -------------------------------------------------------- |
| **Package**                  | `java.util`                                              |
| **Main Interface**           | `Collection<E>`                                          |
| **Subinterfaces**            | `List`, `Set`, `Queue`                                   |
| **Non-Collection Interface** | `Map`                                                    |
| **Benefits**                 | Dynamic storage, efficient manipulation, ready utilities |

---

💡 **Interview Tip:**

> A “Collection” in Java is a **framework that provides architecture to store and manipulate groups of objects** efficiently.
> The **Collection interface** is the **root** of this framework.

---

## 22. Difference between Array and ArrayList?

---

## **Difference Between Array and ArrayList in Java**

| **Feature**           | **Array**                                                    | **ArrayList**                                                |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Definition**        | Fixed-size data structure to store elements of **same type** | Resizable collection that can grow or shrink dynamically     |
| **Size**              | Fixed — must be declared at creation                         | Dynamic — increases/decreases automatically                  |
| **Type of Elements**  | Can store **primitive types** and **objects**                | Can store **only objects** (primitives need wrapper classes) |
| **Syntax**            | `int[] arr = new int[5];`                                    | `ArrayList<Integer> list = new ArrayList<>();`               |
| **Adding Elements**   | Use index → `arr[0] = 10;`                                   | Use `add()` → `list.add(10);`                                |
| **Access Elements**   | `arr[i]`                                                     | `list.get(i)`                                                |
| **Removing Elements** | Not directly possible (manual shifting needed)               | `list.remove(index)` or `list.remove(Object)`                |
| **Resizing**          | Must manually create a new array                             | Automatically managed internally                             |
| **Memory Efficiency** | More memory-efficient                                        | Slight overhead due to dynamic resizing                      |
| **Type Safety**       | Type-safe for primitives                                     | Generic → Type-safe for objects (`ArrayList<Integer>`)       |
| **Iteration**         | `for` or `for-each`                                          | `for`, `for-each`, or `Iterator`                             |
| **Performance**       | Faster for fixed-size data                                   | Slightly slower due to dynamic resizing                      |
| **Multi-dimensional** | Supports multi-dimensional arrays                            | Only single-dimension (can nest ArrayLists)                  |
| **Part of**           | Core Java (no import needed)                                 | Java Collections Framework (`java.util.ArrayList`)           |

---

### **Example: Array**

```java
int[] arr = new int[3];
arr[0] = 10;
arr[1] = 20;
arr[2] = 30;

for (int i : arr) {
    System.out.println(i);
}
```

**Output:**

```
10
20
30
```

---

### **Example: ArrayList**

```java
import java.util.*;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<Integer> list = new ArrayList<>();
        list.add(10);
        list.add(20);
        list.add(30);
        list.remove(1); // removes element at index 1

        for (int num : list) {
            System.out.println(num);
        }
    }
}
```

**Output:**

```
10
30
```

---

### **When to Use Which?**

| **Scenario**                                                 | **Use**       |
| ------------------------------------------------------------ | ------------- |
| Fixed number of elements                                     | **Array**     |
| Dynamic number of elements                                   | **ArrayList** |
| Primitive data (e.g., `int`, `char`)                         | **Array**     |
| Need in-built methods like `add()`, `remove()`, `contains()` | **ArrayList** |
| Performance critical operations                              | **Array**     |

---

### **Quick Summary**

* ✅ **Array** → Fixed size, can store primitives, faster
* ✅ **ArrayList** → Dynamic size, stores only objects, flexible and easy to use

---

💡 **Interview Tip:**

> “An Array is a fixed-size data structure, while ArrayList is a dynamic collection class that automatically grows and provides useful methods like `add()`, `remove()`, and `contains()`.”

---

## 23. What is the difference between ArrayList and LinkedList?

---

## **Difference Between ArrayList and LinkedList**

| **Feature**                       | **ArrayList**                                  | **LinkedList**                                             |
| --------------------------------- | ---------------------------------------------- | ---------------------------------------------------------- |
| **Data Structure**                | Uses **dynamic array** internally              | Uses **doubly linked list** internally                     |
| **Memory Storage**                | Elements are stored **contiguously** in memory | Each node stores **data + pointers (prev, next)**          |
| **Access (get/set)**              | **Fast (O(1))** — direct index access          | **Slow (O(n))** — must traverse nodes sequentially         |
| **Insertion / Deletion (middle)** | **Slow (O(n))** — shifting required            | **Fast (O(1))** — just change links/pointers               |
| **Insertion / Deletion (end)**    | **Fast (O(1))** — if no resize                 | **Fast (O(1))** — add at tail easily                       |
| **Memory Overhead**               | Less — only data stored                        | More — each node stores extra references (prev, next)      |
| **Iteration Speed**               | Faster (due to cache locality)                 | Slower (due to scattered memory locations)                 |
| **Use Case**                      | Best for frequent read/access operations       | Best for frequent insert/delete operations                 |
| **Implements**                    | `List` interface                               | `List`, `Deque`, `Queue` interfaces                        |
| **Random Access Supported?**      | ✅ Yes                                          | ❌ No                                                       |
| **Reverse Traversal**             | ❌ Not directly supported                       | ✅ Supported (via `descendingIterator()` or `ListIterator`) |

---

### **Internal Representation**

* **ArrayList →** Continuous block of memory

  ```
  [10][20][30][40]
  ```

* **LinkedList →** Nodes linked via pointers

  ```
  [10] <-> [20] <-> [30] <-> [40]
  ```

---

### **Example: ArrayList**

```java
import java.util.*;

public class ArrayListExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Aditya");
        list.add("Ram");
        list.add("Dange");

        System.out.println(list.get(1)); // O(1) access
    }
}
```

**Output:**

```
Ram
```

---

### **Example: LinkedList**

```java
import java.util.*;

public class LinkedListExample {
    public static void main(String[] args) {
        List<String> list = new LinkedList<>();
        list.add("Aditya");
        list.add("Ram");
        list.addFirst("Mr.");
        list.remove("Ram");

        for (String s : list) {
            System.out.println(s);
        }
    }
}
```

**Output:**

```
Mr.
Aditya
```

---

### **Performance Comparison Summary**

| **Operation**         | **ArrayList**      | **LinkedList**                   |
| --------------------- | ------------------ | -------------------------------- |
| `get(index)`          | ✅ O(1)             | ❌ O(n)                           |
| `add(element)`        | ✅ O(1) (amortized) | ✅ O(1)                           |
| `add(index, element)` | ❌ O(n)             | ✅ O(1) (if node reference known) |
| `remove(index)`       | ❌ O(n)             | ✅ O(1) (if node reference known) |
| `iterate()`           | ✅ Faster           | ❌ Slower                         |

---

### **When to Use Which**

| **Scenario**                                      | **Recommended**  |
| ------------------------------------------------- | ---------------- |
| Frequent random access (get/set)                  | ✅ **ArrayList**  |
| Frequent insertions/deletions (especially middle) | ✅ **LinkedList** |
| Memory efficiency                                 | ✅ **ArrayList**  |
| Queue or Deque operations (FIFO/LIFO)             | ✅ **LinkedList** |

---

💡 **Interview Tip:**

> “Use **ArrayList** when you mostly read data; use **LinkedList** when you frequently insert or delete elements in the middle of the list.”

---

## 24. What is HashMap? Basic operations?

---

### **What is HashMap? Basic Operations?**

A **HashMap** in Java is part of the `java.util` package.
It is a **data structure that stores key-value pairs**, where each key is unique, and each key maps to exactly one value.
It is **based on hashing**, which allows **constant-time performance (O(1))** for most operations like insertion, deletion, and retrieval.

---

### **Key Characteristics of HashMap**

1. **Stores data as key-value pairs** → `(key, value)`
2. **Does not maintain order** of elements.
3. **Allows one `null` key** and **multiple `null` values**.
4. **Not synchronized** (use `Collections.synchronizedMap()` or `ConcurrentHashMap` for thread safety).
5. **Rehashing** occurs automatically when the number of entries exceeds the capacity * load factor.

---

### **Internal Working**

* Internally uses an array of **buckets**.
* Each bucket holds a **linked list (or tree)** of entries (key-value pairs) that share the same hash.
* The **hash function** determines the index of the bucket.
* If multiple keys map to the same index → **collision** → resolved using **LinkedList (Java 7)** or **balanced tree (Java 8+)** for better performance.

---

### **Basic Operations**

| Operation          | Method                               | Description                                    |
| ------------------ | ------------------------------------ | ---------------------------------------------- |
| **Insert / Add**   | `put(K key, V value)`                | Adds or updates a key-value pair               |
| **Retrieve / Get** | `get(Object key)`                    | Returns the value associated with the key      |
| **Remove**         | `remove(Object key)`                 | Removes the entry with the specified key       |
| **Check Key**      | `containsKey(Object key)`            | Checks if the map contains the key             |
| **Check Value**    | `containsValue(Object value)`        | Checks if the map contains the value           |
| **Size**           | `size()`                             | Returns the number of entries                  |
| **Clear All**      | `clear()`                            | Removes all entries                            |
| **Iterate**        | `entrySet()`, `keySet()`, `values()` | Iterates over keys, values, or key-value pairs |

---

### **Example**

```java
import java.util.HashMap;

public class HashMapExample {
    public static void main(String[] args) {
        HashMap<Integer, String> map = new HashMap<>();

        // Add elements
        map.put(1, "Java");
        map.put(2, "Spring");
        map.put(3, "Hibernate");

        // Access value
        System.out.println(map.get(2)); // Output: Spring

        // Remove key
        map.remove(3);

        // Check key existence
        System.out.println(map.containsKey(1)); // true

        // Iterate over entries
        for (var entry : map.entrySet()) {
            System.out.println(entry.getKey() + " -> " + entry.getValue());
        }
    }
}
```

---

### **Time Complexity**

| Operation  | Average Case | Worst Case (collision-heavy) |
| ---------- | ------------ | ---------------------------- |
| `put()`    | O(1)         | O(n)                         |
| `get()`    | O(1)         | O(n)                         |
| `remove()` | O(1)         | O(n)                         |

---

## 25. What is the difference between HashSet and TreeSet?

---

### **Difference between HashSet and TreeSet**

Both **HashSet** and **TreeSet** are implementations of the **Set interface** in Java, which means they **store unique elements** (no duplicates).
However, they differ in **ordering, performance, and underlying data structures**.

---

### **🔹 1. Definition**

| Feature        | **HashSet**                               | **TreeSet**                                                                      |
| -------------- | ----------------------------------------- | -------------------------------------------------------------------------------- |
| **Purpose**    | Stores unique elements using **hashing**. | Stores unique elements in **sorted (ascending) order** using **Red-Black Tree**. |
| **Package**    | `java.util`                               | `java.util`                                                                      |
| **Implements** | `Set` interface                           | `NavigableSet` interface (extends `SortedSet`)                                   |

---

### **🔹 2. Ordering**

| Aspect                | HashSet                                      | TreeSet                                              |
| --------------------- | -------------------------------------------- | ---------------------------------------------------- |
| **Order of elements** | Unordered (no guarantee of iteration order). | Sorted in natural order (or by custom `Comparator`). |
| **Example Output**    | `[Java, Spring, Hibernate]` (unpredictable)  | `[Hibernate, Java, Spring]` (sorted alphabetically)  |

---

### **🔹 3. Underlying Data Structure**

| Aspect                           | HashSet                              | TreeSet                                |
| -------------------------------- | ------------------------------------ | -------------------------------------- |
| **Data Structure Used**          | Hash table                           | Red-Black tree                         |
| **How uniqueness is determined** | Based on `hashCode()` and `equals()` | Based on `compareTo()` or `Comparator` |

---

### **🔹 4. Performance**

| Operation                           | HashSet | TreeSet                   |
| ----------------------------------- | ------- | ------------------------- |
| **Add / Remove / Search (Average)** | O(1)    | O(log n)                  |
| **Add / Remove / Search (Worst)**   | O(n)    | O(log n)                  |
| **Iteration speed**                 | Faster  | Slower (sorted traversal) |

---

### **🔹 5. Null Elements**

| Feature           | HashSet                               | TreeSet                                 |
| ----------------- | ------------------------------------- | --------------------------------------- |
| **Allows `null`** | Yes (only one `null` element allowed) | No (`NullPointerException` if inserted) |

---

### **🔹 6. Comparator Support**

| Feature            | HashSet       | TreeSet                      |
| ------------------ | ------------- | ---------------------------- |
| **Custom sorting** | Not supported | Supported using `Comparator` |

---

### **🔹 7. Example**

```java
import java.util.*;

public class SetExample {
    public static void main(String[] args) {
        HashSet<String> hashSet = new HashSet<>();
        hashSet.add("Java");
        hashSet.add("Spring");
        hashSet.add("Hibernate");

        System.out.println("HashSet: " + hashSet); // Unordered

        TreeSet<String> treeSet = new TreeSet<>();
        treeSet.add("Java");
        treeSet.add("Spring");
        treeSet.add("Hibernate");

        System.out.println("TreeSet: " + treeSet); // Sorted order
    }
}
```

**Output:**

```
HashSet: [Spring, Hibernate, Java]   // Random order
TreeSet: [Hibernate, Java, Spring]   // Sorted order
```

---

### **🔹 8. When to Use**

| Use Case                                         | Prefer        |
| ------------------------------------------------ | ------------- |
| When order doesn’t matter and performance is key | ✅ **HashSet** |
| When sorted order is required                    | ✅ **TreeSet** |

---

### ✅ **Summary Table**

| Feature        | **HashSet**   | **TreeSet**                          |
| -------------- | ------------- | ------------------------------------ |
| Order          | Unordered     | Sorted (ascending or via Comparator) |
| Data Structure | Hash Table    | Red-Black Tree                       |
| Performance    | Faster (O(1)) | Slower (O(log n))                    |
| Null Allowed   | Yes (one)     | No                                   |
| Comparator     | Not supported | Supported                            |
| Thread-safe    | No            | No                                   |

---

## 26. What is an Iterator?

---

### **What is an Iterator in Java?**

An **Iterator** in Java is an **interface** used to **traverse (iterate)** through elements of a **Collection** (like `ArrayList`, `HashSet`, etc.) **one by one**.
It allows **safe removal of elements** during iteration and works uniformly across all Java Collection types.

---

### **🔹 Definition**

Iterator belongs to the package:

```java
java.util.Iterator
```

It is part of the **Java Collection Framework (JCF)**.

---

### **🔹 Key Features**

1. **Used for traversing collections** (List, Set, Queue, etc.)
2. **Works in a forward-only direction** (unlike `ListIterator`, which can go both ways)
3. **Supports safe removal** of elements while iterating.
4. **Universal cursor** — works for all collection classes.

---

### **🔹 Common Methods of Iterator Interface**

| Method              | Description                                        |
| ------------------- | -------------------------------------------------- |
| `boolean hasNext()` | Returns `true` if the iteration has more elements. |
| `E next()`          | Returns the next element in the iteration.         |
| `void remove()`     | Removes the last element returned by the iterator. |

---

### **🔹 Example: Using Iterator with ArrayList**

```java
import java.util.*;

public class IteratorExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Java");
        list.add("Spring");
        list.add("Hibernate");

        Iterator<String> iterator = list.iterator();

        while (iterator.hasNext()) {
            String item = iterator.next();
            System.out.println(item);

            if (item.equals("Spring")) {
                iterator.remove(); // Safe removal
            }
        }

        System.out.println("After removal: " + list);
    }
}
```

**Output:**

```
Java
Spring
Hibernate
After removal: [Java, Hibernate]
```

---

### **🔹 Why Use Iterator Instead of For Loop?**

✅ Works with all types of collections (unlike index-based loops).
✅ Prevents `ConcurrentModificationException` when removing elements.
✅ Makes code cleaner and independent of collection structure.

---

### **🔹 Limitations**

* Traverses **only in one direction** (forward).
* **Cannot modify elements** (only remove).
* **Not thread-safe** (unless used with synchronized collections or `CopyOnWriteArrayList`).

---

### **🔹 Related Interfaces**

| Interface        | Description                                     |
| ---------------- | ----------------------------------------------- |
| **Iterator**     | Traverses elements in forward direction.        |
| **ListIterator** | Traverses in both directions (only for `List`). |
| **Enumeration**  | Legacy interface (used before Java 1.2).        |

---

### ✅ **Summary**

| Feature             | **Iterator**           |
| ------------------- | ---------------------- |
| Traversal Direction | Forward only           |
| Removal Support     | Yes (`remove()`)       |
| Works On            | All Collection classes |
| Replace Elements    | No                     |
| Introduced In       | JDK 1.2                |

---

## 27. What is the difference between List and Set?

### **27. Difference Between List and Set in Java**

Both **List** and **Set** are part of the **Java Collection Framework (JCF)** and belong to the `java.util` package.
They are used to store groups of objects, but their **behavior, ordering, and uniqueness** differ.

---

### 🔹 **1. Basic Definition**

| Feature        | **List**                                                  | **Set**                                                     |
| -------------- | --------------------------------------------------------- | ----------------------------------------------------------- |
| **Definition** | An ordered collection that allows **duplicate elements**. | An unordered collection that **does not allow duplicates**. |
| **Implements** | `java.util.List` interface                                | `java.util.Set` interface                                   |

---

### 🔹 **2. Key Characteristics**

| Property               | **List**                                 | **Set**                                          |
| ---------------------- | ---------------------------------------- | ------------------------------------------------ |
| **Order of elements**  | Maintains insertion order (index-based). | No guaranteed order (depends on implementation). |
| **Duplicates allowed** | ✅ Yes                                    | ❌ No                                             |
| **Index-based access** | ✅ Yes (`get(int index)`)                 | ❌ No                                             |
| **Null elements**      | Allows multiple `null` values            | Allows at most one `null` value                  |

---

### 🔹 **3. Common Implementations**

| **List** Implementations | **Set** Implementations |
| ------------------------ | ----------------------- |
| `ArrayList`              | `HashSet`               |
| `LinkedList`             | `LinkedHashSet`         |
| `Vector`                 | `TreeSet`               |
| `Stack`                  | `EnumSet`               |

---

### 🔹 **4. Performance Comparison**

| Operation          | **List**            | **Set**                                  |
| ------------------ | ------------------- | ---------------------------------------- |
| **Add element**    | O(1) in `ArrayList` | O(1) in `HashSet`, O(log n) in `TreeSet` |
| **Search element** | O(n) in `ArrayList` | O(1) in `HashSet`, O(log n) in `TreeSet` |
| **Remove element** | O(n) in `ArrayList` | O(1) in `HashSet`, O(log n) in `TreeSet` |

---

### 🔹 **5. Example**

```java
import java.util.*;

public class ListSetExample {
    public static void main(String[] args) {
        // List Example
        List<String> list = new ArrayList<>();
        list.add("Java");
        list.add("Spring");
        list.add("Java"); // duplicate allowed
        System.out.println("List: " + list);

        // Set Example
        Set<String> set = new HashSet<>();
        set.add("Java");
        set.add("Spring");
        set.add("Java"); // duplicate ignored
        System.out.println("Set: " + set);
    }
}
```

**Output:**

```
List: [Java, Spring, Java]
Set: [Java, Spring]
```

---

### 🔹 **6. When to Use What**

| Scenario                                                          | Use                     |
| ----------------------------------------------------------------- | ----------------------- |
| When you need **ordered elements** and **duplicates** are allowed | ✅ Use **List**          |
| When you need **unique elements** and order doesn’t matter        | ✅ Use **Set**           |
| When you need **sorted unique elements**                          | ✅ Use **TreeSet**       |
| When you need **insertion order + uniqueness**                    | ✅ Use **LinkedHashSet** |

---

### ✅ **Summary Table**

| Feature                | **List**              | **Set**                                                    |
| ---------------------- | --------------------- | ---------------------------------------------------------- |
| Order maintained       | Yes                   | Depends (HashSet: No, LinkedHashSet: Yes, TreeSet: Sorted) |
| Duplicates allowed     | Yes                   | No                                                         |
| Index-based            | Yes                   | No                                                         |
| Null elements          | Multiple              | One                                                        |
| Performance            | O(n) search           | O(1) or O(log n) search                                    |
| Common Implementations | ArrayList, LinkedList | HashSet, LinkedHashSet, TreeSet                            |

---

Would you like me to give a **real-world example** (like how `List` and `Set` are used in a project — e.g., employee IDs vs employee names)?

---

## 28. Array vs List

### **28. Difference Between Array and List in Java**

Both **Array** and **List** are used to store multiple elements in Java,
but they differ in **size, flexibility, performance, and implementation**.

---

### 🔹 **1. Basic Definition**

| Feature        | **Array**                                                            | **List**                                                                                 |
| -------------- | -------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| **Definition** | A fixed-size data structure used to store elements of the same type. | A dynamic data structure (part of Collection Framework) that can grow or shrink in size. |
| **Package**    | Part of core Java (`java.lang`)                                      | Part of Collection Framework (`java.util`)                                               |

---

### 🔹 **2. Size & Resizing**

| Property    | **Array**                            | **List**                                                          |
| ----------- | ------------------------------------ | ----------------------------------------------------------------- |
| **Size**    | Fixed — must be defined at creation. | Dynamic — automatically resizes as elements are added or removed. |
| **Example** | `int[] arr = new int[5];`            | `List<Integer> list = new ArrayList<>();`                         |

---

### 🔹 **3. Type Restriction**

| Property             | **Array**                                                | **List**                                        |
| -------------------- | -------------------------------------------------------- | ----------------------------------------------- |
| **Type of elements** | Stores elements of the same type (primitive or objects). | Stores only **objects** (but can use generics). |
| **Example**          | `int[] arr = {1, 2, 3};`                                 | `List<Integer> list = List.of(1, 2, 3);`        |

---

### 🔹 **4. Performance**

| Operation              | **Array** | **List (ArrayList)** |
| ---------------------- | --------- | -------------------- |
| **Access by index**    | O(1)      | O(1)                 |
| **Insertion (end)**    | O(1)      | Amortized O(1)       |
| **Insertion (middle)** | O(n)      | O(n)                 |
| **Deletion**           | O(n)      | O(n)                 |

---

### 🔹 **5. Memory Efficiency**

| Feature          | **Array**                                | **List**                                                     |
| ---------------- | ---------------------------------------- | ------------------------------------------------------------ |
| **Memory usage** | Less memory, as it’s a simple structure. | More memory due to dynamic resizing and internal management. |

---

### 🔹 **6. Flexibility**

| Feature              | **Array**                     | **List**                                                        |
| -------------------- | ----------------------------- | --------------------------------------------------------------- |
| **Resizing**         | Not allowed.                  | Automatically resizes when adding/removing elements.            |
| **Built-in methods** | Very few (manual operations). | Many built-in methods (`add()`, `remove()`, `contains()`, etc.) |

---

### 🔹 **7. Primitive Types**

| Feature                 | **Array**             | **List**                                             |
| ----------------------- | --------------------- | ---------------------------------------------------- |
| **Supports primitives** | ✅ Yes (e.g., `int[]`) | ❌ No (must use wrapper classes like `List<Integer>`) |

---

### 🔹 **8. Example**

```java
import java.util.*;

public class ArrayVsListExample {
    public static void main(String[] args) {
        // Array
        int[] arr = {1, 2, 3, 4};
        System.out.println("Array element: " + arr[2]);

        // List
        List<Integer> list = new ArrayList<>();
        list.add(10);
        list.add(20);
        list.add(30);
        System.out.println("List element: " + list.get(2));
    }
}
```

**Output:**

```
Array element: 3
List element: 30
```

---

### 🔹 **9. Conversion Between Array and List**

| Conversion       | Example                                         |
| ---------------- | ----------------------------------------------- |
| **Array → List** | `List<Integer> list = Arrays.asList(arr);`      |
| **List → Array** | `Integer[] arr = list.toArray(new Integer[0]);` |

---

### ✅ **Summary Table**

| Feature           | **Array**                        | **List**                    |
| ----------------- | -------------------------------- | --------------------------- |
| Size              | Fixed                            | Dynamic                     |
| Type              | Homogeneous (same type)          | Generic (any object type)   |
| Duplicates        | Allowed                          | Allowed                     |
| Primitive support | Yes                              | No (uses wrapper classes)   |
| Performance       | Slightly faster                  | Slightly slower             |
| Resizing          | Not possible                     | Automatically resizes       |
| Null values       | Allowed                          | Allowed                     |
| Common use        | Low-level, performance-sensitive | General-purpose collections |

---

### 💡 **When to Use**

| Scenario                                           | Recommended                          |
| -------------------------------------------------- | ------------------------------------ |
| You need fixed-size, high-performance data storage | ✅ **Array**                          |
| You need dynamic resizing and flexibility          | ✅ **List (ArrayList or LinkedList)** |

---

Would you like me to explain the **difference between `ArrayList` and `LinkedList`** next (in terms of internal working and performance)?

---

## 29. Set vs List

### **29. Difference Between Set and List in Java**

Both **Set** and **List** are part of the **Java Collection Framework (JCF)** and are used to store a group of objects —
but they differ mainly in **ordering, duplication rules, and performance**.

---

### 🔹 **1. Basic Definition**

| Feature         | **List**                                                      | **Set**                                                                     |
| --------------- | ------------------------------------------------------------- | --------------------------------------------------------------------------- |
| **Definition**  | An **ordered** collection that **allows duplicate elements**. | An **unordered (or sorted)** collection that **does not allow duplicates**. |
| **Implements**  | `java.util.List`                                              | `java.util.Set`                                                             |
| **Typical Use** | When you need to maintain insertion order and duplicates.     | When you need unique elements only.                                         |

---

### 🔹 **2. Ordering**

| Feature                | **List**                              | **Set**                                                                                                                         |
| ---------------------- | ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| **Order maintained?**  | ✅ Yes (insertion order is preserved). | ⚠️ Depends on implementation: <br>• `HashSet` → No order <br>• `LinkedHashSet` → Insertion order <br>• `TreeSet` → Sorted order |
| **Index-based access** | ✅ Yes (`list.get(index)`)             | ❌ No (no index)                                                                                                                 |

---

### 🔹 **3. Duplicates**

| Feature                 | **List** | **Set**                        |
| ----------------------- | -------- | ------------------------------ |
| **Duplicates allowed?** | ✅ Yes    | ❌ No (all elements are unique) |

---

### 🔹 **4. Null Elements**

| Feature          | **List**                           | **Set**                                                               |
| ---------------- | ---------------------------------- | --------------------------------------------------------------------- |
| **Null support** | Can contain multiple `null` values | Can contain **only one** `null` value (`TreeSet` does not allow null) |

---

### 🔹 **5. Common Implementations**

| **List**     | **Set**         |
| ------------ | --------------- |
| `ArrayList`  | `HashSet`       |
| `LinkedList` | `LinkedHashSet` |
| `Vector`     | `TreeSet`       |
| `Stack`      | `EnumSet`       |

---

### 🔹 **6. Performance (Average Case)**

| Operation             | **List (ArrayList)** | **Set (HashSet)** |
| --------------------- | -------------------- | ----------------- |
| **Insertion**         | O(1) (amortized)     | O(1)              |
| **Deletion**          | O(n)                 | O(1)              |
| **Search (contains)** | O(n)                 | O(1)              |
| **Access by index**   | O(1)                 | ❌ Not supported   |

---

### 🔹 **7. Example**

```java
import java.util.*;

public class SetVsListExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Java");
        list.add("Spring");
        list.add("Java"); // duplicate allowed

        Set<String> set = new HashSet<>();
        set.add("Java");
        set.add("Spring");
        set.add("Java"); // duplicate ignored

        System.out.println("List: " + list);
        System.out.println("Set: " + set);
    }
}
```

**Output:**

```
List: [Java, Spring, Java]
Set: [Java, Spring]   // Unordered and unique
```

---

### 🔹 **8. When to Use**

| Use Case                             | Prefer              |
| ------------------------------------ | ------------------- |
| Need to maintain insertion order     | ✅ **List**          |
| Need unique elements (no duplicates) | ✅ **Set**           |
| Need fast search without duplicates  | ✅ **HashSet**       |
| Need sorted unique elements          | ✅ **TreeSet**       |
| Need insertion order + uniqueness    | ✅ **LinkedHashSet** |

---

### ✅ **Summary Table**

| Feature            | **List**                           | **Set**                              |
| ------------------ | ---------------------------------- | ------------------------------------ |
| Duplicates allowed | ✅ Yes                              | ❌ No                                 |
| Order maintained   | ✅ Yes                              | ⚙️ Depends on implementation         |
| Index-based access | ✅ Yes                              | ❌ No                                 |
| Null values        | Multiple                           | One (except TreeSet)                 |
| Performance        | Slower for search                  | Faster for search (HashSet)          |
| Use case           | Ordered collection with duplicates | Unique collection without duplicates |

---

### 💡 **Real-World Example**

* **List** → Use for **ordered data** like a list of employees that can contain duplicates (e.g., names).
* **Set** → Use for **unique data** like employee IDs or usernames.

---

Would you like me to explain **HashSet vs LinkedHashSet vs TreeSet** next — with internal workings and use cases?

---

# Exception Handling

## 30. What is an Exception? Types of exceptions?

### **30. What is an Exception in Java? Types of Exceptions**

In Java, **exceptions** are a core concept used for **handling runtime errors** in a program.

---

### **🔹 1. What is an Exception?**

> An **exception** is an **event that occurs during the execution of a program** that **disrupts the normal flow** of instructions.

It is represented as an **object** of the class `Throwable` or its subclasses.

**Hierarchy of Exceptions:**

```
Throwable
 ├── Error
 └── Exception
      ├── Checked Exception
      └── Unchecked Exception (RuntimeException)
```

---

### **🔹 2. Types of Exceptions in Java**

#### **A. Checked Exceptions**

* **Definition:** Exceptions that **must be handled** at **compile-time** using `try-catch` or declared with `throws`.
* **Examples:** `IOException`, `SQLException`, `ClassNotFoundException`
* **When it occurs:** Usually **external errors**, e.g., file not found, database errors.

```java
import java.io.*;

public class CheckedExceptionExample {
    public static void main(String[] args) {
        try {
            FileReader file = new FileReader("file.txt"); // may throw FileNotFoundException
        } catch (FileNotFoundException e) {
            System.out.println("File not found!");
        }
    }
}
```

---

#### **B. Unchecked Exceptions (Runtime Exceptions)**

* **Definition:** Exceptions that **occur during runtime** and **do not need to be declared or caught**.
* **Examples:** `ArithmeticException`, `NullPointerException`, `ArrayIndexOutOfBoundsException`
* **When it occurs:** Usually due to **programming logic errors**.

```java
public class UncheckedExceptionExample {
    public static void main(String[] args) {
        int a = 10, b = 0;
        System.out.println(a / b); // Throws ArithmeticException at runtime
    }
}
```

---

#### **C. Error**

* **Definition:** Severe problems that **applications usually cannot handle**.
* **Examples:** `OutOfMemoryError`, `StackOverflowError`
* **Note:** Errors are **not exceptions** but are subclasses of `Throwable`.

---

### **🔹 3. Common Exception Classes in Java**

| Exception                        | Type      | Description                          |
| -------------------------------- | --------- | ------------------------------------ |
| `IOException`                    | Checked   | Input/output failure (file, network) |
| `SQLException`                   | Checked   | Database access error                |
| `ClassNotFoundException`         | Checked   | Class not found at runtime           |
| `ArithmeticException`            | Unchecked | Arithmetic errors (divide by zero)   |
| `NullPointerException`           | Unchecked | Accessing null reference             |
| `ArrayIndexOutOfBoundsException` | Unchecked | Array index invalid                  |
| `NumberFormatException`          | Unchecked | Invalid parsing of numbers           |

---

### **🔹 4. Key Points**

1. **Checked exceptions** → Compile-time → Must be handled
2. **Unchecked exceptions** → Runtime → Optional to handle
3. **Errors** → Severe → Usually cannot be handled
4. **Throwable** → Base class for both `Error` and `Exception`

---

### **🔹 5. Example: Try-Catch-Finally**

```java
public class ExceptionExample {
    public static void main(String[] args) {
        try {
            int[] arr = {1, 2, 3};
            System.out.println(arr[5]); // ArrayIndexOutOfBoundsException
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Invalid index!");
        } finally {
            System.out.println("Finally block executed.");
        }
    }
}
```

**Output:**

```
Invalid index!
Finally block executed.
```

---

💡 **Interview Tip:**

> "Exceptions represent **abnormal conditions** in a program. Checked exceptions must be **handled at compile-time**, whereas unchecked exceptions occur at **runtime due to programming errors**."

---

I can next explain **Difference between Checked and Unchecked Exceptions** with a **table and real-time examples**, which is a very common follow-up interview question.

Do you want me to do that?

---

## 31. What is the difference between chacked and unchecked exceptions?

### **31. Difference Between Checked and Unchecked Exceptions in Java**

This is a **classic Java interview question**. The distinction is important because it affects **how you handle exceptions in your code**.

---

### **🔹 1. Basic Definitions**

| Type                    | Definition                                                                                                                                             |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Checked Exception**   | Exceptions that are **checked at compile-time**. The compiler forces you to **handle** or **declare** them using `try-catch` or `throws`.              |
| **Unchecked Exception** | Exceptions that are **not checked at compile-time**. They occur **during runtime** due to programming errors and **do not require explicit handling**. |

---

### **🔹 2. Key Differences**

| Feature                | Checked Exception                                                               | Unchecked Exception                                                             |
| ---------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| **Checked at**         | Compile-time                                                                    | Runtime                                                                         |
| **Handling required?** | ✅ Must handle or declare                                                        | ❌ Optional                                                                      |
| **Cause**              | External factors (file, network, database)                                      | Programming errors (null pointer, arithmetic)                                   |
| **Example classes**    | `IOException`, `SQLException`, `ClassNotFoundException`                         | `NullPointerException`, `ArrayIndexOutOfBoundsException`, `ArithmeticException` |
| **Example Code**       | `FileReader file = new FileReader("test.txt");` → compiler error if not handled | `int x = 10/0;` → runtime error                                                 |
| **Hierarchy**          | Subclass of `Exception` (but not `RuntimeException`)                            | Subclass of `RuntimeException`                                                  |

---

### **🔹 3. Example: Checked Exception**

```java
import java.io.*;

public class CheckedExample {
    public static void main(String[] args) {
        try {
            FileReader file = new FileReader("test.txt"); // FileNotFoundException
        } catch (FileNotFoundException e) {
            System.out.println("File not found!");
        }
    }
}
```

**Output:**

```
File not found!
```

> Compiler will throw an error if `FileNotFoundException` is **not handled**.

---

### **🔹 4. Example: Unchecked Exception**

```java
public class UncheckedExample {
    public static void main(String[] args) {
        int a = 10, b = 0;
        System.out.println(a / b); // ArithmeticException
    }
}
```

**Output:**

```
Exception in thread "main" java.lang.ArithmeticException: / by zero
```

> No compile-time error; occurs **only at runtime**.

---

### **🔹 5. Summary Table**

| Feature            | Checked                       | Unchecked                                     |
| ------------------ | ----------------------------- | --------------------------------------------- |
| Checked at         | Compile-time                  | Runtime                                       |
| Handling           | Mandatory                     | Optional                                      |
| Cause              | External problems             | Programming errors                            |
| Examples           | `IOException`, `SQLException` | `NullPointerException`, `ArithmeticException` |
| Compiler Enforces? | Yes                           | No                                            |

---

💡 **Interview Tip:**

> "Use **checked exceptions** for **recoverable conditions** (like file not found), and **unchecked exceptions** for **programming errors** (like dividing by zero)."

---

If you want, I can next explain **Difference between `throw` and `throws` in Java**, which naturally follows the exception topic.

Do you want me to cover that next?

---

## 32. What is try-catch-finally block?

### **32. What is `try-catch-finally` Block in Java**

In Java, **`try-catch-finally`** is used for **handling exceptions** and **ensuring certain code executes** regardless of exceptions.

---

### **🔹 1. Structure of `try-catch-finally`**

```java
try {
    // Code that might throw an exception
} catch (ExceptionType1 e1) {
    // Code to handle ExceptionType1
} catch (ExceptionType2 e2) {
    // Code to handle ExceptionType2
} finally {
    // Code that will always execute
}
```

* **`try` block:** Contains code that may throw exceptions.
* **`catch` block:** Handles the exception. You can have multiple `catch` blocks for different exception types.
* **`finally` block:** Executes **always**, whether an exception occurs or not. Often used for cleanup (e.g., closing files, releasing resources).

---

### **🔹 2. Key Points**

1. `try` block **must be followed by at least one** `catch` or `finally`.

   * ✅ Valid: `try + catch`
   * ✅ Valid: `try + finally`
   * ❌ Invalid: `try` alone
2. **Multiple catch blocks** can be used to handle different exceptions.
3. `finally` executes even if `return` is used in `try` or `catch`.
4. **`finally` block is optional**, but highly recommended for resource cleanup.

---

### **🔹 3. Example: Basic Try-Catch-Finally**

```java
public class TryCatchFinallyExample {
    public static void main(String[] args) {
        try {
            int a = 10, b = 0;
            System.out.println("Result: " + (a / b)); // May throw ArithmeticException
        } catch (ArithmeticException e) {
            System.out.println("Cannot divide by zero!");
        } finally {
            System.out.println("This block always executes.");
        }
    }
}
```

**Output:**

```
Cannot divide by zero!
This block always executes.
```

---

### **🔹 4. Example: Try with Multiple Catch Blocks**

```java
public class MultipleCatchExample {
    public static void main(String[] args) {
        try {
            int[] arr = {1, 2, 3};
            System.out.println(arr[5]); // ArrayIndexOutOfBoundsException
        } catch (ArithmeticException e) {
            System.out.println("Arithmetic error occurred.");
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Array index is out of bounds.");
        } finally {
            System.out.println("Cleanup code executed.");
        }
    }
}
```

**Output:**

```
Array index is out of bounds.
Cleanup code executed.
```

---

### **🔹 5. Example: Try-Finally without Catch**

```java
public class TryFinallyExample {
    public static void main(String[] args) {
        try {
            System.out.println("Inside try block.");
        } finally {
            System.out.println("Finally block executed.");
        }
    }
}
```

**Output:**

```
Inside try block.
Finally block executed.
```

---

### **🔹 6. Use Cases of Finally**

* Closing **file streams**
* Closing **database connections**
* Releasing **network resources**

---

💡 **Interview Tip:**

> "Use `try` for risky code, `catch` to handle exceptions, and `finally` for cleanup. Even if you use `return` in `try`, the `finally` block still executes."

---

Next, I can explain the **difference between `throw` and `throws`** in Java, which naturally follows the `try-catch-finally` topic.

Do you want me to cover that?

---

## 33. Can we use try without catch?

### **33. Can We Use `try` Without `catch` in Java?**

Yes, **you can use a `try` block without a `catch` block**, but **only if it is followed by a `finally` block**.

---

### **🔹 Rules**

1. **`try` must be followed by either `catch` or `finally`** (or both).
2. **`catch` is optional** if you have a `finally` block.
3. `finally` block **always executes**, regardless of whether an exception occurs or not.

---

### **🔹 Syntax**

```java
try {
    // Code that may throw an exception
} finally {
    // Code that always executes
}
```

* This is valid in Java.
* Without `catch` or `finally`, a `try` block alone **is invalid** and will give a compile-time error.

---

### **🔹 Example: Try Without Catch**

```java
public class TryWithoutCatch {
    public static void main(String[] args) {
        try {
            int a = 10, b = 0;
            System.out.println("Result: " + (a / b)); // Throws ArithmeticException
        } finally {
            System.out.println("Finally block executed.");
        }
    }
}
```

**Output:**

```
Finally block executed.
Exception in thread "main" java.lang.ArithmeticException: / by zero
```

* Notice that even though there is **no `catch`**, the **finally block executes**.
* The exception is **not handled** and will propagate to the JVM.

---

### **🔹 Key Points**

1. `try` **cannot exist alone**.
   ❌ Invalid:

   ```java
   try {
       System.out.println("Hello");
   }
   ```
2. `try` **without `catch`** is valid only if followed by `finally`.
3. Useful when you want to **ensure cleanup** but let the exception propagate.

---

💡 **Interview Tip:**

> "You can use `try` without `catch` if you have a `finally` block to execute cleanup code, but any exception will still propagate to the caller."

---

If you want, I can next explain **difference between `throw` and `throws` in Java**, which is the next natural question after `try-catch-finally`.

Do you want me to cover that?

---

## 34. What is throw vs throws?

### **34. Difference Between `throw` and `throws` in Java**

Both **`throw`** and **`throws`** are related to exception handling, but they serve **different purposes**.

---

### **🔹 1. Basic Definitions**

| Keyword    | Definition                                                                                                                                                |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **throw**  | Used **to explicitly throw an exception** in a method or block. It throws **one exception at a time**.                                                    |
| **throws** | Used in a **method declaration** to indicate that the method **might throw one or more exceptions**. It informs the **caller** about possible exceptions. |

---

### **🔹 2. Key Differences**

| Feature                  | **throw**                                       | **throws**                                                         |
| ------------------------ | ----------------------------------------------- | ------------------------------------------------------------------ |
| **Purpose**              | To actually **throw an exception**.             | To **declare exceptions** that a method may throw.                 |
| **Where used**           | Inside **method body** or block.                | In **method signature/declaration**.                               |
| **Number of exceptions** | Can throw **only one exception** at a time.     | Can declare **multiple exceptions**, separated by commas.          |
| **Effect**               | Immediately throws the exception to the caller. | Passes responsibility of handling the exception to the **caller**. |
| **Example**              | `throw new IOException("File missing");`        | `void readFile() throws IOException, SQLException`                 |
| **Checked Exception**    | Must be **handled or declared**.                | Method must **declare checked exceptions** using `throws`.         |

---

### **🔹 3. Example Using `throw`**

```java
public class ThrowExample {
    static void checkAge(int age) {
        if (age < 18) {
            throw new ArithmeticException("Age must be at least 18");
        } else {
            System.out.println("Access granted");
        }
    }

    public static void main(String[] args) {
        checkAge(15); // Will throw exception
    }
}
```

**Output:**

```
Exception in thread "main" java.lang.ArithmeticException: Age must be at least 18
```

---

### **🔹 4. Example Using `throws`**

```java
import java.io.*;

public class ThrowsExample {
    static void readFile() throws IOException {
        FileReader file = new FileReader("test.txt"); // Might throw FileNotFoundException
    }

    public static void main(String[] args) {
        try {
            readFile();
        } catch (IOException e) {
            System.out.println("File not found!");
        }
    }
}
```

* `throws` **declares the exception**, while `throw` **actually throws it**.

---

### **🔹 5. Quick Summary**

| Feature                  | `throw`                  | `throws`                                           |
| ------------------------ | ------------------------ | -------------------------------------------------- |
| **Used for**             | Throwing exception       | Declaring exception in method signature            |
| **Placement**            | Inside method/block      | After method signature                             |
| **Number of exceptions** | One at a time            | Multiple, separated by commas                      |
| **Effect**               | Throws immediately       | Passes exception handling responsibility to caller |
| **Example**              | `throw new Exception();` | `void myMethod() throws IOException, SQLException` |

---

💡 **Interview Tip:**

> "`throw` is used to **throw** an exception, `throws` is used to **declare** it to the caller."

---

If you want, I can next explain **Difference between `final`, `finally`, and `finalize` in Java**, which is another common interview topic linked with exception handling.

Do you want me to cover that next?

---

## 35. What are the use cases of creating user-defined exceptions?

### **35. Use Cases of Creating User-Defined Exceptions in Java**

In Java, you can **create your own custom exceptions** by extending the `Exception` class (checked) or `RuntimeException` class (unchecked).
User-defined exceptions are useful when **built-in exceptions are not descriptive enough** or when you want **specific application-level error handling**.

---

### **🔹 1. Why Create User-Defined Exceptions?**

1. **Better readability & maintainability:**

   * Makes your code **self-explanatory**.
   * Example: `InsufficientBalanceException` clearly indicates the error.

2. **Domain-specific exception handling:**

   * Useful in business logic where standard exceptions are insufficient.

3. **Encapsulation of error details:**

   * You can include **custom messages or error codes**.

4. **Separate normal flow from error handling:**

   * Helps to **differentiate application errors** from system errors.

5. **Promotes clean exception hierarchy:**

   * You can organize multiple custom exceptions for a specific module.

---

### **🔹 2. Common Use Cases**

| Scenario                      | Example Custom Exception                                         |
| ----------------------------- | ---------------------------------------------------------------- |
| **Banking application**       | `InsufficientBalanceException` when withdraw amount > balance    |
| **Authentication / Security** | `InvalidLoginException` for wrong credentials                    |
| **E-commerce application**    | `ProductNotFoundException` when requested product does not exist |
| **Data validation**           | `InvalidAgeException` if age < 18 for registration               |
| **Order processing**          | `OrderNotProcessedException` for failed transactions             |

---

### **🔹 3. Example: Creating a User-Defined Checked Exception**

```java
// Custom Exception Class
class InsufficientBalanceException extends Exception {
    public InsufficientBalanceException(String message) {
        super(message);
    }
}

// Bank Account Class
class BankAccount {
    private double balance = 1000;

    public void withdraw(double amount) throws InsufficientBalanceException {
        if (amount > balance) {
            throw new InsufficientBalanceException("Insufficient balance for withdrawal!");
        } else {
            balance -= amount;
            System.out.println("Withdrawal successful. Remaining balance: " + balance);
        }
    }
}

// Main Class
public class CustomExceptionExample {
    public static void main(String[] args) {
        BankAccount account = new BankAccount();
        try {
            account.withdraw(1500); // Will throw exception
        } catch (InsufficientBalanceException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

**Output:**

```
Insufficient balance for withdrawal!
```

---

### **🔹 4. Example: Creating a User-Defined Unchecked Exception**

```java
class InvalidAgeException extends RuntimeException {
    public InvalidAgeException(String message) {
        super(message);
    }
}

public class Registration {
    public static void registerUser(int age) {
        if (age < 18) {
            throw new InvalidAgeException("User must be at least 18 years old!");
        } else {
            System.out.println("Registration successful.");
        }
    }

    public static void main(String[] args) {
        registerUser(15); // Will throw unchecked exception
    }
}
```

**Output:**

```
Exception in thread "main" java.lang.InvalidAgeException: User must be at least 18 years old!
```

---

### **🔹 5. Summary**

| Feature     | Built-in Exceptions      | User-Defined Exceptions                               |
| ----------- | ------------------------ | ----------------------------------------------------- |
| Purpose     | General-purpose          | Domain-specific / business logic                      |
| Readability | Moderate                 | High (descriptive & self-explanatory)                 |
| Control     | Limited                  | Full control over exception behavior                  |
| Use Cases   | File I/O, network errors | Banking, authentication, validation, custom workflows |

---

💡 **Interview Tip:**

> "Use user-defined exceptions when you want **clear, domain-specific error messages** and better separation of **normal logic and error handling** in your application."

---

If you want, I can next explain **Difference between `final`, `finally`, and `finalize` in Java**, which is another highly asked exception-related topic.

Do you want me to cover that next?

---

## 36. How to handle user-defined exception?

### **36. How to Handle User-Defined Exceptions in Java**

Once you create a **user-defined exception**, handling it works similarly to handling **built-in exceptions** using **try-catch** or **propagating with throws**.

---

### **🔹 1. Handling Checked User-Defined Exceptions**

* If your custom exception **extends `Exception`** (checked exception), the compiler **forces you to handle it**.
* You can use:

  1. **`try-catch` block**
  2. **`throws` keyword** to propagate the exception

---

#### **Example 1: Handling with `try-catch`**

```java
// Custom Checked Exception
class InsufficientBalanceException extends Exception {
    public InsufficientBalanceException(String message) {
        super(message);
    }
}

// Bank Account Class
class BankAccount {
    private double balance = 1000;

    public void withdraw(double amount) throws InsufficientBalanceException {
        if (amount > balance) {
            throw new InsufficientBalanceException("Insufficient balance!");
        }
        balance -= amount;
        System.out.println("Withdrawal successful. Remaining balance: " + balance);
    }
}

// Main Class
public class UserDefinedExceptionHandling {
    public static void main(String[] args) {
        BankAccount account = new BankAccount();
        try {
            account.withdraw(1500); // May throw exception
        } catch (InsufficientBalanceException e) {
            System.out.println("Exception caught: " + e.getMessage());
        }
    }
}
```

**Output:**

```
Exception caught: Insufficient balance!
```

---

#### **Example 2: Propagating with `throws`**

```java
public class ExceptionPropagation {
    static void processWithdrawal(double amount) throws InsufficientBalanceException {
        BankAccount account = new BankAccount();
        account.withdraw(amount); // May throw user-defined exception
    }

    public static void main(String[] args) {
        try {
            processWithdrawal(1500);
        } catch (InsufficientBalanceException e) {
            System.out.println("Exception handled in main: " + e.getMessage());
        }
    }
}
```

---

### **🔹 2. Handling Unchecked User-Defined Exceptions**

* If your custom exception **extends `RuntimeException`**, handling is **optional**.
* Can be handled using `try-catch`, or allowed to propagate to the JVM.

```java
class InvalidAgeException extends RuntimeException {
    public InvalidAgeException(String message) {
        super(message);
    }
}

public class UncheckedExceptionHandling {
    public static void registerUser(int age) {
        if (age < 18) {
            throw new InvalidAgeException("User must be at least 18!");
        }
        System.out.println("Registration successful.");
    }

    public static void main(String[] args) {
        try {
            registerUser(15); // Throws unchecked exception
        } catch (InvalidAgeException e) {
            System.out.println("Caught: " + e.getMessage());
        }
    }
}
```

**Output:**

```
Caught: User must be at least 18!
```

---

### **🔹 3. Summary**

| Feature              | Checked User-Defined Exception             | Unchecked User-Defined Exception |
| -------------------- | ------------------------------------------ | -------------------------------- |
| Base Class           | `Exception`                                | `RuntimeException`               |
| Compiler Enforcement | Must handle or declare                     | Optional to handle               |
| Handling Mechanism   | `try-catch` or `throws`                    | `try-catch` (optional)           |
| Use Case             | Business logic requiring explicit handling | Programming errors / validation  |

---

💡 **Interview Tip:**

> "Always use **checked user-defined exceptions** for **recoverable business errors** and **unchecked exceptions** for **programming/validation errors**. Handle them using **try-catch** or propagate using `throws`."

---

If you want, I can next explain **Difference between `final`, `finally`, and `finalize` in Java**, which is another common interview question related to exceptions and resource management.

Do you want me to cover that next?

---

## 37. What is a NullPointerException & how to prevent it?

### **37. What is a `NullPointerException` & How to Prevent It in Java**

---

### **🔹 1. What is NullPointerException (NPE)?**

A **`NullPointerException`** occurs when your code **tries to use an object reference that is `null`**.

* It is an **unchecked exception** (subclass of `RuntimeException`).
* Common operations that can throw NPE:

  1. Accessing a **method** on a null object.
  2. Accessing a **field** of a null object.
  3. Accessing **array elements** of a null array.
  4. Throwing `null` as a Throwable.

---

### **🔹 2. Examples of NullPointerException**

#### **Example 1: Accessing Method of Null Object**

```java
public class NullPointerExample {
    public static void main(String[] args) {
        String str = null;
        System.out.println(str.length()); // Throws NullPointerException
    }
}
```

#### **Example 2: Accessing Field of Null Object**

```java
class Person {
    String name;
}

public class NullPointerFieldExample {
    public static void main(String[] args) {
        Person p = null;
        System.out.println(p.name); // Throws NullPointerException
    }
}
```

---

### **🔹 3. How to Prevent NullPointerException**

1. **Initialize objects properly**

```java
String str = ""; // instead of null
```

2. **Check for null before using objects**

```java
if (str != null) {
    System.out.println(str.length());
}
```

3. **Use Optional (Java 8+)**

```java
import java.util.Optional;

Optional<String> optionalStr = Optional.ofNullable(null);
System.out.println(optionalStr.orElse("Default Value"));
```

4. **Use default values for object references**

```java
String str = someMethod();
str = (str != null) ? str : "";
```

5. **Avoid returning null from methods**

```java
List<String> getNames() {
    return new ArrayList<>(); // return empty list instead of null
}
```

6. **Use try-catch block (if unavoidable)**

```java
try {
    System.out.println(str.length());
} catch (NullPointerException e) {
    System.out.println("Caught NPE");
}
```

---

### **🔹 4. Best Practices**

* Prefer **Optional** for return types that may be null.
* Avoid **null literals** as much as possible.
* Initialize variables when declared.
* Always perform **null checks** before calling methods or accessing fields.
* Use **`Objects.requireNonNull(obj)`** if a parameter should never be null.

---

### **🔹 5. Example Using Optional**

```java
import java.util.Optional;

public class OptionalExample {
    public static void main(String[] args) {
        String str = null;
        Optional<String> optionalStr = Optional.ofNullable(str);
        System.out.println(optionalStr.orElse("Default Value")); // Prints: Default Value
    }
}
```

---

💡 **Interview Tip:**

> "`NullPointerException` occurs when you access or modify an object reference that is null. Always initialize objects, perform null checks, or use Optional to prevent it."

---

Next, I can explain **Difference between Checked vs Unchecked Exceptions with examples**, which is closely related.

Do you want me to cover that?

---

## 38. What is a ClassCastException?

### **38. What is a `ClassCastException` in Java**

---

### **🔹 1. Definition**

A **`ClassCastException`** occurs when you **try to cast an object to a subclass of which it is **not an instance**.

* It is an **unchecked exception** (subclass of `RuntimeException`).
* Happens **at runtime**, not at compile-time.

---

### **🔹 2. Causes**

1. Casting an object to a class **it doesn’t belong to**.
2. Incorrect downcasting in **inheritance hierarchies**.
3. Casting objects in **collections without generics**.

---

### **🔹 3. Examples**

#### **Example 1: Casting to the Wrong Type**

```java
public class ClassCastExample {
    public static void main(String[] args) {
        Object obj = new Integer(10); // obj holds Integer
        String str = (String) obj;    // Wrong cast → ClassCastException
        System.out.println(str);
    }
}
```

**Output:**

```
Exception in thread "main" java.lang.ClassCastException: java.lang.Integer cannot be cast to java.lang.String
```

---

#### **Example 2: Casting in Inheritance Hierarchy**

```java
class Animal {}
class Dog extends Animal {}
class Cat extends Animal {}

public class CastExample {
    public static void main(String[] args) {
        Animal a = new Dog();
        Cat c = (Cat) a; // Dog cannot be cast to Cat → ClassCastException
    }
}
```

---

### **🔹 4. How to Prevent ClassCastException**

1. **Use `instanceof` before casting**

```java
Animal a = new Dog();
if (a instanceof Cat) {
    Cat c = (Cat) a;
} else {
    System.out.println("Cannot cast to Cat");
}
```

2. **Use Generics in Collections**

```java
List<String> list = new ArrayList<>();
list.add("Hello");
// No need to cast when retrieving element
String str = list.get(0);
```

3. **Avoid raw types**

   * Always use **generics** for type safety.

---

### **🔹 5. Summary**

| Feature           | Details                                                       |
| ----------------- | ------------------------------------------------------------- |
| **Type**          | Runtime (unchecked) exception                                 |
| **Occurs When**   | Object is cast to a class it **is not an instance of**        |
| **Common Causes** | Wrong downcasting, raw collections, incompatible object types |
| **Prevention**    | Use `instanceof`, generics, avoid raw types                   |

---

💡 **Interview Tip:**

> "ClassCastException occurs when you attempt **illegal casting**. Always check the type using `instanceof` or use **generics** to avoid it."

---

If you want, I can next explain **`ArrayIndexOutOfBoundsException`**, which is another very common runtime exception.

Do you want me to cover that?

---

## 39. What is Error vs Exception?

### **39. Difference Between `Error` and `Exception` in Java**

In Java, both **`Error`** and **`Exception`** are subclasses of the **`Throwable`** class, but they are used for **different kinds of problems**.

---

### **🔹 1. Basic Definitions**

| Term          | Definition                                                                                                                                       |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Exception** | An event that occurs during program execution that **disrupts normal flow**, usually caused by **programming errors or recoverable conditions**. |
| **Error**     | A serious problem that **the application usually cannot handle** and is mostly caused by the **JVM or system** (like memory issues).             |

---

### **🔹 2. Key Differences**

| Feature               | **Exception**                                         | **Error**                                          |
| --------------------- | ----------------------------------------------------- | -------------------------------------------------- |
| **Definition**        | Represents **recoverable** problems                   | Represents **serious system-level** problems       |
| **Checked/Unchecked** | Can be **checked or unchecked**                       | Always **unchecked**                               |
| **Recoverable?**      | ✅ Yes, can be handled using `try-catch`               | ❌ Usually cannot be handled                        |
| **Caused By**         | Program logic, user input, file I/O, etc.             | JVM failures, system resource exhaustion           |
| **Examples**          | `IOException`, `SQLException`, `NullPointerException` | `OutOfMemoryError`, `StackOverflowError`           |
| **Handling**          | Can be handled using **try-catch or throws**          | Rarely handled; usually lets the program terminate |
| **Inheritance**       | Subclass of `Throwable` → `Exception`                 | Subclass of `Throwable` → `Error`                  |

---

### **🔹 3. Exception Hierarchy**

```
Throwable
 ├── Error
 │    ├── OutOfMemoryError
 │    ├── StackOverflowError
 │    └── VirtualMachineError
 └── Exception
      ├── Checked Exception
      │    ├── IOException
      │    └── SQLException
      └── Unchecked Exception
           ├── RuntimeException
           │    ├── NullPointerException
           │    ├── ArithmeticException
           │    └── ClassCastException
```

---

### **🔹 4. Example of Exception vs Error**

#### **Exception Example**

```java
try {
    int a = 10 / 0; // ArithmeticException
} catch (ArithmeticException e) {
    System.out.println("Exception caught: " + e.getMessage());
}
```

**Output:**

```
Exception caught: / by zero
```

#### **Error Example**

```java
public class ErrorExample {
    public static void main(String[] args) {
        int[] arr = new int[Integer.MAX_VALUE]; // May throw OutOfMemoryError
    }
}
```

* Program may **terminate abruptly** because errors are usually **not handled**.

---

### **🔹 5. Summary Table**

| Feature           | Exception                             | Error                                    |
| ----------------- | ------------------------------------- | ---------------------------------------- |
| Recoverable       | Yes                                   | No                                       |
| Checked/Unchecked | Both                                  | Unchecked only                           |
| Cause             | Program/logic errors                  | JVM/system failures                      |
| Handling          | try-catch, throws                     | Rarely handled                           |
| Examples          | `IOException`, `NullPointerException` | `OutOfMemoryError`, `StackOverflowError` |

---

💡 **Interview Tip:**

> "`Exceptions` are **recoverable runtime problems**, whereas `Errors` are **serious system-level failures** that applications usually cannot handle."

---

If you want, I can next explain **Difference Between Checked and Unchecked Exceptions with Examples**, which is often asked after Error vs Exception.

Do you want me to cover that?

---

# Basic Control Structures

## 40. Explain the difference between break and continue statement.

### **40. Difference Between `break` and `continue` in Java**

Both **`break`** and **`continue`** are used for controlling the flow inside loops (`for`, `while`, `do-while`), but they behave differently.

---

### **🔹 1. `break` Statement**

* **Purpose:** Terminates the **entire loop** immediately.
* **Effect:** Exits the loop and continues execution with the **first statement after the loop**.
* **Can be used in:** `for`, `while`, `do-while`, and `switch` statements.

#### **Example of break**

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        break; // Loop terminates when i = 3
    }
    System.out.println(i);
}
```

**Output:**

```
1
2
```

---

### **🔹 2. `continue` Statement**

* **Purpose:** Skips the **current iteration** of the loop.
* **Effect:** Jumps to the **next iteration** of the loop.
* **Can be used in:** `for`, `while`, `do-while` loops only (not switch).

#### **Example of continue**

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        continue; // Skip the iteration when i = 3
    }
    System.out.println(i);
}
```

**Output:**

```
1
2
4
5
```

---

### **🔹 3. Key Differences**

| Feature             | `break`                           | `continue`                                          |
| ------------------- | --------------------------------- | --------------------------------------------------- |
| **Function**        | Exits the entire loop immediately | Skips the current iteration and continues with next |
| **Scope**           | Loops and switch                  | Loops only                                          |
| **Effect on loop**  | Terminates the loop               | Loop continues with next iteration                  |
| **Common Use Case** | Stop loop when condition met      | Skip specific iteration(s)                          |

---

### **🔹 4. Example Using Nested Loops**

```java
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 3; j++) {
        if (j == 2) {
            break; // Exits inner loop when j=2
        }
        System.out.println(i + " " + j);
    }
}
```

**Output:**

```
1 1
2 1
3 1
```

```java
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 3; j++) {
        if (j == 2) {
            continue; // Skips current iteration of inner loop when j=2
        }
        System.out.println(i + " " + j);
    }
}
```

**Output:**

```
1 1
1 3
2 1
2 3
3 1
3 3
```

---

💡 **Interview Tip:**

> "`break` exits the loop completely, while `continue` skips the current iteration and moves to the next one."

---

If you want, I can next explain **Difference between `==` and `.equals()` in Java**, which is also a very commonly asked interview question.

Do you want me to cover that next?

---

## 41. What is the difference between == and .equals()?

### **41. Difference Between `==` and `.equals()` in Java**

In Java, both `==` and `.equals()` are used to compare values, but they **work differently** depending on whether you are comparing **primitives** or **objects**.

---

### **🔹 1. `==` Operator**

* **Purpose:** Compares **primitive values** or **object references**.
* **Behavior:**

  * For **primitives:** checks **actual value equality**.
  * For **objects:** checks **whether both references point to the same memory location** (i.e., same object).

#### **Example with Primitives**

```java
int a = 10, b = 10;
System.out.println(a == b); // true (values are equal)
```

#### **Example with Objects**

```java
String s1 = new String("Java");
String s2 = new String("Java");
System.out.println(s1 == s2); // false (different memory locations)
```

---

### **🔹 2. `.equals()` Method**

* **Purpose:** Compares **contents or logical equality** of objects.
* **Behavior:**

  * Defined in **`Object` class**.
  * Most classes (e.g., `String`, `Integer`) **override `.equals()`** to compare values rather than references.
  * If not overridden, it behaves like `==` (reference comparison).

#### **Example with Strings**

```java
String s1 = new String("Java");
String s2 = new String("Java");
System.out.println(s1.equals(s2)); // true (values are equal)
```

#### **Example with Custom Class**

```java
class Person {
    String name;
    Person(String name) { this.name = name; }
}

Person p1 = new Person("Alice");
Person p2 = new Person("Alice");
System.out.println(p1.equals(p2)); // false (Person doesn't override equals)
```

* To compare **custom objects by content**, override `.equals()`:

```java
@Override
public boolean equals(Object obj) {
    if (this == obj) return true;
    if (obj == null || getClass() != obj.getClass()) return false;
    Person other = (Person) obj;
    return this.name.equals(other.name);
}
```

---

### **🔹 3. Key Differences**

| Feature              | `==`                                                  | `.equals()`                                                                               |
| -------------------- | ----------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| **Purpose**          | Compare **primitive values** or **object references** | Compare **logical equality of objects**                                                   |
| **Works for**        | Primitives & Objects                                  | Objects (cannot be used for primitives directly)                                          |
| **Default Behavior** | Reference comparison for objects                      | Reference comparison in `Object` class; overridden in many classes for content comparison |
| **Overridable?**     | No                                                    | Yes (can override for custom objects)                                                     |
| **Example**          | `s1 == s2` → false                                    | `s1.equals(s2)` → true                                                                    |

---

💡 **Interview Tip:**

> "`==` checks if two references point to the **same object**, while `.equals()` checks if **contents/values** are equal. Always use `.equals()` for object content comparison."

---

If you want, I can next explain **Difference between `String`, `StringBuilder`, and `StringBuffer`**, which is a very commonly asked Java string question.

Do you want me to cover that next?

---