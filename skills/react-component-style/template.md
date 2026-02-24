# React component templates

## Function component template

```typescript
import React, { FC } from 'react'

export const MyComponent: FC = () => {
  return <div>Hello world</div>
}
```

## Props interface template

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

## Helper render function template

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

## Custom hook extraction template

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
