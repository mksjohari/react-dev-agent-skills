# React component style examples

## Function components over class components

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

## Props interfaces

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

## Helper render functions for complex UI

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

## Custom hooks for complex hook logic

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
