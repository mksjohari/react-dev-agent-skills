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

**Incorrect:**

```typescript
import React from 'react'

class Component extends React.Component {
  render() {
    return <div>Hello world</div>
  }
}
```

**Correct:**

```typescript
import React, { FC } from 'react'

export const MyComponent: FC = () => {
  return <div>Hello world</div>
}
```

## Use interfaces to define component props

Always use interfaces with strict typing to define component props.

**Incorrect:**

```typescript
import { FC } from "react";

export const MyComponent = (props: any) => {
  return <div>Hello world with {props.firstProp}</div>
}
```

**Correct:**

```typescript
import { FC } from "react";

interface IMyComponentProps {
  firstProp: string
  secondProp: string
}

export const MyComponent: FC<IMyComponentProps> = ({ firstProp, secondProp }) => {
  return <div>Hello world with {firstProp} and {secondProp}</div>
}
```

## Use helper functions and common components to breakdown complex UI elements

When writing code for a complex component, it is inevitable that the definition will grow to be very long. Break down complex UI definitions with helper functions and common components that can be extracted. The return statement of the component itself should be easily readable so users can easily understand what the component will render.

- If there is conditional rendering, extract the condition into a function, and use early returns for the elements that should be rendered.
- If there is a long section that can be grouped together logically, use a utility function with the prefix "render" to extract this section, e.g. `renderLongSection()`.
- If there is repeating UI logic that can be extracted, create another component to reuse this logic.

**Incorrect:**

```typescript
import { FC } from 'react';

export const MyComponent: FC = () => {
  const someCondition = true;

  return (
    <div>
      <div>Long section with many common elements and logic variant 1</div>
      <div>Long section with many common elements and logic variant 2</div>
      <div>Long section with no common elements or logic</div>
      {someCondition ? <div>Condition true section</div> : <div>Condition false section</div>}
      <div>Short section</div>
    </div>
  );
};
```

**Correct:**

```typescript
import { FC } from "react";
import { CommonComponent } from "components";

export const MyComponent: FC = () => {
  const someCondition = true;

  const renderLongSection = () => {
    return <div>Long section with no common elements or logic</div>
  }

  const renderConditionalSection = () => {
    if (someCondition) {
      return <div>Condition true section</div>
    }

    return <div>Condition false section</div>
  }

  return (
    <div>
      <CommonComponent variant={1} />
      <CommonComponent variant={2} />
      {renderLongSectionTwo()}
      {renderConditionalSection()}
      <div>Short section</div>
    </div>
  )
}
```

## Create custom hooks for complex hook logic

When writing code for a complex component, it is inevitable that the hook logic may get complicated. Extract complex hook logic into its own custom hook and import it into the element to keep the element definition readable.

**Incorrect:**

```typescript
import { FC, useEffect, useState } from 'react';

interface IMyComponentProps {
  firstProp: string
  secondProp: string
}

export const MyComponent: FC<IMyComponentProps> = ({ firstProp, secondProp }) => {
  const [firstState, setFirstState] = useState('')
  const [secondState, setSecondState] = useState('')

  useEffect(() => {
    const newFirstState = someComplicatedLogic(firstProp)
    setFirstState(newFirstState)
  }, [firstProp])

  useEffect(() => {
    const newSecondState = someMoreComplicatedLogic(secondProp)
    setSecondState(newSecondState)
  }, [secondProp])

  return (
    <div>
      {firstState}
      {secondState}
    </div>
  );
};
```

**Correct:**

```typescript
// Inside MyComponent.tsx
import { FC, useEffect, useState } from 'react';
import { useMyHook } from 'hooks';

interface IMyComponentProps {
  firstProp: string
  secondProp: string
}

export const MyComponent: FC<IMyComponentProps> = ({ firstProp, secondProp }) => {
  const { firstState, secondState } = useMyHook({ firstProp, secondProp })

  return (
    <div>
      {firstState}
      {secondState}
    </div>
  );
};

// Inside useMyHook.ts
interface IUseMyHookProps {
  firstProp: string
  secondProp: string
}

export const useMyHook = ({ firstProp, secondProp}: IUseMyHookProps) => {
  const [firstState, setFirstState] = useState('')
  const [secondState, setSecondState] = useState('')

  useEffect(() => {
    const newFirstState = someComplicatedLogic(firstProp)
    setFirstState(newFirstState)
  }, [firstProp])

  useEffect(() => {
    const newSecondState = someMoreComplicatedLogic(secondProp)
    setSecondState(newSecondState)
  }, [secondProp])

  return { firstState, secondState }
}
```
