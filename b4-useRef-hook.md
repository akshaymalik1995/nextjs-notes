# The useRef Hook

The `useRef` hook is a React hook that allows you to create a **mutable ref** that persists between renders. This can be useful for things like tracking the value of an input field or the state of a checkbox.

To use the `useRef` hook, you need to import it from the react package. Then, you can use it in any component that you want to create a ref.

The `useRef` hook returns a reference object with the following properties:
* current: The current value of the ref.
* .current = value: The setter method for the ref.

**Questions:**
* What are the advantages of `useRef` over `useState`?
* What are the common use cases of `useRef`?
* When should you use `useRef` over `useState` to track the value of an input?
* What is a "mutable ref"?

https://react.dev/reference/react/useRef
