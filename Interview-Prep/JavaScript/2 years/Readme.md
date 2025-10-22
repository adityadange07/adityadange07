Here are the **Top 50 JavaScript Interview Questions and Answers** tailored for someone with around **2 years of experience**. This covers core concepts, ES6 features, browser behavior, and some hands-on coding logic expected at your level.

---

## 🔥 Top 50 JavaScript Interview Questions (2 Years Experience)

---

### ✅ **1. What are the data types in JavaScript?**
- Primitive: String, Number, Boolean, Null, Undefined, BigInt, Symbol
- Non-Primitive: Object (including Arrays and Functions)

---

### ✅ **2. What is the difference between `==` and `===`?**
- `==` compares **value only** (type coercion)
- `===` compares **value and type** (strict equality)

---

### ✅ **3. What are var, let, and const?**
- `var`: Function scoped, can be redeclared
- `let`: Block scoped, can't be redeclared
- `const`: Block scoped, immutable (value can't change for primitives)

---

### ✅ **4. What is hoisting in JavaScript?**
Hoisting is JavaScript's default behavior of moving declarations to the top of the scope during compilation.

---

### ✅ **5. What is the difference between null and undefined?**
- `null`: Assigned value meaning "no value"
- `undefined`: Variable declared but not assigned a value

---

### ✅ **6. What are closures in JavaScript?**
A closure is a function that remembers its outer variables even after the outer function has finished executing.

---

### ✅ **7. What is the use of arrow functions?**
Arrow functions provide a shorter syntax and do **not have their own `this`** binding.

---

### ✅ **8. What is the difference between function declaration and function expression?**
- **Declaration**: `function add() {}` (hoisted)
- **Expression**: `const add = function() {}` (not hoisted)

---

### ✅ **9. Explain event bubbling and capturing.**
- **Bubbling**: Event propagates from child to parent (default)
- **Capturing**: Event propagates from parent to child

---

### ✅ **10. How does `this` work in JavaScript?**
It refers to the object on which a function is called. It behaves differently in arrow functions, strict mode, and event listeners.

---

### ✅ **11. What are template literals?**
Template strings using backticks (`` ` ``) allowing interpolation:
```js
`Hello, ${name}`
```

---

### ✅ **12. What are JavaScript Promises?**
Promises represent the eventual completion (or failure) of an asynchronous operation.

---

### ✅ **13. What are async and await?**
Syntactic sugar over Promises for writing asynchronous code in a synchronous-like manner.

---

### ✅ **14. What is the difference between `map`, `forEach`, `filter`, and `reduce`?**
- `map`: Returns a new array
- `forEach`: Iterates without returning
- `filter`: Returns a new array with matched elements
- `reduce`: Accumulates into a single value

---

### ✅ **15. What is the spread operator?**
Expands an iterable into individual elements:
```js
let newArr = [...arr1, ...arr2];
```

---

### ✅ **16. What is the rest parameter?**
Condenses arguments into a single array:
```js
function sum(...nums) {}
```

---

### ✅ **17. Difference between synchronous and asynchronous code?**
- **Synchronous**: Executes line by line
- **Asynchronous**: Executes without blocking, using callbacks/promises/async-await

---

### ✅ **18. What are callbacks?**
Functions passed as arguments to be executed after another function finishes.

---

### ✅ **19. What is event delegation?**
Attaching an event listener to a parent instead of each child for better performance.

---

### ✅ **20. What is a higher-order function?**
A function that takes or returns another function.

---

### ✅ **21. Explain debouncing and throttling.**
- **Debouncing**: Delays function execution until after a pause
- **Throttling**: Limits function execution rate

---

### ✅ **22. What is NaN in JavaScript?**
“Not-a-Number”; returned when a mathematical operation fails (e.g., `0 / "hello"`)

---

### ✅ **23. What is the difference between `typeof` and `instanceof`?**
- `typeof`: Checks primitive type
- `instanceof`: Checks object type via prototype chain

---

### ✅ **24. What is a prototype?**
Every JS object has a prototype from which it can inherit methods and properties.

---

### ✅ **25. What is prototypal inheritance?**
An object can inherit properties and methods from another using `__proto__` or `Object.create()`.

---

### ✅ **26. What is the difference between call(), apply(), and bind()?**
- `call`: Invokes with comma-separated args
- `apply`: Invokes with array of args
- `bind`: Returns a new function with `this` bound

---

### ✅ **27. What is an IIFE?**
Immediately Invoked Function Expression:
```js
(function() {
  console.log("IIFE");
})();
```

---

### ✅ **28. What is the event loop in JavaScript?**
Handles async tasks using the call stack, task queue, and microtask queue.

---

### ✅ **29. Explain setTimeout and setInterval.**
- `setTimeout`: Delays execution once
- `setInterval`: Executes repeatedly at intervals

---

### ✅ **30. What are truthy and falsy values?**
Falsy: `false`, `0`, `""`, `null`, `undefined`, `NaN`  
Everything else is truthy.

---

### ✅ **31. What is destructuring in JavaScript?**
Extracting values from arrays or objects:
```js
const {name} = obj;
const [first] = arr;
```

---

### ✅ **32. What is object shorthand in ES6?**
Property shorthand when variable and key names are the same:
```js
let a = 1;
let obj = { a }; // same as { a: a }
```

---

### ✅ **33. What are default parameters?**
Setting default values in function arguments:
```js
function greet(name = "Guest") {}
```

---

### ✅ **34. What is a Symbol?**
A unique and immutable primitive often used as object keys to avoid property collisions.

---

### ✅ **35. What is the difference between Array and Object in JS?**
- Arrays are ordered collections
- Objects are key-value pairs without guaranteed order

---

### ✅ **36. What is `use strict`?**
Enables strict mode, catching common coding errors (e.g., undeclared variables)

---

### ✅ **37. What is a shallow copy vs deep copy?**
- **Shallow**: Copies top-level only (`Object.assign()`, spread)
- **Deep**: Copies all nested levels (e.g., `structuredClone()` or recursion)

---

### ✅ **38. How to clone an object?**
```js
let clone = {...obj};
// or
let clone = JSON.parse(JSON.stringify(obj));
```

---

### ✅ **39. How to check if a variable is an array?**
```js
Array.isArray(arr)
```

---

### ✅ **40. What is `typeof null`?**
Returns `'object'`, a historical bug in JavaScript.

---

### ✅ **41. What is the difference between localStorage and sessionStorage?**
- `localStorage`: persists even after browser close
- `sessionStorage`: cleared when tab is closed

---

### ✅ **42. What is the use of `hasOwnProperty`?**
Checks if a property is directly present in the object, not inherited.

---

### ✅ **43. How to remove duplicates from an array?**
```js
let unique = [...new Set(arr)];
```

---

### ✅ **44. What is the output of `[] + []` and `[] + {}`?**
```js
[] + [] => ""  
[] + {} => "[object Object]"
```

---

### ✅ **45. What is the difference between `Object.freeze()` and `Object.seal()`?**
- `freeze`: No modification or addition
- `seal`: Can't add/remove, but can modify existing

---

### ✅ **46. What are generators in JavaScript?**
Functions that can pause/resume execution using `function*` and `yield`.

---

### ✅ **47. What are modules in JavaScript?**
Used to import/export code between files using `import` and `export`.

---

### ✅ **48. How is memory managed in JavaScript?**
JavaScript uses automatic garbage collection to reclaim unused memory.

---

### ✅ **49. What are WeakMap and WeakSet?**
Similar to Map/Set but keys are weakly referenced (eligible for GC).

---

### ✅ **50. How do you handle errors in JavaScript?**
Using `try`, `catch`, `finally`, and `throw` statements.

---

Would you like:
- A **PDF version** of these questions?
- A follow-up set with **code challenges** or **JavaScript project questions**?
- Or shall we move to **React JS interview questions** next?

Let me know how you'd like to continue!