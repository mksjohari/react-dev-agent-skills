---
title: React application file and folder structures
description: Optimal file and folder structure for easily managed code
---

# React folder and file structures

These guidelines standardise the file and folder structure within a React application such that it simplifies imports and enhances the readabilty for the maintainer.

## File structure

Each component should have its own folder, with barrel exports to keep the imports clean.

### Components

All component related file names should be in pascal case.

**Incorrect:**

```
my-awesome-component.tsx
myAwesomeCopmponent.tsx
```

**Correct:**

```
MyAwesomeComponent.tsx
MyAwesomeComponent.test.tsx
MyAwesomeComponent.service.ts
MyAwesomeComponent.service.test.ts
```

#### Different files should be created for seperation of concerns

- For all UI related code, it should be in the main component file, e.g. `MyAwesomeComponent.tsx`.

- For any helper code scoped only to be used within the component that do not depend on the component state and/or any React code, it should be in a service file prefixed by a component name, e.g. `MyAwesomeComponent.service.ts`. This is so that helper functions do not clutter the code of the component, distracting the user from understanding how the component works.

- For code related to unit tests of the component or the service file, it must be in a test file prefixed by the component name, e.g. `MyAwesomeComponent.test.tsx` and `MyAwesomeComponent.service.test.ts`.

- For exporting the component to be used elsewhere, an `index.ts` file must be created with barrel exports.

  **Incorrect:**

  ```typescript
  export { MyAwesomeCopmponent } from "./MyAwesomeComponent";
  ```

  **Correct:**

  ```typescript
  export * from "./MyAwesomeComponent";
  ```

## Folder structure

For commmon React components, i.e. those that are used in more than one other component or page, they should be inside a `components` folder.
