Here are the **Top 50 JavaScript Interview Questions with Answers**, curated specifically for someone with **3 years of experience** — covering **fundamentals, ES6+, asynchronous concepts, and DOM manipulation**, which are commonly expected at that level.

---

## ✅ Top 50 JavaScript Interview Questions (3 Years Experience)

---

### 🔹 **1. What are the different data types in JavaScript?**
- Primitive: `String`, `Number`, `Boolean`, `Null`, `Undefined`, `Symbol`, `BigInt`
- Non-primitive: `Object`, `Array`, `Function`

---

### 🔹 **2. What is the difference between `==` and `===`?**
- `==`: compares **value**, with type coercion
- `===`: compares **value and type** (strict equality)

---

### 🔹 **3. What is hoisting in JavaScript?**
Variable and function declarations are moved to the top of their scope during compilation phase.

---

### 🔹 **4. What is a closure?**
A closure is a function that has access to its outer function's scope even after the outer function has returned.

---

### 🔹 **5. Explain `var`, `let`, and `const`.**
- `var`: function-scoped, hoisted
- `let`: block-scoped, not hoisted to the top of block
- `const`: block-scoped, read-only after declaration

---

### 🔹 **6. What is the difference between `null` and `undefined`?**
- `null`: intentional absence of value
- `undefined`: variable declared but not assigned a value

---

### 🔹 **7. What are arrow functions?**
Shorter syntax for function expressions. They don't bind `this`.

```js
const add = (a, b) => a + b;
```

---

### 🔹 **8. What is the use of `this` keyword?**
Refers to the object from which a function was called, varies based on context.

---

### 🔹 **9. What is event bubbling and capturing?**
- **Bubbling**: event propagates from child to parent
- **Capturing**: event propagates from parent to child

---

### 🔹 **10. What is a promise in JavaScript?**
An object that represents the eventual completion (or failure) of an asynchronous operation.

---

### 🔹 **11. Difference between `call()`, `apply()`, and `bind()`?**
- `call`: invokes function with arguments, one by one
- `apply`: invokes function with arguments as an array
- `bind`: returns a new function with bound context

---

### 🔹 **12. What are template literals?**
Allow embedded expressions in strings using backticks:

```js
let name = `Aditya`;
let msg = `Hello, ${name}`;
```

---

### 🔹 **13. What is destructuring in JavaScript?**
Extracting values from arrays or objects into variables.

```js
const [a, b] = [1, 2];
const {name} = {name: "Aditya"};
```

---

### 🔹 **14. What are higher-order functions?**
Functions that take other functions as arguments or return functions.

---

### 🔹 **15. What is the difference between `map()`, `filter()`, and `reduce()`?**
- `map()`: transforms array elements
- `filter()`: filters array elements
- `reduce()`: reduces array to a single value

---

### 🔹 **16. What are async/await?**
Syntactic sugar over promises for handling async operations in a cleaner way.

---

### 🔹 **17. What is the event loop in JavaScript?**
Handles asynchronous operations via the call stack and message queue (task/microtask queue).

---

### 🔹 **18. What is the difference between synchronous and asynchronous code?**
- Synchronous: blocks execution
- Asynchronous: non-blocking, executes later via callbacks/promises

---

### 🔹 **19. What is a callback function?**
A function passed as an argument to another function and executed later.

---

### 🔹 **20. What is the difference between `forEach` and `map`?**
- `forEach`: executes a function for each item, doesn't return anything
- `map`: transforms array and returns a new one

---

### 🔹 **21. What is scope and lexical scope?**
- **Scope**: current context of execution
- **Lexical scope**: scope determined by where variables/functions are declared

---

### 🔹 **22. What is the `typeof` operator?**
Returns the type of a variable.

```js
typeof "hello" // "string"
```

---

### 🔹 **23. What is a pure function?**
Function with no side effects and returns same output for same input.

---

### 🔹 **24. What is immutability in JavaScript?**
Data that cannot be changed once created. Promoted using methods like `Object.freeze()` or spread operator for copying.

---

### 🔹 **25. What is the spread operator?**
Expands iterable into individual elements:

```js
const arr = [1, 2];
const copy = [...arr];
```

---

### 🔹 **26. What are rest parameters?**
Collects remaining arguments into an array.

```js
function sum(...nums) {
  return nums.reduce((a, b) => a + b);
}
```

---

### 🔹 **27. What is the DOM?**
Document Object Model — structured representation of HTML, allows interaction via JavaScript.

---

### 🔹 **28. How do you manipulate DOM elements using JavaScript?**
Using methods like:
- `document.getElementById`
- `document.querySelector`
- `element.innerText`, `element.innerHTML`
- `element.style`

---

### 🔹 **29. What is the difference between `==` and `Object.is()`?**
- `==`: loose equality
- `Object.is()`: strict equality with handling for `NaN`, `-0`

---

### 🔹 **30. What is the difference between shallow copy and deep copy?**
- **Shallow copy**: references nested objects
- **Deep copy**: copies all nested objects/values

---

### 🔹 **31. How do you handle errors in JavaScript?**
Using `try...catch`, `throw`, and `.catch()` with promises.

---

### 🔹 **32. What is an IIFE (Immediately Invoked Function Expression)?**
A function that runs immediately after it's defined.

```js
(function() {
  console.log("Hello");
})();
```

---

### 🔹 **33. What is the difference between function declaration and function expression?**
- **Declaration**: hoisted
- **Expression**: not hoisted

---

### 🔹 **34. What are modules in JavaScript?**
Code split into reusable files using `export` and `import`.

---

### 🔹 **35. What are default parameters?**
Allows function to have default values.

```js
function greet(name = "Guest") {
  console.log("Hello", name);
}
```

---

### 🔹 **36. What is optional chaining (`?.`)?**
Safely access deeply nested properties:

```js
obj?.user?.profile?.name
```

---

### 🔹 **37. What is nullish coalescing (`??`)?**
Returns right-hand operand when left-hand is `null` or `undefined`.

```js
let name = userInput ?? "Default";
```

---

### 🔹 **38. How to debounce a function in JavaScript?**
Throttle execution to prevent excessive function calls (used in search, resize, etc.).

---

### 🔹 **39. What is a promise chain?**
Series of `.then()` calls to handle sequential async tasks.

---

### 🔹 **40. What is a memory leak in JavaScript?**
Unintended memory retained due to unused references or closures.

---

### 🔹 **41. What is garbage collection?**
Automatic memory cleanup for unreachable objects.

---

### 🔹 **42. What are the falsy values in JavaScript?**
`false`, `0`, `""`, `null`, `undefined`, `NaN`

---

### 🔹 **43. What are generators?**
Functions that can be paused and resumed using `function*` and `yield`.

---

### 🔹 **44. Difference between `document.ready()` and `window.onload`?**
- `ready()`: DOM is loaded
- `onload`: all resources including images are loaded

---

### 🔹 **45. How to clone an object in JavaScript?**
- `Object.assign({}, obj)`
- `{...obj}`
- `JSON.parse(JSON.stringify(obj))` (for deep copy)

---

### 🔹 **46. What is the temporal dead zone?**
Time between `let/const` declaration and initialization where accessing it throws an error.

---

### 🔹 **47. How is `this` handled inside arrow functions?**
Arrow functions don’t bind `this`; it inherits from parent scope.

---

### 🔹 **48. What are function currying and partial application?**
Breaking a function with multiple arguments into nested functions accepting one argument at a time.

---

### 🔹 **49. What is event delegation?**
Handling events at a parent level instead of child, using event bubbling.

---

### 🔹 **50. What tools are used to debug JavaScript code?**
- Browser DevTools
- `console.log`, `debugger`
- ESLint
- Source maps in production

---

Let me know if you want:
- A **PDF version** of these questions
- 50 **JavaScript coding questions**
- Or the **next set for React, Node.js, or frontend interview prep**

Would you like to continue with **React JS interview questions** next?