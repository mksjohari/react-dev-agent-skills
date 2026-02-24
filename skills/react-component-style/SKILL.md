---
name: react-component-style
description: React component structure conventions. Use when creating or modifying React components (.tsx files with JSX), including function components, props interfaces, helper render functions, and extracting custom hooks from complex components.
user-invocable: false
---

# React component structure

These guidelines standardise the implementation details of React components, ensuring clean code, reusability and readability for the maintainer.

## When to use

Use this skill when implementing any React component.

## Always use function components over class components

Never use class components. Always use arrow function components typed with `FC` from React.

See `template.md` for the function component template and `examples/sample.md` for incorrect/correct comparisons.

## Use interfaces to define component props

Always use interfaces with strict typing to define component props. The interface name should follow the pattern `I<ComponentName>Props`. Destructure props in the function signature.

See `template.md` for the props interface template and `examples/sample.md` for incorrect/correct comparisons.

## Use helper functions and common components to breakdown complex UI elements

When writing code for a complex component, it is inevitable that the definition will grow to be very long. Break down complex UI definitions with helper functions and common components that can be extracted. The return statement of the component itself should be easily readable so users can easily understand what the component will render.

- If there is conditional rendering, extract the condition into a function, and use early returns for the elements that should be rendered.
- If there is a long section that can be grouped together logically, use a utility function with the prefix "render" to extract this section, e.g. `renderLongSection()`.
- If there is repeating UI logic that can be extracted, create another component to reuse this logic.

See `template.md` for the helper render function template and `examples/sample.md` for incorrect/correct comparisons.

## Create custom hooks for complex hook logic

When writing code for a complex component, it is inevitable that the hook logic may get complicated. Extract complex hook logic into its own custom hook and import it into the element to keep the element definition readable.

See `template.md` for the custom hook extraction template and `examples/sample.md` for incorrect/correct comparisons.
