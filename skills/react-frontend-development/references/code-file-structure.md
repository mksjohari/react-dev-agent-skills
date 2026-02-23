---
title: React application file and folder structures
description: Optimal file and folder structure for easily managed code
---

# React folder and file structures

These guidelines standardise the file and folder structure within a React application such that it simplifies imports and enhances the readabilty for any maintainer.

## File structure

Each component should have its own folder, with barrel exports to keep the imports clean.

### Components

#### Different files should be created for seperation of concerns

- For UI related code, e.g. code that defines the behavior across the component lifecycle, it should be in the main component file, e.g. `MyAwesomeComponent.tsx`.
- For helper code scoped only to be used within the component that do not depend on the component state and/or any React code, it should be in a service file prefixed by a component name, e.g. `MyAwesomeComponent.service.ts`.
- For code related to unit tests of the component, it should be in a test file prefixed by the component name, e.g. `MyAwesomeComponent.test.tsx`.
- For exporting the component to be used elsewhere, an `index.ts` file should be created with barrel exports.

**Incorrect:**

```typescript
export { MyAwesomeCopmponent } from "./MyAwesomeComponent";
```

**Correct:**

```typescript
export * from "./MyAwesomeComponent";
```

`MyComponentName.tsx`

#### Component file names should always use PascalCase

All files related to components should always use PascalCase.

**Incorrect:**

`my-component-name.tsx`

**Correct:**

`MyComponentName.tsx`

## Folder structure

For commmon React components, i.e. those that are used in more than one other component or page, they should be inside a `components` folder.
