Here are the **Top 50 JavaScript Interview Questions and Answers** tailored for someone with **1 year of experience**. These questions focus on core concepts, syntax, and real-world scenarios often asked during junior developer interviews.

---

## 🧠 Top 50 JavaScript Interview Questions (1 Year Experience)

---

### ✅ **Basics & Fundamentals**

1. **What is JavaScript?**  
   A scripting language used to create and control dynamic website content.

2. **Difference between var, let, and const?**
    - `var`: Function-scoped, hoisted
    - `let`: Block-scoped, not hoisted
    - `const`: Block-scoped, read-only after declaration

3. **What are data types in JavaScript?**
    - Primitive: `string`, `number`, `boolean`, `null`, `undefined`, `symbol`, `bigint`
    - Non-primitive: `object`, `array`, `function`

4. **What is the difference between == and ===?**
    - `==`: Loose equality (type conversion)
    - `===`: Strict equality (no type conversion)

5. **What is hoisting in JavaScript?**  
   Variable and function declarations are moved to the top of their scope before execution.

6. **What is a closure?**  
   A function that remembers variables from its outer lexical scope even after that scope has closed.

7. **What is the difference between null and undefined?**
    - `null`: Intentional absence of value
    - `undefined`: A variable that has been declared but not assigned a value

8. **What is NaN in JavaScript?**  
   Not-a-Number — result of an invalid or undefined mathematical operation.

9. **How does `typeof` operator work?**  
   It returns the type of a variable, e.g., `typeof "hello"` returns `"string"`.

10. **What is the difference between function declaration and expression?**
- Declaration: `function foo() {}` (hoisted)
- Expression: `const foo = function() {}` (not hoisted)

---

### ✅ **Control Structures & Operators**

11. **What are truthy and falsy values?**  
    Falsy: `0`, `""`, `null`, `undefined`, `NaN`, `false`  
    Everything else is truthy.

12. **What are logical operators in JavaScript?**  
    `&&`, `||`, `!`

13. **Explain ternary operator.**  
    `condition ? expr1 : expr2`

14. **What is a switch statement?**  
    Control structure used to perform different actions based on different conditions.

15. **What is a loop in JavaScript?**  
    A way to execute a block of code repeatedly. Common types: `for`, `while`, `do...while`.

---

### ✅ **Functions & Scope**

16. **What is lexical scope?**  
    Scope defined at the time of writing code, based on where variables and blocks are physically located.

17. **What is the difference between global and local scope?**
- Global: Accessible from anywhere
- Local: Defined within a function/block

18. **What are arrow functions?**  
    A shorter syntax for writing functions:  
    `const add = (a, b) => a + b`

19. **What are callback functions?**  
    A function passed as an argument to another function, to be executed later.

20. **What is the difference between synchronous and asynchronous code?**
- Synchronous: Executes line by line
- Asynchronous: Doesn’t block execution (e.g., `setTimeout`, Promises)

---

### ✅ **Arrays & Objects**

21. **What are arrays in JavaScript?**  
    An ordered list of values:  
    `const arr = [1, 2, 3];`

22. **How to loop through an array?**  
    Using `for`, `for...of`, `forEach()`, `map()`, etc.

23. **What are array methods in JavaScript?**  
    `push`, `pop`, `shift`, `unshift`, `slice`, `splice`, `map`, `filter`, `reduce`

24. **What is the difference between map and forEach?**
- `map` returns a new array
- `forEach` just iterates, doesn't return anything

25. **What is an object in JavaScript?**  
    A collection of key-value pairs:  
    `const user = { name: "Aditya", age: 25 };`

26. **How to access object properties?**  
    Using dot `obj.key` or bracket `obj["key"]` notation.

27. **What is object destructuring?**  
    Extracting values:
   ```js
   const {name, age} = user;
   ```

---

### ✅ **ES6+ Concepts**

28. **What is the spread operator?**  
    `...` expands an iterable into individual elements.

29. **What is rest parameter?**  
    Collects arguments into an array:
   ```js
   function sum(...args) { }
   ```

30. **What is a template literal?**  
    String with embedded expressions:
   ```js
   `Hello, ${name}`
   ```

31. **What are default parameters?**  
    Function parameters with default values:
   ```js
   function greet(name = "Guest") { }
   ```

---

### ✅ **DOM & Events**

32. **What is the DOM?**  
    Document Object Model — represents the structure of a web page.

33. **How to select elements in the DOM?**  
    `getElementById`, `querySelector`, `getElementsByClassName`, etc.

34. **What is event bubbling?**  
    Events propagate from the innermost element to the outermost.

35. **How to handle events in JavaScript?**  
    Using `addEventListener`:
   ```js
   element.addEventListener("click", handler);
   ```

---

### ✅ **Async JavaScript**

36. **What is a Promise?**  
    An object representing eventual completion or failure of an async operation.

37. **What are the states of a Promise?**
- Pending
- Fulfilled
- Rejected

38. **What is async/await?**  
    Syntax to work with Promises in a synchronous manner.

39. **What is `setTimeout()`?**  
    Delays execution of a function.

40. **What is `setInterval()`?**  
    Repeatedly calls a function with a fixed time delay.

---

### ✅ **Miscellaneous**

41. **What is event delegation?**  
    A technique where a single event listener handles events for multiple child elements.

42. **What is a higher-order function?**  
    A function that takes another function as argument or returns a function.

43. **What is the use of `this` keyword?**  
    Refers to the current execution context.

44. **What is type coercion?**  
    Automatic or implicit conversion of values to another type.

45. **What is the difference between deep copy and shallow copy?**
- **Shallow**: Copies reference
- **Deep**: Recursively copies all levels

46. **What is `localStorage` and `sessionStorage`?**  
    Web storage APIs to store data in the browser.
- `localStorage`: Persistent
- `sessionStorage`: Temporary

47. **How is error handling done in JS?**  
    Using `try...catch` blocks.

48. **What is the `arguments` object?**  
    An array-like object available inside all non-arrow functions.

49. **What is a module in JavaScript?**  
    A way to encapsulate code and export/import between files.

50. **How to export and import in ES6 modules?**
- Export: `export default` or `export {}`
- Import: `import x from 'file'`

---

Want a **PDF version** of these questions? Or shall I move on to **React JS**, **Node.js**, or scenario-based JavaScript interview questions next?