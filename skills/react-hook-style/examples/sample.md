# React hook style examples

## Hook props interfaces

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
