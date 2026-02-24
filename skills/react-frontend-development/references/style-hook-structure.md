---
title: React hook structure
description: React hook structure for easy readability
---

# React hook structure

These guidelines standardise the implementation details of React hooks, ensuring clean code, reusability and readability for the maintainer.

## When to use

Use this skill when implementing any React hook.

## Use interfaces to define hook props

Always use interfaces with strict typing to define hook props.

**Incorrect:**

```typescript
import { FC, useState } from "react";

export const useMyHook = (props: any) => {
  const [state, setState] = useState(props.firstProp);

  return {
    state,
    setState,
  };
};
```

**Correct:**

```typescript
import { FC, useState } from "react";

interface IUseMyHookProps {
  firstProp: string;
}

export const useMyHook = ({ firstProp }: IUseMyHookProps) => {
  const [state, setState] = useState(firstProp);

  return {
    state,
    setState,
  };
};
```
