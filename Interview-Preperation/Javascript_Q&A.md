## ✅ Top 100 JavaScript Interview Questions

---

### 🔹 **1–15: JavaScript Basics**

## 1. What are the different data types in JavaScript?

In JavaScript, **data types** define the kind of data a variable can hold. Understanding data types is essential for writing correct and efficient JavaScript code.

---

## 🔹 JavaScript Data Types

JavaScript has **two main categories** of data types:

### 1. **Primitive Data Types**

These are the most basic data types. They are immutable (cannot be changed) and are passed by **value**.

| Data Type   | Description                                                     | Example                    |
| ----------- | --------------------------------------------------------------- | -------------------------- |
| `String`    | A sequence of characters                                        | `"Hello", 'JavaScript'`    |
| `Number`    | Numeric values, including integers and floats                   | `42, 3.14`                 |
| `BigInt`    | For very large integers beyond the safe limit of `Number`       | `12345678901234567890n`    |
| `Boolean`   | Represents logical values                                       | `true, false`              |
| `undefined` | A variable that has been declared but not assigned a value      | `let a; // a is undefined` |
| `null`      | Represents intentional absence of value                         | `let b = null;`            |
| `Symbol`    | Unique and immutable primitive value, often used as object keys | `Symbol('id')`             |

#### 🔸 Example:

```javascript
let name = "Alice";       // String
let age = 25;             // Number
let bigNum = 9007199254740991n; // BigInt
let isStudent = true;     // Boolean
let city;                 // undefined
let car = null;           // null
let uniqueId = Symbol();  // Symbol
```

---

### 2. **Non-Primitive (Reference) Data Types**

These are complex data types. They are mutable and passed by **reference**.

| Data Type              | Description                     | Example                      |
| ---------------------- | ------------------------------- | ---------------------------- |
| `Object`               | A collection of key-value pairs | `{ name: "Alice", age: 25 }` |
| `Array`                | A list-like object              | `[1, 2, 3]`                  |
| `Function`             | A callable object               | `function greet() {}`        |
| `Date`, `RegExp`, etc. | Built-in object types           | `new Date(), /abc/`          |

#### 🔸 Example:

```javascript
let person = {
  name: "John",
  age: 30
}; // Object

let colors = ["red", "green", "blue"]; // Array

function greet() {
  console.log("Hello!");
} // Function
```

---

## 🔹 `typeof` Operator

You can check the type of a variable using the `typeof` operator.

#### Example:

```javascript
typeof "hello";       // "string"
typeof 42;            // "number"
typeof true;          // "boolean"
typeof undefined;     // "undefined"
typeof null;          // "object"  ← (This is a known quirk in JavaScript)
typeof Symbol("id");  // "symbol"
typeof [1, 2, 3];     // "object"
typeof {a:1};         // "object"
typeof greet;         // "function"
```

---

## 🔹 Summary Table

| Type        | Category      | Example        | typeof result |
| ----------- | ------------- | -------------- | ------------- |
| `String`    | Primitive     | `"JS"`         | "string"      |
| `Number`    | Primitive     | `123`          | "number"      |
| `BigInt`    | Primitive     | `123n`         | "bigint"      |
| `Boolean`   | Primitive     | `true`         | "boolean"     |
| `undefined` | Primitive     | `undefined`    | "undefined"   |
| `null`      | Primitive     | `null`         | "object"      |
| `Symbol`    | Primitive     | `Symbol("id")` | "symbol"      |
| `Object`    | Non-Primitive | `{}`           | "object"      |
| `Array`     | Non-Primitive | `[]`           | "object"      |
| `Function`  | Non-Primitive | `function(){}` | "function"    |

---

## ✅ Interview Tip

**Q: What's the difference between `undefined` and `null`?**
**A:**

* `undefined` means a variable has been declared but has not yet been assigned a value.
* `null` is an assignment value that represents "no value" or "empty". It's set explicitly.

---

If you're preparing for interviews, understanding how JavaScript handles types under the hood—especially the difference between **primitive and reference types**, **mutability**, and **type coercion**—can be very important.

Let me know if you'd like to dive deeper into any one of these types or questions like:

* What is type coercion in JavaScript?
* What's the difference between `==` and `===`?

I'm happy to help!
In JavaScript, **data types** define the kind of data a variable can hold. Understanding data types is essential for writing correct and efficient JavaScript code.

---

## 🔹 JavaScript Data Types

JavaScript has **two main categories** of data types:

### 1. **Primitive Data Types**

These are the most basic data types. They are immutable (cannot be changed) and are passed by **value**.

| Data Type   | Description                                                     | Example                    |
| ----------- | --------------------------------------------------------------- | -------------------------- |
| `String`    | A sequence of characters                                        | `"Hello", 'JavaScript'`    |
| `Number`    | Numeric values, including integers and floats                   | `42, 3.14`                 |
| `BigInt`    | For very large integers beyond the safe limit of `Number`       | `12345678901234567890n`    |
| `Boolean`   | Represents logical values                                       | `true, false`              |
| `undefined` | A variable that has been declared but not assigned a value      | `let a; // a is undefined` |
| `null`      | Represents intentional absence of value                         | `let b = null;`            |
| `Symbol`    | Unique and immutable primitive value, often used as object keys | `Symbol('id')`             |

#### 🔸 Example:

```javascript
let name = "Alice";       // String
let age = 25;             // Number
let bigNum = 9007199254740991n; // BigInt
let isStudent = true;     // Boolean
let city;                 // undefined
let car = null;           // null
let uniqueId = Symbol();  // Symbol
```

---

### 2. **Non-Primitive (Reference) Data Types**

These are complex data types. They are mutable and passed by **reference**.

| Data Type              | Description                     | Example                      |
| ---------------------- | ------------------------------- | ---------------------------- |
| `Object`               | A collection of key-value pairs | `{ name: "Alice", age: 25 }` |
| `Array`                | A list-like object              | `[1, 2, 3]`                  |
| `Function`             | A callable object               | `function greet() {}`        |
| `Date`, `RegExp`, etc. | Built-in object types           | `new Date(), /abc/`          |

#### 🔸 Example:

```javascript
let person = {
  name: "John",
  age: 30
}; // Object

let colors = ["red", "green", "blue"]; // Array

function greet() {
  console.log("Hello!");
} // Function
```

---

## 🔹 `typeof` Operator

You can check the type of a variable using the `typeof` operator.

#### Example:

```javascript
typeof "hello";       // "string"
typeof 42;            // "number"
typeof true;          // "boolean"
typeof undefined;     // "undefined"
typeof null;          // "object"  ← (This is a known quirk in JavaScript)
typeof Symbol("id");  // "symbol"
typeof [1, 2, 3];     // "object"
typeof {a:1};         // "object"
typeof greet;         // "function"
```

---

## 🔹 Summary Table

| Type        | Category      | Example        | typeof result |
| ----------- | ------------- | -------------- | ------------- |
| `String`    | Primitive     | `"JS"`         | "string"      |
| `Number`    | Primitive     | `123`          | "number"      |
| `BigInt`    | Primitive     | `123n`         | "bigint"      |
| `Boolean`   | Primitive     | `true`         | "boolean"     |
| `undefined` | Primitive     | `undefined`    | "undefined"   |
| `null`      | Primitive     | `null`         | "object"      |
| `Symbol`    | Primitive     | `Symbol("id")` | "symbol"      |
| `Object`    | Non-Primitive | `{}`           | "object"      |
| `Array`     | Non-Primitive | `[]`           | "object"      |
| `Function`  | Non-Primitive | `function(){}` | "function"    |

---

## ✅ Interview Tip

**Q: What's the difference between `undefined` and `null`?**
**A:**

* `undefined` means a variable has been declared but has not yet been assigned a value.
* `null` is an assignment value that represents "no value" or "empty". It's set explicitly.

---

## 2. What is the difference between `var`, `let`, and `const`?

Understanding the difference between `var`, `let`, and `const` is essential in JavaScript, especially since ES6 (ECMAScript 2015) introduced `let` and `const` as improvements over the older `var`.

---

## 🔹 Summary Table

| Feature            | `var`                                  | `let`                           | `const`                         |
| ------------------ | -------------------------------------- | ------------------------------- | ------------------------------- |
| Scope              | Function-scoped                        | Block-scoped                    | Block-scoped                    |
| Re-declaration     | ✅ Allowed                              | ❌ Not allowed                   | ❌ Not allowed                   |
| Re-assignment      | ✅ Allowed                              | ✅ Allowed                       | ❌ Not allowed                   |
| Hoisting           | ✅ Hoisted (initialized as `undefined`) | ✅ Hoisted (but not initialized) | ✅ Hoisted (but not initialized) |
| Temporal Dead Zone | ❌ No                                   | ✅ Yes                           | ✅ Yes                           |
| Mutable            | ✅ Yes                                  | ✅ Yes                           | ✅ (object can be mutated)       |

---

## 🔹 Detailed Explanation

### 🔸 `var`

* Introduced in **ES5**.
* **Function-scoped**: Only accessible within the function where it’s declared.
* **Hoisted** to the top of its scope and initialized with `undefined`.

#### Example:

```javascript
function exampleVar() {
  console.log(x); // undefined (not ReferenceError)
  var x = 10;
  console.log(x); // 10
}
exampleVar();
```

---

### 🔸 `let`

* Introduced in **ES6**.
* **Block-scoped**: Limited to `{ }` block (e.g., `if`, `for`, etc.).
* **Not hoisted** the same way as `var` — accessing before declaration causes a **ReferenceError** due to the **Temporal Dead Zone** (TDZ).

#### Example:

```javascript
function exampleLet() {
  console.log(x); // ReferenceError
  let x = 10;
}
exampleLet();
```

```javascript
if (true) {
  let y = 20;
}
console.log(y); // ReferenceError: y is not defined
```

---

### 🔸 `const`

* Also introduced in **ES6**.
* Same **block-scoped** behavior as `let`.
* Must be **initialized at declaration** and **cannot be reassigned**.

> 🔹 Important: `const` does not mean **immutable** object — it just means you can’t reassign the variable.

#### Example:

```javascript
const PI = 3.14;
PI = 3.14159; // ❌ TypeError

const user = { name: "Alice" };
user.name = "Bob"; // ✅ Allowed (object is mutable)
```

---

## 🔹 Hoisting Visual

```javascript
// Hoisting example
console.log(a); // undefined
var a = 5;

console.log(b); // ReferenceError
let b = 6;

console.log(c); // ReferenceError
const c = 7;
```

---

## ✅ Interview Tip

**Q: Should I use `var` in modern JavaScript?**
**A:** No. Prefer `let` and `const`. Use `const` by default, and `let` only when you need to reassign the variable. Avoid `var` unless you're maintaining legacy code.

---

## 🔹 Real-World Analogy

Think of a kitchen:

* `var` is like leaving ingredients anywhere in the kitchen — it's globally available within the function, messy and unsafe.
* `let` is like putting ingredients on a specific counter — accessible only where you can see them.
* `const` is like labeling a jar "Sugar" and gluing it shut — you can use the sugar, but you can’t rename or replace the jar.

---

## 3. What are JavaScript hoisting and temporal dead zones?

**hoisting** and the **temporal dead zone (TDZ)** are key JavaScript concepts that often come up in interviews.

---

## ✅ **1. What is Hoisting in JavaScript?**

**Hoisting** is JavaScript’s default behavior of **moving declarations to the top of their scope** (either function scope or global scope) during the compilation phase **before code is executed**.

### 🔹 What gets hoisted?

* **Variable declarations** (`var`, `let`, `const`)
* **Function declarations** (not expressions)

But **only declarations** are hoisted — **initializations are not.**

---

### 🔸 Example 1: `var` Hoisting

```javascript
console.log(x);  // Output: undefined
var x = 5;
```

#### What happens internally:

```javascript
var x;         // Declaration hoisted
console.log(x); // undefined
x = 5;         // Initialization happens later
```

---

### 🔸 Example 2: Function Hoisting

```javascript
greet(); // Output: Hello!

function greet() {
  console.log("Hello!");
}
```

✅ Function **declarations** are fully hoisted (both name and body).

---

### 🔸 Example 3: Function Expression is NOT hoisted

```javascript
greet(); // ❌ TypeError: greet is not a function

var greet = function() {
  console.log("Hello!");
};
```

Only the **`var greet`** declaration is hoisted, not the assignment.

---

## ✅ **2. What is Temporal Dead Zone (TDZ)?**

**TDZ** is the time between the start of a block and the point where a `let` or `const` variable is declared.
Accessing the variable during this period **throws a ReferenceError**.

---

### 🔹 Example:

```javascript
console.log(a); // ❌ ReferenceError
let a = 10;
```

* Variable `a` is **in scope**, but not **initialized**, so it’s in the **TDZ**.
* `let` and `const` are **hoisted**, but not initialized like `var`.

---

### 🔹 TDZ and `const`

```javascript
{
  console.log(myConst); // ❌ ReferenceError
  const myConst = "JavaScript";
}
```

Same behavior — accessing `myConst` before initialization is invalid.

---

## 🔍 Visualizing Hoisting + TDZ

```javascript
function test() {
  console.log(a); // undefined (var hoisted)
  // console.log(b); // ReferenceError (TDZ for let)
  // console.log(c); // ReferenceError (TDZ for const)

  var a = 1;
  let b = 2;
  const c = 3;
}
```

---

## ✅ Interview Tip

**Q: Are `let` and `const` hoisted?**

**A:** Yes, but unlike `var`, they are not initialized with `undefined`. They remain in the **Temporal Dead Zone** until the line where they are declared.

---

## 🔹 Summary

| Feature                   | `var`                        | `let` / `const`    |
| ------------------------- | ---------------------------- | ------------------ |
| Hoisted?                  | ✅ Yes                        | ✅ Yes              |
| Initialized on Hoist?     | ✅ With `undefined`           | ❌ No (TDZ applies) |
| Access before declaration | ✅ Allowed (gets `undefined`) | ❌ ReferenceError   |

---

## 4. Explain the concept of scope in JavaScript.

**Scope** is a fundamental concept in JavaScript and often appears in both beginner and advanced interview questions.

---

## 🔹 What is Scope in JavaScript?

**Scope** determines the **visibility** or **accessibility** of variables, functions, and objects in different parts of your code.

In simpler terms:

> Scope answers the question: **“Where can I use this variable?”**

---

## 🔸 Types of Scope in JavaScript

### 1. **Global Scope**

* Variables declared **outside** of any function or block.
* Accessible **anywhere** in the script.

```javascript
let globalVar = "I’m global";

function show() {
  console.log(globalVar); // Accessible
}
```

---

### 2. **Function Scope**

* Variables declared with `var` inside a function are **only accessible inside that function**.

```javascript
function test() {
  var a = 10;
  console.log(a); // 10
}
console.log(a); // ❌ ReferenceError
```

> `var` is **function-scoped**, not block-scoped!

---

### 3. **Block Scope** (introduced in ES6)

* Variables declared with `let` and `const` inside `{}` (blocks like `if`, `for`, etc.) are only accessible **within that block**.

```javascript
{
  let x = 5;
  const y = 10;
  console.log(x, y); // OK
}
console.log(x); // ❌ ReferenceError
```

---

### 4. **Lexical (Static) Scope**

* JavaScript uses **lexical scoping**, meaning scope is determined by the **physical placement** of code in the source file.
* Inner functions have access to variables defined in outer scopes.

```javascript
function outer() {
  let a = "outer";

  function inner() {
    console.log(a); // ✅ "outer"
  }

  inner();
}
outer();
```

---

## 🔸 Scope Chain

When a variable is accessed, JavaScript looks for it in the **current scope**, and if it’s not found, it moves **up the scope chain** until it reaches the global scope.

```javascript
let a = "global";

function first() {
  let b = "first";

  function second() {
    let c = "second";
    console.log(a); // ✅ "global"
    console.log(b); // ✅ "first"
    console.log(c); // ✅ "second"
  }

  second();
}
first();
```

---

## 🔸 Example Comparison

```javascript
function scopeTest() {
  if (true) {
    var x = 1;
    let y = 2;
    const z = 3;
  }
  console.log(x); // ✅ 1 (function scoped)
  console.log(y); // ❌ ReferenceError (block scoped)
  console.log(z); // ❌ ReferenceError (block scoped)
}
scopeTest();
```

---

## 🔹 Summary Table

| Keyword | Scope Type     | Accessible Outside Block? | Hoisted?             | Re-declarable? |
| ------- | -------------- | ------------------------- | -------------------- | -------------- |
| `var`   | Function Scope | ✅ Yes (within function)   | ✅ Yes (as undefined) | ✅ Yes          |
| `let`   | Block Scope    | ❌ No                      | ✅ TDZ applies        | ❌ No           |
| `const` | Block Scope    | ❌ No                      | ✅ TDZ applies        | ❌ No           |

---

## ✅ Interview Tip

**Q: What’s the difference between function scope and block scope?**

**A:**

* `var` is function-scoped: visible throughout the function it's declared in.
* `let` and `const` are block-scoped: visible only in the `{}` where they're declared.

---

## 5. What is the difference between `==` and `===`?

This is one of the most **commonly asked JavaScript interview topics**, and understanding it well shows a solid grasp of JavaScript type coercion and comparison behavior.

---

## 🔹 `==` vs `===` in JavaScript

| Operator | Name                       | Compares       | Type Conversion? | Example               |
| -------- | -------------------------- | -------------- | ---------------- | --------------------- |
| `==`     | Loose Equality             | Values         | ✅ Yes            | `'5' == 5` → `true`   |
| `===`    | Strict Equality / Identity | Values + Types | ❌ No             | `'5' === 5` → `false` |

---

## 🔸 `==` (Loose Equality)

* **Performs type coercion** before comparison.
* If the values are of **different types**, JavaScript tries to convert them to a common type.

### ✅ Example:

```javascript
'5' == 5       // true  (string converted to number)
null == undefined // true
0 == false     // true
' ' == 0       // true
```

### ⚠️ Can lead to **unexpected results**:

```javascript
[] == 0         // true
'' == 0         // true
false == '0'    // true
```

---

## 🔸 `===` (Strict Equality)

* **No type coercion**.
* Compares both **value and data type**.

### ✅ Example:

```javascript
5 === 5         // true
'5' === 5       // false (string ≠ number)
null === undefined // false
0 === false     // false
```

---

## 🔸 When to Use

> ✅ **Best practice**: Always use `===` and `!==` unless you have a specific reason to use `==`.

It helps you avoid bugs caused by **implicit type conversion**.

---

## 🔸 Real-World Example

```javascript
let userInput = "0";
if (userInput == false) {
  console.log("Falsy input!"); // This will run
}

if (userInput === false) {
  console.log("Falsy input!"); // This won't run
}
```

---

## ✅ Interview Tip

**Q: Why does `[] == false` return `true`, but `[] === false` returns `false`?**

**A:**

* `==` converts `[]` to an empty string (`''`), then to `0`, and `false` to `0` ⇒ `0 == 0` → `true`.
* `===` checks type: array vs boolean ⇒ not equal.

---

## 🔹 Summary Table of Weird `==` Cases

```javascript
'' == 0          // true
'0' == 0         // true
0 == false       // true
null == undefined // true
[] == ''         // true
[] == 0          // true
[1] == 1         // true
[1,2] == '1,2'   // true
{} == {}         // false (reference types)
```

---

## 🔚 Conclusion

| Use Case              | Recommended Operator |
| --------------------- | -------------------- |
| Type-safe comparison  | `===`                |
| Value-only comparison | `==` (use carefully) |

---

## 6. What are truthy and falsy values?

The concept of **truthy** and **falsy** values in JavaScript is **fundamental** when working with conditionals (`if`, `while`, ternary `? :`, etc.) — and it's a **very common interview topic**.

---

## ✅ **Definition**

In JavaScript, every value has an inherent **boolean value**, which is used when the value is evaluated in a **boolean context** (e.g., inside an `if` statement).

* A **truthy** value behaves like `true`.
* A **falsy** value behaves like `false`.

---

## 🔹 **Falsy Values in JavaScript**

There are only **7 falsy values**:

| Value       | Explanation     |
| ----------- | --------------- |
| `false`     | Boolean `false` |
| `0`         | Number zero     |
| `-0`        | Negative zero   |
| `0n`        | BigInt zero     |
| `""`        | Empty string    |
| `null`      | Null            |
| `undefined` | Undefined       |
| `NaN`       | Not a Number    |

### 🔸 Example:

```javascript
if (0) {
  console.log("Will not run"); // falsy
}

if ("") {
  console.log("Will not run"); // falsy
}

if (null) {
  console.log("Will not run"); // falsy
}
```

---

## 🔹 **Truthy Values**

Everything **else** is considered **truthy** — including:

| Value              | Explanation                   |
| ------------------ | ----------------------------- |
| `"hello"`          | Non-empty string              |
| `1`, `-42`, `3.14` | Any non-zero number           |
| `[]`               | Empty array (still truthy!)   |
| `{}`               | Empty object                  |
| `function() {}`    | Any function                  |
| `Infinity`         | Positive or negative infinity |

### 🔸 Example:

```javascript
if ("hello") {
  console.log("Will run"); // truthy
}

if ([]) {
  console.log("Will run"); // truthy!
}

if ({}) {
  console.log("Will run"); // truthy!
}
```

---

## 🔹 Using Truthy/Falsy in Real Code

### ✅ Example: Short-circuiting

```javascript
let name = "";
let displayName = name || "Guest";
console.log(displayName); // "Guest"
```

### ✅ Example: Conditional Rendering

```javascript
let isLoggedIn = true;

if (isLoggedIn) {
  console.log("Welcome!");
}
```

---

## 🔍 Gotchas and Interview Traps

### ❗ Empty arrays and objects are **truthy**

```javascript
if ([]) {
  console.log("Yes, an empty array is truthy!"); // ✅
}

if ({}) {
  console.log("Yes, an empty object is truthy!"); // ✅
}
```

---

## 🔸 Quick Quiz

What will each of the following log?

```javascript
if (false || null || undefined || 0 || "") {
  console.log("Truthy"); 
} else {
  console.log("Falsy"); // ✅ This will log
}

if ("0") {
  console.log("Truthy"); // ✅ Yes, non-empty string
}

if ([]) {
  console.log("Truthy"); // ✅ Empty array is truthy
}
```

---

## ✅ Summary

| Type       | Values                                                     |
| ---------- | ---------------------------------------------------------- |
| **Falsy**  | `false`, `0`, `-0`, `0n`, `""`, `null`, `undefined`, `NaN` |
| **Truthy** | Everything else (`"abc"`, `1`, `[]`, `{}`, `function(){}`) |

---

## 7. What is type coercion?

**Type coercion** is a key concept in JavaScript that often appears in interviews because it’s the root of many unexpected behaviors in code.

---

## ✅ What is Type Coercion?

**Type coercion** in JavaScript is the **automatic (or implicit) conversion** of one data type to another.
It usually happens when you perform operations involving **different types**, like comparing a number to a string.

---

## 🔹 Types of Type Coercion

### 1. **Implicit Coercion** (Automatic)

JavaScript **automatically** converts data types during comparison or operations.

### 2. **Explicit Coercion** (Manual)

You **manually** convert one type to another using built-in functions like `Number()`, `String()`, etc.

---

## 🔸 1. Implicit Type Coercion Examples

### ✅ Coercion in Comparisons (`==`)

```javascript
'5' == 5        // true: string '5' converted to number 5
false == 0      // true: false converted to 0
'' == 0         // true: both become 0
```

### ✅ Coercion in Arithmetic

```javascript
'5' - 2         // 3: string '5' becomes number
'5' + 2         // '52': string concatenation
true + 1        // 2: true becomes 1
null + 1        // 1: null becomes 0
```

### ❗ Weird Examples:

```javascript
[] + {}         // '[object Object]' (array becomes string, object becomes string)
{} + []         // 0 (confusing due to block vs object parsing)
```

---

## 🔸 2. Explicit Type Coercion Examples

You can control coercion with:

### ✅ To Number

```javascript
Number("123")   // 123
Number(true)    // 1
Number(null)    // 0
Number("abc")   // NaN
```

### ✅ To String

```javascript
String(123)     // "123"
String(false)   // "false"
String(null)    // "null"
```

### ✅ To Boolean

```javascript
Boolean(0)      // false
Boolean("0")    // true (non-empty string)
Boolean([])     // true
Boolean("")     // false
```

---

## 🔹 Why It Matters in Interviews

Interviewers love to test your understanding with confusing examples:

### ❓ Quiz:

```javascript
console.log([] == false);     // true
console.log([] === false);    // false
console.log('' == 0);         // true
console.log(null == undefined); // true
```

### ✅ Explanation:

* `[] == false`: `[]` → `''` → `0`, `false` → `0` ⇒ `0 == 0` ⇒ `true`
* `===` checks both **type and value**, so no coercion happens.

---

## 🔹 Summary

| Type Coercion | Description                       | Example           |
| ------------- | --------------------------------- | ----------------- |
| Implicit      | Auto-conversion by JS engine      | `'5' == 5 → true` |
| Explicit      | Manual conversion using functions | `Number('5') → 5` |

---

## ✅ Interview Tip

> Always use `===` instead of `==` to **avoid unexpected coercion**.

---

## 8. What is NaN? How can you check if a value is NaN?

**NaN** (Not-a-Number) is a special value in JavaScript that often causes confusion — and it’s a **frequent interview topic**.

---

## ✅ What is `NaN`?

`NaN` stands for **"Not a Number"**.

It is a **special numeric value** in JavaScript that represents a **failed or invalid number operation**.

---

## 🔸 When Do You Get `NaN`?

You get `NaN` when an operation **doesn't produce a valid number** but the result is still of type `number`.

### 🔹 Examples:

```javascript
0 / 0           // NaN
Math.sqrt(-1)   // NaN (no real square root for -1)
'abc' - 5       // NaN ('abc' can't be converted to number)
parseInt("xyz") // NaN
```

---

## 🔍 Key Properties of `NaN`

| Property        | Description                              |
| --------------- | ---------------------------------------- |
| Type            | `typeof NaN === "number"`                |
| Equality check  | `NaN === NaN` → ❌ `false`                |
| Unique Behavior | Only value in JS **not equal to itself** |

---

## ❓ Why `NaN === NaN` is `false`?

Because per the IEEE 754 standard, **NaN is not equal to anything, including itself**.

This means:

```javascript
NaN === NaN     // false
NaN == NaN      // false
```

---

## ✅ How to Check if a Value is `NaN`

### 1. `isNaN()` function (Built-in, but has quirks)

```javascript
isNaN(NaN)       // true
isNaN("hello")   // true → because "hello" can't be coerced to number
isNaN(123)       // false
```

### ❗ Problem: `isNaN()` **coerces** the argument to a number

```javascript
isNaN("123abc") // true (bad if you want strict check)
```

---

### 2. ✅ `Number.isNaN()` (ES6+) – Recommended!

```javascript
Number.isNaN(NaN)        // true ✅
Number.isNaN("hello")    // false ✅
Number.isNaN(undefined)  // false
Number.isNaN(123)        // false
```

✅ Safer — **no coercion** is done.

---

## 🔹 Real-World Use Case

When parsing user input:

```javascript
let input = "abc";
let num = Number(input);

if (Number.isNaN(num)) {
  console.log("Invalid number input");
}
```

---

## 🔸 Summary

| Method                | Checks if value is NaN       | Does Type Coercion?             |
| --------------------- | ---------------------------- | ------------------------------- |
| `isNaN(value)`        | ✅ Yes                        | ❌ No (may give false positives) |
| `Number.isNaN(value)` | ✅ Yes (strict)               | ✅ No (recommended)              |
| `value !== value`     | ✅ Yes (true if value is NaN) | ✅ No (trick method)             |

---

## ✅ Interview Tip

> Always prefer `Number.isNaN()` over `isNaN()` for accurate and safe checking.

---

## 9. How does `typeof` work?

The `typeof` operator is a **fundamental tool** in JavaScript used to check the **type of a value**. It's simple, but there are some **important edge cases** interviewers love to ask about.

---

## ✅ What is `typeof`?

The `typeof` operator returns a **string** indicating the **type of the operand**.

### 🔹 Syntax:

```javascript
typeof operand
```

Or:

```javascript
typeof(operand) // parentheses are optional
```

---

## 🔸 Common Examples

```javascript
typeof 42             // "number"
typeof "hello"        // "string"
typeof true           // "boolean"
typeof undefined      // "undefined"
typeof Symbol("id")   // "symbol"
typeof 123n           // "bigint"
typeof null           // ❗ "object" (we’ll explain below)
typeof {}             // "object"
typeof []             // "object"
typeof function(){}   // "function"
```

---

## 🔹 All Possible `typeof` Return Values

| JavaScript Type | `typeof` Result |
| --------------- | --------------- |
| Number          | `"number"`      |
| String          | `"string"`      |
| Boolean         | `"boolean"`     |
| Undefined       | `"undefined"`   |
| BigInt          | `"bigint"`      |
| Symbol          | `"symbol"`      |
| Object          | `"object"`      |
| Function        | `"function"`    |

---

## ❗ Important Gotchas

### 1. `typeof null === "object"`

* This is a **well-known bug** in JavaScript (exists for legacy reasons).
* `null` is **not** an object, but `typeof` reports it as one.

```javascript
typeof null     // "object" ❌ misleading
```

Use:

```javascript
value === null  // ✅ for checking null directly
```

---

### 2. Arrays

```javascript
typeof []       // "object"
Array.isArray([]) // ✅ true (use this instead)
```

`typeof` can't distinguish arrays from plain objects. Use `Array.isArray()` for that.

---

### 3. Functions

```javascript
typeof function() {} // "function"
```

Yes, functions are technically objects, but `typeof` gives a special `"function"` result to help developers.

---

## ✅ When to Use `typeof`

* To **check primitive types**: number, string, boolean, etc.
* To **safely check if a variable is undefined**:

  ```javascript
  if (typeof someVar === "undefined") {
    console.log("Variable is not defined");
  }
  ```

> This is useful because using `typeof someVar` won’t throw an error even if `someVar` is undeclared!

---

## 🔸 Example Comparison Table

```javascript
typeof 123         // "number"
typeof "abc"       // "string"
typeof true        // "boolean"
typeof undefined   // "undefined"
typeof null        // "object" ❌
typeof {}          // "object"
typeof []          // "object" ❌
typeof (() => {})  // "function"
typeof NaN         // "number" ✅ (because NaN is still a number)
```

---

## ✅ Summary

| Value          | `typeof` Result |
| -------------- | --------------- |
| `"hello"`      | `"string"`      |
| `123`          | `"number"`      |
| `true`         | `"boolean"`     |
| `undefined`    | `"undefined"`   |
| `null`         | `"object"` ❗    |
| `[]`           | `"object"` ❗    |
| `{}`           | `"object"`      |
| `function(){}` | `"function"`    |

---

## Interview Tip

**Q: Why does `typeof null === "object"`?**
**A:** It's a **historical bug** in JavaScript's implementation. `null` was originally considered a type of object in early versions, and it was never fixed due to backward compatibility.

---

## 10. What is the difference between `null` and `undefined`?

Understanding the difference between `null` and `undefined` is essential in JavaScript and often comes up in interviews because it reveals your grasp of JavaScript’s type system and variable initialization.

---

## ✅ What is `undefined`?

* `undefined` means a **variable has been declared but has NOT been assigned a value**.
* It is the **default value** of variables that are declared but not initialized.
* It is also the **return value of functions** that don’t explicitly return anything.
* It is a primitive type itself (`typeof undefined === "undefined"`).

### Example:

```javascript
let a;
console.log(a);            // undefined
console.log(typeof a);     // "undefined"

function foo() {}
console.log(foo());        // undefined
```

---

## ✅ What is `null`?

* `null` is an **assignment value** that represents **"no value" or "empty"**.
* It is explicitly set by the programmer to indicate the absence of any object value.
* It’s a primitive value and its type is actually `"object"` (due to legacy reasons).

### Example:

```javascript
let b = null;
console.log(b);            // null
console.log(typeof b);     // "object"
```

---

## 🔹 Key Differences

| Aspect           | `undefined`                                                | `null`                                             |
| ---------------- | ---------------------------------------------------------- | -------------------------------------------------- |
| Meaning          | Variable declared but no value assigned                    | Intentional absence of any object/value            |
| Type             | `undefined`                                                | `object` (historical quirk)                        |
| Assigned by      | JavaScript engine (default)                                | Programmer                                         |
| Use case         | Uninitialized variables, missing arguments, missing return | To clear or reset a variable, or indicate no value |
| Equality (`==`)  | `undefined == null` → `true`                               | `null == undefined` → `true`                       |
| Equality (`===`) | `undefined === null` → `false`                             | `null === undefined` → `false`                     |

---

## 🔹 Examples

```javascript
let x;
console.log(x);          // undefined (declared but not assigned)

let y = null;
console.log(y);          // null (explicitly assigned)

console.log(x == y);     // true (both represent "no value")
console.log(x === y);    // false (different types)
```

---

## 🔹 When to Use Which?

* Use **`undefined`** to check if a variable is **not initialized or missing**.
* Use **`null`** to **explicitly reset or clear** a variable’s value.

---

## 🔹 Summary

| Variable State                  | Value       |
| ------------------------------- | ----------- |
| Declared but not assigned       | `undefined` |
| Explicitly set to “empty” value | `null`      |
| Missing function return value   | `undefined` |

---

## ✅ Interview Tip

**Q:** What will this print?

```javascript
let a;
let b = null;

console.log(a == b);    // true
console.log(a === b);   // false
```

**A:**

* `a == b` is true because `==` treats `null` and `undefined` as equal.
* `a === b` is false because their types differ (`undefined` vs `object`).

---

## 11. What is the use of `typeof null` being an object?

The fact that `typeof null` returns `"object"` is one of those quirky JavaScript oddities that often surprises beginners and even experienced developers.

---

## ✅ Why Does `typeof null` Return `"object"`?

This behavior is a **longstanding bug in JavaScript** that dates back to its very first implementation.

### The Root Cause:

* In the original JavaScript implementation, values were stored in a way that used the **lowest bits of a value to indicate its type**.
* The **null value was represented as a null pointer (`0x00`)**.
* The type tag for objects was also `0`.
* Because of this, `null` was **incorrectly identified as an object**.

---

## 🔸 Historical Context

* This is a **bug in the language itself**, present since the beginning.
* It was never fixed because fixing it would break **existing code that depends on this behavior**.
* As a result, it remains part of JavaScript for **backward compatibility**.

---

## 🔸 What Does This Mean for Developers?

* `null` is **not actually an object**, it is its own primitive type representing “no value.”
* When you check `typeof null`, you get `"object"`, which is misleading.
* Therefore, **to check for null, always use direct comparison**:

```javascript
if (value === null) {
  // Correct way to check for null
}
```

---

## 🔸 How to Distinguish `null` from Objects?

If you want to distinguish between `null` and objects:

```javascript
const value = null;

console.log(typeof value);       // "object"
console.log(value === null);     // true
console.log(value !== null);     // false
console.log(value && typeof value === 'object'); // null is falsy, so false
```

---

## 🔸 Practical Impact

* This quirk rarely causes serious issues because most code uses strict equality (`===`) or explicit null checks.
* Some libraries and frameworks **account for this quirk** internally.

---

## ✅ Summary

| Check            | Result                 | Notes                         |
| ---------------- | ---------------------- | ----------------------------- |
| `typeof null`    | `"object"`             | Legacy bug, misleading        |
| `null === null`  | `true`                 | Correct way to check for null |
| `value === null` | `true` (if value null) | Use this for null checks      |

---

## Interview Tip

If asked **why** `typeof null` is `"object"`, just say it’s a **historical bug from JavaScript’s early implementation** that was never fixed for backward compatibility.

---

## 12. What are primitive and reference types?

Understanding **primitive** vs **reference** types is fundamental in JavaScript and often comes up in interviews to test your grasp on how data is stored, copied, and compared.

---

## ✅ What Are Primitive Types?

**Primitive types** are the most basic data types in JavaScript. They **hold simple values** that are **stored directly in the variable**.

### Characteristics of primitives:

* Immutable (cannot be changed once created)
* Stored by **value** (copy of the actual value is assigned)
* Comparing two primitives compares their values directly

### JavaScript Primitive Types:

| Type        | Example         |
| ----------- | --------------- |
| `string`    | `"hello"`       |
| `number`    | `42`, `3.14`    |
| `boolean`   | `true`, `false` |
| `undefined` | `undefined`     |
| `null`      | `null`          |
| `symbol`    | `Symbol('id')`  |
| `bigint`    | `123n`          |

### Example:

```javascript
let a = 5;
let b = a;  // copy value 5
b = 10;

console.log(a); // 5 (unchanged)
console.log(b); // 10
```

---

## ✅ What Are Reference Types?

**Reference types** are objects, arrays, functions, etc. These **store references (memory addresses)** to the actual data.

### Characteristics of reference types:

* Mutable (contents can be changed)
* Stored by **reference** (variable holds a pointer to the location in memory)
* Comparing two references compares their memory address, not the content

### Examples of reference types:

* Objects: `{ name: "John" }`
* Arrays: `[1, 2, 3]`
* Functions: `function () {}`

### Example:

```javascript
let obj1 = { name: "Alice" };
let obj2 = obj1;  // copy reference, both point to the same object
obj2.name = "Bob";

console.log(obj1.name); // "Bob" (changed because both point to same object)
console.log(obj2.name); // "Bob"
```

---

## 🔹 Key Differences Summary

| Feature        | Primitive Types               | Reference Types               |
| -------------- | ----------------------------- | ----------------------------- |
| Stored as      | Value                         | Reference (memory address)    |
| Mutability     | Immutable                     | Mutable                       |
| Copy behavior  | Copies value                  | Copies reference              |
| Equality check | Compares value                | Compares reference (memory)   |
| Examples       | `string`, `number`, `boolean` | `object`, `array`, `function` |

---

## 🔹 Why It Matters?

* Understanding this helps avoid bugs related to **unintended mutations**.
* Helps in **performance optimization** and **memory management**.
* Essential when passing variables to functions (by value vs by reference).

---

## ✅ Interview Tip

**Q:** What happens when you compare two different objects with the same content?

```javascript
let obj1 = { a: 1 };
let obj2 = { a: 1 };

console.log(obj1 === obj2);  // false
```

Because they reference **different memory locations**, even though their contents are identical.

---

## 13. What is pass-by-value and pass-by-reference in JS?

Understanding **pass-by-value** vs **pass-by-reference** is crucial in JavaScript, especially because it impacts how function arguments behave and how data changes propagate.

---

## ✅ Pass-by-Value vs Pass-by-Reference: What Do They Mean?

* **Pass-by-value:**
  The function receives a **copy of the actual value**. Changes inside the function do **not** affect the original variable.

* **Pass-by-reference:**
  The function receives a **reference (pointer) to the original object**. Changes inside the function **do affect** the original object.

---

## 🔹 How Does JavaScript Handle This?

JavaScript is **always pass-by-value**, but **for objects and arrays, the “value” passed is actually a reference to the object in memory**.

---

### 1. Pass-by-Value for Primitives

For **primitive types** (`number`, `string`, `boolean`, `null`, `undefined`, `symbol`, `bigint`), the **actual value is copied** and passed.

```javascript
function changeValue(val) {
  val = 100;
}

let num = 50;
changeValue(num);
console.log(num);  // 50 (unchanged)
```

The function receives a **copy** of `num`, so changing `val` inside the function does not affect `num`.

---

### 2. Pass-by-Value for Reference Types (Objects, Arrays)

For **objects and arrays**, the **reference to the object** is copied and passed. This means the function has access to the **same object** in memory.

```javascript
function changeObject(obj) {
  obj.name = "Alice";
}

let person = { name: "Bob" };
changeObject(person);
console.log(person.name);  // "Alice" (changed!)
```

Here, the function receives a **copy of the reference**, but **both the original variable and the parameter point to the same object**. So modifying the object affects the original.

---

## 🔹 Important Clarification

* The **reference itself is passed by value**.
  You cannot reassign the original object by assigning the parameter to a new object inside the function.

```javascript
function replaceObject(obj) {
  obj = { name: "Charlie" };
}

let person = { name: "Bob" };
replaceObject(person);
console.log(person.name);  // "Bob" (unchanged)
```

Because `obj` parameter is a copy of the reference, reassigning it inside the function does **not** affect the original variable.

---

## Summary Table

| Type            | What is passed              | Effect of modifying parameter inside function |
| --------------- | --------------------------- | --------------------------------------------- |
| Primitive types | Copy of the value           | Original value unchanged                      |
| Objects/Arrays  | Copy of reference to object | Original object modified if you mutate it     |
| Objects/Arrays  | Copy of reference           | Reassigning parameter doesn't change original |

---

## ✅ Interview Tip

**Q:** Why can you modify an object inside a function but not reassign it?

**A:** Because JavaScript passes a copy of the **reference**, so you can change the object's properties, but assigning a new object to the parameter only changes the local copy of the reference.

---

## 14. What is the difference between `Object.freeze()` and `Object.seal()`?

Both `Object.freeze()` and `Object.seal()` are methods in JavaScript used to control how objects can be modified, but they differ in **how strictly they restrict changes**.

---

## ✅ `Object.freeze()`

* **Freezes an object completely** — makes it **immutable**.
* You **cannot add, delete, or modify** any property.
* Existing properties become **non-writable** and **non-configurable**.
* The object becomes deeply unchangeable **only at the first level** (shallow freeze).

### Example:

```javascript
const person = {
  name: "Alice",
  age: 25
};

Object.freeze(person);

person.age = 30;         // ❌ Ignored in strict mode or silently fails
person.city = "NYC";     // ❌ Cannot add new properties
delete person.name;      // ❌ Cannot delete properties

console.log(person);
// Output: { name: "Alice", age: 25 }
```

---

## ✅ `Object.seal()`

* **Seals the object** — **you cannot add or delete properties**, but you **can modify existing property values** (if writable).
* Existing properties become **non-configurable**, but their values can still change.
* Prevents changing the structure but **allows modifying property values**.

### Example:

```javascript
const person = {
  name: "Alice",
  age: 25
};

Object.seal(person);

person.age = 30;         // ✅ Allowed
person.city = "NYC";     // ❌ Cannot add new property
delete person.name;      // ❌ Cannot delete properties

console.log(person);
// Output: { name: "Alice", age: 30 }
```

---

## 🔹 Key Differences Summary

| Feature                  | `Object.freeze()`                          | `Object.seal()`                               |
| ------------------------ | ------------------------------------------ | --------------------------------------------- |
| Add new properties       | ❌ Not allowed                              | ❌ Not allowed                                 |
| Delete properties        | ❌ Not allowed                              | ❌ Not allowed                                 |
| Modify existing props    | ❌ Not allowed                              | ✅ Allowed (if writable)                       |
| Configurable             | No (properties become non-configurable)    | No (properties become non-configurable)       |
| Writable                 | No (properties become non-writable)        | Yes (if property was writable before sealing) |
| Effect on nested objects | Shallow (nested objects not frozen/sealed) | Shallow (nested objects not sealed)           |

---

## 🔹 Important Notes

* Both are **shallow** — nested objects inside the object are **not frozen or sealed automatically**.
* To deeply freeze or seal, you need to recursively apply these methods.

---

## ✅ When to Use Which?

* Use **`Object.freeze()`** when you want to make an object **completely immutable**.
* Use **`Object.seal()`** when you want to prevent **adding or removing properties**, but still allow **updating existing properties**.

---

## Interview Tip

> If asked about immutability in JavaScript objects, mention `Object.freeze()` for full immutability and `Object.seal()` for partial immutability.

---

## 15. What are spread and rest operators?

The **spread** and **rest** operators in JavaScript look identical (both use `...`), but they serve **different purposes** depending on the context. Understanding them is crucial for writing clean and flexible code.

---

## ✅ Spread Operator (`...`)

The **spread operator** is used to **expand (spread) elements of an iterable (like an array or object) into individual elements**.

### Use cases:

* Expanding arrays or objects into individual elements or key-value pairs
* Copying arrays or objects (shallow copy)
* Combining arrays or objects
* Passing multiple arguments to a function

### Examples:

#### 1. Spread in Arrays:

```javascript
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5];  // Spread arr1 elements and add more
console.log(arr2);              // [1, 2, 3, 4, 5]
```

#### 2. Spread in Function Calls:

```javascript
function sum(a, b, c) {
  return a + b + c;
}

const numbers = [1, 2, 3];
console.log(sum(...numbers));  // 6
```

#### 3. Spread in Objects:

```javascript
const obj1 = { a: 1, b: 2 };
const obj2 = { ...obj1, c: 3 };
console.log(obj2);  // { a: 1, b: 2, c: 3 }
```

---

## ✅ Rest Operator (`...`)

The **rest operator** is used in **function parameters** or **destructuring assignment** to **collect multiple elements into a single array or object**.

### Use cases:

* Gathering **remaining function arguments** into an array
* Collecting **remaining elements or properties** during destructuring

### Examples:

#### 1. Rest in Function Parameters:

```javascript
function sumAll(...args) {
  return args.reduce((acc, val) => acc + val, 0);
}

console.log(sumAll(1, 2, 3, 4));  // 10
```

#### 2. Rest in Array Destructuring:

```javascript
const [first, second, ...rest] = [10, 20, 30, 40, 50];
console.log(first);   // 10
console.log(second);  // 20
console.log(rest);    // [30, 40, 50]
```

#### 3. Rest in Object Destructuring:

```javascript
const { a, b, ...rest } = { a: 1, b: 2, c: 3, d: 4 };
console.log(a);    // 1
console.log(b);    // 2
console.log(rest); // { c: 3, d: 4 }
```

---

## 🔹 Key Differences

| Feature  | Spread (`...`)                                    | Rest (`...`)                                          |
| -------- | ------------------------------------------------- | ----------------------------------------------------- |
| Usage    | Expands iterable/objects into individual elements | Collects multiple elements into an array or object    |
| Position | Used in **calls, literals, and assignments**      | Used in **function parameters** and **destructuring** |
| Purpose  | Expanding items                                   | Gathering items                                       |

---

## Summary:

| Operator       | Example Usage             | Purpose                        |
| -------------- | ------------------------- | ------------------------------ |
| Spread (`...`) | `let arr2 = [...arr1, 4]` | Expand elements of an iterable |
| Rest (`...`)   | `function fn(...args) {}` | Collect remaining arguments    |

---

## Interview Tip

If you get asked:
**“What’s the difference between spread and rest?”**
Explain that **syntax is the same**, but their role depends on context — spread **expands**, rest **collects**.

---

### 🔹 **16–30: Functions & Closures**

## 16. What is a first-class function in JavaScript?

The concept of **first-class functions** is fundamental to JavaScript's power and flexibility.

---

## ✅ What is a First-Class Function?

In JavaScript, **functions are first-class citizens (or first-class objects)**, meaning functions are treated like any other value. You can:

* **Assign a function to a variable**
* **Pass a function as an argument to another function**
* **Return a function from another function**
* **Store functions in data structures like arrays or objects**

---

## 🔹 Explanation

A **first-class function** means the function can be:

1. **Created dynamically** at runtime.
2. **Stored** in variables or data structures.
3. **Passed** as arguments to other functions (callbacks).
4. **Returned** from functions.

---

## 🔹 Why is this Important?

This capability enables **functional programming patterns** like:

* Callbacks
* Closures
* Higher-order functions
* Function composition

---

## 🔹 Example

```javascript
// 1. Assigning function to a variable
const greet = function(name) {
  return `Hello, ${name}!`;
};

// 2. Passing function as argument
function callFunction(fn, value) {
  return fn(value);
}

console.log(callFunction(greet, "Alice"));  // Hello, Alice!

// 3. Returning a function
function multiplier(factor) {
  return function(number) {
    return number * factor;
  };
}

const double = multiplier(2);
console.log(double(5));  // 10

// 4. Storing functions in an array
const operations = [
  function(x) { return x + 1; },
  function(x) { return x * 2; }
];

console.log(operations );  // 6
console.log(operations );  // 10
```

---

## ✅ Summary

| Property                  | Explanation                       |
| ------------------------- | --------------------------------- |
| First-class function      | Functions treated as values       |
| Can be assigned           | `const f = function() {}`         |
| Can be passed as argument | `func(fn)`                        |
| Can be returned           | `return function() {}`            |
| Can be stored             | `const arr = [function(){}, ...]` |

---

## Interview Tip

If asked what makes a language support first-class functions, say it means functions can be manipulated just like other data types — assigned, passed, and returned freely.

---

## 17. What is a callback function?

Let’s dive into **callback functions**, a core concept in JavaScript, especially in asynchronous programming.

---

## ✅ What is a Callback Function?

A **callback function** is a function **passed as an argument** to another function and is **invoked (called back)** inside that function to complete some kind of action or task.

---

## 🔹 Why Callbacks?

Callbacks allow you to:

* Execute code **after** another function finishes (especially async tasks).
* Customize or extend behavior of functions.
* Handle events or responses (e.g., from user actions, timers, or server requests).

---

## 🔹 Basic Example

```javascript
function greet(name) {
  console.log(`Hello, ${name}!`);
}

function processUserInput(callback) {
  const name = "Alice";
  callback(name);  // Call the callback function with data
}

processUserInput(greet);
// Output: Hello, Alice!
```

Here, `greet` is passed as a callback to `processUserInput` and is invoked inside it.

---

## 🔹 Callback with Asynchronous Example

```javascript
function fetchData(callback) {
  setTimeout(() => {
    const data = { id: 1, message: "Hello" };
    callback(data);  // Called when data is "fetched"
  }, 1000);
}

fetchData(function(result) {
  console.log("Received data:", result);
});
```

This simulates fetching data asynchronously and uses a callback to handle the result once ready.

---

## 🔹 Callback vs Function Argument

* All callbacks are functions passed as arguments.
* But not all function arguments are callbacks (only those intended to be called later).

---

## 🔹 Common Use Cases

* Event handlers (e.g., `button.onclick = callback`)
* Timers (`setTimeout`, `setInterval`)
* Network requests (XHR, fetch with `.then()`)
* Array methods (`map`, `filter`, `forEach`)

---

## Summary

| Aspect       | Description                                                  |
| ------------ | ------------------------------------------------------------ |
| Callback     | Function passed into another function                        |
| Purpose      | To be invoked later, often after an event or task completion |
| Allows async | Enables code to run after async operations                   |
| Example      | `array.forEach(item => console.log(item));`                  |

---

## Interview Tip

If asked **what a callback is**, describe it as a function passed as an argument to be executed later, enabling asynchronous behavior or customizable function logic.

---

## 18. What are arrow functions and how are they different?

**Arrow functions** are a concise syntax for writing functions in JavaScript, introduced in ES6 (ECMAScript 2015). They come with some important differences compared to regular function expressions.

---

## ✅ What are Arrow Functions?

Arrow functions let you write functions using a shorter syntax:

```javascript
// Regular function
const add = function(a, b) {
  return a + b;
};

// Arrow function equivalent
const add = (a, b) => a + b;
```

---

## 🔹 Syntax Overview

| Function Type    | Syntax                      |
| ---------------- | --------------------------- |
| Regular function | `function (params) { ... }` |
| Arrow function   | `(params) => expression`    |

* If the function body is a **single expression**, it implicitly returns its value (no `return` keyword needed).
* If you have multiple statements, you use curly braces and `return` explicitly:

```javascript
const multiply = (a, b) => {
  const result = a * b;
  return result;
};
```

---

## 🔹 Key Differences Between Arrow Functions and Regular Functions

| Feature                | Arrow Functions                                                  | Regular Functions                          |
| ---------------------- | ---------------------------------------------------------------- | ------------------------------------------ |
| **`this` binding**     | Lexically bound to the surrounding scope (no own `this`)         | Has its own `this` depending on how called |
| **`arguments` object** | Does **not** have its own `arguments`                            | Has its own `arguments` object             |
| **`new` operator**     | Cannot be used as constructors (no `new`)                        | Can be used with `new`                     |
| **Syntax**             | Shorter, concise                                                 | More verbose                               |
| **Methods in objects** | Arrow functions are not suited for object methods needing `this` | Regular functions can use `this`           |

---

## 🔹 Example: `this` Difference

```javascript
const obj = {
  value: 42,
  regularFunc: function() {
    console.log(this.value);
  },
  arrowFunc: () => {
    console.log(this.value);
  }
};

obj.regularFunc();  // 42 (this refers to obj)
obj.arrowFunc();    // undefined (this refers to outer/global scope)
```

Here, the arrow function’s `this` is **not** bound to the object but inherits from the enclosing scope (likely the global object or undefined in strict mode).

---

## 🔹 Use Cases

* Use arrow functions for **short callbacks** or functions that **don’t need their own `this`**.
* Avoid arrow functions for **object methods** or **constructors**.

---

## Summary

| Aspect         | Arrow Function                 | Regular Function          |
| -------------- | ------------------------------ | ------------------------- |
| `this` binding | Lexical (inherits from parent) | Dynamic (based on caller) |
| `arguments`    | No                             | Yes                       |
| Can use `new`  | No                             | Yes                       |
| Syntax         | Concise                        | Verbose                   |

---

## Interview Tip

If asked why arrow functions are useful, highlight their **short syntax** and how they **fix the common issue of `this` inside callbacks**.

---

## 19. What is a closure? Give a real-world example.

**Closures** are one of the most powerful and sometimes tricky concepts in JavaScript. Let’s break it down clearly.

---

## ✅ What is a Closure?

A **closure** is created when a function **retains access to its lexical scope**, even when the function is executed **outside that scope**.

In simpler terms:
A closure **“closes over” variables from its surrounding scope**, allowing the function to remember and access those variables even after the outer function has finished executing.

---

## 🔹 Why does this happen?

Because JavaScript functions form **closures by default**. When a function is defined inside another function, the inner function has access to:

* Its own variables
* Variables of the outer function
* Global variables

Even if the outer function has returned, the inner function **remembers** the outer function’s variables.

---

## 🔹 Real-world analogy

Imagine a **backpack** (closure) where a function carries around some supplies (variables from outer scope). Even if the function moves somewhere else (executes later), it still has the supplies it needs.

---

## 🔹 Example: Counter with Closure

```javascript
function createCounter() {
  let count = 0;  // Private variable

  return function() {   // Inner function is the closure
    count++;
    return count;
  };
}

const counter = createCounter();

console.log(counter());  // 1
console.log(counter());  // 2
console.log(counter());  // 3
```

* Here, `createCounter` returns an **inner function**.
* The inner function **remembers** the `count` variable, even though `createCounter` has finished executing.
* `count` acts like a **private variable** that’s preserved in the closure.

---

## 🔹 Why use closures?

* To **encapsulate private data** (like `count` above).
* To create **factory functions** that generate customized functions.
* To maintain state in **asynchronous callbacks** or event handlers.
* To write modular, maintainable code.

---

## 🔹 Another quick example: Greeting

```javascript
function greetMaker(greeting) {
  return function(name) {
    console.log(`${greeting}, ${name}!`);
  };
}

const sayHello = greetMaker("Hello");
sayHello("Alice");  // Hello, Alice!
sayHello("Bob");    // Hello, Bob!
```

`sayHello` remembers the `"Hello"` greeting because of closure.

---

## Summary

| Concept    | Explanation                                               |
| ---------- | --------------------------------------------------------- |
| Closure    | Function + lexical environment it remembers               |
| Allows     | Access to outer scope variables after outer function ends |
| Useful for | Data privacy, maintaining state, function factories       |

---

## Interview Tip

If asked **“what’s a closure?”**, describe it as a function that **remembers the variables from its surrounding scope even after that scope has finished**, enabling powerful patterns like private state.

---

## 20. How does lexical scoping work?

**Lexical scoping** is a fundamental concept that underpins how variable lookup works in JavaScript and many other programming languages.

---

## ✅ What is Lexical Scoping?

**Lexical scoping** means that the accessibility (scope) of variables is determined **by their physical placement in the source code (the lexical context)**. In other words, where you **write** your variables and functions in the code defines their scope.

* The scope is **fixed at the time the code is written**, not when it is executed.
* Inner functions have access to variables defined in their **outer (parent) functions** or global scope.

---

## 🔹 Key idea:

* Each function creates a **scope**.
* Functions are executed in the environment where they were **defined** (lexical environment), not where they are called.

---

## 🔹 Example:

```javascript
const globalVar = 'global';

function outer() {
  const outerVar = 'outer';

  function inner() {
    const innerVar = 'inner';

    console.log(globalVar); // accessible: 'global'
    console.log(outerVar);  // accessible: 'outer'
    console.log(innerVar);  // accessible: 'inner'
  }

  inner();
}

outer();
```

* `inner` function can access `innerVar`, `outerVar`, and `globalVar` because of lexical scoping.
* If `inner` is executed elsewhere, it still remembers the variables where it was **defined**.

---

## 🔹 What if `inner` is assigned elsewhere?

```javascript
const globalVar = 'global';

function outer() {
  const outerVar = 'outer';

  function inner() {
    console.log(outerVar);
  }

  return inner;
}

const innerFn = outer();
innerFn();  // Logs: 'outer'
```

Even though `innerFn` is called outside `outer`, it still accesses `outerVar` because it **closes over the lexical environment** where it was defined.

---

## 🔹 Contrast with Dynamic Scoping (not used in JS)

In dynamic scoping (not JavaScript), variable scope depends on the **call stack** at runtime, i.e., where a function is called, not where it's defined.

---

## Summary

| Aspect              | Lexical Scoping (JavaScript)                                    |
| ------------------- | --------------------------------------------------------------- |
| Scope determined by | Position in source code (where functions/variables are written) |
| Variable lookup     | From inner scope outward to outer lexical environments          |
| Functions remember  | The environment where they were created (lexical environment)   |
| Enables             | Closures and predictable variable access                        |

---

## Interview Tip

If asked **“How does lexical scoping work?”**, say:
*"It means that functions access variables based on where they are physically written in the code, not where they are called. This allows inner functions to access variables of outer functions where they were defined."*

---

## 21. What is the purpose of an IIFE (Immediately Invoked Function Expression)?

**IIFE** stands for **Immediately Invoked Function Expression**. It’s a pattern in JavaScript used to **run a function as soon as it’s defined**.

---

## ✅ What is an IIFE?

An IIFE is a function expression that is **defined and executed immediately**, without needing to be called later.

### Syntax:

```javascript
(function() {
  // code runs immediately
})();
```

or

```javascript
(() => {
  // arrow function IIFE
})();
```

---

## 🔹 Why use an IIFE? Purpose and Benefits

1. **Creates a new scope** — Variables declared inside the IIFE are **not accessible outside**, preventing pollution of the global scope.

2. **Avoids naming collisions** — Helps in modularizing code and preventing conflicts between variable names in larger projects.

3. **Data privacy** — Encapsulates private variables and functions.

4. **Initialization code** — Runs setup code once without cluttering global namespace.

---

## 🔹 Example: Avoid Global Pollution

```javascript
var x = 10;

(function() {
  var x = 20;  // local to this IIFE
  console.log(x);  // 20
})();

console.log(x);  // 10 (global x unchanged)
```

---

## 🔹 Example: Module Pattern (using IIFE)

```javascript
const counter = (function() {
  let count = 0;

  return {
    increment: function() {
      count++;
      return count;
    },
    reset: function() {
      count = 0;
    }
  };
})();

console.log(counter.increment());  // 1
console.log(counter.increment());  // 2
counter.reset();
console.log(counter.increment());  // 1
```

* The `count` variable is private to the IIFE and cannot be accessed directly.
* The returned object exposes only specific methods.

---

## Summary

| Purpose                      | Explanation                                       |
| ---------------------------- | ------------------------------------------------- |
| Encapsulation                | Creates a private scope                           |
| Avoid global scope pollution | Keeps variables/functions out of global namespace |
| Initialization               | Run code immediately without extra calls          |
| Module pattern foundation    | Build self-contained modules                      |

---

## Interview Tip

If asked about IIFE, emphasize **immediate execution and creating a private scope to avoid polluting the global environment**.

---

## 22. What is currying in JavaScript?

**Currying** is a powerful functional programming technique often used in JavaScript.

---

## ✅ What is Currying?

**Currying** is the process of transforming a function that takes multiple arguments into a sequence of functions, each taking a single argument.

Instead of a function like:

```js
function add(a, b) {
  return a + b;
}
```

You create a **curried version**:

```js
function add(a) {
  return function(b) {
    return a + b;
  };
}

add(2)(3); // 5
```

---

## 🔹 How does currying work?

* You call the function with one argument.
* It returns another function that expects the next argument.
* This continues until all arguments are provided, then the final result is returned.

---

## 🔹 Why use currying?

* **Partial application**: Fix some arguments and create a new function.
* **Function reuse**: Build more specific functions from general ones.
* Can improve **readability** and **composability**.

---

## 🔹 Example: Curried multiply function

```js
function multiply(a) {
  return function(b) {
    return a * b;
  };
}

const double = multiply(2);
console.log(double(5)); // 10
```

Here, `double` is a new function with `a` fixed to 2.

---

## 🔹 Using ES6 arrow functions for currying

```js
const add = a => b => a + b;
console.log(add(5)(10)); // 15
```

---

## 🔹 Currying vs Partial Application

* **Currying** always transforms a function into unary (single-argument) functions.
* **Partial application** fixes some arguments, but the function can still take multiple arguments afterward.

---

## Summary

| Aspect   | Explanation                                                    |
| -------- | -------------------------------------------------------------- |
| Currying | Transform multi-arg function into chained single-arg functions |
| Benefit  | Enables partial application and function reuse                 |
| Syntax   | `fn(a)(b)(c)`                                                  |
| Example  | `const add = a => b => a + b;`                                 |

---

## Interview Tip

If asked about currying, explain it as **breaking down a function so it takes one argument at a time, returning new functions for the next argument, until all are provided**.

---

## 23. What is function composition?

**Function composition** is a fundamental concept in functional programming and is widely used in JavaScript to create powerful, reusable, and clean code.

---

## ✅ What is Function Composition?

**Function composition** is the process of combining two or more functions to produce a new function, where the output of one function becomes the input of the next.

In math terms:
If you have two functions `f` and `g`, the composition `f ∘ g` means:
`f(g(x))` — first apply `g` to `x`, then apply `f` to the result.

---

## 🔹 Why use function composition?

* To build complex operations by combining simpler functions.
* To improve code readability and modularity.
* To enable functional programming style.

---

## 🔹 Example in JavaScript

Suppose we have two simple functions:

```js
const double = x => x * 2;
const increment = x => x + 1;
```

We want to create a new function that increments a number and then doubles it.

```js
const incrementThenDouble = x => double(increment(x));

console.log(incrementThenDouble(3)); // (3 + 1) * 2 = 8
```

---

## 🔹 General Compose Function

You can create a reusable `compose` utility function:

```js
const compose = (f, g) => x => f(g(x));
```

Use it like this:

```js
const incrementThenDouble = compose(double, increment);
console.log(incrementThenDouble(3)); // 8
```

This applies `increment` first, then `double`.

---

## 🔹 Compose with Multiple Functions

For more than two functions, a common pattern is:

```js
const composeMultiple = (...fns) => x =>
  fns.reduceRight((acc, fn) => fn(acc), x);

const add3 = x => x + 3;
const multiplyBy5 = x => x * 5;
const square = x => x * x;

const composed = composeMultiple(square, multiplyBy5, add3);
console.log(composed(2)); 
// add3(2) = 5 -> multiplyBy5(5) = 25 -> square(25) = 625
```

---

## 🔹 Difference between compose and pipe

* **compose** applies functions right-to-left: `compose(f, g)(x) = f(g(x))`
* **pipe** applies left-to-right: `pipe(f, g)(x) = g(f(x))`

---

## Summary

| Aspect               | Description                                              |
| -------------------- | -------------------------------------------------------- |
| Function Composition | Combining functions so output of one is input to another |
| Purpose              | Build complex logic from simple functions                |
| Benefits             | Cleaner, reusable, modular code                          |
| Common usage         | `compose(f, g)`, chaining functions                      |

---

## Interview Tip

Explain function composition as **the act of chaining functions together so the output of one becomes the input to another, enabling modular and readable code**.

---

## 24. What is memoization?

**Memoization** is a powerful optimization technique often used in JavaScript to improve performance by caching results of expensive function calls.

---

## ✅ What is Memoization?

**Memoization** is a process where a function **remembers (caches) the results of its previous executions** based on the input arguments. If the function is called again with the same inputs, it returns the cached result instead of recalculating it.

This avoids redundant computations and speeds up the program, especially useful for functions with heavy or repeated calculations.

---

## 🔹 How does it work?

* When the function is called, check if the result for those arguments already exists in the cache.
* If yes, return the cached value.
* If no, compute the result, store it in the cache, then return it.

---

## 🔹 Simple Example: Fibonacci with Memoization

Calculating Fibonacci numbers recursively without memoization is inefficient because it repeats the same calculations multiple times.

```javascript
function fibonacci(n, memo = {}) {
  if (n <= 1) return n;
  
  if (memo[n]) return memo[n];  // Return cached result if exists
  
  memo[n] = fibonacci(n - 1, memo) + fibonacci(n - 2, memo);  // Compute and cache
  return memo[n];
}

console.log(fibonacci(40));  // Fast compared to non-memoized version
```

---

## 🔹 Benefits of Memoization

* **Improves performance** by avoiding repeated work.
* Particularly useful in **recursive functions** and **pure functions** (same output for same input).
* Can be implemented manually or using libraries.

---

## 🔹 Memoization vs Caching

* **Memoization** is a specific type of caching focused on function calls.
* Caching can be more general (e.g., storing API responses).

---

## Summary

| Aspect      | Explanation                                    |
| ----------- | ---------------------------------------------- |
| Memoization | Cache function results for given inputs        |
| Purpose     | Optimize performance by avoiding recomputation |
| Use cases   | Recursive calculations, expensive operations   |
| Example     | Fibonacci sequence with caching results        |

---

## Interview Tip

If asked about memoization, explain it as a technique that **stores the results of expensive function calls so repeated calls with the same inputs are faster**.

---

## 25. What is the difference between a pure function and impure function?

Understanding **pure** vs **impure** functions is key in functional programming and writing predictable code.

---

## ✅ What is a Pure Function?

A **pure function** is a function that:

1. **Always returns the same output for the same input** (deterministic).
2. **Has no side effects** — it doesn’t modify any external state or variables outside its scope.

---

### Characteristics of Pure Functions:

* Output depends only on input parameters.
* No mutation of external variables or data.
* No I/O operations like logging, fetching data, or modifying DOM.
* Easier to test and reason about.

---

### Example of Pure Function:

```javascript
function add(a, b) {
  return a + b;
}

console.log(add(2, 3)); // Always 5
```

Given the same inputs, `add` always returns the same output, and it does not affect anything outside itself.

---

## ✅ What is an Impure Function?

An **impure function** is a function that:

* **May return different outputs for the same inputs**.
* **Has side effects** — modifies external state, performs I/O, changes variables outside its scope, etc.

---

### Characteristics of Impure Functions:

* Depends on external variables or mutable state.
* Causes side effects like modifying global variables, logging, network requests.
* Less predictable and harder to test.

---

### Example of Impure Function:

```javascript
let count = 0;

function increment() {
  count++;  // modifies external variable
  return count;
}

console.log(increment()); // 1
console.log(increment()); // 2 (different outputs)
```

Calling `increment()` changes `count` outside the function, so output varies and side effects exist.

---

## 🔹 Summary Table

| Aspect             | Pure Function               | Impure Function                          |
| ------------------ | --------------------------- | ---------------------------------------- |
| Output consistency | Same output for same input  | Output can vary                          |
| Side effects       | None                        | Has side effects (modifies state, I/O)   |
| Predictability     | High                        | Low                                      |
| Testing            | Easy                        | Harder                                   |
| Examples           | `Math.sqrt(x)`, `add(a, b)` | Functions that update UI, modify globals |

---

## Interview Tip

If asked, emphasize pure functions are **deterministic and side-effect free**, making code more predictable and easier to debug and test.

---

## 26. What is `this` keyword in JS?

The `this` keyword in JavaScript is a fundamental—but often confusing—concept. Let’s break it down clearly.

---

## ✅ What is `this` in JavaScript?

`this` is a **special keyword** that refers to the **context object** for the current execution of a function. It tells you *which object* is currently calling or owning the function.

---

## 🔹 How `this` is determined

Unlike many languages where `this` is fixed to the instance of the class, in JavaScript, the value of `this` depends on **how a function is called**, not where or how it is defined.

---

## 🔹 Different `this` behaviors by context

| Context                       | `this` refers to                                           |
| ----------------------------- | ---------------------------------------------------------- |
| Global scope (non-strict)     | Global object (`window` in browser, `global` in Node)      |
| Global scope (strict mode)    | `undefined`                                                |
| Object method                 | The object calling the method                              |
| Constructor function (`new`)  | The newly created instance                                 |
| `call()`, `apply()`, `bind()` | Explicitly set to the first argument                       |
| Arrow functions               | `this` is **lexically inherited** from the enclosing scope |

---

## 🔹 Examples

### 1. `this` in global scope (non-strict mode)

```js
console.log(this);  // window (browser global object)
```

### 2. Inside an object method

```js
const obj = {
  name: "Alice",
  greet: function() {
    console.log(this.name);
  }
};

obj.greet();  // "Alice" — `this` refers to `obj`
```

### 3. Inside a regular function (non-strict mode)

```js
function show() {
  console.log(this);
}

show();  // window (in browser)
```

### 4. Inside a constructor function

```js
function Person(name) {
  this.name = name;
}

const p = new Person("Bob");
console.log(p.name);  // "Bob"
```

### 5. Using `call()` or `apply()`

```js
function sayHello() {
  console.log(this.name);
}

const user = { name: "Charlie" };

sayHello.call(user);  // "Charlie"
```

### 6. Arrow function `this`

Arrow functions **do not have their own `this`** — they inherit it from their defining context.

```js
const obj = {
  name: "Dana",
  greet: () => {
    console.log(this.name);
  }
};

obj.greet();  // undefined (or window.name if defined), because `this` is lexically inherited from global scope
```

To fix this, use regular functions for methods needing `this`.

---

## 🔹 Summary Table

| Scenario             | `this` value                         |
| -------------------- | ------------------------------------ |
| Global scope         | Global object (`window` or `global`) |
| Object method        | Object owning the method             |
| Constructor function | New instance                         |
| `call/apply/bind`    | Explicitly set value                 |
| Arrow functions      | Lexical (from surrounding scope)     |

---

## Interview Tip

Explain `this` as **the object context of function execution**, determined by **how** the function is called, with arrow functions being special because they capture `this` from where they are defined rather than called.

---

## 27. How does `this` behave in arrow functions?

The behavior of `this` in **arrow functions** is one of their defining features and a key difference from regular functions.

---

## ✅ How does `this` behave in arrow functions?

* **Arrow functions do NOT have their own `this`**.
* Instead, `this` inside an arrow function is **lexically inherited** from the **surrounding (enclosing) scope** where the arrow function is defined.
* This means the value of `this` inside an arrow function is fixed and **cannot be changed** by calling methods like `.call()`, `.apply()`, or `.bind()`.

---

## 🔹 Why does this matter?

In traditional functions, `this` depends on **how the function is called**, which can sometimes cause confusion, especially in callbacks or event handlers.

Arrow functions solve this by capturing the `this` value of their **lexical context** (surrounding code).

---

## 🔹 Example:

```javascript
const obj = {
  name: "Alice",
  regularFunc: function() {
    console.log(this.name);  // 'Alice' — this refers to obj

    const arrowFunc = () => {
      console.log(this.name);  // 'Alice' — inherits this from regularFunc scope
    };

    arrowFunc();
  }
};

obj.regularFunc();
```

* The arrow function inside `regularFunc` uses the same `this` as `regularFunc`, which is `obj`.
* If `arrowFunc` was a regular function, `this` inside it would be `undefined` (strict mode) or global object.

---

## 🔹 Another example: Arrow function in global scope

```javascript
const arrow = () => {
  console.log(this);
};

arrow();  // In browser: window (global object)
```

* Here, `this` refers to the **global object** because the arrow function is defined in global scope.

---

## 🔹 Arrow functions ignore `.call()`, `.apply()`, `.bind()`

```javascript
const obj1 = { name: "Obj1" };
const obj2 = { name: "Obj2" };

const arrow = () => {
  console.log(this.name);
};

arrow.call(obj1);  // undefined or global name, NOT 'Obj1'
arrow.apply(obj2); // same here
```

---

## Summary:

| Aspect                   | Arrow Function `this`                            |
| ------------------------ | ------------------------------------------------ |
| Own `this`               | No                                               |
| Lexical `this`           | Yes, inherits from defining scope                |
| `call/apply/bind` effect | Ignored                                          |
| Common use case          | Keeps context in callbacks, avoids `.bind(this)` |

---

## Interview Tip

Explain that **arrow functions capture `this` from the surrounding scope at the time they are defined**, making them useful for preserving context in callbacks and avoiding surprises with `this`.

---

## 28. What is the difference between call, apply, and bind?

`call`, `apply`, and `bind` are three JavaScript methods used to explicitly set the value of `this` inside a function. They’re similar but have key differences.

---

## ✅ What are `call`, `apply`, and `bind`?

All three methods are functions on JavaScript’s `Function.prototype` and let you specify the `this` context when invoking a function.

---

## 🔹 `call`

* Calls a function **immediately** with a specified `this` value.
* Accepts arguments **passed one by one**.

```js
function greet(greeting, punctuation) {
  console.log(greeting + ', ' + this.name + punctuation);
}

const person = { name: "Alice" };

greet.call(person, "Hello", "!");  // Hello, Alice!
```

---

## 🔹 `apply`

* Calls a function **immediately** with a specified `this` value.
* Accepts arguments as an **array or array-like object**.

```js
greet.apply(person, ["Hi", "?"]);  // Hi, Alice?
```

---

## 🔹 `bind`

* Returns a **new function** with `this` permanently bound to the specified object.
* Does **not** call the function immediately.
* You can also **partially apply arguments** (preset some arguments).

```js
const greetAlice = greet.bind(person, "Hey");
greetAlice("!!!");  // Hey, Alice!!!
```

---

## 🔹 Summary Table

| Method  | Invocation | Arguments format            | Returns                 | Use case                                                         |
| ------- | ---------- | --------------------------- | ----------------------- | ---------------------------------------------------------------- |
| `call`  | Immediate  | List of arguments           | Result of function call | Call function once with explicit `this` and args                 |
| `apply` | Immediate  | Arguments as array          | Result of function call | Call function once with explicit `this` and args array           |
| `bind`  | Deferred   | List of arguments (partial) | New bound function      | Create new function with bound `this` and optionally preset args |

---

## 🔹 Example comparing all three

```js
function introduce(age, city) {
  console.log(`My name is ${this.name}, I am ${age} years old, living in ${city}.`);
}

const user = { name: "Bob" };

// call - immediate, args separated
introduce.call(user, 25, "New York");

// apply - immediate, args as array
introduce.apply(user, [30, "San Francisco"]);

// bind - returns new function, partial args allowed
const boundIntroduce = introduce.bind(user, 35);
boundIntroduce("Los Angeles");  // My name is Bob, I am 35 years old, living in Los Angeles.
```

---

## Interview Tip

If asked, explain:

* `call` and `apply` **invoke the function immediately** with a specified `this`.
* The difference between them is **how arguments are passed**.
* `bind` returns a **new function with `this` permanently bound** but does not call it immediately.

---

## 29. What is function debouncing and throttling?

**Debouncing** and **throttling** are two popular techniques to control how often a function gets executed, especially in scenarios like user input, scrolling, or resizing where events can fire very frequently.

---

## ✅ What is Function Debouncing?

**Debouncing** ensures that a function is only called **after a certain amount of time has passed since the last time it was invoked**. It delays the execution until the user **stops triggering the event** for a specified time.

### Use case:

* User stops typing in a search box, then you send a search query.
* Prevent excessive API calls while the user is still typing.

### How it works:

* The function execution is postponed until no new event happens for the delay period.
* If a new event comes before the delay ends, the timer resets.

---

### Debounce Example:

```js
function debounce(fn, delay) {
  let timeoutId;
  return function(...args) {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => fn.apply(this, args), delay);
  };
}

// Usage: 
const handleInput = debounce(() => {
  console.log('Input processed!');
}, 300);

document.getElementById('search').addEventListener('input', handleInput);
```

In this example, the `handleInput` function runs only after 300ms have passed **without** another input event.

---

## ✅ What is Function Throttling?

**Throttling** ensures that a function is called **at most once in a specified time interval**. It limits the execution rate, so the function runs repeatedly but not too often.

### Use case:

* Handling scroll events to update UI, but not on every pixel scrolled.
* Resize events where continuous firing is heavy on performance.

### How it works:

* When the function is called, it runs immediately.
* Then it ignores subsequent calls until the wait period expires.

---

### Throttle Example:

```js
function throttle(fn, delay) {
  let lastCall = 0;
  return function(...args) {
    const now = Date.now();
    if (now - lastCall >= delay) {
      lastCall = now;
      fn.apply(this, args);
    }
  };
}

// Usage:
const handleScroll = throttle(() => {
  console.log('Scroll event processed!');
}, 200);

window.addEventListener('scroll', handleScroll);
```

Here, `handleScroll` runs **at most once every 200ms**, regardless of how many scroll events fire.

---

## 🔹 Key Differences

| Aspect          | Debouncing                                  | Throttling                        |
| --------------- | ------------------------------------------- | --------------------------------- |
| When to trigger | After user **stops** triggering event       | At regular intervals during event |
| Function calls  | Only once after delay                       | Repeatedly, but limited frequency |
| Use cases       | Search input, window resizing, autocomplete | Scroll, resize, mousemove         |

---

## Interview Tip

Explain that **debounce** delays the function call until inactivity, while **throttle** guarantees a function is called at most once per specified time — both help optimize performance by controlling event frequency.

---

## 30. What is recursion and how is it used in JS?

Let’s dive into **recursion** and how it’s used in JavaScript.

---

## ✅ What is Recursion?

**Recursion** is a programming technique where a function **calls itself** to solve a smaller instance of the same problem until it reaches a base case (a condition where it stops calling itself).

---

## Why use recursion?

* To break down complex problems into simpler, smaller problems.
* Especially useful for tasks involving **nested or hierarchical data**, like trees or graphs.
* Useful for algorithms like factorial, Fibonacci sequence, traversing directories, etc.

---

## 🔹 Key components of recursion:

1. **Base Case** — condition to stop recursion (prevents infinite calls).
2. **Recursive Case** — the part where the function calls itself with modified arguments.

---

## Example: Factorial function using recursion

The factorial of a number `n` is defined as:

* `factorial(n) = n * factorial(n-1)`
* Base case: `factorial(0) = 1`

```javascript
function factorial(n) {
  if (n === 0) {
    return 1;  // Base case
  }
  return n * factorial(n - 1);  // Recursive case
}

console.log(factorial(5));  // 120
```

---

## Example: Fibonacci sequence using recursion

```javascript
function fibonacci(n) {
  if (n <= 1) {
    return n;  // Base case
  }
  return fibonacci(n - 1) + fibonacci(n - 2);  // Recursive case
}

console.log(fibonacci(6));  // 8
```

---

## How recursion works step-by-step (factorial(3)):

1. `factorial(3)` calls `factorial(2)`
2. `factorial(2)` calls `factorial(1)`
3. `factorial(1)` calls `factorial(0)`
4. `factorial(0)` returns 1 (base case)
5. `factorial(1)` returns 1 \* 1 = 1
6. `factorial(2)` returns 2 \* 1 = 2
7. `factorial(3)` returns 3 \* 2 = 6

---

## Things to be careful about

* **Always have a base case** to prevent infinite recursion (which causes stack overflow).
* Recursive solutions can be less efficient and more memory-heavy than iterative solutions.
* Sometimes recursion can be optimized with **memoization** or **tail recursion** (though tail call optimization support varies).

---

## Interview tip

Explain recursion as a function calling itself with smaller input until a base case stops it, and give a simple example like factorial or Fibonacci.

---

### 🔹 **31–45: Objects & Prototypes**

## 31. What are objects in JavaScript?

Objects are a core part of JavaScript and understanding them is essential.

---

## ✅ What are Objects in JavaScript?

An **object** in JavaScript is a **collection of key-value pairs** where:

* **Keys (also called properties)** are strings (or symbols).
* **Values** can be of any data type — primitives, functions, arrays, or even other objects.

Objects are used to **store and organize data** and represent **real-world entities** with properties and behaviors.

---

## 🔹 How to create objects?

### 1. Object literal syntax (most common)

```js
const person = {
  name: "Alice",
  age: 30,
  greet: function() {
    console.log("Hello, " + this.name);
  }
};

person.greet();  // Hello, Alice
```

### 2. Using the `new Object()` syntax

```js
const car = new Object();
car.make = "Toyota";
car.model = "Corolla";
```

### 3. Using constructor functions (older way)

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}

const bob = new Person("Bob", 25);
```

### 4. Using ES6 `class` syntax (syntactic sugar over constructor functions)

```js
class Animal {
  constructor(type) {
    this.type = type;
  }
}

const dog = new Animal("Dog");
```

---

## 🔹 Accessing object properties

* Dot notation: `obj.key`
* Bracket notation: `obj["key"]` (useful for dynamic keys)

```js
console.log(person.name);     // Alice
console.log(person["age"]);   // 30
```

---

## 🔹 Objects can store functions (methods)

```js
const calculator = {
  add: function(a, b) {
    return a + b;
  }
};

console.log(calculator.add(5, 3));  // 8
```

---

## 🔹 Objects are **reference types**

When you assign an object to another variable, both variables reference the same object in memory.

```js
const obj1 = { x: 10 };
const obj2 = obj1;

obj2.x = 20;
console.log(obj1.x);  // 20 (changed via obj2)
```

---

## Summary

* Objects store related data and functions together.
* They have properties (key-value pairs).
* They are reference types.
* You can create objects in multiple ways (literals, constructors, classes).
* Methods are functions inside objects.

---

## Interview Tip

Explain objects as **containers of related data and behavior**, accessible via keys, and fundamental to JS programming.

---

## 32. What is the prototype chain?

The **prototype chain** is a fundamental concept behind JavaScript’s inheritance and object behavior.

---

## ✅ What is the Prototype Chain?

In JavaScript, **every object has a hidden internal property called `[[Prototype]]`**, which points to another object (or `null`).

* This linked object is called the **prototype**.
* When you try to access a property or method on an object, JavaScript looks for it **on the object itself first**.
* If it’s not found, it looks **up the prototype chain**, following the `[[Prototype]]` links until it finds the property or reaches the end (`null`).

This mechanism allows **inheritance of properties and methods** between objects.

---

## 🔹 How the prototype chain works?

Imagine:

```
obj ---> obj.__proto__ ---> obj.__proto__.__proto__ ---> ... ---> null
```

* `obj` is your object.
* `obj.__proto__` (or `Object.getPrototypeOf(obj)`) is the prototype object.
* This chain continues until it hits `null`, which is the end of the chain.

---

## 🔹 Example:

```js
const animal = {
  eats: true,
  walk() {
    console.log("Animal walks");
  }
};

const rabbit = {
  jumps: true,
};

// Set rabbit’s prototype to animal
Object.setPrototypeOf(rabbit, animal);

console.log(rabbit.jumps);  // true (own property)
console.log(rabbit.eats);   // true (inherited from animal)
rabbit.walk();              // "Animal walks" (inherited method)
```

* `rabbit` doesn’t have `eats` or `walk`, so JS looks up to `animal` and finds them.

---

## 🔹 Prototype chain with functions and constructors

When you create a function in JS, it automatically has a `.prototype` property.

When you create an object with `new` from a constructor function:

```js
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  console.log(`Hello, ${this.name}`);
};

const bob = new Person("Bob");
bob.greet();  // Hello, Bob
```

Here:

* `bob`’s internal prototype (`bob.__proto__`) points to `Person.prototype`.
* The `greet` method is found on `Person.prototype`.

---

## 🔹 Visualizing the chain:

```
bob
  |
  v
Person.prototype  (has greet method)
  |
  v
Object.prototype (has methods like toString, hasOwnProperty)
  |
  v
null
```

If a property is not found on `bob`, JS looks at `Person.prototype`, then `Object.prototype`, then `null`.

---

## 🔹 Important:

* `Object.prototype` is the root of most prototype chains.
* You can check prototype with `Object.getPrototypeOf(obj)` or `__proto__`.
* Prototype chain is how inheritance and property lookup happens in JS.

---

## Interview Tip

Explain prototype chain as a **linked chain of objects** used for property lookup and inheritance, where if a property isn’t found on the object itself, JavaScript looks up the chain until it finds it or reaches null.

---

## 33. What is prototypal inheritance?

Prototypal inheritance is key to understanding JavaScript’s object model!

---

## ✅ What is Prototypal Inheritance?

**Prototypal inheritance** is a way for one object to inherit properties and methods from another object.

Unlike classical inheritance in languages like Java or C++, where classes define blueprints, JavaScript uses objects that **directly inherit from other objects** via the prototype chain.

---

## How does it work?

* Every JavaScript object has an internal link (`[[Prototype]]`) to another object (its prototype).
* When you access a property on an object, JS looks for it **on the object itself first**.
* If the property is not found, JS checks the prototype object.
* This lookup continues up the **prototype chain** until the property is found or the chain ends (`null`).

---

## 🔹 Example:

```js
const parent = {
  greet() {
    console.log("Hello from parent");
  }
};

const child = Object.create(parent);  // child inherits from parent

child.greet();  // Hello from parent
```

* `child` doesn’t have its own `greet` method.
* JS looks up `child`'s prototype (`parent`) and finds `greet`.

---

## 🔹 Using constructor functions:

```js
function Person(name) {
  this.name = name;
}

Person.prototype.sayHi = function() {
  console.log(`Hi, I'm ${this.name}`);
};

const alice = new Person("Alice");
alice.sayHi();  // Hi, I'm Alice
```

Here:

* `alice` inherits from `Person.prototype`.
* `sayHi` is available through the prototype chain.

---

## 🔹 ES6 Classes (syntactic sugar)

```js
class Animal {
  constructor(name) {
    this.name = name;
  }
  
  speak() {
    console.log(`${this.name} makes a noise.`);
  }
}

class Dog extends Animal {
  speak() {
    console.log(`${this.name} barks.`);
  }
}

const dog = new Dog("Rex");
dog.speak();  // Rex barks.
```

Even though it looks like classical inheritance, under the hood this is prototypal inheritance.

---

## Summary

| Aspect                                  | Description                                              |
| --------------------------------------- | -------------------------------------------------------- |
| What                                    | Objects inherit directly from other objects              |
| Mechanism                               | Prototype chain lookup                                   |
| How to create                           | `Object.create()`, constructor functions, classes        |
| Difference from class-based inheritance | No classes, inheritance is delegation through prototypes |

---

## Interview Tip

Explain prototypal inheritance as **objects inheriting from other objects via prototypes**, enabling property and method sharing without classes.

---

## 34. How is inheritance implemented in ES6?

ES6 introduced the `class` syntax, which provides a clearer, more concise way to implement inheritance in JavaScript, while under the hood it’s still using prototypal inheritance.

---

## ✅ How is inheritance implemented in ES6?

Using **`class`** and the **`extends`** keyword, ES6 lets you create a class that inherits from another class.

---

## Basic syntax

```js
class Parent {
  constructor(name) {
    this.name = name;
  }
  
  greet() {
    console.log(`Hello, I'm ${this.name}`);
  }
}

class Child extends Parent {
  constructor(name, age) {
    super(name);  // Calls Parent's constructor
    this.age = age;
  }
  
  info() {
    console.log(`I'm ${this.age} years old`);
  }
}

const childInstance = new Child("Alice", 25);
childInstance.greet(); // Hello, I'm Alice
childInstance.info();  // I'm 25 years old
```

---

## How it works internally

* `Child` class **inherits** from `Parent` class.
* The `extends` keyword sets up the prototype chain:

    * `Child.prototype.__proto__ === Parent.prototype`
* `super()` calls the parent class’s constructor and must be called before using `this` in the subclass constructor.
* Methods declared in the parent are available on instances of the child class.

---

## Prototype chain visualization

```
childInstance
  |
  v
Child.prototype
  |
  v
Parent.prototype
  |
  v
Object.prototype
  |
  v
null
```

---

## Key points

* ES6 classes are **syntactic sugar** over the existing prototype-based inheritance.
* You still get dynamic dispatch (overriding methods) and access to superclass methods via `super`.
* Classes provide a more familiar syntax for developers coming from class-based OOP languages.

---

## Example: Overriding methods and using `super`

```js
class Animal {
  speak() {
    console.log("Animal makes a sound");
  }
}

class Dog extends Animal {
  speak() {
    super.speak();  // Call parent method
    console.log("Dog barks");
  }
}

const dog = new Dog();
dog.speak();
// Output:
// Animal makes a sound
// Dog barks
```

---

## Interview tip

Mention that ES6 inheritance uses `class` and `extends` for clear syntax, but underneath, it’s prototype-based inheritance. Emphasize the use of `super()` to call the parent constructor or methods.

---

## 35. What is `Object.create()`?

`Object.create()` is a very useful and important method in JavaScript, especially when dealing with prototypal inheritance.

---

## ✅ What is `Object.create()`?

`Object.create()` is a method that creates a **new object** with its **prototype set to a specified object**.

It allows you to create an object that directly inherits from another object.

---

## Syntax:

```js
Object.create(proto, [propertiesObject])
```

* `proto`: The object to be used as the new object's prototype.
* `propertiesObject` (optional): An object specifying additional properties to add to the new object (same format as `Object.defineProperties`).

---

## Why use `Object.create()`?

* To create an object with a specific prototype.
* To set up inheritance without using constructor functions or classes.
* It’s a clean way to do **prototypal inheritance**.

---

## Example 1: Simple inheritance

```js
const parent = {
  greet() {
    console.log("Hello from parent");
  }
};

const child = Object.create(parent);

child.greet();  // Output: Hello from parent
console.log(Object.getPrototypeOf(child) === parent);  // true
```

Here:

* `child` is a new object.
* `child`'s prototype is set to `parent`.
* `child` can access `greet` method through prototype chain.

---

## Example 2: Adding own properties after creation

```js
const animal = {
  eats: true
};

const rabbit = Object.create(animal);
rabbit.jumps = true;

console.log(rabbit.eats);   // true (inherited)
console.log(rabbit.jumps);  // true (own property)
```

---

## Example 3: Using second argument to define properties

```js
const person = Object.create({}, {
  name: {
    value: "John",
    writable: true,
    enumerable: true,
    configurable: true
  },
  greet: {
    value: function() {
      console.log("Hi, I'm " + this.name);
    }
  }
});

person.greet();  // Hi, I'm John
```

---

## Summary

* `Object.create()` creates a new object with a specified prototype.
* It’s a straightforward way to implement prototypal inheritance.
* More flexible than constructor functions.
* Useful when you want to create objects without classes or constructors.

---

## Interview tip

Explain `Object.create()` as a method to create a new object that directly inherits from another object, making it ideal for prototypal inheritance in JavaScript.

---

## 36. What are getters and setters in JS?

**Getters and setters** are special methods in JavaScript that allow you to **control access** to an object’s properties, enabling you to run code when properties are read or assigned.

---

## ✅ What are Getters and Setters?

* **Getter**: A method that **gets** (retrieves) the value of a property.
* **Setter**: A method that **sets** (modifies) the value of a property.

They let you define **custom behavior** when accessing or updating properties.

---

## Why use getters and setters?

* To **encapsulate** internal data.
* To **validate** or **transform** data on assignment or retrieval.
* To create **computed properties** that look like regular properties but run code.

---

## How to define getters and setters

### 1. Using object literal syntax

```js
const person = {
  firstName: "John",
  lastName: "Doe",
  
  get fullName() {
    return this.firstName + " " + this.lastName;
  },
  
  set fullName(name) {
    const parts = name.split(" ");
    this.firstName = parts[0];
    this.lastName = parts[1];
  }
};

console.log(person.fullName);  // John Doe  (getter called)

person.fullName = "Jane Smith";  // setter called
console.log(person.firstName);    // Jane
console.log(person.lastName);     // Smith
```

### 2. Using `Object.defineProperty()`

```js
const person = {
  firstName: "John",
  lastName: "Doe"
};

Object.defineProperty(person, 'fullName', {
  get() {
    return this.firstName + " " + this.lastName;
  },
  set(name) {
    const parts = name.split(" ");
    this.firstName = parts[0];
    this.lastName = parts[1];
  },
  enumerable: true,
  configurable: true
});

console.log(person.fullName); // John Doe
person.fullName = "Jane Smith";
console.log(person.firstName); // Jane
```

---

## Important points

* Getters and setters behave like **normal properties** — you access or assign them without calling them like functions.
* They can help maintain **data integrity** and encapsulation.
* They enable **computed properties** that depend on other internal values.

---

## Interview tip

Explain getters and setters as **special object methods** to **control how properties are read or written**, useful for validation, computed properties, or encapsulation.

---

## 37. What are object destructuring and nested destructuring?

**Object destructuring** is a powerful and concise syntax in JavaScript that allows you to extract properties from objects into variables easily. **Nested destructuring** extends this idea to extract values from nested objects.

---

## ✅ What is Object Destructuring?

It’s a syntax that lets you unpack values from an object into distinct variables in a single, clean statement.

---

### Basic example:

```js
const person = {
  name: "Alice",
  age: 30,
  city: "New York"
};

const { name, age } = person;

console.log(name); // Alice
console.log(age);  // 30
```

* `{ name, age }` on the left side means: create variables `name` and `age` and assign them the corresponding values from `person`.

---

## ✅ What is Nested Destructuring?

When you have objects inside objects, you can destructure nested properties directly.

---

### Example:

```js
const person = {
  name: "Bob",
  address: {
    street: "123 Main St",
    city: "Boston",
    zip: 02118
  }
};

const { name, address: { city, zip } } = person;

console.log(name); // Bob
console.log(city); // Boston
console.log(zip);  // 2118
```

* Here, `address: { city, zip }` extracts the `city` and `zip` from the nested `address` object.

---

## Additional features

### 1. Default values

```js
const person = { name: "Alice" };

const { name, age = 25 } = person;

console.log(age); // 25 (default used because age is undefined in person)
```

### 2. Renaming variables

```js
const person = { name: "Alice", age: 30 };

const { name: firstName, age: years } = person;

console.log(firstName); // Alice
console.log(years);     // 30
```

---

## Summary

| Feature              | Description                                         | Example                              |
| -------------------- | --------------------------------------------------- | ------------------------------------ |
| Object destructuring | Extract properties into variables                   | `const { name, age } = obj;`         |
| Nested destructuring | Extract nested object properties                    | `const { address: { city } } = obj;` |
| Default values       | Provide defaults for missing properties             | `const { age = 20 } = obj;`          |
| Renaming variables   | Assign properties to variables with different names | `const { name: firstName } = obj;`   |

---

## Interview tip

Explain destructuring as a convenient way to **extract values from objects**, showing a simple example and mention nested destructuring for deeper objects.

---

## 38. What is the difference between `in` and `hasOwnProperty()`?

Both `in` and `hasOwnProperty()` are used to check if an object contains a certain property, but they work differently and serve different purposes.

---

## ✅ The difference between `in` and `hasOwnProperty()`

| Feature                   | `in` Operator                                                              | `hasOwnProperty()` Method                                               |
| ------------------------- | -------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| What it checks            | Checks if the property exists **anywhere** in the object’s prototype chain | Checks if the property exists **directly** on the object (own property) |
| Syntax                    | `'propertyName' in object`                                                 | `object.hasOwnProperty('propertyName')`                                 |
| Includes inherited props? | **Yes**                                                                    | **No**                                                                  |
| Usage scenario            | To check if an object or its prototypes have a property                    | To check if the property is an own property (not inherited)             |

---

## 🔹 Examples

```js
const parent = { inheritedProp: 42 };
const child = Object.create(parent);
child.ownProp = 7;

console.log('ownProp' in child);          // true (own property)
console.log('inheritedProp' in child);    // true (inherited property)

console.log(child.hasOwnProperty('ownProp'));       // true
console.log(child.hasOwnProperty('inheritedProp')); // false
```

---

## When to use which?

* Use **`in`** when you want to check if a property exists on the object **or anywhere in its prototype chain**.
* Use **`hasOwnProperty()`** when you want to ensure the property is an **own property** of the object (not inherited).

---

## Interview tip

Explain that:

* `in` checks for property presence anywhere (own or prototype).
* `hasOwnProperty()` strictly checks own properties only.
* This distinction is important to avoid errors, especially when iterating or manipulating objects.

---

Want me to also explain `Object.prototype.hasOwnProperty.call()` usage and why it’s safer sometimes?

---

## 39. What is a factory function?

Great question! A **factory function** is a common and powerful pattern in JavaScript for creating objects.

---

## ✅ What is a Factory Function?

A **factory function** is simply a **regular function** that **creates and returns a new object**. Instead of using classes or constructors with `new`, you call the factory function to get new objects.

---

## Why use factory functions?

* They avoid issues related to `this` and `new`.
* They allow encapsulation and can create private variables using closures.
* They can return different types of objects based on logic.
* They’re easy to understand and flexible.

---

## Example:

```js
function createPerson(name, age) {
  return {
    name,
    age,
    greet() {
      console.log(`Hi, I'm ${this.name}`);
    }
  };
}

const person1 = createPerson("Alice", 30);
const person2 = createPerson("Bob", 25);

person1.greet(); // Hi, I'm Alice
person2.greet(); // Hi, I'm Bob
```

Here:

* `createPerson` is a factory function.
* Each call returns a new object with its own properties and methods.

---

## Advantages over constructor functions:

* No need to use `new` keyword.
* Avoids mistakes like forgetting `new`.
* Can easily create private state via closures.

---

## Example with private variables (using closure):

```js
function createCounter() {
  let count = 0;  // private variable

  return {
    increment() {
      count++;
      console.log(count);
    },
    decrement() {
      count--;
      console.log(count);
    }
  };
}

const counter = createCounter();
counter.increment(); // 1
counter.increment(); // 2
counter.decrement(); // 1
```

`count` is **not accessible directly** from outside — only through the returned methods.

---

## Interview tip

Explain factory functions as **functions that create and return objects**, highlighting simplicity, flexibility, and advantages over constructor functions.

---

## 40. What is the difference between a shallow and deep copy?

Understanding **shallow vs deep copy** is crucial when working with objects and arrays in JavaScript.

---

## ✅ What is a Shallow Copy?

A **shallow copy** creates a new object or array that copies the **top-level properties**, but **nested objects or arrays are still referenced** (not copied).

* Changes to nested objects inside the copy affect the original and vice versa.
* Only the first level is duplicated; deeper levels share references.

---

## ✅ What is a Deep Copy?

A **deep copy** duplicates **everything recursively**, creating an entirely independent clone of the original object, including all nested objects and arrays.

* Changes in the deep copy do **not** affect the original object at any level.
* Requires more processing than shallow copying.

---

## 🔹 Example to illustrate:

```js
const original = {
  name: "Alice",
  address: {
    city: "New York",
    zip: 10001
  }
};

// Shallow copy using Object.assign
const shallowCopy = Object.assign({}, original);

// Deep copy using JSON methods (simple but with caveats)
const deepCopy = JSON.parse(JSON.stringify(original));

// Modify nested property in shallow copy
shallowCopy.address.city = "Boston";

console.log(original.address.city); // Boston — affected by change (shared reference)

// Modify nested property in deep copy
deepCopy.address.city = "Chicago";

console.log(original.address.city); // Boston — not affected by deep copy
console.log(deepCopy.address.city); // Chicago
```

---

## Why does this happen?

* **Shallow copy** duplicates only references of nested objects.
* **Deep copy** duplicates all nested structures recursively.

---

## Common ways to make shallow copies

* For objects: `Object.assign({}, obj)`
* For arrays: `arr.slice()`, `[...arr]`

## Common ways to make deep copies

* Using `JSON.parse(JSON.stringify(obj))` (simple, but loses functions, `undefined`, symbols, dates, etc.)
* Using libraries like `lodash`'s `_.cloneDeep()`
* Writing custom recursive cloning functions

---

## Summary

| Copy Type    | What is copied?                     | Nested objects/arrays                  | Example method(s)                               |
| ------------ | ----------------------------------- | -------------------------------------- | ----------------------------------------------- |
| Shallow copy | Top-level properties only           | Nested objects are shared (references) | `Object.assign()`, spread `{...obj}`            |
| Deep copy    | Entire object structure recursively | Entirely independent                   | `JSON.parse(JSON.stringify())`, `_.cloneDeep()` |

---

## Interview tip

Explain shallow copy copies only the top level, so nested objects are shared, while deep copy duplicates everything recursively, making independent copies of nested objects.

---

## 41. How do you clone an object in JavaScript?

Cloning objects in JavaScript can be done in multiple ways depending on whether you want a **shallow** or **deep** copy. Here’s a detailed explanation with examples.

---

## 1. Shallow Cloning

A **shallow clone** copies only the first level of the object. Nested objects or arrays inside will still be referenced (not duplicated).

### Common ways to shallow clone an object:

### a) Using `Object.assign()`

```js
const original = { a: 1, b: 2 };
const clone = Object.assign({}, original);

console.log(clone); // { a: 1, b: 2 }
```

### b) Using spread operator `{ ...obj }`

```js
const original = { a: 1, b: 2 };
const clone = { ...original };

console.log(clone); // { a: 1, b: 2 }
```

---

### Important:

Both methods above **do not deep clone nested objects**. For example:

```js
const original = { a: 1, b: { c: 2 } };
const clone = { ...original };

clone.b.c = 42;
console.log(original.b.c);  // 42 (changed because `b` is referenced)
```

---

## 2. Deep Cloning

A **deep clone** duplicates the entire object including nested objects and arrays, making the clone fully independent.

### Common ways to deep clone:

### a) Using `JSON.parse(JSON.stringify())`

```js
const original = { a: 1, b: { c: 2 } };
const deepClone = JSON.parse(JSON.stringify(original));

deepClone.b.c = 42;
console.log(original.b.c);  // 2 (original unaffected)
```

#### Limitations:

* Cannot clone functions, `undefined`, `Symbol`, `Date`, `RegExp`, Maps, Sets, etc.
* Loses special object types and methods.

---

### b) Using libraries like **Lodash**

Lodash’s `_.cloneDeep()` handles deep cloning with better support.

```js
const _ = require('lodash');

const original = { a: 1, b: { c: 2 } };
const deepClone = _.cloneDeep(original);

deepClone.b.c = 42;
console.log(original.b.c); // 2 (original unaffected)
```

---

### c) Writing a custom recursive deep clone function

This is more advanced and covers special cases. Example (simplified):

```js
function deepClone(obj) {
  if (obj === null || typeof obj !== 'object') {
    return obj; // Return primitive values as is
  }
  
  if (Array.isArray(obj)) {
    return obj.map(deepClone);
  }
  
  const clone = {};
  for (const key in obj) {
    if (obj.hasOwnProperty(key)) {
      clone[key] = deepClone(obj[key]);
    }
  }
  return clone;
}
```

---

## Summary

| Clone type    | How it works                     | Pros                       | Cons                        |
| ------------- | -------------------------------- | -------------------------- | --------------------------- |
| Shallow clone | Copies top-level properties only | Simple, fast               | Nested objects still shared |
| Deep clone    | Recursively copies everything    | Independent nested objects | More complex, slower        |

---

## Interview tip

* Mention shallow cloning with spread or `Object.assign()`.
* Explain deep cloning via JSON or libraries, noting limitations.
* Optionally mention custom recursive cloning for full control.

---

## 42. What is the use of `Object.assign()`?

`Object.assign()` is a very handy method in JavaScript used for **copying properties** from one or more source objects to a target object.

---

## ✅ What is `Object.assign()`?

`Object.assign(target, ...sources)` copies **enumerable own properties** from one or more source objects to a target object and returns the target object.

---

## Main uses of `Object.assign()`:

### 1. **Shallow copying an object**

```js
const original = { a: 1, b: 2 };
const copy = Object.assign({}, original);

console.log(copy);  // { a: 1, b: 2 }
```

### 2. **Merging multiple objects**

```js
const obj1 = { a: 1 };
const obj2 = { b: 2 };
const merged = Object.assign({}, obj1, obj2);

console.log(merged);  // { a: 1, b: 2 }
```

### 3. **Adding or overriding properties**

```js
const obj = { a: 1, b: 2 };
Object.assign(obj, { b: 3, c: 4 });

console.log(obj);  // { a: 1, b: 3, c: 4 }
```

---

## Important notes:

* **Shallow copy only**: Nested objects or arrays inside are still referenced, not deeply copied.

```js
const original = { a: 1, b: { c: 2 } };
const copy = Object.assign({}, original);

copy.b.c = 42;
console.log(original.b.c);  // 42 (nested object shared)
```

* **Only copies enumerable own properties**: It does **not** copy inherited properties or non-enumerable properties.

---

## Summary:

| Purpose                 | Usage                                     |
| ----------------------- | ----------------------------------------- |
| Shallow clone object    | `Object.assign({}, obj)`                  |
| Merge objects           | `Object.assign(target, source1, source2)` |
| Add/override properties | `Object.assign(obj, { key: value })`      |

---

## Interview tip

Explain `Object.assign()` as a method for **copying and merging objects**, emphasizing it performs **shallow copying** and only copies **own enumerable properties**.

---

## 43. How can you iterate over object properties?

In JavaScript, there are several ways to **iterate over the properties of an object**. Here’s a detailed explanation with examples:

---

## 1. Using `for...in` loop

* Iterates over **all enumerable properties**, including inherited ones.
* Often combined with `hasOwnProperty()` to filter own properties.

```js
const obj = { a: 1, b: 2, c: 3 };

for (const key in obj) {
  if (obj.hasOwnProperty(key)) {  // ensure own properties only
    console.log(key, obj[key]);
  }
}
```

Output:

```
a 1
b 2
c 3
```

---

## 2. Using `Object.keys()`

* Returns an **array of own enumerable property names** (keys).
* Use with `forEach()`, `for...of`, or other array methods.

```js
const obj = { a: 1, b: 2, c: 3 };

Object.keys(obj).forEach(key => {
  console.log(key, obj[key]);
});
```

---

## 3. Using `Object.values()`

* Returns an array of the object's **own enumerable property values**.

```js
const obj = { a: 1, b: 2, c: 3 };

Object.values(obj).forEach(value => {
  console.log(value);
});
```

---

## 4. Using `Object.entries()`

* Returns an array of `[key, value]` pairs for the object's own enumerable properties.

```js
const obj = { a: 1, b: 2, c: 3 };

for (const [key, value] of Object.entries(obj)) {
  console.log(key, value);
}
```

---

## Summary of methods:

| Method             | Iterates over             | Includes inherited? | Output type                  |
| ------------------ | ------------------------- | ------------------- | ---------------------------- |
| `for...in`         | Enumerable properties     | Yes                 | Property names (keys)        |
| `Object.keys()`    | Own enumerable properties | No                  | Array of keys                |
| `Object.values()`  | Own enumerable properties | No                  | Array of values              |
| `Object.entries()` | Own enumerable properties | No                  | Array of \[key, value] pairs |

---

## Interview tip

* Mention `for...in` with `hasOwnProperty()` for own props.
* Show usage of `Object.keys()`, `Object.values()`, `Object.entries()`.
* Explain difference between inherited and own properties.

---

## 44. How do you merge two objects in JavaScript?

Merging two (or more) objects in JavaScript is a common task and can be done in several ways. Here’s a detailed explanation with examples:

---

## 1. Using `Object.assign()`

`Object.assign(target, ...sources)` copies properties from source objects into the target object. Later sources overwrite earlier ones on conflict.

```js
const obj1 = { a: 1, b: 2 };
const obj2 = { b: 3, c: 4 };

const merged = Object.assign({}, obj1, obj2);

console.log(merged); // { a: 1, b: 3, c: 4 }
```

* Here, `{}` is the empty target object, so original objects stay unchanged.
* Property `b` is overwritten by `obj2`.

---

## 2. Using Spread Operator `{ ...obj }`

ES6 introduced the spread syntax, which is a clean way to merge objects.

```js
const obj1 = { a: 1, b: 2 };
const obj2 = { b: 3, c: 4 };

const merged = { ...obj1, ...obj2 };

console.log(merged); // { a: 1, b: 3, c: 4 }
```

* Works similarly to `Object.assign()`.
* Later spreads overwrite earlier properties.

---

## Important notes:

* Both methods create **shallow merges**: nested objects inside are not deeply merged, but replaced.

```js
const obj1 = { a: 1, b: { x: 10 } };
const obj2 = { b: { y: 20 }, c: 3 };

const merged = { ...obj1, ...obj2 };

console.log(merged.b); // { y: 20 } — replaced entirely, not merged deeply
```

---

## For deep merging

* You need libraries like Lodash's `_.merge()`.
* Or write a custom deep merge function.

---

## Summary:

| Method            | Syntax                          | Notes                             |
| ----------------- | ------------------------------- | --------------------------------- |
| `Object.assign()` | `Object.assign({}, obj1, obj2)` | Shallow merge, modifies target    |
| Spread operator   | `{ ...obj1, ...obj2 }`          | Shallow merge, creates new object |

---

## Interview tip

Explain that merging copies properties into one object and that `Object.assign()` and spread operator are the two common ways, both shallow merges.

---

## 45. What are Symbol and Symbol.iterator?

Both `Symbol` and `Symbol.iterator` are important concepts in modern JavaScript (ES6+). Let me explain them in detail:

---

## 1. What is a **Symbol**?

* **Symbol** is a **primitive data type** introduced in ES6.
* It represents a **unique and immutable identifier**.
* Every Symbol is unique, even if two Symbols have the same description.
* Typically used to create **unique property keys** for objects to avoid name collisions.

### How to create a Symbol:

```js
const sym1 = Symbol('description');
const sym2 = Symbol('description');

console.log(sym1 === sym2); // false — each symbol is unique
```

### Using Symbols as object keys:

```js
const id = Symbol('id');
const user = {
  name: 'Alice',
  [id]: 123
};

console.log(user[id]); // 123
```

---

## 2. What is `Symbol.iterator`?

* `Symbol.iterator` is a **well-known Symbol** that defines the default **iterator** for an object.
* It’s the key that JavaScript looks for when you use **`for...of` loops**, spread operator (`...`), or other constructs that iterate.
* Objects that implement `Symbol.iterator` are called **iterable**.

### Example: Using `Symbol.iterator` on arrays (arrays have it by default)

```js
const arr = [1, 2, 3];

const iterator = arr[Symbol.iterator]();

console.log(iterator.next()); // { value: 1, done: false }
console.log(iterator.next()); // { value: 2, done: false }
console.log(iterator.next()); // { value: 3, done: false }
console.log(iterator.next()); // { value: undefined, done: true }
```

### Custom iterable example:

```js
const myIterable = {
  data: [10, 20, 30],
  [Symbol.iterator]() {
    let index = 0;
    const data = this.data;
    return {
      next() {
        if (index < data.length) {
          return { value: data[index++], done: false };
        } else {
          return { done: true };
        }
      }
    };
  }
};

for (const value of myIterable) {
  console.log(value); // 10, then 20, then 30
}
```

---

## Why use Symbols?

* To create **unique keys** that won’t collide with other properties.
* To implement **custom iteration protocols** using `Symbol.iterator`.
* To define other well-known Symbol behaviors like `Symbol.toStringTag`, `Symbol.asyncIterator`, etc.

---

## Summary

| Term              | Description                                        | Usage example                                           |
| ----------------- | -------------------------------------------------- | ------------------------------------------------------- |
| `Symbol`          | Unique, immutable primitive for unique keys        | `const sym = Symbol('key')`                             |
| `Symbol.iterator` | Well-known symbol used to define iterable behavior | Implement `[Symbol.iterator]()` to make object iterable |

---

## Interview tip

Explain:

* `Symbol` is used for unique property keys.
* `Symbol.iterator` enables objects to be iterable in loops and spreads.
* Show example of custom iterable to demonstrate understanding.

---

### 🔹 **46–60: Arrays & Strings**

## 46. What are array methods like `map()`, `filter()`, `reduce()`?

`map()`, `filter()`, and `reduce()` are some of the most powerful and commonly used **array methods** in JavaScript. They help you transform, select, or accumulate array data in a clean, functional style.

---

## 1. `map()`

* **Purpose:** Creates a new array by applying a function to each element of the original array.
* It **transforms** each element.
* Returns a new array of the same length.

### Example:

```js
const numbers = [1, 2, 3];
const doubled = numbers.map(num => num * 2);

console.log(doubled); // [2, 4, 6]
```

---

## 2. `filter()`

* **Purpose:** Creates a new array with all elements that pass a test (predicate function).
* It **filters** elements based on a condition.
* Returns a new array with possibly fewer elements.

### Example:

```js
const numbers = [1, 2, 3, 4, 5];
const evens = numbers.filter(num => num % 2 === 0);

console.log(evens); // [2, 4]
```

---

## 3. `reduce()`

* **Purpose:** Reduces the array to a single value by applying a function that accumulates results.
* Takes a callback with parameters: accumulator, current value, index, and the array.
* Can take an initial value for the accumulator.

### Example: Sum of numbers

```js
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((accumulator, current) => accumulator + current, 0);

console.log(sum); // 10
```

### Example: Flatten an array of arrays

```js
const arrays = [[1, 2], [3, 4], [5]];
const flattened = arrays.reduce((acc, curr) => acc.concat(curr), []);

console.log(flattened); // [1, 2, 3, 4, 5]
```

---

## Summary

| Method     | Purpose                              | Returns                 | Does it mutate original array? |
| ---------- | ------------------------------------ | ----------------------- | ------------------------------ |
| `map()`    | Transform each element               | New array (same length) | No                             |
| `filter()` | Select elements by condition         | New array (<= length)   | No                             |
| `reduce()` | Accumulate all elements to one value | Single value            | No                             |

---

## Interview tip

* Explain each method clearly with use-cases.
* Mention they do **not mutate** the original array.
* Optionally show chaining like `arr.filter(...).map(...)`.

---

## 47. How does `reduce()` work internally?

Understanding how `reduce()` works internally helps grasp its power and flexibility.

---

## What is `reduce()`?

`reduce()` takes an array and **reduces it to a single value** by repeatedly applying a callback function on each element while maintaining an **accumulator**.

---

## How does it work internally?

When you call:

```js
array.reduce(callback(accumulator, currentValue, currentIndex, array), initialValue)
```

**Steps internally:**

1. **Initialization:**

* If `initialValue` is provided:

    * `accumulator` is set to `initialValue`.
    * Iteration starts from index `0`.
* If `initialValue` is **not provided**:

    * `accumulator` is set to the **first element** (`array[0]`).
    * Iteration starts from index `1`.

2. **Iteration:**

* For each element from start index to end:

    * The callback is called:

      ```js
      accumulator = callback(accumulator, currentValue, currentIndex, array);
      ```
    * The returned value becomes the new `accumulator`.

3. **Return:**

* After the last element is processed, `reduce()` returns the final value of `accumulator`.

---

## Visual example

```js
const arr = [1, 2, 3, 4];

const result = arr.reduce((acc, curr) => {
  console.log(`acc: ${acc}, curr: ${curr}`);
  return acc + curr;
}, 0);

console.log(result);  // 10
```

Output:

```
acc: 0, curr: 1
acc: 1, curr: 2
acc: 3, curr: 3
acc: 6, curr: 4
10
```

---

## Key points:

* `reduce()` **does not mutate** the original array.
* The callback is called exactly once for each element (except if empty array and no initialValue).
* If the array is empty and no `initialValue` is passed, `reduce()` throws a `TypeError`.
* You can use `reduce()` for many operations: sum, product, flattening arrays, grouping, counting, etc.

---

## Simplified internal behavior (pseudocode):

```js
function reduce(array, callback, initialValue) {
  let accumulator, startIndex;

  if (initialValue !== undefined) {
    accumulator = initialValue;
    startIndex = 0;
  } else {
    accumulator = array[0];
    startIndex = 1;
  }

  for (let i = startIndex; i < array.length; i++) {
    accumulator = callback(accumulator, array[i], i, array);
  }

  return accumulator;
}
```

---

## Interview tip:

* Explain how accumulator updates at each step.
* Mention difference in behavior when initial value is provided or not.
* Highlight flexibility of `reduce()`.

---

## 48. What is the difference between `forEach()` and `map()`?

Both `forEach()` and `map()` are used to iterate over arrays in JavaScript, but they have important differences in behavior and use cases.

---

## 1. Purpose & Return Value

| Feature      | `forEach()`                                           | `map()`                                       |
| ------------ | ----------------------------------------------------- | --------------------------------------------- |
| Purpose      | Execute a function on each element (for side effects) | Transform each element and create a new array |
| Return value | `undefined` (does **not** return anything)            | New array with transformed elements           |

---

## 2. Does it mutate original array?

* Neither method **mutates** the original array by default.
* But `forEach()` is often used to mutate external variables or the original array by side effects.
* `map()` returns a **new array** without modifying the original.

---

## 3. Example: Using `forEach()`

```js
const numbers = [1, 2, 3];
let sum = 0;

numbers.forEach(num => {
  sum += num;  // side effect: updating external variable
});

console.log(sum);  // 6
```

---

## 4. Example: Using `map()`

```js
const numbers = [1, 2, 3];
const doubled = numbers.map(num => num * 2);

console.log(doubled);  // [2, 4, 6]
console.log(numbers);  // [1, 2, 3] (original unchanged)
```

---

## 5. When to use which?

| Use Case                                                                    | Recommended Method |
| --------------------------------------------------------------------------- | ------------------ |
| You want to **transform** array elements and get a new array                | `map()`            |
| You want to **perform side effects** (like logging, updating external vars) | `forEach()`        |

---

## Summary

| Aspect     | `forEach()`  | `map()`             |
| ---------- | ------------ | ------------------- |
| Returns    | `undefined`  | New array           |
| Usage      | Side effects | Data transformation |
| Chainable? | No           | Yes (returns array) |

---

## Interview tip

* Highlight that `map()` returns a new array, while `forEach()` does not return anything.
* Mention that `map()` is chainable with other array methods; `forEach()` is not.
* Clarify the difference between transformation (`map`) and iteration for side effects (`forEach`).

---

## 49. How do you remove duplicates from an array?

Removing duplicates from an array is a very common task in JavaScript, and there are several efficient ways to do it. Here are some popular methods with explanations and examples:

---

## 1. Using a `Set`

* A `Set` is a built-in object that **stores unique values** of any type.
* You can convert an array to a `Set` to automatically remove duplicates, then convert back to an array.

```js
const arr = [1, 2, 2, 3, 4, 4, 5];

const uniqueArr = [...new Set(arr)];

console.log(uniqueArr); // [1, 2, 3, 4, 5]
```

---

## 2. Using `filter()` and `indexOf()`

* Use `filter()` to keep only the elements whose **first index matches the current index**, effectively removing duplicates.

```js
const arr = [1, 2, 2, 3, 4, 4, 5];

const uniqueArr = arr.filter((item, index) => arr.indexOf(item) === index);

console.log(uniqueArr); // [1, 2, 3, 4, 5]
```

---

## 3. Using a temporary object or map (for older environments)

* Use an object to track seen values.

```js
const arr = [1, 2, 2, 3, 4, 4, 5];
const seen = {};
const uniqueArr = [];

for (const item of arr) {
  if (!seen[item]) {
    uniqueArr.push(item);
    seen[item] = true;
  }
}

console.log(uniqueArr); // [1, 2, 3, 4, 5]
```

---

## Summary

| Method                         | Pros                        | Cons                                |
| ------------------------------ | --------------------------- | ----------------------------------- |
| Using `Set`                    | Simple, concise, efficient  | Only works for primitives           |
| Using `filter()` + `indexOf()` | Works well, no extra memory | Less efficient for large arrays     |
| Using object tracking          | Works in older JS versions  | More verbose, limited to primitives |

---

## Interview tip

* Mention `Set` as the modern and most concise solution.
* Explain the logic behind `filter()` and `indexOf()` approach.
* If asked, mention complexity: `Set` uses hash internally and is faster on large data.

---

## 50. How do you flatten an array?

Flattening an array means converting a nested array (an array with arrays inside it) into a single-level array.

---

## 1. Using `Array.prototype.flat()` (ES2019+)

The easiest and most modern way is the built-in `.flat()` method:

```js
const nested = [1, 2, [3, 4], [5, [6, 7]]];

const flattened = nested.flat();

console.log(flattened); // [1, 2, 3, 4, 5, [6, 7]]
```

* By default, `.flat()` flattens **one level** deep.
* You can pass a depth argument to flatten deeper:

```js
const deeplyNested = [1, 2, [3, 4], [5, [6, 7]]];

const fullyFlattened = deeplyNested.flat(2);

console.log(fullyFlattened); // [1, 2, 3, 4, 5, 6, 7]
```

---

## 2. Using `reduce()` and recursion (works in older JS versions)

If `.flat()` is not available, you can write a recursive function with `reduce()`:

```js
function flatten(arr) {
  return arr.reduce((acc, val) => {
    if (Array.isArray(val)) {
      acc = acc.concat(flatten(val)); // recursively flatten
    } else {
      acc.push(val);
    }
    return acc;
  }, []);
}

const nested = [1, 2, [3, 4], [5, [6, 7]]];
console.log(flatten(nested)); // [1, 2, 3, 4, 5, 6, 7]
```

---

## 3. Using `while` loop and `some()` (iterative approach)

```js
function flatten(arr) {
  while (arr.some(Array.isArray)) {
    arr = [].concat(...arr);
  }
  return arr;
}

const nested = [1, 2, [3, 4], [5, [6, 7]]];
console.log(flatten(nested)); // [1, 2, 3, 4, 5, 6, 7]
```

---

## Summary

| Method                 | Description                   | Notes                            |
| ---------------------- | ----------------------------- | -------------------------------- |
| `.flat(depth)`         | Built-in, easy to use         | Available in modern browsers     |
| Recursive `reduce()`   | Works in all JS versions      | More code but flexible           |
| Iterative `while` loop | Flatten by repeatedly merging | Useful if recursion is a concern |

---

## Interview tip

* Mention `.flat()` as the modern approach.
* Be ready to explain recursion with `reduce()`.
* Demonstrate understanding by showing how to flatten different nested depths.

---

## 51. How do you reverse a string in JavaScript?

Reversing a string in JavaScript is a common task and can be done efficiently using built-in methods. Here's how it works step-by-step:

---

## How to Reverse a String

JavaScript strings are **immutable**, so you can't reverse them in place. Instead, the common approach is:

1. Convert the string into an **array of characters**.
2. Reverse the array.
3. Join the array back into a string.

---

## Example using built-in methods:

```js
const str = "hello";

// Step 1: Convert to array of characters
const arr = str.split('');  // ["h", "e", "l", "l", "o"]

// Step 2: Reverse the array
arr.reverse();              // ["o", "l", "l", "e", "h"]

// Step 3: Join back to string
const reversedStr = arr.join(''); // "olleh"

console.log(reversedStr);
```

**Output:**

```
olleh
```

---

## One-liner:

```js
const reversed = "hello".split('').reverse().join('');
console.log(reversed);  // olleh
```

---

## Handling Unicode and surrogate pairs (optional advanced note)

Some characters (like emojis or certain foreign characters) are represented by **two code units** (surrogate pairs). The simple approach above can break such characters.

For full Unicode safety, you can use:

```js
const reversed = [...str].reverse().join('');
```

Here, `[...str]` uses the spread operator, which correctly splits string by Unicode code points.

---

## Interview tip

* Explain string immutability.
* Show basic method with `split()`, `reverse()`, `join()`.
* Mention Unicode caveat and spread operator if you want to impress!

---

## 52. How do you check if a string is a palindrome?

Checking if a string is a **palindrome** means verifying whether it reads the same forward and backward.

---

## Basic steps to check palindrome:

1. **Normalize** the string (optional but recommended)

    * Convert to lowercase to ignore case
    * Remove non-alphanumeric characters (spaces, punctuation) if you want to ignore those

2. **Reverse** the string.

3. **Compare** the normalized string with its reversed version.

---

## Example: Palindrome check function

```js
function isPalindrome(str) {
  // Normalize: lowercase and remove non-alphanumeric chars
  const normalized = str.toLowerCase().replace(/[^a-z0-9]/g, '');
  
  // Reverse the normalized string
  const reversed = normalized.split('').reverse().join('');
  
  // Check if palindrome
  return normalized === reversed;
}

// Test cases
console.log(isPalindrome("Racecar"));            // true
console.log(isPalindrome("A man, a plan, a canal, Panama!"));  // true
console.log(isPalindrome("Hello"));              // false
```

---

## Explanation

* `toLowerCase()` makes the comparison case-insensitive.
* `replace(/[^a-z0-9]/g, '')` removes all characters except letters and numbers.
* Then we reverse and compare.

---

## Interview tip

* Mention handling case sensitivity and special characters.
* Explain step-by-step normalization and comparison.
* Show sample test cases.

---

## 53. How do you convert an array to a string?

Converting an array to a string in JavaScript is straightforward and there are a few ways to do it depending on how you want the output formatted.

---

## 1. Using `toString()`

* Converts the array elements to strings and **joins them with commas** by default.

```js
const arr = [1, 2, 3, 4];
console.log(arr.toString()); // "1,2,3,4"
```

---

## 2. Using `join()` (more flexible)

* Joins array elements into a string with a **custom separator** you specify.

```js
const arr = [1, 2, 3, 4];

console.log(arr.join());     // "1,2,3,4"  (default is comma)
console.log(arr.join(''));   // "1234"     (no separator)
console.log(arr.join(' '));  // "1 2 3 4"  (space separator)
console.log(arr.join('-'));  // "1-2-3-4"  (hyphen separator)
```

---

## 3. Using `String()` function

* Converts array to string implicitly calls `toString()` internally.

```js
const arr = [1, 2, 3, 4];
console.log(String(arr)); // "1,2,3,4"
```

---

## Summary

| Method       | Output Example             | Separator Used |
| ------------ | -------------------------- | -------------- |
| `toString()` | `"1,2,3,4"`                | Comma (`,`)    |
| `join()`     | Custom (e.g., `"1-2-3-4"`) | User-defined   |
| `String()`   | Same as `toString()`       | Comma (`,`)    |

---

## Interview tip

* Explain the difference between `toString()` and `join()`.
* Emphasize that `join()` is the preferred method when you want control over the separator.
* Mention that all elements are converted to strings in the process.

---

## 54. What are `find()`, `findIndex()`, `some()`, and `every()`?

These are very useful **array iteration methods** in JavaScript that help you search and test elements based on conditions.

---

## 1. `find()`

* Returns the **first element** in the array that satisfies the provided testing function.
* If no element matches, returns `undefined`.

```js
const arr = [5, 12, 8, 130, 44];

const found = arr.find(element => element > 10);
console.log(found);  // 12
```

---

## 2. `findIndex()`

* Returns the **index** of the first element that satisfies the testing function.
* Returns `-1` if no element matches.

```js
const arr = [5, 12, 8, 130, 44];

const index = arr.findIndex(element => element > 10);
console.log(index);  // 1  (index of 12)
```

---

## 3. `some()`

* Tests whether **at least one element** in the array passes the test implemented by the provided function.
* Returns `true` if **any** element matches; otherwise, `false`.

```js
const arr = [1, 2, 3, 4, 5];

const hasEven = arr.some(num => num % 2 === 0);
console.log(hasEven);  // true (because 2 and 4 are even)
```

---

## 4. `every()`

* Tests whether **all elements** in the array pass the test implemented by the provided function.
* Returns `true` only if **every** element matches; otherwise, `false`.

```js
const arr = [2, 4, 6, 8];

const allEven = arr.every(num => num % 2 === 0);
console.log(allEven);  // true
```

---

## Summary Table

| Method        | Returns                         | Stops iteration when?     | Use case example                    |
| ------------- | ------------------------------- | ------------------------- | ----------------------------------- |
| `find()`      | First matching element          | When first match found    | Get first user with age > 30        |
| `findIndex()` | Index of first matching element | When first match found    | Find index of item to update        |
| `some()`      | `true` if any element matches   | When first match found    | Check if array contains even number |
| `every()`     | `true` if all elements match    | When first mismatch found | Check if all users are active       |

---

## Interview tip

* Explain what each method returns and when the iteration stops.
* Mention that all accept a callback with `(element, index, array)` parameters.
* Highlight typical use cases for each method.

---

## 55. How do you sort an array of objects?

Sorting an array of objects in JavaScript is commonly done using the `.sort()` method, where you provide a **compare function** that tells how to order the objects based on one or more properties.

---

## Basics of `.sort()`

* The `.sort()` method sorts **in place** (modifies the original array).
* It accepts an optional **compare function** `(a, b) => number`.
* The compare function should return:

    * A **negative number** if `a` should come before `b`.
    * Zero if `a` and `b` are equal (order unchanged).
    * A **positive number** if `a` should come after `b`.

---

## Example: Sort by a numeric property

Suppose you have an array of objects representing people with an `age` property:

```js
const people = [
  { name: "Alice", age: 25 },
  { name: "Bob", age: 20 },
  { name: "Charlie", age: 30 }
];

// Sort by age ascending
people.sort((a, b) => a.age - b.age);

console.log(people);
```

**Output:**

```js
[
  { name: "Bob", age: 20 },
  { name: "Alice", age: 25 },
  { name: "Charlie", age: 30 }
]
```

---

## Example: Sort by string property (alphabetically)

Sort by `name` (case insensitive):

```js
people.sort((a, b) => {
  const nameA = a.name.toLowerCase();
  const nameB = b.name.toLowerCase();

  if (nameA < nameB) return -1;
  if (nameA > nameB) return 1;
  return 0;
});

console.log(people);
```

---

## Example: Sort descending by age

```js
people.sort((a, b) => b.age - a.age);
```

---

## Sorting by multiple properties

For example, sort by `age` ascending, and if ages are equal, sort by `name` ascending:

```js
people.sort((a, b) => {
  if (a.age === b.age) {
    return a.name.localeCompare(b.name);
  }
  return a.age - b.age;
});
```

---

## Summary

| Step                   | Description                                       |
| ---------------------- | ------------------------------------------------- |
| Use `.sort(compareFn)` | Pass a compare function to define order           |
| Numeric properties     | Use subtraction `a.prop - b.prop`                 |
| String properties      | Use `localeCompare()` or conditional comparisons  |
| Multiple criteria      | Use if/else or chained comparisons inside compare |

---

## Interview tip

* Explain that `.sort()` mutates the original array.
* Show examples with numbers and strings.
* Mention how to handle case-insensitive string sorting.
* Demonstrate sorting by multiple fields.

---

## 56. What is the difference between `Array.from()` and `Array.of()`?

Both `Array.from()` and `Array.of()` are methods introduced in ES6 to create arrays, but they serve **different purposes** and behave differently.

---

## 1. `Array.from()`

* Creates a new array **from an iterable or array-like object** (e.g., strings, Sets, Maps, arguments, NodeLists).
* Can also take a **mapping function** as the second argument to transform elements.
* Commonly used to convert non-array objects into arrays.

### Examples:

```js
// From a string (iterable)
console.log(Array.from('hello')); 
// Output: ['h', 'e', 'l', 'l', 'o']

// From a Set (iterable)
const set = new Set([1, 2, 3]);
console.log(Array.from(set)); 
// Output: [1, 2, 3]

// From an arguments object (array-like)
function fn() {
  console.log(Array.from(arguments));
}
fn(1, 2, 3); 
// Output: [1, 2, 3]

// With a mapping function
console.log(Array.from([1, 2, 3], x => x * 2)); 
// Output: [2, 4, 6]
```

---

## 2. `Array.of()`

* Creates a new array **from the arguments passed to it**, **regardless of the number or type**.
* Useful because the `Array` constructor behaves differently with numeric arguments.

### Examples:

```js
// Array.of creates array with all args as elements
console.log(Array.of(1, 2, 3)); 
// Output: [1, 2, 3]

// Compare with Array constructor
console.log(Array(3));    // [ <3 empty items> ] (array of length 3)
console.log(Array.of(3)); // [3] (array with one element 3)
```

---

## Key difference:

| Feature                     | `Array.from()`                       | `Array.of()`                 |
| --------------------------- | ------------------------------------ | ---------------------------- |
| Input                       | Iterable or array-like object        | Any number of arguments      |
| Purpose                     | Convert iterable/array-like to array | Create array from arguments  |
| Behavior with single number | Converts single iterable element     | Creates single-element array |
| Supports mapping function   | Yes (second argument)                | No                           |

---

## Interview tip

* Explain that `Array.from()` is for converting iterables or array-likes to arrays.
* Emphasize that `Array.of()` creates arrays from arguments, useful to avoid surprises with `Array()` constructor.
* Show example comparing `Array.of(3)` and `Array(3)`.

---

## 57. What is the difference between slice and splice?

Both `slice()` and `splice()` are array methods in JavaScript that deal with extracting or modifying parts of an array, but **they behave very differently**.

---

## `slice()`

* Returns a **shallow copy** of a portion of the array **without modifying** the original array.
* Syntax: `arr.slice(startIndex, endIndex)`

    * `startIndex` is inclusive.
    * `endIndex` is exclusive (not included).
* If `endIndex` is omitted, slice extracts till the end.
* Works like a **non-destructive substring** operation for arrays.

### Example:

```js
const arr = [1, 2, 3, 4, 5];
const newArr = arr.slice(1, 4);

console.log(newArr); // [2, 3, 4]
console.log(arr);    // [1, 2, 3, 4, 5]  (original array unchanged)
```

---

## `splice()`

* **Modifies the original array** by adding/removing elements.
* Syntax: `arr.splice(startIndex, deleteCount, item1, item2, ...)`

    * `startIndex`: where to start modifying.
    * `deleteCount`: number of elements to remove.
    * Optional additional items: elements to insert at `startIndex`.
* Returns an array of the deleted elements.

### Examples:

**Remove elements:**

```js
const arr = [1, 2, 3, 4, 5];
const removed = arr.splice(1, 2);

console.log(removed); // [2, 3]
console.log(arr);     // [1, 4, 5]  (original array changed)
```

**Insert elements:**

```js
const arr = [1, 4, 5];
arr.splice(1, 0, 2, 3);

console.log(arr); // [1, 2, 3, 4, 5]
```

---

## Summary table:

| Feature         | `slice()`                        | `splice()`                           |
| --------------- | -------------------------------- | ------------------------------------ |
| Modifies array? | No (non-destructive)             | Yes (destructive)                    |
| Returns         | New sliced array                 | Array of removed elements            |
| Parameters      | `start`, `end` (end exclusive)   | `start`, `deleteCount`, items to add |
| Use case        | Extract a portion without change | Add/remove elements in place         |

---

## Interview tip

* Clearly state that `slice` does **not** modify original array while `splice` **does**.
* Show examples of both removing and adding with `splice`.
* Mention that `slice` is good for copying parts, `splice` for editing arrays.

---

## 58. What are template literals?

Template literals are a powerful and flexible way to work with strings in JavaScript, introduced in **ES6**.

---

## What are Template Literals?

* Template literals are **string literals** that allow **embedded expressions**, **multi-line strings**, and **string interpolation**.
* They are enclosed by backticks (`` ` ``), not single `'` or double `"` quotes.

---

## Features & Benefits:

### 1. **String Interpolation**

Embed variables or expressions inside strings using `${...}`:

```js
const name = "Alice";
const age = 25;

const message = `My name is ${name} and I am ${age} years old.`;
console.log(message);
// Output: My name is Alice and I am 25 years old.
```

---

### 2. **Multi-line Strings**

Create strings spanning multiple lines without `\n` or concatenation:

```js
const multiLine = `This is line 1
This is line 2
This is line 3`;

console.log(multiLine);
```

---

### 3. **Expression Evaluation**

You can put any JavaScript expression inside `${}`:

```js
const a = 5;
const b = 10;

console.log(`The sum of ${a} and ${b} is ${a + b}.`);
// Output: The sum of 5 and 10 is 15.
```

---

### 4. **Tagged Template Literals** (Advanced)

Functions can process template literals for custom parsing (rare in interviews, but good to know).

```js
function tag(strings, ...values) {
  console.log(strings);
  console.log(values);
  return "Tagged!";
}

const result = tag`Hello ${name}, you are ${age} years old.`;
console.log(result);
```

---

## Summary:

| Feature               | Description                             |
| --------------------- | --------------------------------------- |
| Delimiters            | Backticks `` `...` ``                   |
| Interpolation         | `${expression}` inside template         |
| Multi-line support    | Yes, without extra characters           |
| Expression evaluation | Supports any JS expression inside `${}` |
| Tagged templates      | Functions to customize processing       |

---

## Interview tip

* Mention how template literals improve readability.
* Show examples of interpolation and multi-line strings.
* Optionally mention tagged templates to impress!

---

## 59. How do you deep clone an array?

Deep cloning an array means creating a **new array** with **all nested objects or arrays also copied**, so changes in the clone **don’t affect** the original.

---

## Why deep clone?

* Simple assignment or shallow copy copies references for objects/arrays inside.
* So nested objects/arrays remain linked to the original.
* Deep clone solves this by fully copying nested structures.

---

## 1. Simple shallow copy methods (not deep):

```js
const arr = [1, 2, 3];
const shallow = arr.slice();  // or [...arr], Array.from(arr)
```

**Problem:**
If the array contains nested objects or arrays, inner elements are still references.

---

## 2. Deep cloning techniques

### a) Using `JSON.parse(JSON.stringify())` (common quick method)

```js
const original = [1, {a: 2}, [3, 4]];

const deepClone = JSON.parse(JSON.stringify(original));

deepClone[1].a = 99;
deepClone[2][0] = 100;

console.log(original);
// Output: [1, {a: 2}, [3, 4]]  (unchanged)

console.log(deepClone);
// Output: [1, {a: 99}, [100, 4]]
```

**Pros:**

* Simple and works for many cases.

**Cons:**

* Fails if array contains functions, `undefined`, `Date`, `RegExp`, or circular references.
* Loses prototype and special object types.

---

### b) Using a custom recursive function

For full control, write a recursive deep clone function:

```js
function deepCloneArray(arr) {
  return arr.map(item => {
    if (Array.isArray(item)) {
      return deepCloneArray(item);
    } else if (item && typeof item === 'object') {
      return deepCloneObject(item);
    }
    return item;
  });
}

function deepCloneObject(obj) {
  const clone = {};
  for (const key in obj) {
    if (Array.isArray(obj[key])) {
      clone[key] = deepCloneArray(obj[key]);
    } else if (obj[key] && typeof obj[key] === 'object') {
      clone[key] = deepCloneObject(obj[key]);
    } else {
      clone[key] = obj[key];
    }
  }
  return clone;
}

const original = [1, {a: 2, b: [3, 4]}, [5, 6]];

const cloned = deepCloneArray(original);
cloned[1].b[0] = 99;

console.log(original[1].b[0]); // 3  (unchanged)
console.log(cloned[1].b[0]);   // 99
```

---

### c) Using structured cloning (modern approach)

```js
const original = [1, {a: 2}, [3, 4]];
const cloned = structuredClone(original);
```

* `structuredClone()` is a new built-in browser and Node.js API for deep cloning.
* Supports many types including Date, RegExp, Map, Set, etc.
* Throws on circular references.
* Check compatibility before use.

---

## Summary:

| Method                         | Pros                                   | Cons                                    |
| ------------------------------ | -------------------------------------- | --------------------------------------- |
| `JSON.parse(JSON.stringify())` | Simple, widely supported               | Loses functions, special types          |
| Custom recursive function      | Full control, supports complex types   | More code, potential bugs               |
| `structuredClone()`            | Native deep clone, supports many types | Not fully supported in all environments |

---

## Interview tip

* Start with JSON method for simple cases.
* Mention its limitations.
* Show awareness of recursive or modern solutions.

---

## 60. What is the use of `includes()` in arrays and strings?

The `.includes()` method is available both on **arrays** and **strings** in JavaScript, and it’s used to **check if a certain element or substring exists** within them.

---

## 1. `Array.prototype.includes()`

* **Purpose:** Checks if an **array** contains a specific element.
* Returns `true` if found, otherwise `false`.
* Uses **strict equality** (`===`) for comparison.
* Optional second parameter lets you specify the **starting index** for the search.

### Syntax:

```js
arr.includes(valueToFind, fromIndex);
```

* `valueToFind`: The element to search for.
* `fromIndex` (optional): Index to start searching from (default is 0).

### Example:

```js
const fruits = ['apple', 'banana', 'mango'];

console.log(fruits.includes('banana')); // true
console.log(fruits.includes('grape'));  // false
console.log(fruits.includes('banana', 2)); // false (starts searching at index 2)
```

---

## 2. `String.prototype.includes()`

* **Purpose:** Checks if a **string** contains a specific substring.
* Returns `true` if found, otherwise `false`.
* Optional second parameter specifies the **position** to start the search.

### Syntax:

```js
str.includes(searchString, position);
```

* `searchString`: The substring to search for.
* `position` (optional): The position to start searching (default is 0).

### Example:

```js
const sentence = "Hello world!";

console.log(sentence.includes('world'));     // true
console.log(sentence.includes('World'));     // false (case sensitive)
console.log(sentence.includes('Hello', 1));  // false (starts at index 1)
```

---

## Key points:

| Feature         | Array `.includes()`   | String `.includes()` |
| --------------- | --------------------- | -------------------- |
| Checks for      | Element in array      | Substring in string  |
| Case sensitive? | Yes (strict equality) | Yes                  |
| Returns         | Boolean               | Boolean              |
| Optional param  | `fromIndex`           | `position`           |

---

## Interview tip

* Mention `.includes()` is a **simple, readable alternative** to using `indexOf(...) !== -1`.
* Note that it’s **case sensitive**.
* Highlight that for arrays, it checks elements; for strings, it checks substrings.

---

Want me to show how to polyfill `.includes()` for older browsers or alternatives?

---

### 🔹 **61–70: Asynchronous JavaScript**

## 61. What is the event loop in JavaScript?

Awesome topic! The **JavaScript Event Loop** is fundamental to understanding how JS handles asynchronous operations despite being single-threaded.

---

## What is the Event Loop?

* JavaScript runs on a **single thread**, meaning it can execute only one task at a time.
* The **Event Loop** is a mechanism that allows JavaScript to perform **non-blocking asynchronous operations** (like timers, network requests) by managing a queue of tasks.
* It constantly checks if the **call stack** is empty and picks tasks from the **task queue** to execute.

---

## Key concepts:

### 1. **Call Stack**

* Where the JavaScript engine keeps track of function calls.
* Runs functions synchronously, one at a time.
* When a function is called, it’s pushed on the stack.
* When a function returns, it’s popped off.

---

### 2. **Web APIs / Browser APIs**

* Things like `setTimeout`, DOM events, AJAX requests run outside the main JS thread in the browser environment.
* When these async operations complete, their callbacks are sent to the **task queue**.

---

### 3. **Task Queue (Message Queue)**

* Holds callbacks ready to be executed.
* The event loop checks this queue **only when the call stack is empty**.

---

### 4. **Event Loop**

* Continuously monitors the call stack and task queue.
* If the call stack is empty, it takes the first callback from the task queue and pushes it to the call stack to run.

---

## Visual flow:

1. JS executes code on the call stack.
2. Async operations are sent to Web APIs.
3. When async operations finish, their callbacks are queued in the task queue.
4. Event Loop picks callbacks from the task queue and pushes them onto the call stack once it’s free.

---

## Example:

```js
console.log('Start');

setTimeout(() => {
  console.log('Timeout callback');
}, 0);

console.log('End');
```

**Output:**

```
Start
End
Timeout callback
```

* Even with 0ms delay, the `setTimeout` callback is executed **after** the synchronous code because it goes to the task queue and waits for the call stack to clear.

---

## Why is this important?

* Explains how JS handles async operations **without multithreading**.
* Helps understand behavior of `setTimeout`, Promises, DOM events, etc.
* Crucial for writing non-blocking, performant code.

---

## Bonus: Microtasks vs Macrotasks

* **Microtasks** (e.g., Promises `.then()`) have higher priority than macrotasks (e.g., `setTimeout`).
* Microtasks are processed **immediately after the current task**, before the event loop picks next macrotask.

Example with Promise:

```js
console.log('Start');

setTimeout(() => console.log('Timeout'), 0);

Promise.resolve().then(() => console.log('Promise'));

console.log('End');
```

**Output:**

```
Start
End
Promise
Timeout
```

---

## Summary

| Part       | Role                                                |
| ---------- | --------------------------------------------------- |
| Call Stack | Runs functions synchronously                        |
| Web APIs   | Handles async tasks outside JS engine               |
| Task Queue | Queues callbacks after async completion             |
| Event Loop | Moves tasks from queue to stack when stack is empty |

---

## Interview tip

* Explain single-threaded nature of JS.
* Describe call stack, task queue, and event loop.
* Give examples with `setTimeout` and Promises.
* Mention microtasks vs macrotasks if comfortable.

---

## 62. Explain the call stack, callback queue, and microtask queue.

These three components—**Call Stack**, **Callback Queue**, and **Microtask Queue**—are key players in how JavaScript handles **asynchronous behavior** in its **single-threaded** environment.

---

## 🔁 Quick Overview

| Component                            | Role                                                              |
| ------------------------------------ | ----------------------------------------------------------------- |
| **Call Stack**                       | Executes synchronous (immediate) code                             |
| **Callback Queue** (Macrotask Queue) | Queues tasks like `setTimeout`, `setInterval`, UI events          |
| **Microtask Queue**                  | Queues Promises `.then()`, `queueMicrotask()`, `MutationObserver` |

The **Event Loop** continuously checks these queues to manage execution order.

---

## 1. 📚 Call Stack

* The **Call Stack** is where JS keeps track of function execution.
* It's **LIFO** (Last-In-First-Out): The last function called is the first to finish.
* Every time a function is called, it's **pushed** onto the stack.
* When it finishes, it's **popped** off the stack.

### Example:

```js
function greet() {
  console.log("Hello");
}
greet();
```

Stack flow:

```
1. Global()
2. greet() pushed
3. console.log() pushed
4. console.log() popped
5. greet() popped
6. Global() ends
```

---

## 2. ⏳ Callback Queue (Macrotask Queue)

* Holds **callbacks** from asynchronous operations:

    * `setTimeout`
    * `setInterval`
    * DOM events
    * `fetch` (after Promise resolution)
* **Event Loop** will execute these **after** the call stack is empty and all microtasks have run.

---

## 3. 🧵 Microtask Queue

* Queues high-priority async tasks:

    * Promises (`.then`, `.catch`, `.finally`)
    * `queueMicrotask()`
    * `MutationObserver`
* Always executed **before** the callback queue (macrotasks), **immediately** after the call stack is empty.

---

## 🔄 How They Work Together (With Event Loop)

```js
console.log("Start");

setTimeout(() => {
  console.log("Timeout callback");
}, 0);

Promise.resolve().then(() => {
  console.log("Promise resolved");
});

console.log("End");
```

### Execution Flow:

1. `console.log("Start")` → **Call Stack**
2. `setTimeout(...)` → Scheduled → **Callback Queue**
3. `Promise.then(...)` → Scheduled → **Microtask Queue**
4. `console.log("End")` → **Call Stack**
5. Call stack is now empty.
6. **Microtask Queue** runs → logs "Promise resolved"
7. Then **Callback Queue** runs → logs "Timeout callback"

### Output:

```
Start
End
Promise resolved
Timeout callback
```

---

## 🎯 Summary Table

| Component           | Example Tasks                           | Priority | Executes When                       |
| ------------------- | --------------------------------------- | -------- | ----------------------------------- |
| **Call Stack**      | Regular function calls, `console.log()` | Highest  | Immediately                         |
| **Microtask Queue** | `Promise.then()`, `queueMicrotask()`    | Higher   | After call stack is empty           |
| **Callback Queue**  | `setTimeout()`, DOM events              | Lower    | After call stack **and** microtasks |

---

## 🧠 Interview Tip

* Draw the event loop cycle or give a step-by-step example.
* Emphasize **microtasks run before macrotasks**.
* Know that this affects order of logs and potential **race conditions**.

---

## 63. What is a Promise?

A **Promise** in JavaScript is an object that represents the **eventual completion (or failure)** of an **asynchronous operation** and its resulting **value**.

It allows you to write asynchronous code in a **clean, readable, and manageable** way.

---

## 🔑 Key Concepts

### ✅ A Promise has three states:

1. **Pending** – The initial state; the operation hasn't completed yet.
2. **Fulfilled** – The operation completed successfully.
3. **Rejected** – The operation failed with an error.

---

## 🧪 Promise Syntax

```js
const promise = new Promise((resolve, reject) => {
  // async task
  if (success) {
    resolve("Data loaded");
  } else {
    reject("Error occurred");
  }
});
```

### Using `.then()` and `.catch()`

```js
promise
  .then(result => {
    console.log("Success:", result);
  })
  .catch(error => {
    console.log("Error:", error);
  });
```

---

## 🛠 Example: Simulating async operation

```js
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const data = "📦 Data received!";
      resolve(data); // or reject("❌ Error");
    }, 1000);
  });
}

fetchData()
  .then(res => console.log(res))      // 📦 Data received!
  .catch(err => console.log(err));
```

---

## 🧵 Why Use Promises?

Before Promises, we used **callbacks**, which led to **callback hell** (deep nesting, unreadable code).

Promises:

* Flatten async flow.
* Enable **chaining** of multiple operations.
* Handle errors gracefully via `.catch()`.

---

## 🔗 Promise Chaining

```js
fetchData()
  .then(res => {
    console.log("Step 1:", res);
    return res + " Step 2 done.";
  })
  .then(updated => {
    console.log("Step 2:", updated);
  })
  .catch(err => console.log("Error:", err));
```

---

## 🔄 Combined with `async/await` (ES2017+)

```js
async function loadData() {
  try {
    const result = await fetchData();
    console.log(result);
  } catch (err) {
    console.log("Error:", err);
  }
}
```

---

## 👨‍🏫 Summary

| Feature      | Description                         |
| ------------ | ----------------------------------- |
| Purpose      | Handle async operations cleanly     |
| States       | Pending, Fulfilled, Rejected        |
| Core Methods | `.then()`, `.catch()`, `.finally()` |
| Alternatives | Callbacks, `async/await`            |

---

## 🧠 Interview Tip

* Explain real-world analogy (like ordering food: you wait for it to be prepared — it either succeeds or fails).
* Know how to chain Promises and catch errors.
* Bonus: mention `Promise.all`, `Promise.race`, etc.

---

## 64. What are the states of a Promise?

A **JavaScript Promise** represents an asynchronous operation that can be in one of **three distinct states**:

---

## 🔁 The Three States of a Promise

| State         | Description                                                             |
| ------------- | ----------------------------------------------------------------------- |
| **Pending**   | Initial state, neither fulfilled nor rejected.                          |
| **Fulfilled** | The asynchronous operation completed successfully and returned a value. |
| **Rejected**  | The asynchronous operation failed and returned a reason (error).        |

---

## 1. 🟡 **Pending**

* This is the **default state** when the Promise is created.
* The operation is still ongoing.
* The Promise has **not yet been resolved or rejected**.

```js
const p = new Promise((resolve, reject) => {
  // still pending
});
```

---

## 2. ✅ **Fulfilled (Resolved)**

* The Promise was successfully completed.
* The `resolve()` function was called with a result.
* Moves from **pending → fulfilled**.

```js
const p = new Promise((resolve, reject) => {
  resolve("Success!");
});

p.then(result => console.log(result)); // "Success!"
```

---

## 3. ❌ **Rejected**

* The Promise failed.
* The `reject()` function was called with an error or failure reason.
* Moves from **pending → rejected**.

```js
const p = new Promise((resolve, reject) => {
  reject("Something went wrong");
});

p.catch(error => console.log(error)); // "Something went wrong"
```

---

## 🔒 Once Settled

A Promise is **immutable** once it is either **fulfilled or rejected**—it cannot change state again.

```js
const p = new Promise((resolve, reject) => {
  resolve("First");
  reject("Second"); // This will be ignored!
});

p.then(console.log); // "First"
```

---

## 🎯 Summary Table

| State     | What Triggers It          | Can Transition To     |
| --------- | ------------------------- | --------------------- |
| Pending   | When a Promise is created | Fulfilled or Rejected |
| Fulfilled | `resolve(value)` called   | Final state           |
| Rejected  | `reject(error)` called    | Final state           |

---

## 🧠 Interview Tip

* Explain all three states clearly.
* Mention that **state transitions are one-way** (can't go back to pending).
* Show how `.then()` is for fulfilled, `.catch()` is for rejected, and `.finally()` runs regardless.

---

## 65. How is `async/await` different from `.then()`?

Both `async/await` and `.then()` are used to handle **Promises** in JavaScript, but they differ in **syntax**, **readability**, and **error handling**.

---

## 🔧 1. `.then()` — Promise Chaining

### ✅ Syntax:

```js
fetchData()
  .then(response => process(response))
  .then(result => display(result))
  .catch(error => console.error(error));
```

### ✅ Features:

* Uses **callbacks** inside `.then()`.
* Can become **nested** or hard to read with complex logic.
* Works in **ES6** and up.

---

## 🔧 2. `async/await` — Syntactic Sugar for Promises

### ✅ Syntax:

```js
async function run() {
  try {
    const response = await fetchData();
    const result = await process(response);
    display(result);
  } catch (error) {
    console.error(error);
  }
}
```

### ✅ Features:

* Introduced in **ES2017 (ES8)**.
* Makes async code look **synchronous**.
* **Easier to read**, especially when chaining multiple async operations.
* Use inside functions declared with `async`.

---

## 📊 Comparison Table

| Feature        | `.then()`                     | `async/await`                               |
| -------------- | ----------------------------- | ------------------------------------------- |
| Syntax Style   | Chained callbacks             | Synchronous-like with `await`               |
| Readability    | Gets messy with nested chains | Cleaner, especially with multiple awaits    |
| Error Handling | `.catch()`                    | `try...catch` block                         |
| Debugging      | Harder stack traces           | Easier to trace line-by-line                |
| Return Value   | Returns a Promise             | Returns a Promise (even if returning value) |
| Compatibility  | ES6 and up                    | ES2017 and up                               |

---

## 🎯 Example Side-by-Side

### With `.then()`

```js
getUser()
  .then(user => getPosts(user.id))
  .then(posts => console.log(posts))
  .catch(err => console.error(err));
```

### With `async/await`

```js
async function showPosts() {
  try {
    const user = await getUser();
    const posts = await getPosts(user.id);
    console.log(posts);
  } catch (err) {
    console.error(err);
  }
}
```

---

## 🧠 Interview Tip

* Say that `async/await` is just syntactic sugar for Promises.
* Mention `await` pauses execution until the Promise resolves.
* Emphasize that both return Promises under the hood.

---

## 66. What is the difference between `Promise.all()`, `Promise.any()`, `Promise.race()`?

Understanding the differences between `Promise.all()`, `Promise.any()`, and `Promise.race()` is key for effective handling of **multiple asynchronous operations** in JavaScript.

---

## 📦 Overview of Each Method

| Method           | Resolves When...                               | Rejects When...                         |
| ---------------- | ---------------------------------------------- | --------------------------------------- |
| `Promise.all()`  | **All** promises are fulfilled                 | **Any one** promise is rejected         |
| `Promise.any()`  | **First fulfilled** promise resolves           | **All** promises are rejected           |
| `Promise.race()` | **First settled** (fulfilled or rejected) wins | First rejected wins if it settles first |

---

## 🔹 1. `Promise.all()` – Wait for **All**

* Takes an array of promises.
* Resolves with an array of values.
* **Fails fast**: if any promise rejects, the whole thing rejects.

### ✅ Example:

```js
Promise.all([
  Promise.resolve("A"),
  Promise.resolve("B"),
  Promise.resolve("C")
]).then(results => {
  console.log(results); // ["A", "B", "C"]
}).catch(err => {
  console.error(err);
});
```

### ❌ If one fails:

```js
Promise.all([
  Promise.resolve("A"),
  Promise.reject("Error"),
  Promise.resolve("C")
]).catch(err => console.error(err)); // "Error"
```

---

## 🔹 2. `Promise.any()` – First **Success**

* Resolves as soon as **any one** Promise **fulfills**.
* Ignores rejected promises unless **all** reject.
* If all reject, throws `AggregateError`.

### ✅ Example:

```js
Promise.any([
  Promise.reject("Fail 1"),
  Promise.resolve("Success 1"),
  Promise.resolve("Success 2")
]).then(result => {
  console.log(result); // "Success 1"
});
```

### ❌ All fail:

```js
Promise.any([
  Promise.reject("Fail 1"),
  Promise.reject("Fail 2")
]).catch(err => {
  console.error(err); // AggregateError: All promises were rejected
});
```

---

## 🔹 3. `Promise.race()` – First Settled (Win or Fail)

* Resolves or rejects as soon as the **first promise settles** (fulfilled or rejected).
* Useful for **timeouts** and performance races.

### ✅ Example:

```js
Promise.race([
  new Promise(resolve => setTimeout(() => resolve("Fast"), 100)),
  new Promise(resolve => setTimeout(() => resolve("Slow"), 500))
]).then(result => console.log(result)); // "Fast"
```

### ❌ First to reject:

```js
Promise.race([
  Promise.reject("Fail First"),
  Promise.resolve("Success Later")
]).catch(err => console.error(err)); // "Fail First"
```

---

## 🧠 Summary Table

| Method           | Resolves With           | Rejects If                   | Use Case                              |
| ---------------- | ----------------------- | ---------------------------- | ------------------------------------- |
| `Promise.all()`  | Array of all results    | Any one rejects              | Run all in parallel; need all results |
| `Promise.any()`  | First successful result | All reject (AggregateError)  | Need **any one** to succeed           |
| `Promise.race()` | First settled (any)     | First reject wins (if first) | Timeout or first response wins        |

---

## ⚠️ Notes

* All three return **a new Promise**.
* If you want **all results** (even if some fail), use `Promise.allSettled()`.

---

## 67. What is a callback hell and how do you avoid it?

**Callback Hell** is a situation in JavaScript where callbacks are nested within other callbacks several levels deep, making the code:

* Hard to read 😵
* Hard to debug 🐞
* Hard to maintain 🧩

---

## 🔥 What is Callback Hell?

It happens when asynchronous functions are **nested** in a way that each depends on the result of the previous one, leading to **"pyramid-shaped" code**.

### 🔻 Example of Callback Hell:

```js
getUser(function(user) {
  getPosts(user.id, function(posts) {
    getComments(posts[0].id, function(comments) {
      saveToDB(comments, function(result) {
        console.log("Done!");
      });
    });
  });
});
```

This quickly becomes unreadable and error-prone as more nested logic is added.

---

## ✅ How to Avoid Callback Hell

### 1. 🔄 **Use Named Functions**

Break the logic into named functions instead of nesting anonymous ones.

```js
function handleUser(user) {
  getPosts(user.id, handlePosts);
}

function handlePosts(posts) {
  getComments(posts[0].id, handleComments);
}

function handleComments(comments) {
  saveToDB(comments, () => console.log("Done!"));
}

getUser(handleUser);
```

---

### 2. 📦 **Use Promises**

Promises allow chaining and help **flatten** the code.

```js
getUser()
  .then(user => getPosts(user.id))
  .then(posts => getComments(posts[0].id))
  .then(comments => saveToDB(comments))
  .then(() => console.log("Done!"))
  .catch(err => console.error(err));
```

---

### 3. 🧘 **Use `async/await`**

Async/await makes asynchronous code look **synchronous** and readable.

```js
async function run() {
  try {
    const user = await getUser();
    const posts = await getPosts(user.id);
    const comments = await getComments(posts[0].id);
    await saveToDB(comments);
    console.log("Done!");
  } catch (err) {
    console.error(err);
  }
}

run();
```

---

### 4. 🧰 Use Control Flow Libraries (Legacy)

Libraries like `async.js` used to help avoid callback hell using patterns like `async.series`, `async.parallel`, etc. However, Promises and async/await are now standard and preferred.

---

## 📌 Summary

| Method          | Benefit                             |
| --------------- | ----------------------------------- |
| Named functions | Improves structure, reduces nesting |
| Promises        | Chaining avoids deep nesting        |
| Async/Await     | Most readable and modern            |

---

## 🧠 Interview Tip

* Define what callback hell is clearly.
* Mention real problems: unreadable, hard to debug, deeply nested.
* Emphasize **Promises** and **async/await** as solutions.
* Bonus: compare syntax side-by-side if asked.

---

## 68. What is the fetch API? How does it work?

The **Fetch API** is a modern JavaScript interface for making HTTP requests (like `GET`, `POST`, `PUT`, etc.) to servers, similar to `XMLHttpRequest` but with a cleaner, Promise-based syntax.

---

## 🔍 What is the Fetch API?

* Built into the browser (no library needed).
* Returns a **Promise**.
* Can be used for **asynchronous** requests (like fetching data from a REST API).
* Supports modern features like **async/await**.

---

## 🧪 Basic Syntax

```js
fetch(url, options)
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

---

## 🧰 Example: GET Request

```js
fetch('https://jsonplaceholder.typicode.com/posts/1')
  .then(res => {
    if (!res.ok) throw new Error('Network error');
    return res.json(); // parses JSON
  })
  .then(data => console.log(data))
  .catch(err => console.error(err));
```

### Output:

```json
{
  "userId": 1,
  "id": 1,
  "title": "Post title",
  "body": "Post body..."
}
```

---

## 📝 Example: POST Request

```js
fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    title: 'New Post',
    body: 'This is the content',
    userId: 1
  })
})
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => console.error(err));
```

---

## 🔁 How Fetch Works Internally

1. Makes a **network request** using `fetch(url, options)`.
2. Returns a **Promise** that resolves to a `Response` object.
3. You must call `.json()`, `.text()`, or `.blob()` to read the body.
4. Errors like **network failures** reject the Promise, but **HTTP errors (e.g. 404, 500)** don’t — you must check `response.ok`.

---

## 🎯 Common Response Methods

| Method            | Description                      |
| ----------------- | -------------------------------- |
| `response.ok`     | `true` if status code is 200–299 |
| `response.status` | HTTP status code (e.g. 404, 200) |
| `response.json()` | Parses response as JSON          |
| `response.text()` | Parses response as plain text    |

---

## 🧠 Interview Tip

* Emphasize that `fetch()` returns a **Promise**, unlike `XMLHttpRequest`.
* Mention it doesn’t throw for HTTP errors — you need to check `response.ok`.
* Highlight the use of `await` with fetch for modern code:

```js
const res = await fetch(url);
if (!res.ok) throw new Error('Failed');
const data = await res.json();
```

---

## 69. How does error handling work with `try-catch` and async/await?

In JavaScript, when you're using `async/await` to work with Promises, you handle errors using a `try...catch` block — just like you would for synchronous code. This approach makes error handling much **cleaner** and more **readable** compared to `.then().catch()` chains.

---

## ✅ How `try...catch` Works with `async/await`

### Basic Syntax:

```js
async function fetchData() {
  try {
    const response = await fetch('https://api.example.com/data');
    if (!response.ok) {
      throw new Error(`HTTP Error: ${response.status}`);
    }
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error('Caught an error:', error.message);
  }
}
```

* `try`: Contains the code that might throw an error.
* `catch`: Catches any error that happens in the `try` block.
* Works with both **sync** and **async** errors (including rejected Promises).

---

## ⚠️ Common Sources of Errors

| Source                  | Needs Handling? | Example                                       |
| ----------------------- | --------------- | --------------------------------------------- |
| `fetch()` network error | ✅               | Network offline, server down                  |
| `response.ok === false` | ✅               | 404, 500, etc. (Fetch doesn't throw for this) |
| JSON parsing error      | ✅               | Malformed JSON in `response.json()`           |
| Logic/JS errors         | ✅               | Type errors, null references, etc.            |

---

## 🧪 Example With Nested Calls

```js
async function getUserData(userId) {
  try {
    const userRes = await fetch(`/api/users/${userId}`);
    if (!userRes.ok) throw new Error('User not found');
    const user = await userRes.json();

    const postsRes = await fetch(`/api/users/${userId}/posts`);
    if (!postsRes.ok) throw new Error('Posts not found');
    const posts = await postsRes.json();

    console.log({ user, posts });
  } catch (err) {
    console.error('Something went wrong:', err.message);
  }
}
```

---

## ✨ Advantages Over `.catch()`

| Feature                | `.then().catch()`          | `async/await + try...catch`        |
| ---------------------- | -------------------------- | ---------------------------------- |
| Readability            | Less readable with nesting | Cleaner and more like sync code    |
| Error handling         | Only at end unless nested  | Fine-grained control with blocks   |
| Debugging stack traces | Can be messy               | Easier with line-by-line debugging |

---

## 🧠 Interview Tip

* Explain that `await` can **throw** just like `throw new Error()`.
* Emphasize that `try...catch` **must** be used inside `async` functions.
* You can also use `.catch()` on an `await`ed Promise if needed, but `try...catch` is cleaner.

---

## 70. What is the difference between synchronous and asynchronous code?

Understanding the difference between **synchronous** and **asynchronous** code is fundamental in JavaScript — especially because JavaScript is **single-threaded**, meaning it executes one command at a time.

---

## 🔁 Synchronous Code

Synchronous code is **executed line-by-line**, **blocking** the program until each operation is complete.

### Example:

```js
console.log("Start");

const result = 1 + 1;
console.log("Result:", result);

console.log("End");
```

### Output:

```
Start
Result: 2
End
```

⛔ **Blocking behavior**: If a task takes time (like file reading, API calls), it **blocks everything else** until it's done.

---

## 🔄 Asynchronous Code

Asynchronous code allows **non-blocking execution**. Long-running tasks (like network requests, timers) are delegated to the **browser** or **Node.js APIs**, and the rest of the code continues running.

### Example using `setTimeout`:

```js
console.log("Start");

setTimeout(() => {
  console.log("Async Task Done");
}, 2000);

console.log("End");
```

### Output:

```
Start
End
Async Task Done
```

💡 The async task runs **in the background**, and its callback is executed **later**, after other code finishes.

---

## ✅ Key Differences

| Feature            | Synchronous                  | Asynchronous                                               |
| ------------------ | ---------------------------- | ---------------------------------------------------------- |
| Execution Order    | Line-by-line (blocking)      | Non-blocking, can be delayed                               |
| Performance Impact | Can freeze UI or block logic | Smooth execution for long tasks                            |
| Examples           | Loops, math operations       | setTimeout, fetch, event listeners                         |
| Error Handling     | `try...catch`                | `try...catch` with `async/await` or `.catch()` on Promises |

---

## 🧰 Common Async Patterns in JS

* `setTimeout()` / `setInterval()`
* `fetch()` for HTTP requests
* Event Listeners
* Promises and `async/await`

---

## 📌 Interview Tip

* Say: "In JS, synchronous code runs top-to-bottom and blocks the thread, while asynchronous code uses the event loop to defer tasks."
* Mention that **asynchronous behavior is crucial for I/O operations** and improving user experience in web apps.

---

Would you like a visual diagram of the event loop to complement this explanation?

---

### 🔹 **71–80: DOM & Events**

## 71. What is the DOM?

### 🌳 What is the DOM?

The **DOM (Document Object Model)** is a **programming interface** that represents an **HTML** or **XML** document as a **tree structure** of objects that can be accessed and manipulated with JavaScript.

---

## 🧠 Think of it as:

> A **bridge** between your HTML content and JavaScript code — it lets you **read**, **change**, **add**, or **remove** elements dynamically in the browser.

---

## 🧱 Structure of the DOM

When a web page is loaded, the browser parses the HTML and creates a **DOM tree** where:

* Each **HTML tag** becomes a **Node** (e.g., `<div>`, `<p>`, `<ul>`)
* Each **text inside tags** becomes a **Text Node**
* The entire page is represented as a **hierarchy/tree** of nodes

```
<html>
  <body>
    <h1>Hello</h1>
    <p>Welcome to DOM</p>
  </body>
</html>
```

Becomes:

```
Document
 └── html
     └── body
         ├── h1 → "Hello"
         └── p → "Welcome to DOM"
```

---

## 📦 DOM Components

| Term        | Description                                |
| ----------- | ------------------------------------------ |
| `document`  | The root of the DOM, representing the page |
| `node`      | Any single item in the DOM tree            |
| `element`   | A node representing an HTML tag            |
| `text`      | The text content inside an element         |
| `attribute` | A node representing attributes of elements |

---

## 🧰 Common DOM Manipulation Methods

### 🔍 Selecting Elements

```js
document.getElementById('myId');
document.querySelector('.myClass');
```

### ✏️ Changing Content

```js
element.textContent = 'Hello World';
element.innerHTML = '<strong>Bold</strong>';
```

### 🎨 Changing Styles

```js
element.style.color = 'red';
```

### 🧱 Creating Elements

```js
const div = document.createElement('div');
div.textContent = 'New Div';
document.body.appendChild(div);
```

### 🗑️ Removing Elements

```js
element.remove();
```

---

## 🔄 DOM Events

You can attach **event listeners** to DOM elements:

```js
button.addEventListener('click', () => {
  alert('Button clicked!');
});
```

---

## 🧠 Interview Tip

* Emphasize that the DOM is a **live, in-memory representation** of the document.
* Mention it's part of the **Web APIs provided by the browser**, not part of core JavaScript.
* Explain that **manipulating the DOM** is central to dynamic web pages and frameworks like React and Vue build on top of this concept.

---

## 72. How do you select elements in the DOM?

Selecting elements in the DOM is one of the most common tasks in JavaScript for manipulating web pages. There are several methods to **select elements**, each useful in different situations.

---

## 🧰 Common DOM Element Selection Methods

### 1. `getElementById()`

* Selects a **single element** by its unique `id`.
* Returns the element or `null` if not found.

```js
const header = document.getElementById('main-header');
```

---

### 2. `getElementsByClassName()`

* Selects **all elements** with the given class name.
* Returns a **live HTMLCollection** (array-like).

```js
const items = document.getElementsByClassName('list-item');
```

---

### 3. `getElementsByTagName()`

* Selects **all elements** with the specified tag name.
* Returns a **live HTMLCollection**.

```js
const paragraphs = document.getElementsByTagName('p');
```

---

### 4. `querySelector()`

* Selects the **first element** that matches a CSS selector.
* Returns a single element or `null`.

```js
const firstItem = document.querySelector('.list-item');
const header = document.querySelector('#main-header');
```

---

### 5. `querySelectorAll()`

* Selects **all elements** matching a CSS selector.
* Returns a **static NodeList** (array-like).

```js
const allItems = document.querySelectorAll('.list-item');
```

---

## 📝 Notes on Collections

* **HTMLCollection** (from `getElementsByClassName`, `getElementsByTagName`) is **live** — it updates automatically when DOM changes.
* **NodeList** (from `querySelectorAll`) is **static** — does NOT update automatically.

---

## 📋 Example

```html
<ul>
  <li class="list-item">Apple</li>
  <li class="list-item">Banana</li>
  <li class="list-item">Cherry</li>
</ul>
```

```js
// Select all list items (returns NodeList)
const items = document.querySelectorAll('.list-item');

items.forEach(item => {
  console.log(item.textContent);
});
```

---

## 🧠 Interview Tip

* Mention that `querySelector` and `querySelectorAll` are the **most flexible** since they accept any CSS selector.
* Point out the difference between **live** and **static** collections.
* For selecting **single elements by id**, `getElementById` is usually faster and clearer.

---

## 73. How do you add/remove classes to DOM elements?

Adding and removing classes is a very common way to manipulate the appearance and behavior of DOM elements, especially when using CSS.

---

## ✅ How to Add and Remove Classes in JavaScript

### Using the `.classList` API (Recommended)

The `.classList` property gives you convenient methods to work with the classes of an element.

---

### 1. Add a class: `element.classList.add()`

```js
const box = document.querySelector('.box');
box.classList.add('active');
```

This adds the class `"active"` to the element.

---

### 2. Remove a class: `element.classList.remove()`

```js
box.classList.remove('active');
```

This removes the `"active"` class.

---

### 3. Toggle a class: `element.classList.toggle()`

```js
box.classList.toggle('active');
```

* Adds `"active"` if it's not present.
* Removes `"active"` if it is present.

---

### 4. Check if an element has a class: `element.classList.contains()`

```js
if (box.classList.contains('active')) {
  console.log('Box is active');
}
```

---

## ❌ Older Method: Using `className`

Before `.classList`, developers manipulated the `className` string directly.

```js
// Add a class (not recommended)
box.className += ' active';

// Remove a class (more complex)
box.className = box.className.replace(/\bactive\b/, '');
```

**Downside:** Messy and error-prone compared to `.classList`.

---

## 🧪 Complete Example

```html
<div id="myDiv" class="box"></div>

<script>
  const div = document.getElementById('myDiv');
  
  // Add class
  div.classList.add('highlight');
  
  // Remove class
  div.classList.remove('box');
  
  // Toggle class
  div.classList.toggle('active');
  
  // Check class
  if (div.classList.contains('active')) {
    console.log('Active class is present');
  }
</script>
```

---

## 🧠 Interview Tip

* Always prefer `.classList` over modifying `className` directly.
* `.classList` methods are **cleaner**, **more readable**, and **handle edge cases** like duplicate classes.
* Useful in toggling UI states, themes, animations, etc.

---

## 74. What is event bubbling and event capturing?

Understanding **event bubbling** and **event capturing** is key to mastering how events flow through the DOM in JavaScript.

---

## 🌊 What is Event Propagation?

When an event happens on an element (like a click), it doesn't just affect that element. Instead, the event **propagates** through the DOM in phases:

1. **Capturing phase** (top-down)
2. **Target phase** (at the target element)
3. **Bubbling phase** (bottom-up)

---

## 1️⃣ Event Capturing (Trickling Down)

* The event starts at the **root** of the DOM tree (like `document` or `window`) and moves **downward** through the ancestors **until it reaches the target element**.
* Event listeners registered for **capturing** run during this phase.

---

## 2️⃣ Event Bubbling (Bubbling Up)

* After the event reaches the target, it **bubbles up** through the **ancestors**, from the target element back up to the root.
* Event listeners registered for **bubbling** run during this phase.

---

## How to Register Listeners for Capturing or Bubbling?

```js
element.addEventListener('click', handler, useCapture);
```

* `useCapture` is a boolean (default `false`).
* If `true` → listener listens in **capturing** phase.
* If `false` (or omitted) → listener listens in **bubbling** phase.

---

## Example to Visualize

Given this HTML:

```html
<div id="parent">
  <button id="child">Click me</button>
</div>
```

```js
const parent = document.getElementById('parent');
const child = document.getElementById('child');

parent.addEventListener('click', () => {
  console.log('Parent clicked - bubbling');
}, false); // bubbling

parent.addEventListener('click', () => {
  console.log('Parent clicked - capturing');
}, true); // capturing

child.addEventListener('click', () => {
  console.log('Child clicked');
});
```

If you click the button:

**Output:**

```
Parent clicked - capturing
Child clicked
Parent clicked - bubbling
```

Explanation:

* Capturing phase: Event travels from `document` down → triggers parent's capturing listener first.
* Target phase: Child's listener runs.
* Bubbling phase: Event bubbles up → triggers parent's bubbling listener last.

---

## Why does this matter?

* You can control **when** and **where** your event handlers run.
* Helps **manage event flow** in complex UIs.
* Useful for **delegation** and **stopping propagation**.

---

## Bonus: Stop Propagation

* `event.stopPropagation()` — stops the event from moving further (both capturing and bubbling).
* `event.stopImmediatePropagation()` — stops other listeners of the same event on the same element.

---

## 🧠 Interview Tip

* Be clear that **bubbling is the default** behavior.
* Explain the **three phases**: capturing → target → bubbling.
* Mention that **delegated event handling** relies on bubbling to capture events higher up in the DOM.

---

## 75. How do you stop event propagation?

Stopping event propagation is crucial when you want to control how events flow through the DOM.

---

## 🚦 What is Event Propagation?

Remember: events flow through the DOM in **three phases** — capturing, target, and bubbling. Sometimes you want to **stop the event from moving further** to prevent unintended side effects.

---

## How to Stop Event Propagation?

### 1. `event.stopPropagation()`

* Stops the event from propagating **further** in the capturing and bubbling phases.
* The event **won’t travel to ancestor elements** after this is called.

```js
element.addEventListener('click', (event) => {
  event.stopPropagation();
  console.log('Clicked, propagation stopped');
});
```

---

### 2. `event.stopImmediatePropagation()`

* Does everything `stopPropagation()` does, **plus** it **prevents any other event listeners on the same element** from running.
* Useful if you want to make sure **no other listeners** for the same event execute.

```js
element.addEventListener('click', (event) => {
  event.stopImmediatePropagation();
  console.log('Clicked, immediate propagation stopped');
});

// This listener on the same element won’t run if stopImmediatePropagation is called above
element.addEventListener('click', () => {
  console.log('This will NOT run if stopImmediatePropagation was called');
});
```

---

## 3. `event.preventDefault()`

* Note: This **does NOT stop propagation**.
* It **prevents the default action** of the event (like following a link or submitting a form).

```js
link.addEventListener('click', (event) => {
  event.preventDefault(); // Stops link from navigating
});
```

---

## Example Showing Propagation Stop

```html
<div id="parent">
  <button id="child">Click me</button>
</div>
```

```js
const parent = document.getElementById('parent');
const child = document.getElementById('child');

parent.addEventListener('click', () => {
  console.log('Parent clicked');
});

child.addEventListener('click', (event) => {
  event.stopPropagation();
  console.log('Child clicked and propagation stopped');
});
```

* Clicking the button logs:

  ```
  Child clicked and propagation stopped
  ```
* The parent's click listener **does NOT run** because propagation was stopped.

---

## 🧠 Interview Tip

* Use `stopPropagation()` to control bubbling/capturing.
* Use `stopImmediatePropagation()` to stop other listeners on the same element.
* Clarify difference between stopping propagation and preventing default behavior.

---

## 76. What is `event.target` vs `event.currentTarget`?

Understanding the difference between `event.target` and `event.currentTarget` is very important when working with DOM events, especially with event delegation.

---

## `event.target` vs `event.currentTarget`

| Property                  | What it refers to                                                                                           |
| ------------------------- | ----------------------------------------------------------------------------------------------------------- |
| **`event.target`**        | The **actual element** on which the event originated (where the user clicked, for example)                  |
| **`event.currentTarget`** | The **element whose event listener is currently being executed** (the element you attached the listener to) |

---

### Explanation

* **`event.target`** can be a **child element** inside the element with the event listener.
* **`event.currentTarget`** is always the element where the listener is registered, regardless of which child triggered the event.

---

## Example to Illustrate

```html
<div id="parent">
  <button id="child">Click me</button>
</div>
```

```js
const parent = document.getElementById('parent');

parent.addEventListener('click', (event) => {
  console.log('event.target:', event.target.id);
  console.log('event.currentTarget:', event.currentTarget.id);
});
```

---

### What happens when you click the **button**?

* `event.target` → `"child"` (the actual element clicked)
* `event.currentTarget` → `"parent"` (the element where listener is attached)

---

### What happens when you click directly on the **parent** div (outside the button)?

* Both `event.target` and `event.currentTarget` → `"parent"`

---

## Why is this useful?

* When you do **event delegation** (attach a listener on a parent but handle events on children), you often use `event.target` to figure out which child triggered the event.
* `event.currentTarget` lets you know **where the listener is running**, which is useful for clarity or if you need to refer back to that element.

---

## Quick summary:

```js
element.addEventListener('click', (event) => {
  console.log(event.target);        // actual clicked element
  console.log(event.currentTarget); // element with the listener
});
```

---

## 🧠 Interview Tip

* Highlight that `event.target` is dynamic and can change depending on where the user clicks inside the element.
* Emphasize that `event.currentTarget` is always the element the handler was attached to.
* Mention that these properties help in **event delegation** patterns to handle many elements efficiently.

---

## 77. What is event delegation?

**Event delegation** is a powerful technique in JavaScript for efficiently handling events on multiple elements, especially dynamic or large lists of elements.

---

## What is Event Delegation?

Event delegation means:

> Instead of attaching event listeners to **many child elements individually**, you attach **one listener to their common ancestor** (parent element).
> Then, when an event happens on any child, it **bubbles up** to the parent, where you handle it based on the actual target.

---

## Why use Event Delegation?

* **Performance:** Fewer event listeners — less memory and processing.
* **Dynamic elements:** Handles elements added to the DOM later, without adding new listeners.
* **Simpler code:** Manage events in one place instead of many.

---

## How does it work?

1. Attach one event listener to a parent element.
2. Inside the handler, use `event.target` to find which child triggered the event.
3. Optionally, check if the target matches certain criteria (like a class or tag).
4. Run the handler logic accordingly.

---

## Example: Delegating Clicks on List Items

```html
<ul id="menu">
  <li class="item">Home</li>
  <li class="item">About</li>
  <li class="item">Contact</li>
</ul>
```

```js
const menu = document.getElementById('menu');

menu.addEventListener('click', (event) => {
  // Check if clicked element has class "item"
  if (event.target.classList.contains('item')) {
    console.log('Clicked item:', event.target.textContent);
  }
});
```

* Instead of attaching listeners to each `<li>`, just one on `<ul>`.
* When you click any list item, the event bubbles up to `<ul>`.
* The handler uses `event.target` to detect which `<li>` was clicked.

---

## Real-world benefit

If later you add new `<li class="item">Blog</li>` dynamically, you don't need to add another event listener — it just works.

---

## Visualizing the flow

```
User clicks <li> ---> Event bubbles up ---> <ul> listener handles event
```

---

## 🧠 Interview Tip

* Explain bubbling is key to delegation.
* Mention delegation is better for performance and dynamic elements.
* Show how `event.target` helps identify the exact element inside the handler.

---

## 78. How do you handle form validation in JavaScript?

Handling **form validation** in JavaScript is a fundamental skill for creating interactive and user-friendly web applications.

---

## What is Form Validation?

Form validation is the process of checking user inputs before submitting a form to ensure the data is correct, complete, and secure.

---

## Types of Form Validation

1. **Client-side validation** (using JavaScript in the browser)
2. **Server-side validation** (done on the backend, always needed for security)

Here, we'll focus on **client-side validation** using JavaScript.

---

## Basic Steps for Client-Side Validation

1. **Select the form and its input elements**
2. **Listen for form submission**
3. **Check input values against validation rules**
4. **Show error messages if validation fails**
5. **Prevent form submission if invalid**

---

## Example: Simple Form Validation

```html
<form id="signupForm">
  <label>
    Username:
    <input type="text" id="username" required />
  </label>
  <br />
  <label>
    Email:
    <input type="email" id="email" required />
  </label>
  <br />
  <label>
    Password:
    <input type="password" id="password" required minlength="6" />
  </label>
  <br />
  <button type="submit">Sign Up</button>
  <div id="errorMessages" style="color: red;"></div>
</form>
```

```js
const form = document.getElementById('signupForm');
const username = document.getElementById('username');
const email = document.getElementById('email');
const password = document.getElementById('password');
const errorMessages = document.getElementById('errorMessages');

form.addEventListener('submit', function (event) {
  errorMessages.innerHTML = ''; // Clear previous errors
  let errors = [];

  // Username validation
  if (username.value.trim() === '') {
    errors.push('Username is required.');
  }

  // Email validation (simple regex)
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  if (!emailRegex.test(email.value)) {
    errors.push('Please enter a valid email address.');
  }

  // Password validation
  if (password.value.length < 6) {
    errors.push('Password must be at least 6 characters long.');
  }

  if (errors.length > 0) {
    event.preventDefault(); // Prevent form submission
    errorMessages.innerHTML = errors.join('<br>');
  }
});
```

---

## Explanation

* We listen for the form’s `submit` event.
* Run validation checks on each input field.
* If errors exist, display them and **prevent form submission** with `event.preventDefault()`.
* Otherwise, the form submits normally.

---

## Advanced Techniques

* Use **HTML5 built-in validation** properties like `required`, `pattern`, `minlength`, `maxlength`.
* Use the **Constraint Validation API**, e.g., `input.validity` and `input.checkValidity()`.
* Use **custom validation messages** with `setCustomValidity()`.
* Use libraries like **Formik, Yup, or validator.js** for complex validation.

---

## 🧠 Interview Tips

* Explain why client-side validation improves UX by giving instant feedback.
* Mention it **does NOT replace server-side validation** — security always requires backend checks.
* Demonstrate how to prevent form submission on invalid input.
* Show how to give clear feedback to users.

---

## 79. What is `localStorage`, `sessionStorage`, and `cookies`?

`localStorage`, `sessionStorage`, and cookies are all ways to store data on the client side in a web browser, but they have important differences in terms of scope, lifetime, size, and use cases.

---

## 1️⃣ `localStorage`

* **What?** A key-value storage in the browser.
* **Scope:** Data persists **across browser sessions** and tabs/windows on the same origin.
* **Lifetime:** Data stays until explicitly cleared by JavaScript or the user.
* **Size:** Typically around 5–10 MB per origin (varies by browser).
* **Accessible from:** JavaScript running on the same origin (protocol + domain + port).
* **Use cases:** Storing user preferences, themes, tokens, caching non-sensitive data.

### Example:

```js
localStorage.setItem('theme', 'dark');
console.log(localStorage.getItem('theme')); // "dark"
localStorage.removeItem('theme');
```

---

## 2️⃣ `sessionStorage`

* **What?** Similar to `localStorage` but scoped to a **single browser tab/window**.
* **Scope:** Data is **unique per tab** (different tabs have different `sessionStorage`).
* **Lifetime:** Data persists only until the tab or window is closed.
* **Size:** Similar to `localStorage`, but smaller limits may apply.
* **Use cases:** Temporary data needed during a browsing session, like form state or wizard progress.

### Example:

```js
sessionStorage.setItem('step', '2');
console.log(sessionStorage.getItem('step')); // "2"
// Data gone after tab/window closed
```

---

## 3️⃣ Cookies

* **What?** Small pieces of data stored by the browser, sent automatically to the server with every HTTP request.
* **Scope:** Can be scoped by domain and path.
* **Lifetime:** Set by expiration date or session cookies (deleted when browser closes).
* **Size:** Very small (\~4 KB max).
* **Use cases:** Sessions management, authentication tokens, tracking, server-side state.
* **Accessible from:** Both JavaScript (`document.cookie`) and the server via HTTP headers.

### Example:

```js
// Set cookie (expires in 7 days)
document.cookie = "username=John; expires=" + new Date(Date.now() + 7*24*60*60*1000).toUTCString() + "; path=/";

// Read cookies
console.log(document.cookie); // "username=John"
```

---

## Key Differences

| Feature            | localStorage | sessionStorage   | Cookies                                   |
| ------------------ | ------------ | ---------------- | ----------------------------------------- |
| Lifetime           | Persistent   | Until tab closes | Configurable (session or expiration date) |
| Scope              | Per origin   | Per tab + origin | Per domain/path                           |
| Sent with Requests | No           | No               | Yes (sent with every HTTP request)        |
| Size Limit         | \~5-10 MB    | \~5-10 MB        | \~4 KB                                    |
| Accessible via JS  | Yes          | Yes              | Yes                                       |

---

## When to Use What?

* Use **`localStorage`** for long-term client-side storage (preferences, caching).
* Use **`sessionStorage`** for temporary state specific to a tab/session.
* Use **cookies** when data must be sent to the server automatically (like auth tokens or session IDs).

---

## 🧠 Interview Tip

* Mention cookies are used for server communication, while `localStorage` and `sessionStorage` are purely client-side.
* Highlight lifetime and scope differences.
* Be aware of security implications — never store sensitive info in `localStorage` or cookies without proper security flags.

---

## 80. How do you manipulate the DOM using JavaScript?

Manipulating the **DOM (Document Object Model)** with JavaScript is how you dynamically change the structure, content, and style of a webpage after it loads.

---

## What is DOM Manipulation?

The DOM represents the HTML elements as a tree of objects. JavaScript can interact with this tree to:

* Add, remove, or modify elements
* Change attributes, styles, or content
* React to user events dynamically

---

## Key Steps to Manipulate the DOM

### 1. Select elements

Use methods to get references to elements:

* `document.getElementById('id')`
* `document.querySelector(selector)` (returns first match)
* `document.querySelectorAll(selector)` (returns all matches as NodeList)
* `document.getElementsByClassName('className')`
* `document.getElementsByTagName('tagName')`

---

### 2. Change content

* `.textContent` — changes plain text inside element
* `.innerHTML` — changes HTML inside element (can add nested tags)

```js
const heading = document.getElementById('title');
heading.textContent = 'Hello, world!';
heading.innerHTML = '<em>Hello, world!</em>';
```

---

### 3. Change attributes or styles

* `.setAttribute('attr', value)`
* `.getAttribute('attr')`
* `.style.property = value`

```js
const img = document.querySelector('img');
img.setAttribute('src', 'new-image.jpg');
img.style.border = '2px solid red';
```

---

### 4. Create and insert new elements

```js
const newDiv = document.createElement('div');
newDiv.textContent = 'I am new!';

const container = document.getElementById('container');
container.appendChild(newDiv);  // add at end
container.insertBefore(newDiv, container.firstChild); // add at start
```

---

### 5. Remove elements

```js
const toRemove = document.getElementById('old');
toRemove.remove(); // removes from DOM
```

---

### 6. Event handling (interactivity)

```js
const btn = document.getElementById('myButton');
btn.addEventListener('click', () => {
  alert('Button clicked!');
});
```

---

## Example: Changing a Paragraph’s Text and Style

```html
<p id="message">Original text</p>
<button id="changeBtn">Change Message</button>
```

```js
const msg = document.getElementById('message');
const btn = document.getElementById('changeBtn');

btn.addEventListener('click', () => {
  msg.textContent = 'Text changed!';
  msg.style.color = 'blue';
  msg.style.fontWeight = 'bold';
});
```

---

## Summary

| Task                     | Method / Property                    |
| ------------------------ | ------------------------------------ |
| Select element           | `getElementById`, `querySelector`    |
| Change text content      | `.textContent`, `.innerHTML`         |
| Change attributes/styles | `.setAttribute()`, `.style.property` |
| Create element           | `document.createElement()`           |
| Add element              | `.appendChild()`, `.insertBefore()`  |
| Remove element           | `.remove()`                          |
| Listen to events         | `.addEventListener()`                |

---

## 🧠 Interview Tip

* Demonstrate both selecting and modifying elements.
* Mention performance tips like minimizing DOM queries.
* Show knowledge of event handling to make pages interactive.

---

Want me to show you how to manipulate the DOM with a live example or how to optimize DOM changes?

---

### 🔹 **81–90: ES6+ Features**

## 81. What are let and const in ES6?

Great question! `let` and `const` were introduced in **ES6 (ECMAScript 2015)** as new ways to declare variables in JavaScript, improving on the older `var`. They bring better scoping rules and help write safer, clearer code.

---

## `let`

* Declares a **block-scoped** variable.
* You can **reassign** a new value to it.
* Cannot be redeclared in the same scope.
* Helps avoid issues caused by `var`’s function/global scoping.

### Example:

```js
let count = 10;
count = 20;  // valid

if (true) {
  let count = 30;  // different variable inside this block
  console.log(count); // 30
}

console.log(count); // 20
```

---

## `const`

* Declares a **block-scoped** constant variable.
* **Cannot be reassigned** after initialization.
* Must be initialized when declared.
* Note: For objects/arrays, the reference is constant, but object contents **can be changed**.

### Example:

```js
const name = 'Alice';
// name = 'Bob';  // Error: Assignment to constant variable

const user = { age: 25 };
user.age = 26;  // Allowed! Object properties can be changed
console.log(user.age); // 26
```

---

## Differences between `var`, `let`, and `const`

| Feature                  | var                              | let                   | const                 |
| ------------------------ | -------------------------------- | --------------------- | --------------------- |
| Scope                    | Function or global               | Block                 | Block                 |
| Hoisting                 | Yes (initialized with undefined) | Yes (not initialized) | Yes (not initialized) |
| Reassignable             | Yes                              | Yes                   | No                    |
| Redeclarable             | Yes                              | No                    | No                    |
| Temporal Dead Zone (TDZ) | No                               | Yes                   | Yes                   |

---

## Why use `let` and `const`?

* They reduce bugs related to variable scope.
* `const` makes your intent clear when a variable shouldn’t change.
* Block scoping helps avoid accidental global variables.
* Encourage immutability with `const` where possible.

---

## 🧠 Interview tip

* Explain **block scope** as the key improvement over `var`.
* Talk about **temporal dead zone** (TDZ), which prevents accessing variables before declaration.
* Emphasize `const` for variables that should never be reassigned.
* Show examples where `let` and `const` prevent bugs common with `var`.

---

## 82. What is the use of arrow functions?

**Arrow functions** (`=>`) were introduced in ES6 to provide a shorter syntax for writing functions and to change how `this` behaves inside functions.

---

## What are Arrow Functions?

Arrow functions are a concise way to write function expressions.

### Syntax:

```js
// Traditional function expression
const add = function(a, b) {
  return a + b;
};

// Arrow function equivalent
const add = (a, b) => a + b;
```

If the function has a single expression, it returns the result implicitly without needing `return` or braces `{}`.

---

## Main Uses and Benefits of Arrow Functions

### 1. **Concise syntax**

Less code, easier to read especially for small functions, callbacks, and inline functions.

```js
[1, 2, 3].map(n => n * 2); // [2, 4, 6]
```

---

### 2. **Lexical `this` binding**

Arrow functions do **not** have their own `this`. Instead, they capture the `this` value from the **surrounding context** where they are defined.

This avoids common problems with `this` inside callbacks.

```js
function Person() {
  this.age = 0;

  setInterval(() => {
    this.age++; // 'this' refers to the Person instance
    console.log(this.age);
  }, 1000);
}

const p = new Person();
```

If you used a traditional function inside `setInterval`, `this` would refer to the global object or `undefined` (in strict mode), which is usually not what you want.

---

### 3. **No `arguments` object**

Arrow functions do **not** have their own `arguments` object. To access arguments, use rest parameters `(...args)`.

---

### Limitations

* Cannot be used as constructors (`new` won’t work).
* Cannot use `yield` inside (no generator arrow functions).
* No own `this`, `arguments`, `super`, or `new.target`.

---

## Summary

| Feature            | Traditional Function          | Arrow Function                |
| ------------------ | ----------------------------- | ----------------------------- |
| Syntax             | Verbose                       | Concise                       |
| `this` binding     | Dynamic, depends on call site | Lexical (inherits from outer) |
| `arguments` object | Available                     | Not available                 |
| Can be constructor | Yes                           | No                            |

---

## 🧠 Interview Tip

* Highlight arrow functions fix common `this` bugs.
* Mention the concise syntax saves lines in callbacks and functional programming.
* Be aware of limitations and when **not** to use arrow functions.

---

## 83. What is object and array destructuring?

**Destructuring** in JavaScript is a convenient way to extract values from objects or arrays into distinct variables using a concise syntax. It makes your code cleaner and easier to read.

---

## 1️⃣ Object Destructuring

Extracts properties from an object into variables with matching names.

### Syntax:

```js
const person = { name: 'Alice', age: 25, city: 'NYC' };

const { name, age } = person;

console.log(name); // "Alice"
console.log(age);  // 25
```

You can also:

* Rename variables
* Provide default values
* Destructure nested objects

### Examples:

```js
// Rename
const { name: firstName, city } = person;
console.log(firstName); // "Alice"

// Default value
const { country = 'USA' } = person;
console.log(country); // "USA"

// Nested destructuring
const user = {
  id: 1,
  profile: {
    username: 'user1',
    email: 'user1@example.com'
  }
};

const { profile: { username, email } } = user;
console.log(username); // "user1"
```

---

## 2️⃣ Array Destructuring

Extracts elements from arrays based on their position.

### Syntax:

```js
const numbers = [10, 20, 30];

const [first, second] = numbers;

console.log(first);  // 10
console.log(second); // 20
```

You can also:

* Skip elements
* Provide default values
* Use rest operator to capture remaining elements

### Examples:

```js
// Skip second element
const [one, , three] = numbers;
console.log(one, three); // 10 30

// Default value
const [a = 1, b = 2, c = 3, d = 4] = [10];
console.log(a, b, c, d); // 10 2 3 4

// Rest operator
const [head, ...tail] = numbers;
console.log(head); // 10
console.log(tail); // [20, 30]
```

---

## Why Use Destructuring?

* Makes code shorter and more readable
* Avoids repetitive code accessing properties or indices
* Makes it easier to work with function parameters

---

## Example: Function Parameter Destructuring

```js
function greet({ name, age }) {
  console.log(`Hello, ${name}! You are ${age} years old.`);
}

const person = { name: 'Alice', age: 25 };
greet(person);
```

---

## Summary

| Feature            | Object Destructuring                 | Array Destructuring    |
| ------------------ | ------------------------------------ | ---------------------- |
| Syntax             | `{ prop1, prop2 } = object`          | `[val1, val2] = array` |
| Order              | By property name                     | By position            |
| Default values     | Supported                            | Supported              |
| Rename variables   | Supported (e.g. `{ prop: newName }`) | Not applicable         |
| Nested destructure | Supported                            | Supported              |

---

## 🧠 Interview Tip

* Explain both syntax and use cases.
* Show examples with renaming and defaults.
* Mention function parameter destructuring as a common use.

---

## 84. What is the spread operator?

The **spread operator** in JavaScript is a powerful syntax represented by three dots: `...`. It allows you to **expand** iterable elements (like arrays or strings) or object properties into individual elements or key-value pairs.

---

## What does the spread operator do?

It **“spreads”** the elements of an iterable (array, string, etc.) or properties of an object into a new context.

---

## Common uses of the spread operator

### 1. **Copying arrays**

```js
const arr1 = [1, 2, 3];
const arr2 = [...arr1];
console.log(arr2); // [1, 2, 3]
```

This creates a **shallow copy** of the array (not just a reference).

---

### 2. **Merging arrays**

```js
const arr1 = [1, 2];
const arr2 = [3, 4];
const merged = [...arr1, ...arr2];
console.log(merged); // [1, 2, 3, 4]
```

---

### 3. **Spread in function calls**

Allows passing an array of values as individual arguments.

```js
const nums = [4, 7, 1];
const max = Math.max(...nums);
console.log(max); // 7
```

---

### 4. **Copying and merging objects**

```js
const obj1 = { a: 1, b: 2 };
const obj2 = { b: 3, c: 4 };

const copy = { ...obj1 };
console.log(copy); // { a: 1, b: 2 }

const merged = { ...obj1, ...obj2 };
console.log(merged); // { a: 1, b: 3, c: 4 }
```

Note: If keys overlap, later values overwrite earlier ones.

---

### 5. **Convert string to array**

```js
const str = "hello";
const chars = [...str];
console.log(chars); // ['h', 'e', 'l', 'l', 'o']
```

---

## Spread vs Rest operator

* Both use `...` syntax but serve different purposes:

    * **Spread** expands elements (used in expressions).
    * **Rest** collects multiple elements into an array (used in function params or destructuring).

Example Rest:

```js
function sum(...numbers) {
  return numbers.reduce((a, b) => a + b);
}
```

---

## Summary

| Use case              | Example                | Result                      |
| --------------------- | ---------------------- | --------------------------- |
| Copy array            | `[...arr]`             | New array copy              |
| Merge arrays          | `[...arr1, ...arr2]`   | Combined array              |
| Pass args to function | `fn(...args)`          | Individual arguments        |
| Copy object           | `{ ...obj }`           | New object copy             |
| Merge objects         | `{ ...obj1, ...obj2 }` | Combined object (last wins) |

---

## 🧠 Interview Tip

* Explain how spread simplifies copying and merging.
* Mention shallow copy nature and possible gotchas with nested objects.
* Show difference with rest parameters to clarify confusion.

---

## 85. What are template literals?

**Template literals** are a feature introduced in ES6 that make working with strings much easier and more readable compared to traditional string concatenation.

---

## What are Template Literals?

* Template literals are **string literals** that allow embedded expressions.
* They use **backticks** `` ` `` instead of single `'` or double `"` quotes.
* They support **multiline strings** and **string interpolation** (embedding variables or expressions).

---

## Key Features of Template Literals

### 1. **String interpolation**

You can embed variables or any JavaScript expressions inside `${}`.

```js
const name = "Alice";
const age = 25;

const greeting = `Hello, my name is ${name} and I am ${age} years old.`;
console.log(greeting);
// Output: Hello, my name is Alice and I am 25 years old.
```

---

### 2. **Multiline strings**

Template literals preserve whitespace and newlines without special characters.

```js
const message = `This is line 1
This is line 2
This is line 3`;

console.log(message);
/* Output:
This is line 1
This is line 2
This is line 3
*/
```

---

### 3. **Expression evaluation**

You can put any valid JavaScript expression inside `${}`.

```js
const a = 5;
const b = 10;
console.log(`Sum of ${a} and ${b} is ${a + b}`); // Sum of 5 and 10 is 15
```

---

### 4. **Tagged template literals** (Advanced)

You can create custom functions to process template literals for advanced use cases like localization, sanitization, etc.

```js
function tag(strings, ...values) {
  console.log(strings); // array of string parts
  console.log(values);  // array of interpolated values
  return 'custom string';
}

const result = tag`Hello ${name}, you are ${age} years old.`;
console.log(result); // custom string
```

---

## Why use Template Literals?

* Cleaner, more readable string construction.
* Avoids tedious string concatenation using `+`.
* Easy multiline string support.
* Supports dynamic expressions directly inside strings.

---

## Comparison

| Feature              | Traditional Strings              | Template Literals              |
| -------------------- | -------------------------------- | ------------------------------ |
| String concatenation | `"Hello " + name + "!"`          | `` `Hello ${name}!` ``         |
| Multiline strings    | Use `\n` or `+` with line breaks | Simply write on multiple lines |
| Expression embedding | No                               | Yes, with `${}`                |

---

## Example

```js
const user = {
  name: 'Bob',
  age: 30
};

const msg = `User Info:
Name: ${user.name}
Age: ${user.age}`;

console.log(msg);
```

Output:

```
User Info:
Name: Bob
Age: 30
```

---

## 🧠 Interview Tip

* Highlight ease of string interpolation and multiline support.
* Mention use cases like building dynamic strings in UI or logging.
* If confident, briefly mention tagged templates as a powerful extension.

---

## 86. What are default parameters?

**Default parameters** were introduced in ES6 to make function parameter handling more concise and clear.

---

## What are Default Parameters?

Default parameters allow you to specify a **default value** for a function parameter if no argument (or `undefined`) is passed for that parameter when the function is called.

---

## Why use Default Parameters?

Before ES6, you had to manually check if a parameter was passed or not, like this:

```js
function greet(name) {
  name = name || 'Guest';
  console.log('Hello, ' + name);
}
greet();         // Hello, Guest
greet('Alice');  // Hello, Alice
```

This approach works but has caveats (e.g., falsy values like `''`, `0` are replaced).

---

## Syntax of Default Parameters

You declare default values directly in the function signature:

```js
function greet(name = 'Guest') {
  console.log(`Hello, ${name}`);
}

greet();          // Hello, Guest
greet('Alice');   // Hello, Alice
```

---

## How it works:

* If the caller **does not provide an argument** or passes `undefined`, the default value is used.
* If `null` or any other falsy value (like `''`, `0`, `false`) is passed, the default value is **not** used.

Example:

```js
function showMessage(msg = 'No message') {
  console.log(msg);
}

showMessage();        // No message (default used)
showMessage(undefined); // No message (default used)
showMessage(null);     // null (default NOT used)
showMessage('Hi');     // Hi
```

---

## Default Parameters with Other Parameters

You can mix default and non-default parameters:

```js
function multiply(a, b = 1) {
  return a * b;
}

console.log(multiply(5));    // 5 (b defaults to 1)
console.log(multiply(5, 2)); // 10
```

---

## Default Parameters and Functions

You can use expressions or functions as default values:

```js
function getRandom() {
  return Math.floor(Math.random() * 10);
}

function printNumber(num = getRandom()) {
  console.log(num);
}

printNumber(); // prints random number
```

---

## Summary

| Behavior                         | Example         | Output            |
| -------------------------------- | --------------- | ----------------- |
| Parameter missing or undefined   | `greet()`       | Uses default      |
| Parameter is null or falsy       | `greet(null)`   | Uses passed value |
| Parameter has default expression | `printNumber()` | Calls function    |

---

## 🧠 Interview Tip

* Explain the improved readability and convenience over older patterns.
* Mention difference between `undefined` and other falsy values regarding default parameters.
* Show example with default parameters as functions or expressions.

---

## 87. What are rest parameters?

Let’s dive into **rest parameters** — they’re a very handy feature introduced in ES6.

---

## What are Rest Parameters?

Rest parameters allow a function to accept **an indefinite number of arguments** as an array. They gather all remaining arguments passed to the function into a **single array**.

---

## Syntax

Use `...` before the last parameter in a function to collect all remaining arguments into an array:

```js
function myFunc(...args) {
  console.log(args);
}

myFunc(1, 2, 3);  // [1, 2, 3]
```

---

## Why use Rest Parameters?

Before ES6, to access extra arguments, you had to use the **`arguments`** object which is array-like but not a real array, so methods like `.map()` or `.filter()` were unavailable without conversion.

---

## Example with Rest Parameters

```js
function sum(...numbers) {
  return numbers.reduce((acc, curr) => acc + curr, 0);
}

console.log(sum(1, 2, 3));    // 6
console.log(sum(4, 5));       // 9
console.log(sum());           // 0
```

---

## Rest Parameters vs `arguments` Object

| Feature                | Rest Parameters                       | `arguments` Object                                |
| ---------------------- | ------------------------------------- | ------------------------------------------------- |
| Type                   | Real Array                            | Array-like object                                 |
| Methods available      | All array methods (map, filter, etc.) | Limited, no array methods directly                |
| Syntax                 | Clear and modern (`...args`)          | Implicit inside function                          |
| Works with arrow funcs | Yes                                   | No (`arguments` not available in arrow functions) |

---

## Using Rest Parameters with Other Parameters

You can combine fixed parameters and rest parameters, but rest must be last:

```js
function greet(greeting, ...names) {
  names.forEach(name => console.log(`${greeting}, ${name}!`));
}

greet('Hello', 'Alice', 'Bob', 'Charlie');
// Hello, Alice!
// Hello, Bob!
// Hello, Charlie!
```

---

## Summary

* **Rest parameters** collect all remaining arguments into an array.
* Must be **last** parameter in the function signature.
* Provide a cleaner and more powerful way to handle variable numbers of arguments.

---

## 🧠 Interview Tip

* Mention the advantage over the older `arguments` object.
* Show example combining fixed and rest parameters.
* Note that rest parameters give you a proper array.

---

## 88. What are modules in JavaScript (import/export)?

**Modules** in JavaScript are a way to organize and reuse code by splitting it into separate files, each with its own scope. ES6 introduced a standardized module system with `import` and `export` keywords.

---

## What are Modules?

* Modules allow you to **encapsulate code** (variables, functions, classes) in one file.
* You can **export** parts of that code to be used in other files.
* You can **import** those exported parts into another file.
* This helps avoid polluting the global scope and improves maintainability.

---

## Exporting in JavaScript Modules

You can export values (variables, functions, classes) from a file:

### 1. Named exports

Export multiple things by name.

```js
// mathUtils.js
export function add(a, b) {
  return a + b;
}

export const PI = 3.14159;
```

### 2. Default export

Export a single value as the default export of the module.

```js
// logger.js
export default function log(message) {
  console.log(message);
}
```

---

## Importing Modules

### 1. Import named exports

Use curly braces and exact names.

```js
// main.js
import { add, PI } from './mathUtils.js';

console.log(add(2, 3)); // 5
console.log(PI);        // 3.14159
```

### 2. Import default export

No curly braces, you can choose any name.

```js
// main.js
import log from './logger.js';

log('Hello World'); // prints Hello World
```

### 3. Import all as an object

Import all named exports under a single namespace.

```js
import * as math from './mathUtils.js';

console.log(math.add(1, 2));  // 3
console.log(math.PI);         // 3.14159
```

---

## Notes

* Module files usually have `.js` extension but are loaded as modules via `<script type="module">` in browsers or via bundlers (Webpack, Rollup) or Node.js with ES modules support.
* Modules are **always in strict mode**.
* Import and export statements must be at the top level, not inside functions or blocks.
* Circular dependencies are possible but can be tricky.

---

## Why use Modules?

* Better code organization.
* Reusability of code.
* Avoid global namespace pollution.
* Easy maintenance and testing.

---

## Example

**mathUtils.js**

```js
export function multiply(a, b) {
  return a * b;
}

export const E = 2.718;
```

**app.js**

```js
import { multiply, E } from './mathUtils.js';

console.log(multiply(3, 4)); // 12
console.log(E);              // 2.718
```

---

## 🧠 Interview Tip

* Explain difference between **named exports** and **default exports**.
* Show how `import` corresponds to `export`.
* Mention browser and Node.js support and module loading differences.
* Talk about advantages of modular code.

---

## 89. What is optional chaining `?.`?

The **optional chaining operator (`?.`)** is a very useful feature introduced in ES2020 that helps you **safely access deeply nested object properties** without worrying about runtime errors when a property doesn’t exist.

---

## What is Optional Chaining?

* It lets you **access properties or call functions on objects that might be `null` or `undefined`**.
* Instead of throwing an error when trying to access a property of `null` or `undefined`, it **short-circuits and returns `undefined`**.
* It reduces the need for multiple `if` checks or `&&` operators.

---

## Syntax

```js
obj?.prop
obj?.[expr]
obj?.method()
```

---

## How it works?

### Without optional chaining:

Trying to access a nested property without checking can cause an error:

```js
const user = {
  profile: {
    name: 'Alice',
  },
};

console.log(user.profile.name);   // Alice
console.log(user.account.balance); // Error! Cannot read property 'balance' of undefined
```

### With optional chaining:

```js
console.log(user.account?.balance);  // undefined (no error)
```

Here, `user.account` is `undefined`, but instead of erroring, `?.` returns `undefined`.

---

## Examples

### Access nested properties safely

```js
const user = {
  address: {
    city: 'New York'
  }
};

console.log(user.address?.city);     // New York
console.log(user.contact?.phone);    // undefined (no error)
```

### Call a method only if it exists

```js
const person = {
  greet() {
    console.log('Hello!');
  }
};

person.greet?.();      // Hello!
person.sayBye?.();     // Does nothing, no error
```

### Access dynamic properties safely

```js
const key = 'email';
const obj = { email: 'test@example.com' };

console.log(obj?.[key]);  // test@example.com
console.log(obj?.['phone']); // undefined (no error)
```

---

## Important Notes

* Optional chaining stops evaluation as soon as it encounters `null` or `undefined`.
* It works with **property access**, **array elements**, and **function calls**.
* It does **not** prevent errors if the base object itself is not defined (e.g., `user` in `user?.profile` must be defined).

---

## Summary Table

| Expression      | Result if path is valid | Result if part is null/undefined |
| --------------- | ----------------------- | -------------------------------- |
| `obj?.prop`     | value of `prop`         | `undefined` (no error)           |
| `obj?.method()` | method call result      | `undefined` (no error)           |
| `obj?.[expr]`   | property access result  | `undefined` (no error)           |

---

## 🧠 Interview Tip

* Emphasize how `?.` reduces boilerplate code for safe property access.
* Mention it's very handy when working with APIs or JSON where data may be missing.
* Show comparison with the older `&&` chaining:

```js
// Old way:
const city = user && user.address && user.address.city;

// With optional chaining:
const city = user?.address?.city;
```

---

## 90. What is nullish coalescing `??`?

**Nullish coalescing (`??`)** is a useful operator introduced in ES2020 that works great alongside optional chaining. Let me explain it in detail.

---

## What is Nullish Coalescing (`??`)?

* The `??` operator returns the **right-hand side operand** when the **left-hand side operand is `null` or `undefined`**.
* Otherwise, it returns the **left-hand side operand**.
* It’s like the logical OR operator (`||`), but **only treats `null` and `undefined` as “nullish”**, unlike `||` which treats all **falsy values** (`0`, `''`, `false`, `NaN`) as falsey.

---

## Why use Nullish Coalescing?

Sometimes you want to provide a **default value** only when a variable is `null` or `undefined`, **not when it is falsy** like `0` or an empty string.

---

## Syntax

```js
let result = value ?? defaultValue;
```

---

## Examples

### Using `||` (logical OR)

```js
let count = 0;
let value = count || 10;  
console.log(value); // 10, because 0 is falsy
```

### Using `??` (nullish coalescing)

```js
let count = 0;
let value = count ?? 10;  
console.log(value); // 0, because 0 is NOT null or undefined
```

---

### More Examples

```js
let name = null;
console.log(name ?? 'Guest');   // Guest (because name is null)

let age = undefined;
console.log(age ?? 18);          // 18 (because age is undefined)

let score = 0;
console.log(score ?? 100);       // 0 (score is 0, which is NOT null/undefined)
```

---

## Use Case with Optional Chaining

You can combine with optional chaining to safely access deeply nested values with defaults:

```js
const user = {
  profile: {
    age: 0
  }
};

const age = user.profile?.age ?? 18;
console.log(age);  // 0, because age exists and is not null/undefined
```

---

## Difference between `||` and `??`

\| Operator | Checks for falsy values? | Checks only `null` or `undefined`? | Example: `0 ?? 10` | Example: `0 || 10` |
\|----------|-------------------------|------------------------------------|--------------------|--------------------|
\| `||`     | Yes                     | No                                 | 0                  | 10                 |
\| `??`     | No                      | Yes                                | 0                  | 0                  |

---

## Summary

* `??` helps avoid unintended fallback when a value is falsy but valid (like `0` or `''`).
* It returns right side only if the left side is `null` or `undefined`.
* Often used for setting default values safely.

---

## 🧠 Interview Tip

* Explain how `??` improves upon `||` for default values.
* Mention typical use cases: defaulting variables, optional chaining fallback.
* Show examples comparing `||` and `??`.

---

Would you like a practical example combining optional chaining and nullish coalescing for handling API response data?

---

### 🔹 **91–100: Advanced Topics & Misc**

## 91. What is event loop with an example?

Absolutely! The **event loop** is a fundamental concept in JavaScript that explains how JS handles asynchronous operations while still being single-threaded. Understanding this is key for interview prep.

---

## What is the Event Loop?

* JavaScript is **single-threaded**: it executes one piece of code at a time.
* However, it can perform **asynchronous operations** (like timers, network requests) without blocking the main thread.
* The **event loop** is the mechanism that manages these asynchronous callbacks, making JavaScript **non-blocking**.

---

## How does the Event Loop Work?

1. **Call Stack**: Where JavaScript keeps track of the currently executing function.
2. **Web APIs (Browser/Environment)**: Handles async operations like `setTimeout`, HTTP requests.
3. **Callback Queue (Task Queue)**: Stores callbacks ready to be executed after async operations finish.
4. **Event Loop**: Constantly checks if the call stack is empty, and if so, pushes the next callback from the callback queue to the stack.

---

## Visualization:

```
+-----------------+         +----------------+       +-------------------+
|    Call Stack   |  <----  | Event Loop     | <---> | Callback Queue    |
+-----------------+         +----------------+       +-------------------+
        |                                                       ^
        v                                                       |
   Executes JS code                                  Async callbacks wait here
```

---

## Simple Example

```js
console.log('Start');

setTimeout(() => {
  console.log('Inside timeout');
}, 0);

console.log('End');
```

### Output:

```
Start
End
Inside timeout
```

---

### Explanation:

* `console.log('Start')` runs immediately, goes on call stack, executes, then removed.
* `setTimeout(..., 0)` is called:

    * The callback is sent to Web APIs and scheduled to run after 0ms.
* `console.log('End')` runs next.
* After the call stack is empty, the **event loop** picks the timeout callback from the **callback queue** and pushes it to the call stack.
* Then `console.log('Inside timeout')` runs.

---

## Why does `setTimeout(..., 0)` not execute immediately?

Even with 0ms delay, the callback waits until the current call stack is empty. The event loop ensures callbacks run asynchronously.

---

## Real-World Use

* Managing API responses.
* Handling user input events.
* Animations.
* Any asynchronous code (promises, timers, etc.).

---

## Summary

* The event loop **enables asynchronous behavior in a single-threaded language**.
* It manages execution order of synchronous and asynchronous code.
* Callbacks are queued and executed only when the call stack is empty.

---

## 🧠 Interview Tip

* Explain call stack and callback queue roles.
* Show an example with `setTimeout` or `fetch`.
* Mention that promises use a **microtask queue**, which has higher priority than callback queue (task queue).

---

## 92. What is the difference between deep copy and shallow copy?

Understanding **deep copy** vs **shallow copy** is important for working with objects and arrays in JavaScript, especially when dealing with mutations and state management.

---

## What is a Shallow Copy?

* A **shallow copy** copies the **top-level properties** of an object or array.
* If any property is a **reference type** (like an object or array), the reference is copied — **not the actual nested object**.
* This means both the original and the copied object share the same nested objects.

---

## What is a Deep Copy?

* A **deep copy** duplicates **all levels** of an object or array recursively.
* Nested objects or arrays are **fully cloned**, so the copy and original do **not share references**.
* Changes to nested objects in the copy **do not affect** the original.

---

## Visual Example

```js
const original = {
  name: 'Alice',
  address: {
    city: 'Wonderland'
  }
};
```

### Shallow Copy

```js
const shallowCopy = { ...original };

shallowCopy.name = 'Bob';
shallowCopy.address.city = 'Looking Glass';

console.log(original.name);          // Alice  (primitive copied)
console.log(original.address.city);  // Looking Glass (changed because nested object is shared)
```

**Explanation:**
The `address` object is shared between `original` and `shallowCopy`. Changing nested properties affects both.

---

### Deep Copy

```js
const deepCopy = JSON.parse(JSON.stringify(original));

deepCopy.name = 'Bob';
deepCopy.address.city = 'Looking Glass';

console.log(original.name);          // Alice
console.log(original.address.city);  // Wonderland (unchanged)
```

**Explanation:**
`deepCopy` creates an entirely new nested object, so changes don’t affect the original.

---

## Important Notes

* **Shallow copy methods**:

    * Object spread: `{ ...obj }`
    * `Object.assign({}, obj)`
    * Array methods like `slice()`, `concat()` (for arrays)

* **Deep copy methods**:

    * `JSON.parse(JSON.stringify(obj))` (simple but has limitations: doesn't copy functions, dates, undefined, etc.)
    * Libraries like Lodash’s `_.cloneDeep()`
    * Custom recursive cloning functions

---

## Summary Table

| Aspect         | Shallow Copy                         | Deep Copy                           |
| -------------- | ------------------------------------ | ----------------------------------- |
| Level copied   | Top-level properties only            | Entire object structure recursively |
| Nested objects | Shared references                    | New cloned nested objects           |
| Changes affect | Original if nested properties change | Original unaffected                 |
| Common usage   | Quick copy when no nested mutation   | When full independent copy needed   |

---

## 🧠 Interview Tip

* Explain difference clearly with examples.
* Mention shallow copy copies references, deep copy duplicates everything.
* Point out limitations of `JSON.parse/stringify` and alternatives.

---

## 93. How does garbage collection work in JavaScript?

Understanding **garbage collection** in JavaScript is important to know how memory management happens under the hood.

---

## What is Garbage Collection?

* JavaScript automatically **reclaims memory** that is no longer needed.
* When objects or variables are no longer **reachable or referenced**, their memory is **freed**.
* This process is called **Garbage Collection (GC)**.
* You don’t manually free memory like in languages such as C/C++.

---

## How Does Garbage Collection Work?

### Key Idea: Reachability

* JS engine tracks which objects are **reachable** from roots.
* **Roots** are:

    * Global variables
    * Currently executing function’s local variables and parameters
    * Other active references

If an object is **not reachable** from these roots, it is considered **garbage** and eligible for collection.

---

### Example

```js
function foo() {
  let a = { name: 'Alice' };
  let b = a;
  a = null;  // 'a' no longer references the object, but 'b' does
}

foo();
// After foo ends, both 'a' and 'b' are out of scope, so the object is unreachable and can be collected.
```

---

## Garbage Collection Algorithms in JS engines

### 1. Reference Counting (historical, less used)

* Each object keeps a count of references to it.
* When count drops to zero, object is collected.
* Problem: Cannot handle **circular references** (two objects referencing each other).

### 2. Mark-and-Sweep (most modern engines use this)

* The engine **marks** all reachable objects starting from roots.
* Unmarked objects are considered garbage and swept (collected).
* Handles circular references well.

---

## What triggers Garbage Collection?

* Garbage collection runs **periodically** or when memory is low.
* It’s **non-deterministic** — you can’t predict exactly when GC will run.
* You should not rely on it to immediately free memory.

---

## How to help the Garbage Collector?

* **Remove references** to objects when no longer needed (e.g., setting variables to `null`).
* Avoid creating **unnecessary global variables**.
* Be careful with **closures** that hold onto variables longer than needed.
* Avoid memory leaks by cleaning event listeners and DOM references.

---

## Summary

| Aspect              | Description                                            |
| ------------------- | ------------------------------------------------------ |
| What it does        | Frees memory of unreachable objects                    |
| Reachability        | Objects reachable from roots are retained              |
| Algorithm used      | Mark-and-Sweep is common                               |
| Developer control   | No direct control, but can help by removing references |
| Circular references | Handled well by Mark-and-Sweep                         |

---

## 🧠 Interview Tip

* Explain automatic memory management and reachability.
* Mention mark-and-sweep algorithm.
* Give an example with variables and scope.
* Discuss how to avoid memory leaks.

---

## 94. What is the temporal dead zone?

The **Temporal Dead Zone (TDZ)** is a key concept related to `let` and `const` variables in JavaScript, important for interview prep.

---

## What is Temporal Dead Zone?

* The **Temporal Dead Zone** is the time period **between the start of a block scope and the moment the variable is declared and initialized**.
* During this time, the variable **cannot be accessed**, and trying to do so throws a **ReferenceError**.
* It applies to variables declared with `let` and `const` (but **not** `var`).

---

## Why does TDZ exist?

* To prevent accessing variables **before they are initialized**, making your code safer and less error-prone.
* Helps enforce the **block scoping rules** introduced in ES6.

---

## Example

```js
{
  console.log(x); // ReferenceError: Cannot access 'x' before initialization
  let x = 10;
}
```

* Here, `x` is in the TDZ from the start of the block until `let x = 10;` executes.
* Accessing `x` before its declaration throws an error.

---

## Contrast with `var`

```js
{
  console.log(y); // undefined (no error)
  var y = 10;
}
```

* `var` declarations are **hoisted and initialized with `undefined`**, so no error here.
* But this can lead to bugs from accessing variables before assignment.

---

## Visual Timeline for `let`/`const`:

| Time                      | Access to variable                   |
| ------------------------- | ------------------------------------ |
| Block start               | Variable is in TDZ (no access)       |
| Variable declaration line | Variable initialized, access allowed |

---

## Summary

| Feature                   | `var`                                | `let` / `const`                |
| ------------------------- | ------------------------------------ | ------------------------------ |
| Hoisting                  | Hoisted & initialized to `undefined` | Hoisted but NOT initialized    |
| Access before declaration | Allowed (value is `undefined`)       | Not allowed (TDZ causes error) |
| Scope                     | Function or global scope             | Block scope                    |

---

## 🧠 Interview Tip

* Explain TDZ as the “zone” before a `let` or `const` variable is declared.
* Show the ReferenceError example.
* Contrast with `var` hoisting behavior.
* Mention TDZ helps catch bugs early.

---

## 95. What are JavaScript engines (V8, SpiderMonkey)?

Understanding **JavaScript engines** is helpful for grasping how JS code runs behind the scenes, which can impress interviewers.

---

## What is a JavaScript Engine?

A **JavaScript engine** is a program (or interpreter) that **executes JavaScript code**. It reads your JS source code, parses it, compiles it (often to machine code), and runs it on your device.

---

## Key Functions of a JavaScript Engine

1. **Parsing:** Reads JS code and turns it into an Abstract Syntax Tree (AST).
2. **Compilation:** Converts the AST into executable machine code, often using Just-In-Time (JIT) compilation.
3. **Execution:** Runs the machine code.
4. **Memory management:** Handles garbage collection.
5. **Optimization:** Speeds up frequently executed code paths dynamically.

---

## Popular JavaScript Engines

| Engine                     | Maintained By | Used In                                         |
| -------------------------- | ------------- | ----------------------------------------------- |
| **V8**                     | Google        | Chrome, Node.js, Edge (Chromium-based browsers) |
| **SpiderMonkey**           | Mozilla       | Firefox                                         |
| **JavaScriptCore (Nitro)** | Apple         | Safari                                          |
| **Chakra**                 | Microsoft     | Legacy Edge (pre-Chromium)                      |

---

## Example: V8 Engine (Google)

* Developed for Google Chrome and Node.js.
* Uses **JIT compilation** to convert JS to optimized machine code at runtime.
* Implements **hidden classes** and **inline caching** to optimize object property access.
* Handles garbage collection via **generational GC** (young/old generation heaps).

---

## Why Knowing JS Engines Matters

* Helps you understand performance: why some code runs faster.
* Explains behavior like **hoisting**, **scoping**, and **closures** based on engine internals.
* Useful for debugging and optimization.

---

## Summary

* JavaScript engines **run JS code** by parsing, compiling, and executing.
* V8 and SpiderMonkey are popular examples powering browsers and Node.js.
* Engines use techniques like **JIT compilation** and **garbage collection** to improve performance.

---

## 96. What is the difference between eval and new Function()?

Both `eval` and `new Function()` allow you to execute JavaScript code dynamically as strings, but they behave quite differently and have different use cases and security implications.

---

## What is `eval`?

* `eval` takes a **string of JavaScript code** and executes it **in the current scope**.
* It can access and modify local variables.
* Syntax:

  ```js
  eval("console.log('Hello from eval');");
  ```

---

## What is `new Function()`?

* `new Function()` creates a **new function object** from a string.
* The code inside runs in the **global scope**, **not** the current local scope.
* Syntax:

  ```js
  const fn = new Function('a', 'b', 'return a + b;');
  console.log(fn(2, 3)); // 5
  ```

---

## Key Differences

| Aspect              | `eval`                                 | `new Function()`                                              |
| ------------------- | -------------------------------------- | ------------------------------------------------------------- |
| Scope               | Executes in **current local scope**    | Executes in **global scope**                                  |
| Access to variables | Can access local variables             | Cannot access local variables                                 |
| Usage               | Executes arbitrary code immediately    | Returns a new function object                                 |
| Performance         | Generally slower, harder to optimize   | Faster than `eval` since it creates a function                |
| Security            | Riskier, can lead to injection attacks | Still risky but slightly safer than `eval`                    |
| Use cases           | Dynamic expressions, quick eval        | Dynamic function creation, safer alternative for complex code |

---

## Example Showing Scope Difference

```js
function test() {
  let x = 10;
  eval('console.log(x)'); // 10 — can access local 'x'
  
  const fn = new Function('console.log(typeof x)');
  fn(); // undefined — no access to local 'x'
}

test();
```

---

## Why avoid `eval`?

* Security: It can run **any code**, so it's vulnerable to injection attacks.
* Performance: JS engines can’t optimize code using `eval` well.
* Debugging: Harder to debug and maintain.

---

## When to use `new Function()`?

* When you need to create functions dynamically and don’t need local scope access.
* Safer alternative to `eval` but still requires caution.

---

## Summary

| Feature          | `eval`                      | `new Function()`      |
| ---------------- | --------------------------- | --------------------- |
| Runs code in     | Current local scope         | Global scope          |
| Returns          | Result of executed code     | New function object   |
| Access to locals | Yes                         | No                    |
| Performance      | Slower                      | Faster                |
| Security         | Risky (avoid when possible) | Safer but still risky |

---

## 🧠 Interview Tip

Explain the **scope difference** clearly with examples and why `eval` is discouraged. Mention security risks and use cases.

---

## 97. What is tail call optimization?

**Tail Call Optimization (TCO)** is an important concept in functional programming and JavaScript performance, especially relevant in recursive function calls.

---

## What is Tail Call Optimization?

* **Tail Call Optimization (TCO)** is a technique where the compiler or JavaScript engine **optimizes recursive function calls that happen in the "tail position"** to avoid growing the call stack.
* A **tail call** is a function call that is the **last operation** in a function before it returns.
* With TCO, instead of adding a new stack frame for the recursive call, the engine **reuses the current function's stack frame**, thus preventing stack overflow and improving performance.

---

## Why is TCO useful?

* It allows writing **recursive functions without fear of stack overflow**, even for very deep recursion.
* Makes recursive algorithms more efficient in terms of memory.

---

## Example of Tail Call (Proper Tail Call)

```js
function factorial(n, acc = 1) {
  if (n <= 1) return acc;
  // The recursive call is the last action, tail call position
  return factorial(n - 1, n * acc);
}
console.log(factorial(5)); // 120
```

* The call to `factorial` inside the `return` is in tail position.
* TCO would reuse the current stack frame instead of adding a new one.

---

## What is NOT a tail call?

```js
function factorial(n) {
  if (n <= 1) return 1;
  return n * factorial(n - 1); // Not tail call, multiplication after recursion
}
```

* Here, after the recursive call, you still do `n * ...`.
* So it cannot optimize the call because it needs to keep the current frame until multiplication completes.

---

## Does JavaScript support TCO?

* The **ES6 specification requires proper tail calls (PTC)** in strict mode.
* **However, most JavaScript engines (like V8, SpiderMonkey) do NOT implement TCO yet** because of complexity and debugging concerns.
* So, TCO is often not available in practice, even if your code is written in a tail-recursive style.

---

## Summary

| Aspect                  | Explanation                                                        |
| ----------------------- | ------------------------------------------------------------------ |
| Tail Call               | Function call as the last operation                                |
| TCO                     | Reusing the current stack frame for tail calls                     |
| Benefit                 | Avoid stack overflow, improve recursive performance                |
| JS Support              | Specified in ES6, but mostly not implemented in engines            |
| How to write tail calls | Recursive call must be last expression without further computation |

---

## 🧠 Interview Tip

* Explain what a tail call is.
* Show example of tail recursive vs non-tail recursive functions.
* Mention ES6 spec vs real engine support.
* Explain why TCO matters (memory optimization).

---

## 98. What is Service Worker and how does it work in JavaScript?

**Service Workers** are a powerful feature in modern web development, especially for building **Progressive Web Apps (PWAs)** with offline capabilities, background sync, and more.

---

## What is a Service Worker?

* A **Service Worker** is a **JavaScript script** that runs in the **background**, separate from the web page.
* It acts as a **proxy between the web page and the network**, allowing you to intercept and handle network requests, cache assets, and provide offline functionality.
* It runs **event-driven**, without access to the DOM.
* Registered per origin and controlled by HTTPS (secure context).

---

## How Does a Service Worker Work?

### Lifecycle

1. **Register:** The web page registers the service worker (usually on page load).
2. **Install:** The browser installs the service worker — good place to cache assets.
3. **Activate:** Service worker takes control of pages (can clean up old caches here).
4. **Fetch:** Intercepts network requests and serves responses from cache or network.
5. **Sync & Push:** Can handle background sync and push notifications.

---

## Basic Example

```js
// Register service worker (in main JS file)
if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('/sw.js')
    .then(reg => console.log('Service Worker registered', reg))
    .catch(err => console.error('Registration failed', err));
}
```

```js
// sw.js - Service Worker script
self.addEventListener('install', event => {
  event.waitUntil(
    caches.open('my-cache-v1').then(cache => {
      return cache.addAll([
        '/',
        '/index.html',
        '/styles.css',
        '/app.js',
      ]);
    })
  );
});

self.addEventListener('fetch', event => {
  event.respondWith(
    caches.match(event.request).then(response => {
      return response || fetch(event.request);
    })
  );
});
```

---

## Key Points

* Runs **separately from the main thread**, so it doesn’t block UI.
* Can **intercept network requests** (`fetch` event).
* Provides **offline experience** by serving cached content.
* Can be updated independently from web pages.
* Works only over **HTTPS** (except localhost).

---

## Use Cases

* Offline caching and fallback pages.
* Background data sync.
* Push notifications.
* Performance improvements by caching static assets.

---

## Summary

| Feature          | Description                           |
| ---------------- | ------------------------------------- |
| Runs in          | Background thread, separate from page |
| Scope            | Per origin and path                   |
| Lifecycle events | `install`, `activate`, `fetch`, etc.  |
| Key abilities    | Cache resources, intercept requests   |
| Security         | Requires HTTPS                        |
| Use cases        | Offline, push notifications, caching  |

---

## 🧠 Interview Tip

* Define Service Worker as a background script for offline & network control.
* Explain registration, installation, activation, fetch interception.
* Give a simple caching example.
* Mention security (HTTPS) and lifecycle.

---

## 99. What are WeakMap and WeakSet?

**WeakMap** and **WeakSet** are special built-in JavaScript collections designed to help with **memory management** and **garbage collection** by holding "weak" references to objects.

---

## What is WeakMap?

* A **WeakMap** is a collection of key-value pairs where:

    * **Keys must be objects** (not primitive types).
    * The reference to the key is **weak** — meaning if there are no other references to the key object, it can be garbage collected.
* Values can be anything.
* Because keys are weakly held, **WeakMaps do not prevent garbage collection** of keys.
* WeakMaps are **not iterable** (no `.keys()`, `.values()`, or `.entries()` methods).

---

### Example of WeakMap

```js
let wm = new WeakMap();

let obj = { name: 'Alice' };
wm.set(obj, 'some metadata');

console.log(wm.get(obj)); // 'some metadata'

obj = null; // Now the key object has no references, can be garbage collected
// WeakMap entry will be removed automatically
```

---

## What is WeakSet?

* A **WeakSet** is a collection of **objects only** (no primitives).
* Like WeakMap, it holds **weak references** to the objects.
* Objects in a WeakSet can be garbage collected if no other references exist.
* WeakSets are **not iterable**.

---

### Example of WeakSet

```js
let ws = new WeakSet();

let obj = { name: 'Bob' };
ws.add(obj);

console.log(ws.has(obj)); // true

obj = null; // Object can be garbage collected, removed from WeakSet
```

---

## Key Differences from Map and Set

| Feature            | Map / Set                                     | WeakMap / WeakSet                                      |
| ------------------ | --------------------------------------------- | ------------------------------------------------------ |
| Keys / Values      | Keys can be primitives or objects             | Keys (WeakMap) / values (WeakSet) must be objects only |
| References         | Strong references                             | Weak references (don't prevent GC)                     |
| Iteration          | Iterable                                      | Not iterable                                           |
| Garbage Collection | Keys/values retained as long as in collection | Keys/values can be garbage collected if no other refs  |

---

## Why use WeakMap and WeakSet?

* To **avoid memory leaks** by not preventing garbage collection of unused objects.
* Useful for **storing metadata** or **private data** associated with objects without modifying them.
* In cases where you want **automatic cleanup** when the object is no longer referenced elsewhere.

---

## Summary

| Collection | Key/Value type            | Iterable? | Garbage collection behavior               | Use case                     |
| ---------- | ------------------------- | --------- | ----------------------------------------- | ---------------------------- |
| Map        | Any (primitive or object) | Yes       | Strong references; no GC while referenced | General key-value storage    |
| WeakMap    | Object keys only          | No        | Weak references; keys can be GC’d         | Metadata, private data       |
| Set        | Any                       | Yes       | Strong references                         | General unique value storage |
| WeakSet    | Objects only              | No        | Weak references; objects can be GC’d      | Tracking object existence    |

---

## 🧠 Interview Tip

* Emphasize **weak references** and how they enable better memory management.
* Mention **no iteration** and **object-only keys/values** restrictions.
* Give a simple example showing how objects can be garbage collected from WeakMap/WeakSet.

---

## 100. What are some common JavaScript memory leaks and how to avoid them?

Memory leaks in JavaScript can cause your web app to consume more and more memory over time, leading to poor performance or even crashing. Understanding common causes and how to avoid them is crucial, especially for interview prep.

---

## What is a Memory Leak?

A **memory leak** happens when your application **holds references to objects that are no longer needed**, preventing the garbage collector from freeing that memory.

---

## Common JavaScript Memory Leaks and How to Avoid Them

### 1. **Global Variables**

* Variables declared without `var`, `let`, or `const` automatically become global.
* Globals persist as long as the page is loaded, causing leaks if large objects are assigned.

**Avoid:**

* Always declare variables properly.
* Use IIFEs or modules to limit scope.

```js
// Leak
x = 10; // creates global variable unintentionally

// Fix
let x = 10;
```

---

### 2. **Forgotten Timers and Callbacks**

* `setInterval` or `setTimeout` callbacks that aren’t cleared keep references alive.
* Event listeners that aren’t removed also cause leaks.

**Avoid:**

* Clear timers when no longer needed (`clearInterval`, `clearTimeout`).
* Remove event listeners (`removeEventListener`) when appropriate.

```js
const interval = setInterval(() => {
  // do something
}, 1000);

// Later when not needed
clearInterval(interval);
```

---

### 3. **Closures Holding References**

* Closures keep references to outer scope variables.
* If closures are long-lived, they keep memory alive even if the outer scope is no longer used.

**Avoid:**

* Be mindful of what variables your closures capture.
* Nullify references if closure is no longer needed.

```js
function createClosure() {
  let largeObject = { /* big data */ };
  return function() {
    console.log(largeObject);
  };
}

const fn = createClosure();
// If fn lives long but largeObject is no longer needed, memory is retained.
```

---

### 4. **Detached DOM Nodes**

* If DOM nodes are removed from the document but still referenced by JavaScript, they can’t be garbage collected.

**Avoid:**

* Remove references to detached nodes.
* Use event delegation to reduce the need for attaching many listeners.

```js
let node = document.getElementById('myDiv');
document.body.removeChild(node);
// If you keep reference: node, it will still consume memory
node = null; // helps GC
```

---

### 5. **Unintended References in Data Structures**

* Objects stored in closures, arrays, or maps that are never cleaned up.

**Avoid:**

* Clean up references in data structures.
* Use `WeakMap` or `WeakSet` for caches to allow GC.

---

### 6. **Caching Without Limits**

* Storing huge amounts of data in memory (like caching images or responses) without limits causes leaks.

**Avoid:**

* Implement cache size limits.
* Use data structures that allow eviction (like LRU caches).

---

## Summary Table

| Leak Type                 | Cause                             | Avoidance                            |
| ------------------------- | --------------------------------- | ------------------------------------ |
| Global Variables          | Implicit globals                  | Always declare variables properly    |
| Timers and Callbacks      | Not clearing intervals/timeouts   | Clear timers, remove listeners       |
| Closures                  | Holding large references          | Manage closure variables carefully   |
| Detached DOM Nodes        | References to removed elements    | Nullify references, event delegation |
| Data Structure References | Persistent objects in collections | Clean up, use WeakMap/WeakSet        |
| Unlimited Caches          | Unbounded memory usage            | Implement limits and evictions       |

---

## 🧠 Interview Tip

* Explain what memory leaks are in JS context.
* Mention common patterns causing leaks.
* Describe practical ways to avoid or fix leaks.
* Optionally mention browser tools (Chrome DevTools) for detecting leaks.

---