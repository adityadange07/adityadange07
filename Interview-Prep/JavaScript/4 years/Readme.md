Here are the **Top 50 JavaScript Interview Questions with Answers** tailored for someone with **4 years of experience** — covering core concepts, ES6+, DOM manipulation, async handling, performance, and best practices.

---

## 🔥 Top 50 JavaScript Interview Questions (4 Years Experience)

---

### ✅ **1. What are the different data types in JavaScript?**
- Primitive: `String`, `Number`, `BigInt`, `Boolean`, `Undefined`, `Symbol`, `Null`
- Non-Primitive: `Object`, `Array`, `Function`

---

### ✅ **2. What is the difference between `==` and `===`?**
- `==` compares values after type coercion.
- `===` compares values and types strictly.

---

### ✅ **3. What are closures in JavaScript?**
A closure is a function that remembers its lexical scope even when the function is executed outside that scope.

```js
function outer() {
  let count = 0;
  return function inner() {
    return ++count;
  };
}
```

---

### ✅ **4. Explain `let`, `const`, and `var`.**
- `var`: Function-scoped, hoisted
- `let`: Block-scoped, no hoisting
- `const`: Block-scoped, immutable reference

---

### ✅ **5. What is hoisting in JavaScript?**
Variables and function declarations are moved to the top of their scope before code execution.

---

### ✅ **6. What is the difference between `null` and `undefined`?**
- `undefined`: variable declared but not assigned
- `null`: explicit assignment representing "no value"

---

### ✅ **7. What is the event loop in JavaScript?**
It's the mechanism that handles asynchronous callbacks via a queue system (`call stack`, `event queue`, `web APIs`, `microtasks`).

---

### ✅ **8. What are promises in JavaScript?**
Promises handle asynchronous operations.
```js
new Promise((resolve, reject) => {
  resolve("Success");
});
```

---

### ✅ **9. What is async/await in JavaScript?**
Syntactic sugar over promises to write asynchronous code in a synchronous manner.
```js
async function fetchData() {
  const res = await fetch(url);
}
```

---

### ✅ **10. What is the difference between `map()`, `filter()`, and `reduce()`?**
- `map`: Transforms array items
- `filter`: Filters items based on condition
- `reduce`: Reduces array to a single value

---

### ✅ **11. What is destructuring?**
Extracting values from arrays/objects into variables.
```js
const { name, age } = user;
```

---

### ✅ **12. What are template literals?**
String literals allowing embedded expressions: `` `Hello ${name}` ``

---

### ✅ **13. What is the `this` keyword in JavaScript?**
Refers to the object that is executing the current function.

---

### ✅ **14. Difference between arrow functions and regular functions?**
- Arrow functions don’t bind their own `this`
- Cannot be used as constructors
- No `arguments` object

---

### ✅ **15. What is a callback function?**
A function passed as an argument to another function and executed later.

---

### ✅ **16. What are higher-order functions?**
Functions that take other functions as arguments or return them.

---

### ✅ **17. What is the difference between `call`, `apply`, and `bind`?**
- `call`: `func.call(obj, arg1, arg2)`
- `apply`: `func.apply(obj, [arg1, arg2])`
- `bind`: Returns a new function with `this` bound

---

### ✅ **18. Explain prototypal inheritance.**
Objects inherit from other objects via the prototype chain.

---

### ✅ **19. What is the difference between shallow copy and deep copy?**
- Shallow copy copies only the first level
- Deep copy recursively copies all levels

---

### ✅ **20. What is event delegation?**
Attaching a single event listener to a parent element to manage events on its children.

---

### ✅ **21. What are IIFEs (Immediately Invoked Function Expressions)?**
Functions that run as soon as they are defined.
```js
(function() { console.log("IIFE"); })();
```

---

### ✅ **22. What is a debounce function?**
A function that delays execution until a specified time has passed since the last call.

---

### ✅ **23. What is throttling in JavaScript?**
Throttling limits function execution to once per specified time.

---

### ✅ **24. What is the difference between synchronous and asynchronous code?**
- Synchronous: Blocks execution
- Asynchronous: Does not block; uses callbacks, promises, async/await

---

### ✅ **25. What is the use of `Symbol` in JavaScript?**
Used to create unique object keys, often for meta-programming.

---

### ✅ **26. What is the difference between `Object.freeze()` and `Object.seal()`?**
- `freeze`: Makes object immutable
- `seal`: Prevents new properties, allows value change

---

### ✅ **27. What is the spread and rest operator?**
- Spread: Expands iterable `...arr`
- Rest: Collects arguments `function(...args)`

---

### ✅ **28. What is the difference between `forEach` and `map`?**
- `forEach`: Iterates but doesn't return
- `map`: Returns a new array

---

### ✅ **29. What is the difference between deep and shallow equality?**
- Shallow: Compares references
- Deep: Compares structure and values recursively

---

### ✅ **30. What is a memory leak in JavaScript?**
When allocated memory is not released even though it's no longer used.

---

### ✅ **31. How to prevent memory leaks?**
- Remove event listeners
- Use weak references
- Avoid global variables

---

### ✅ **32. What are JavaScript modules?**
Files that export and import code using `export`/`import`.

---

### ✅ **33. What is currying in JavaScript?**
Transforming a function with multiple arguments into a sequence of functions.
```js
function curry(a) {
  return function(b) {
    return a + b;
  }
}
```

---

### ✅ **34. What is composition in JavaScript?**
Combining functions to build complex behavior.

---

### ✅ **35. What is the Temporal Dead Zone?**
Time between variable declaration and initialization where access results in a `ReferenceError`.

---

### ✅ **36. Explain the concept of microtasks and macrotasks.**
- Microtasks: `Promise.then`, `MutationObserver`
- Macrotasks: `setTimeout`, `setInterval`, `setImmediate`

---

### ✅ **37. What are WeakMap and WeakSet?**
Collections that hold weak references, allowing garbage collection.

---

### ✅ **38. What is a generator function?**
Functions that can pause execution using `yield`.
```js
function* gen() {
  yield 1;
  yield 2;
}
```

---

### ✅ **39. What is event bubbling and capturing?**
- Bubbling: Inner to outer
- Capturing: Outer to inner

---

### ✅ **40. What is optional chaining `?.`?**
Safely access nested properties without errors.

---

### ✅ **41. What is nullish coalescing `??`?**
Returns the right-hand side if left-hand is `null` or `undefined`.

---

### ✅ **42. What is `typeof` and `instanceof`?**
- `typeof`: Returns data type as string
- `instanceof`: Checks prototype inheritance

---

### ✅ **43. How does JavaScript handle concurrency?**
Via the event loop, web APIs, and the call stack.

---

### ✅ **44. What are service workers?**
Background scripts for offline support, caching, and push notifications.

---

### ✅ **45. What are some ES6 features you use regularly?**
- Arrow functions
- Destructuring
- Promises
- let/const
- Spread/Rest
- Modules

---

### ✅ **46. How does JavaScript garbage collection work?**
Uses mark-and-sweep algorithm to remove unreachable objects.

---

### ✅ **47. What are the falsy values in JavaScript?**
`false`, `0`, `''`, `null`, `undefined`, `NaN`

---

### ✅ **48. How do you clone an object in JavaScript?**
```js
const clone = { ...obj };  
const deepClone = JSON.parse(JSON.stringify(obj));
```

---

### ✅ **49. What is the use of `Object.assign()`?**
Copies properties from source to target object.

---

### ✅ **50. What is Tail Call Optimization (TCO)?**
An optimization technique to reuse stack frames for recursive calls in tail position (currently not widely supported).

---

Would you like these in **PDF format**, or should I move on to **React JS** or **System Design for Frontend** questions next?