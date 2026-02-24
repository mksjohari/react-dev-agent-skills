# React hook templates

## Hook with props interface template

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
