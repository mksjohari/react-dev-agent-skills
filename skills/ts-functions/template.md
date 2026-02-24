# Function Templates

## Arrow function with types

```typescript
const combine = (val1: number, val2: number): number => {
  return val1 + val2;
};
```

## Destructured object params with interface

```typescript
interface ICreateMenuProps {
  title: string;
  body: string;
  buttonText: string;
  cancellable: boolean;
}

const createMenu = ({
  title,
  body,
  buttonText,
  cancellable,
}: ICreateMenuProps) => {
  // ...
};
```

## Early return pattern

```typescript
const someCondition = (condition1: boolean, condition2: boolean) => {
  if (!condition1) return;
  if (!condition2) return;
  // do something
};
```

## Object.assign defaults

```typescript
const menuConfig = {
  title: "Order",
  // User did not include 'body' key
  buttonText: "Send",
  cancellable: true,
};

function createMenu(config) {
  let finalConfig = Object.assign(
    {
      title: "Foo",
      body: "Bar",
      buttonText: "Baz",
      cancellable: true,
    },
    config,
  );
  return finalConfig;
}

// config now equals: {title: "Order", body: "Bar", buttonText: "Send", cancellable: true}
createMenu(menuConfig);
```

## Functional programming (reduce) pattern

```typescript
const programmerOutput = [
  {
    name: "Uncle Bobby",
    linesOfCode: 500,
  },
  {
    name: "Suzie Q",
    linesOfCode: 1500,
  },
];

const totalOutput = programmerOutput.reduce(
  (totalLines, output) => totalLines + output.linesOfCode,
  0,
);
```
