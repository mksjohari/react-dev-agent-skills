---
name: react-query-hooks
description: TanStack Query (React Query) hook conventions. Use when writing API calls, useQuery hooks, useMutation hooks, query keys, axios requests, or data fetching/mutating hooks in React.
user-invocable: false
---

# API calls in React

Always use Tanstack Query to fetch data in React applications. It handles all the complexities of fetching, caching, syncronizing and updating server state. For all logical groupings of hooks related to an API endpoint, the relevant files should live inside a `queries` folder.

For example, if I have multiple different API calls to `/api/client`, then all related query fetching code should go inside a `hooks/queries/client` folder.

## When to use

Use this skill when writing code to fetch / mutate data in React.

## Use the useQuery hook for fetching data

Create a hook to wrap the useQuery hook to fetch the data. The hook name should indicate what data it is fetching. This hook should be inside a `hook.ts` file.

See `template.md` for the useQuery hook pattern and `examples/sample.md` for incorrect/correct examples.

## Use the useMutation hook for mutating data

Create a hook to wrap the useMutation hook to mutate the data. The hook name should indicate what data it is mutating. Then we should invalidate the related query that queries this data. This hook should be inside a `hook.ts` file.

See `template.md` for the useMutation hook pattern and `examples/sample.md` for incorrect/correct examples.

## Create type file to keep all request and response shapes

Create `types.ts` to keep all the type definitions of request params and response DTOs.

See `template.md` for the types.ts pattern.

## Create transformer file to map DTO to client useable viewmodel

If the data from API response needs to be transformed to match frontend client use case, create a `transformer.ts` file to do the mapping, and type this transformed shape as a VM. Use this transform function in the `select` param of `useQuery`.

See `template.md` for the transformer.ts pattern with select.

## Folder structure

All query-related files follow a consistent folder structure convention.

See `template.md` for the complete folder structure.
