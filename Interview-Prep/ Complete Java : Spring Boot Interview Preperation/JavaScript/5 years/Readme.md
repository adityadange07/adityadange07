Here are the **Top 50 JavaScript Interview Questions and Answers**, tailored for someone with **5 years of experience**, covering **ES6+ features**, **asynchronous programming**, **DOM manipulation**, **OOP**, **design patterns**, **performance optimization**, and more.

---

## ✅ Top 50 JavaScript Interview Questions (5 Years Experience)

---

### 🔹 **Core Concepts**

1. **What is the difference between `var`, `let`, and `const`?**
    - `var`: Function-scoped, hoisted
    - `let`/`const`: Block-scoped
    - `const`: Immutable binding (not value)

---

2. **What are JavaScript data types?**
    - Primitive: `string`, `number`, `boolean`, `null`, `undefined`, `bigint`, `symbol`
    - Reference: `object`, `array`, `function`

---

3. **Explain hoisting in JavaScript.**  
   Variable and function declarations are moved to the top of their scope before code execution.

---

4. **What is the difference between `==` and `===`?**
    - `==`: Loose equality, performs type coercion
    - `===`: Strict equality, no coercion

---

5. **What are closures in JavaScript?**  
   A closure is a function that retains access to its lexical scope even when executed outside that scope.

---

6. **Explain scope and types in JS.**
    - Global Scope
    - Function Scope
    - Block Scope (`let`, `const`)

---

7. **What is the Temporal Dead Zone (TDZ)?**  
   The time between variable hoisting and its declaration where accessing it throws a ReferenceError.

---

8. **Difference between function declaration and expression?**
    - Declaration: `function fn() {}` (hoisted)
    - Expression: `const fn = function() {}` (not hoisted)

---

9. **What is the 'this' keyword in JavaScript?**  
   Refers to the object it belongs to. Its value depends on how a function is called.

---

10. **What is the difference between arrow functions and regular functions?**
- Arrow functions don't have their own `this`, `arguments`, or `super`.

---

### 🔹 **Asynchronous JavaScript**

11. **What is the event loop in JavaScript?**  
    A mechanism that handles async operations via a queue and the call stack.

---

12. **Difference between microtasks and macrotasks?**
- Microtasks (e.g., Promises) run before the next event loop tick
- Macrotasks (e.g., `setTimeout`) run after microtasks

---

13. **What is a Promise and its states?**
- States: `pending`, `fulfilled`, `rejected`
- Used to handle async operations

---

14. **How do async/await work in JS?**  
    `async` functions return a Promise; `await` pauses execution until the Promise resolves.

---

15. **What is callback hell and how to avoid it?**  
    Nested callbacks => messy code. Avoid using Promises or async/await.

---

16. **How do you handle errors in async/await?**  
    Use `try...catch` blocks.

---

17. **What is the difference between `Promise.all`, `Promise.any`, `Promise.race`?**
- `all`: Waits for all
- `any`: Waits for first resolved
- `race`: First settled (resolve/reject)

---

### 🔹 **Advanced Concepts**

18. **What is currying in JavaScript?**  
    Transforming a function with multiple arguments into a sequence of functions with one argument.

---

19. **What is memoization?**  
    Caching the result of function calls to improve performance.

---

20. **Explain debouncing and throttling.**
- Debounce: Delay until pause
- Throttle: Limit execution rate

---

21. **What is the difference between `call`, `apply`, and `bind`?**
- `call`: Calls with `this`, individual args
- `apply`: Calls with `this`, args as array
- `bind`: Returns a new function with bound `this`

---

22. **Explain prototypal inheritance.**  
    Objects inherit from other objects via `[[Prototype]]`.

---

23. **What is the difference between `Object.create()` and constructor functions?**
- `Object.create()`: Directly sets prototype
- Constructor: Uses `new` keyword, adds properties inside function

---

24. **How does garbage collection work in JS?**  
    JS uses mark-and-sweep to clean up unreferenced memory.

---

25. **What is an IIFE?**  
    Immediately Invoked Function Expression:
   ```js
   (function() { /* code */ })();
   ```

---

26. **What is a module in JavaScript?**
- Encapsulated code in ES6 using `import`/`export` statements.

---

27. **What are symbols in JS?**  
    A unique and immutable primitive used as object property keys.

---

28. **What is event delegation?**  
    Using a single event listener on a parent to handle events for child elements.

---

29. **What is a higher-order function?**  
    A function that takes or returns another function.

---

30. **Explain spread vs rest operator.**
- Spread: Expands elements
- Rest: Collects remaining elements

---

### 🔹 **DOM & Browser APIs**

31. **How do you select elements from DOM?**  
    `getElementById`, `querySelector`, `querySelectorAll`

---

32. **How to create and append elements dynamically?**
   ```js
   const el = document.createElement('div');  
   parent.appendChild(el);
   ```

---

33. **What is event bubbling and capturing?**  
    Bubbling: Event moves from child to parent  
    Capturing: Parent to child

---

34. **What is localStorage vs sessionStorage?**
- localStorage: persists across sessions
- sessionStorage: per tab/session

---

35. **Difference between `DOMContentLoaded` and `load`?**
- `DOMContentLoaded`: After HTML is parsed
- `load`: After all resources (images, scripts) are loaded

---

36. **How do you prevent default behavior in JS?**  
    `event.preventDefault()`

---

37. **How do you stop event propagation?**  
    `event.stopPropagation()`

---

38. **What is the difference between `innerHTML`, `textContent`, `innerText`?**
- `innerHTML`: Includes HTML
- `textContent`: All text
- `innerText`: Visible text only

---

### 🔹 **OOP in JS**

39. **What are classes in JS?**  
    ES6 syntax for constructor functions with inheritance.

---

40. **What is encapsulation in JavaScript?**  
    Wrapping data and behavior into objects, hiding implementation using closures or `#private` fields.

---

41. **Explain inheritance using `extends` and `super`.**  
    `extends` is used to inherit from another class.  
    `super()` calls the parent constructor.

---

42. **What is polymorphism in JS?**  
    Different classes can define methods with the same name but different behavior.

---

### 🔹 **ES6+ Features**

43. **What are template literals?**  
    Multi-line strings and expression interpolation using backticks.

---

44. **What are destructuring assignments?**  
    Unpack values from arrays/objects into distinct variables.

---

45. **Explain optional chaining `?.` and nullish coalescing `??`.**
- `?.`: Avoid errors when accessing nested properties
- `??`: Fallback for `null`/`undefined`

---

46. **What is a Set and Map in JS?**
- **Set**: Unique values
- **Map**: Key-value pairs with any data type as key

---

47. **What is the use of `Object.freeze()` and `Object.seal()`?**
- `freeze`: Makes object immutable
- `seal`: Prevents new properties, but allows value updates

---

48. **What are generator functions?**  
    Functions that yield multiple values over time using `function*` and `yield`.

---

### 🔹 **Testing & Tools**

49. **What is the difference between unit and integration testing?**
- Unit: Tests isolated functions
- Integration: Tests interactions between modules/components

---

50. **How do you debug JavaScript code effectively?**
- Use `console.log()`, browser DevTools, breakpoints, `debugger` keyword

---

Would you like a **PDF**, or should I prepare **React + JavaScript combined interview questions**, or go into **JavaScript system design patterns**, or **real-time coding challenges**?