# React Development Guidelines

## 1. Component Structure & Design
- **Functional Components with Hooks:** Default to functional components and Hooks for all new development. Use class components only if Hooks are insufficient for a specific, justified use case.
- **Props:**
    - **Destructuring:** Destructure props at the beginning of the component for clarity.
    - **PropTypes / TypeScript:** MANDATORY use of PropTypes (for JavaScript projects) or TypeScript interfaces/types (for TypeScript projects) for all component props to ensure type safety and serve as documentation.
    - **`children` Prop:** Use `props.children` for generic content containment.
- **Component Naming:** Use `PascalCase` for component file names (e.g., `UserProfile.jsx`, `UserProfile.tsx`) and component names.
- **File Organization:** Group related components, hooks, and styles together, typically in their own directory (e.g., `/components/Button/Button.jsx, Button.module.css, Button.test.js`).

## 2. State Management
- **Local State (`useState`):** Use `useState` for simple, component-local state.
- **Complex Local State (`useReducer`):** For more complex state logic within a component or closely related components, prefer `useReducer`.
- **Global State:**
    - **Context API:** For global state that doesn't change very frequently or for passing data deep down the component tree without prop drilling, use React Context API (often combined with `useReducer`).
    - **Dedicated Libraries (Zustand, Redux, Jotai, etc.):** For applications with complex, frequently changing global state, or when advanced features like middleware and devtools are needed, use a dedicated state management library. [Project Owner: Specify preferred library if one is standard, e.g., "This project uses Zustand for global state."].
- **Derived State:** Avoid storing state that can be easily derived from props or other state. Calculate it during rendering.

## 3. Hooks
- **Custom Hooks:** Encapsulate reusable component logic (especially stateful logic or side effects) into custom Hooks (e.g., `useFormInput`, `useFetchData`). Name custom hooks with the `use` prefix.
- **Rules of Hooks:** Strictly adhere to the Rules of Hooks:
    - Only call Hooks at the top level of functional components or custom Hooks.
    - Do not call Hooks inside loops, conditions, or nested functions.
- **Effect Hook (`useEffect`):**
    - Manage side effects (data fetching, subscriptions, manually changing the DOM).
    - Always provide a dependency array. If the effect should only run once on mount/unmount, use an empty array `[]`.
    - Clean up side effects (e.g., unsubscribe, clear timers) in the return function of `useEffect`.

## 4. Styling
- **CSS Modules:** Preferred method for component-level styling to ensure scoped styles. Name files as `ComponentName.module.css`.
- **Styled-components / Emotion:** If CSS-in-JS is used, [Project Owner: specify the library and any conventions].
- **Global Styles:** Keep global styles to a minimum, typically for base styling, resets, or themes.
- **Conditional Styling:** Use JavaScript logic within the component to apply conditional classes or styles rather than complex CSS selectors.

## 5. Performance Optimization
- **`React.memo`:** Wrap components in `React.memo` to prevent re-renders if props haven't changed. Use judiciously, especially for components that render often or have expensive render logic.
- **`useMemo`:** Memoize expensive calculations.
- **`useCallback`:** Memoize callback functions passed to optimized child components that rely on reference equality.
- **Lazy Loading:** Use `React.lazy` and Suspense for code-splitting and lazy loading components/routes to improve initial load time.
- **Virtualization:** For long lists or large tables, use windowing libraries like `react-window` or `react-virtualized`.
- **Bundle Analysis:** Regularly analyze the bundle size (e.g., using `source-map-explorer` or Webpack Bundle Analyzer) to identify and optimize large dependencies.

## 6. Accessibility (a11y)
- **Semantic HTML:** Use semantic HTML elements (`<nav>`, `<article>`, `<button>`, etc.) where appropriate.
- **ARIA Attributes:** Use ARIA attributes correctly to enhance accessibility for dynamic content or custom controls.
- **Keyboard Navigation:** Ensure all interactive elements are keyboard accessible and focusable.
- **Image `alt` Text:** Provide meaningful `alt` text for all images.
- **Testing:** Use accessibility testing tools (e.g., Axe, Lighthouse) during development.

## 7. Forms
- **Controlled Components:** Prefer controlled components for forms to have React manage the form data.
- **Form Libraries:** For complex forms, consider using libraries like Formik or React Hook Form. [Project Owner: Specify preferred library if one is standard].
- **Validation:** Implement client-side validation for better UX, but always ensure server-side validation as the authoritative source.

## 8. Error Boundaries
- Implement Error Boundaries at appropriate levels in the component tree to catch JavaScript errors in their child component tree, log those errors, and display a fallback UI.