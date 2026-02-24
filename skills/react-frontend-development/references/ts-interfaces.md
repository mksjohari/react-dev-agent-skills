---
title: Prefer interfaces over types
description: Always prefer interfaces over types for extensibility
---

# Prefer Typescript interfaces over types

Type aliases and interfaces are very similar, and in many cases you can choose between them freely. Almost all features of an interface are available in type, the key distinction is that a type cannot be re-opened to add new properties vs an interface which is always extendable. Furthermore, Typescript recommends using interfaces over type aliases because of performance and display gains. For this reason we will always use interfaces over types.

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

## When to use

Use this skill when creating Typescript interface or type definitions.

## Reference

[Typescript documentation on performance](https://github.com/microsoft/TypeScript/wiki/Performance#preferring-interfaces-over-intersections)
