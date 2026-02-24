# React repo structure examples

## Component and page file naming

**Incorrect:**

```
my-awesome-component.tsx
myAwesomeCopmponent.tsx

my-first-page.tsx
myFirstPage.tsx
```

**Correct:**

```
MyAwesomeComponent.tsx
MyAwesomeComponent.test.tsx
MyAwesomeComponent.service.ts
MyAwesomeComponent.service.test.ts

MyFirstPage.tsx
MyFirstPage.test.tsx
MyFirstPage.service.ts
MyFirstPage.service.test.ts
```

## Hook file naming

**Incorrect:**

```
my-awesome-hook.ts
MyAwesomeHook.ts
```

**Correct:**

```
myAwesomeHook.ts
myAwesomeHook.test.tsx
myAwesomeHook.service.ts
myAwesomeHook.service.test.ts
```

## Barrel exports

**Incorrect:**

```typescript
export { MyAwesomeCopmponent } from "./MyAwesomeComponent";
```

**Correct:**

```typescript
export * from "./MyAwesomeComponent";
```

## Full example application folder structure

Here is an example folder structure of a well structured vanilla React app:

```
src/
  └── common/
    └── types.ts // Common type and interface definitions
    └── enums.ts // Common enums
    └── services.ts // Common utility and helper functions
    └── index.ts
  └── components/
    └── MyFirstComponent/
      └── MyFirstComponent.tsx // Comopnent definition
      └── MyFirstComponent.test.tsx // Component unit tests
      └── MyFirstComponent.services.ts // Specific utility and helper functions
      └── MyFirstComponent.services.test.ts // Unit tests of the utility and helper functions
      └── index.ts
    └── index.ts
  └── hooks/
    └── myFirstHook/
      └── myFirstHook.tsx // Hook definition
      └── myFirstHook.test.tsx // Hook unit tests
      └── myFirstHook.services.ts // Specific utility and helper functions
      └── myFirstHook.services.test.ts // Unit tests of the utility and helper functions
      └── index.ts
    └── index.ts
  └── pages/
    └── FirstPage
      └── FirstPage.tsx // Page definition
      └── FirstPage.test.tsx // Page unit tests
      └── FirstPage.service.ts // Specific utility and helper functions
      └── FirstPage.service.test.ts // Unit tests of the utility and helper functions
      └── index.ts
    └── index.ts
  └── App.tsx
```
