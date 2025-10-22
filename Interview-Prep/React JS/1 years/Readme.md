Here’s a curated list of the **Top 50 React JS Interview Questions** tailored for someone with **1 year of experience**. These cover basic to intermediate concepts, ideal for junior frontend developer roles or entry-level full-stack developers.

---

## ✅ Top 50 React JS Interview Questions (1 Year Experience)

---

### 🔹 1. **React Basics**

1. **What is React?**  
   A JavaScript library for building user interfaces, especially SPAs (Single Page Applications).

2. **What are the features of React?**
    - Virtual DOM
    - Component-based architecture
    - Unidirectional data flow
    - JSX

3. **What is JSX?**  
   JSX stands for JavaScript XML – a syntax extension that allows HTML to be written within JavaScript.

4. **What are components in React?**  
   Reusable pieces of UI. Types: Class and Functional components.

5. **What is the difference between functional and class components?**
    - Functional: Stateless, uses hooks
    - Class: Stateful, uses lifecycle methods

6. **What is a Virtual DOM?**  
   A lightweight copy of the actual DOM that React uses to detect changes and update efficiently.

7. **What is the purpose of `key` in React lists?**  
   Uniquely identifies elements in a list to help React optimize re-rendering.

8. **What are props in React?**  
   Inputs passed from parent to child components – read-only.

9. **What is state in React?**  
   A local data storage that influences how a component behaves and renders.

10. **How do you update the state in React?**  
    Using `setState()` in class components and `useState()` hook in functional components.

---

### 🔹 2. **Hooks (Beginner Level)**

11. **What are React Hooks?**  
    Functions that let you use state and lifecycle features in functional components.

12. **What is `useState` hook?**  
    Allows functional components to manage local state.

13. **What is `useEffect` hook?**  
    Handles side effects like API calls, DOM updates, or subscriptions.

14. **How does `useEffect` work with dependencies?**  
    It runs when specified dependency values change.

15. **What is the difference between `useEffect` and `componentDidMount`?**  
    `useEffect(() => {}, [])` behaves like `componentDidMount`.

---

### 🔹 3. **Props vs State**

16. **Difference between props and state?**
- Props: External, passed from parent
- State: Internal, managed within component

17. **Can we pass state as props?**  
    Yes, state from a parent can be passed to child as props.

18. **Are props mutable?**  
    No, props are read-only.

19. **How do you pass data from child to parent?**  
    By passing a callback function from the parent to the child.

20. **Can a component have both props and state?**  
    Yes, it can receive props and also manage internal state.

---

### 🔹 4. **Events and Forms**

21. **How do you handle events in React?**  
    By attaching handlers like `onClick`, `onChange`, etc., and defining callback functions.

22. **How do you handle forms in React?**  
    Use `useState` to track form inputs and handle submission with `onSubmit`.

23. **What is controlled vs uncontrolled components?**
- Controlled: React state controls input
- Uncontrolled: DOM manages input value via refs

24. **How do you prevent default form submission?**  
    Use `event.preventDefault()` in the handler.

25. **How do you handle multiple input fields in a form?**  
    Use a single handler function and access inputs via `event.target.name` and `value`.

---

### 🔹 5. **Component Lifecycle (Class-based)**

26. **What are React lifecycle methods?**  
    Methods that run at different phases of a component's life.

27. **What are `componentDidMount` and `componentWillUnmount`?**
- `componentDidMount`: Runs after component mounts
- `componentWillUnmount`: Runs before unmounting

28. **Can we use lifecycle methods in functional components?**  
    Not directly; instead, we use `useEffect`.

29. **Which method is used to fetch data on mount?**  
    `componentDidMount` or `useEffect(() => {}, [])`

30. **What is the constructor method used for in class components?**  
    To initialize state and bind methods.

---

### 🔹 6. **Rendering and Conditional Logic**

31. **What is conditional rendering in React?**  
    Dynamically render content based on a condition using `if`, `ternary`, or `&&`.

32. **What is the difference between `null` and `undefined` in JSX?**  
    Both render nothing, but `null` is commonly used for conditional rendering.

33. **How do you render lists in React?**  
    Using `.map()` and assigning `key` to each element.

34. **What is fragment in React?**  
    A wrapper (`<></>`) to group elements without adding extra DOM nodes.

35. **How do you render multiple elements from a component?**  
    Use a fragment or wrap in a div.

---

### 🔹 7. **React Router (Basics)**

36. **What is React Router?**  
    A routing library for SPAs in React.

37. **What is the difference between `BrowserRouter` and `HashRouter`?**
- `BrowserRouter`: Uses HTML5 history
- `HashRouter`: Uses URL hash for routing

38. **How do you define a route?**
   ```jsx
   <Route path="/home" element={<Home />} />
   ```

39. **How do you navigate programmatically in React Router?**  
    Using `useNavigate()` hook.

40. **How do you pass params in the URL?**  
    Define route as `/user/:id` and access via `useParams()`.

---

### 🔹 8. **Miscellaneous**

41. **What is React.StrictMode?**  
    A wrapper that helps detect potential problems in an app.

42. **What are higher-order components (HOC)?**  
    Functions that take a component and return a new component with added behavior.

43. **What is Context API in React?**  
    A way to share state between deeply nested components without props.

44. **How do you use Context API?**  
    Use `React.createContext()`, a `Provider`, and `useContext()`.

45. **What are React DevTools?**  
    Browser extension to inspect and debug React components.

46. **What is reconciliation in React?**  
    The process of comparing old and new Virtual DOM and updating the real DOM.

47. **What is `React.memo` used for?**  
    Optimizes performance by memoizing functional components.

48. **What is the use of `useRef`?**  
    Access DOM nodes or store mutable values that persist between renders.

49. **What is prop drilling and how to avoid it?**  
    Passing props through many levels; avoid it with Context API or state management tools.

50. **How to optimize performance in React apps?**
- Use memoization (`React.memo`, `useMemo`)
- Lazy loading
- Avoid unnecessary re-renders
- Use keys properly in lists

---

Would you like these in **PDF format**, or should we move to **React JS interview questions for 3–5 years of experience** next?