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

See `examples/sample.md` for incorrect/correct naming comparisons.

### Hooks

Each hook should have its own folder. All hook related file names should be in camelCase.

See `examples/sample.md` for incorrect/correct naming comparisons.

### Barrel exports

For all exports, always use barrel exports to keep the imports clean. Always use an `index.ts` file and export everything using `export *` syntax rather than named re-exports.

See `examples/sample.md` for incorrect/correct barrel export comparisons.

## Different files should be created for separation of concerns

- For the main UI and state logic of the code, it should be in the main file.
  - For components, this is the component file, e.g. `MyAwesomeComponent.tsx`.
  - For hooks, this is the hook file, e.g. `myFirstHook.ts`.
  - For pages, this is the page file, e.g. `MyFirstPage.tsx`.
- For helper code that do not depend on the state and/or any React code, that is only to be used in the main file, it should be in a service file prefixed by the main file name. This is so that the service code does not clutter the main file, distracting the user from understanding how the component/hook/page works.
  - For components, this should be `MyAwesomeComponent.service.ts`.
  - For hooks, this should be `myFirstHook.service.ts`.
  - For pages, this should be `MyFirstPage.service.tsx`.
- For code related to the unit tests of the main file or the service file, it must be in a test file prefixed by the main file name.
  - For components, this should be `MyAwesomeComponent.test.tsx` and `MyAwesomeComponent.service.test.ts`.
  - For hooks, this should be `myFirstHook.test.tsx` and `myFirstHook.service.test.ts`.
  - For pages, this should be `MyFirstPage.test.tsx` and `MyFirstPage.service.test.ts`.

## Folder structure

Depending on the structure of the project, the path of the folders may be slightly different, but they should exist somewhere.

- For common React components, i.e. those that are used in more than one other component or page, they should be inside a `components` folder.
- For custom hooks, they should be inside a `hooks` folder.
- For different pages, they should be inside a `pages` folder.
- For utility and helper functions, and also common type and interface definitions, they should be inside a `common` folder.

If you are unable to find them or are unsure, ask the user where the folders should be placed at. If the user already has an existing convention for the folder structure, follow their existing convention of organising the folders. However, new files created inside the folder should also follow the structure defined above.

See `template.md` for folder structure templates and `examples/sample.md` for a full example application folder structure.
