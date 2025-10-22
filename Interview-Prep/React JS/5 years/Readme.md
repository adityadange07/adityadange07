Here are the **Top 50 React.js Interview Questions with Answers** tailored for **5 years of experience**. These questions are suitable for **mid-to-senior level roles**, covering core concepts, hooks, performance, architecture, testing, and advanced patterns.

---

## ✅ Top 50 React.js Interview Questions (5 Years Experience)

---

### 🔹 1. Core Concepts

1. **What is React and why is it used?**  
   React is a JavaScript library for building UI components. It offers a virtual DOM, component-based architecture, and unidirectional data flow.

2. **What are the main features of React?**
    - Virtual DOM
    - JSX
    - Component-based architecture
    - Hooks
    - Unidirectional data flow

3. **What is JSX?**  
   JSX is a syntax extension of JavaScript that allows writing HTML-like code inside JS.

4. **What is the virtual DOM?**  
   A lightweight copy of the real DOM. React updates the virtual DOM first and then reconciles it with the actual DOM for better performance.

5. **What are components in React?**  
   Independent and reusable pieces of UI. Two types: Class and Functional.

6. **What is the difference between functional and class components?**  
   Functional: Stateless, uses hooks.  
   Class: Stateful, uses lifecycle methods.

7. **What are props in React?**  
   Props are inputs to components that are passed down from parent to child.

8. **What is state in React?**  
   State is a built-in object that stores dynamic data and determines the component's behavior and rendering.

9. **How does data flow work in React?**  
   One-way data binding: Parent → Child via props.

10. **What is the difference between state and props?**
- Props: Passed from parent, read-only
- State: Local to component, mutable

---

### 🔹 2. React Hooks

11. **What are React Hooks?**  
    Functions that let you use state and other features in functional components.

12. **Explain `useState` hook.**  
    Allows functional components to maintain internal state.
   ```js
   const [count, setCount] = useState(0);
   ```

13. **What does the `useEffect` hook do?**  
    Handles side-effects (API calls, subscriptions, timers).  
    Runs after render by default.

14. **How does `useEffect` dependency array work?**  
    Controls when the effect runs. Empty `[]` = only on mount.

15. **What is `useRef` used for?**  
    For accessing DOM nodes or persisting mutable values across renders.

16. **What is the difference between `useMemo` and `useCallback`?**
- `useMemo`: Memoizes **values**
- `useCallback`: Memoizes **functions**

17. **When would you use `useReducer` instead of `useState`?**  
    For complex state logic or multiple state transitions.

18. **What are custom hooks in React?**  
    Functions starting with `use` to encapsulate reusable hook logic.

19. **Can you use hooks inside class components?**  
    No, hooks only work in functional components.

20. **What rules must hooks follow?**
- Call at top level
- Only call from React functions

---

### 🔹 3. Lifecycle, Performance & Optimization

21. **What are lifecycle methods in class components?**
- Mount: `constructor`, `componentDidMount`
- Update: `componentDidUpdate`
- Unmount: `componentWillUnmount`

22. **What is reconciliation in React?**  
    The process React uses to determine what parts of the DOM to update.

23. **What is the key prop and why is it important?**  
    Helps React identify which elements changed in a list.

24. **How do you optimize performance in React apps?**
- Use `React.memo`
- Lazy loading
- Code splitting
- Avoid unnecessary renders

25. **What is React.memo?**  
    A HOC that prevents re-renders if props haven't changed.

26. **What is the purpose of `shouldComponentUpdate`?**  
    Allows control over component rendering to avoid unnecessary re-renders.

27. **What are controlled vs uncontrolled components?**
- Controlled: Form elements managed via state
- Uncontrolled: Managed via DOM (using `ref`)

28. **What is context API and how is it used?**  
    Provides a way to share values between components without prop drilling.

29. **How does React handle events?**  
    React uses synthetic events—a cross-browser wrapper around native events.

30. **What is the difference between local state and global state?**
- Local: Component-specific
- Global: App-wide, often using context or Redux

---

### 🔹 4. Routing, Forms, and Error Handling

31. **What is React Router?**  
    A library for handling routing in single-page applications.

32. **What are the key components of React Router v6?**
- `<BrowserRouter>`
- `<Routes>`
- `<Route>`
- `useNavigate`, `useParams`

33. **How do you pass params via URL in React Router?**  
    `/user/:id` and use `useParams()` to access `id`.

34. **How do you handle forms in React?**
- Controlled inputs
- `onChange`, `onSubmit` handlers
- Optional: use Formik or React Hook Form

35. **What is form validation and how is it handled?**  
    Validate input fields using state, or libraries like Yup, Formik.

36. **How do you handle errors in React?**
- Try/catch
- Error boundaries (`componentDidCatch`)
- Fallback UIs

37. **What are error boundaries?**  
    Special components that catch JS errors during rendering and show fallback UIs.

---

### 🔹 5. Advanced Patterns, Testing, and Ecosystem

38. **What are Higher-Order Components (HOC)?**  
    Functions that take a component and return a new component with added behavior.

39. **What is a render prop?**  
    A technique for sharing logic by passing a render function as a prop.

40. **What is code splitting?**  
    Splitting JS into smaller chunks, loading them as needed using `React.lazy`.

41. **What is lazy loading in React?**  
    Dynamically loads components when needed to reduce initial load time.

42. **What is suspense in React?**  
    Handles loading state for components using lazy loading or data fetching.

43. **How do you test React components?**  
    Using tools like Jest, React Testing Library, Enzyme.

44. **What is React Testing Library?**  
    A testing library focused on testing user interactions and behavior.

45. **How do you mock APIs in React tests?**
- Jest mock functions
- `msw` (Mock Service Worker)

46. **What are some best practices for structuring React projects?**
- Feature-based folder structure
- Keep components small
- Reusable hooks & utilities

47. **What are portals in React?**  
    Render children into a DOM node outside the parent component hierarchy.

48. **What are Fragments and why are they used?**  
    `<></>` used to group elements without adding extra nodes to the DOM.

49. **What is Server-Side Rendering (SSR)?**  
    Rendering React components on the server (e.g., with Next.js) for SEO and performance.

50. **What is hydration in React?**  
    The process of attaching event listeners to static HTML rendered from SSR.

---

Would you like a **PDF version** of these questions, or a **mini project idea** to practice real-world React concepts?