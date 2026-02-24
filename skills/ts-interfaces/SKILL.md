---
name: ts-interfaces
description: TypeScript interface conventions. Use when defining TypeScript interfaces or type aliases, including preferring interfaces over types, using the "I" prefix for interface names, and extending interfaces.
user-invocable: false
---

# Typescript interfaces

Type aliases and interfaces are very similar, and in many cases you can choose between them freely. Almost all features of an interface are available in type, the key distinction is that a type cannot be re-opened to add new properties vs an interface which is always extendable. Furthermore, Typescript recommends using interfaces over type aliases because of performance and display gains. For this reason we will always use interfaces over types.

## When to use

Use this skill when creating Typescript interface or type definitions.

## Prefer Typescript interfaces over types

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

Makes it easier to read.

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

## Reference

[Typescript documentation on performance](https://github.com/microsoft/TypeScript/wiki/Performance#preferring-interfaces-over-intersections)
