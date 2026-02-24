# Enum Examples

## Use enums over magic strings

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
