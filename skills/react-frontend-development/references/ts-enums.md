---
title: Typescript enums
description: Always use enums over magic strings
---

# Always use enums over magic strings

When there is a situation where you want to do string comparisons for a finite amount of known values, always prefer to use enums over using types or string literal comparisons. Enums are easier to change and manage than both of them, and should be placed in an `enum.ts` file.

**Incorrect:**

```typescript
const currentPage = "home";

if (currentPage === "home") {
  // do something
} else if (currentPage === "someOtherPage") {
  // do something
} else if (currentPage === "anotherPage") {
  // do something
}
```

**Correct:**

```typescript
// in enums.ts

export enum Pages {
  Home = "home",
  SomeOtherPage = "someOtherPage",
  AnotherPage = "anotherPage",
}

// in the component
const currentPage = Pages.Home;

if (currentPage === Pages.Home) {
  // do something
} else if (currentPage === Pages.SomeOtherPage) {
  // do something
} else if (currentPage === Pages.AnotherPage) {
  // do something
}
```

## When to use

Use this skill when doing any form of string comparisons.
