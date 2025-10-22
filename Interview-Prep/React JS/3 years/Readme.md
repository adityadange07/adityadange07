Here are the **Top 50 React JS Interview Questions and Answers** tailored specifically for **3 years of experience**. This list covers **core React concepts**, **component lifecycle**, **hooks**, **state management**, **performance optimization**, and **integration with APIs**, making it ideal for mid-level developers.

---

## ✅ Top 50 React JS Interview Questions (3 Years Experience)

---

### 🔹 1. **React Fundamentals**

1. **What is React?**  
   A JavaScript library for building user interfaces using a component-based architecture.

2. **What are the main features of React?**
    - JSX
    - Virtual DOM
    - Components
    - One-way data binding
    - Hooks

3. **What is JSX?**  
   A syntax extension that allows writing HTML-like code in JavaScript.

4. **What is the difference between Element and Component in React?**
    - Element: A plain object describing what to render.
    - Component: A function or class that returns elements.

5. **What are functional and class components?**
    - Functional: Stateless, use hooks
    - Class: Stateful, use lifecycle methods

6. **What is the Virtual DOM and how does it work?**  
   A lightweight in-memory representation of the real DOM. It compares diffs and applies updates efficiently.

7. **What are keys in React and why are they important?**  
   Keys help React identify which items have changed in a list, improving performance.

8. **What is the purpose of `props` in React?**  
   Props are read-only inputs used to pass data from parent to child components.

9. **What is `state` in React?**  
   State is a built-in object that allows components to manage dynamic data.

10. **What is the difference between `state` and `props`?**
- Props: Read-only, passed from parent
- State: Mutable, local to the component

---

### 🔹 2. **React Hooks (Advanced)**

11. **What are React Hooks?**  
    Functions that let you use state and lifecycle features in functional components.

12. **Explain `useState` hook.**  
    Initializes and manages local state in functional components.

13. **What is `useEffect` and when is it used?**  
    Handles side effects (API calls, subscriptions) and mimics lifecycle methods.

14. **What’s the difference between `useEffect(() => {}, [])` and `useEffect(() => {}, [dependency])`?**
- `[]`: Runs once
- `[dep]`: Runs when `dep` changes

15. **What is the purpose of `useRef`?**  
    Holds mutable values that persist across renders, often used for DOM references.

16. **What does `useMemo` do?**  
    Memoizes expensive calculations to prevent unnecessary recalculations.

17. **What is the difference between `useCallback` and `useMemo`?**
- `useCallback`: Memoizes functions
- `useMemo`: Memoizes values

18. **What is a custom hook?**  
    A reusable function that uses hooks internally.

19. **Can you use hooks inside class components?**  
    No, hooks can only be used in functional components.

20. **Why can’t hooks be called conditionally?**  
    Hooks rely on consistent order of execution to track state properly.

---

### 🔹 3. **Component Lifecycle and Class Components**

21. **What are React lifecycle methods?**  
    Methods in class components like `componentDidMount`, `componentDidUpdate`, `componentWillUnmount`.

22. **Explain `componentDidMount`.**  
    Runs after the component is rendered; often used for API calls.

23. **What is the equivalent of `componentDidMount` in hooks?**  
    `useEffect(() => {}, [])`

24. **What happens during `render()` in a class component?**  
    Returns JSX which gets converted into real DOM elements.

25. **What is `shouldComponentUpdate` used for?**  
    To prevent unnecessary renders by checking changes in props/state.

---

### 🔹 4. **React Routing and Navigation**

26. **What is React Router?**  
    A standard library for routing in React applications.

27. **How do you implement routing in React?**  
    Using `react-router-dom` with `<BrowserRouter>`, `<Route>`, `<Link>`, etc.

28. **What is the difference between `<Link>` and `<a>` in React?**  
    `<Link>` prevents full page reload, providing client-side navigation.

29. **What is dynamic routing in React?**  
    Creating routes based on data (e.g., `/user/:id`).

30. **How do you pass route parameters in React Router?**  
    Using `useParams()` from `react-router-dom`.

---

### 🔹 5. **State Management & Performance**

31. **What are the different ways to manage state in React?**
- Local state (`useState`)
- Context API
- Redux / Zustand / Recoil (external state managers)

32. **What is Context API?**  
    A way to share state globally without prop drilling.

33. **When would you use Redux over Context API?**  
    For large-scale apps with complex and shared state logic.

34. **What is memoization in React?**  
    Caching the result of expensive function calls to optimize rendering.

35. **What is `React.memo`?**  
    A HOC that prevents re-rendering unless props change.

36. **What is lazy loading in React?**  
    Loading components only when needed using `React.lazy()` and `Suspense`.

37. **How to prevent unnecessary re-renders in React?**
- Use `React.memo`
- Use `useCallback`, `useMemo`
- Avoid changing props/state unnecessarily

38. **What is prop drilling and how do you avoid it?**  
    Passing props through multiple layers. Avoid using Context API or Redux.

39. **What is reconciliation in React?**  
    The process of updating the DOM by comparing current and previous virtual DOM.

40. **What is the difference between controlled and uncontrolled components?**
- Controlled: React controls the input state
- Uncontrolled: DOM manages its own state

---

### 🔹 6. **API Integration and Testing**

41. **How do you make API calls in React?**  
    Using `fetch`, `axios`, or libraries like `react-query`.

42. **Where should you make API calls in React?**  
    Inside `useEffect` or `componentDidMount`.

43. **What is Axios and why is it preferred over fetch?**  
    Axios is a promise-based HTTP client with better defaults, error handling, and interceptors.

44. **How do you handle error boundaries in React?**  
    Using `componentDidCatch()` or a custom ErrorBoundary component.

45. **How do you test React components?**  
    Using testing libraries like Jest and React Testing Library.

---

### 🔹 7. **Advanced & Real-World**

46. **What is server-side rendering (SSR) in React?**  
    Rendering components on the server for faster initial load and SEO.

47. **What is hydration in React?**  
    Attaching event handlers to pre-rendered HTML during SSR.

48. **What are portals in React?**  
    Render components outside the main DOM tree (e.g., modals).

49. **What is the purpose of `StrictMode` in React?**  
    Helps identify potential problems in the app during development.

50. **What are some common performance optimization techniques in React?**
- Code splitting
- Memoization
- Lazy loading
- Avoid unnecessary re-renders
- Using keys properly

---

Would you like this as a **PDF**, or want the **same level of questions for React + TypeScript or Next.js** next?