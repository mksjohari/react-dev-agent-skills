# Interface Examples

## Prefer interfaces over type aliases

**Incorrect:**

```typescript
type Foo = { prop: string };
type Bar = { otherProp: string };

type FooBarBaz = Foo &
  Bar & {
    someProp: string;
  };
```

**Correct:**

```typescript
interface Foo {
  prop: string;
}

interface Bar {
  otherProp: string;
}

interface FooBarBaz extends Foo, Bar {
  someProp: string;
}
```

## Prefix interface definitions with "I"

**Incorrect:**

```typescript
interface SomeInterface {
  prop: string;
}
```

**Correct:**

```typescript
interface ISomeInterface {
  prop: string;
}
```
