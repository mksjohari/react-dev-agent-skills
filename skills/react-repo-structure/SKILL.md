---
name: react-repo-structure
description: React project file and folder structure conventions. Use when creating new files or folders in a React project, including component folders, hook folders, page folders, barrel exports, and service/test file naming.
user-invocable: false
---

# React folder and file structure

These guidelines standardise the file and folder structure within a React application such that it simplifies imports, maintains logical structure and enhances the readabilty for the maintainer. All files should use Typescript for type safety.

## When to use

Use this skill when creating any file or folder with React code.

## File structure

### Components and Pages

Each component or page should have its own folder. All component or page related file names should be in PascalCase.

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

### Hooks

Each hook should have its own folder. All hook related file names should be in camelCase.

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

### Barrel exports

For all exports, always use barrel exports to keep the imports clean. Always use an `index.ts` file and export everything.

**Incorrect:**

```typescript
export { MyAwesomeCopmponent } from "./MyAwesomeComponent";
```

**Correct:**

```typescript
export * from "./MyAwesomeComponent";
```

## Different files should be created for seperation of concerns

- For the main UI and state logic of the code, it should be in the main file.
  - For comopnents, this is the componet file, e.g. `MyAwesomeComponent.tsx`.
  - For hooks, this is the hook file, e.g. `myFirstHook.ts`.
  - For pages, this is the page file, e.g. `MyFirstPage.tsx`.
- For helper code that do not depend on the state and/or any React code, that is only to be used in the main file, it should be in a service file prefixed by the main file name. This is so that the service code does not clutter the main file, distracting the user from understanding how the component/hook/page works.
  - For comopnents, this should be `MyAwesomeComponent.service.ts`.
  - For hooks, this should be `myFirstHook.service.ts`.
  - For pages, this should be `MyFirstPage.service.tsx`.
- For code related to the unit tests of the main file or the service file, it must be in a test file prefixed by the main file name.
  - For comopnents, this should be `MyAwesomeComponent.test.tsx` and
    `MyAwesomeComponent.service.test.ts`.
  - For hooks, this should be `myFirstHook.test.tsx` and
    `myFirstHook.service.test.ts`.
  - For pages, this should be `MyFirstPage.test.tsx` and `MyFirstPage.service.test.ts`.

## Folder structure

Depending on the structure of the project, the path of the folders may be slightly different, but they should exist somewhere.

- For commmon React components, i.e. those that are used in more than one other component or page, they should be inside a `components` folder.
- For custom hooks, they should be inside a `hooks` folder.
- For different pages, they should be inside a `pages` folder.
- For utility and helper functions, and also common type and interface definitions, they should be inside a `common` folder.

If you are unable to find them or are unsure, ask the user where the folders should be placed at. If the user already has an existing convention for the folder structure, follow their existing convention of organising the folders. However, new files created inside the folder should also follow the structure defined above.

## Example application folder structure

Here is an example folder structure of a well structured vanilla React app

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
