---
name: react-query-components
description: Using TanStack Query hooks inside React components. Use when consuming useQuery or useMutation results in a component, handling loading/error/refetching states, providing default values for query data, or calling mutations with onSuccess/onError callbacks.
user-invocable: false
---

# Best practices for using Tanstack Query in a React component

These guidelines standardise the usage of the Tanstack Query hooks in a React component.

## When to use

Use this skill when fetching data inside a React component. Refer to the react-query-hooks skill for the query hooks format.

## Using a query in the component

Destructure the return of the `useQuery` hook, and always handle the loading, refetching and error states.

See `template.md` for the query usage pattern and `examples/sample.md` for a complete example.

## Using a mutation in the component

Always handle the success and error state of the mutation, giving the user some form of indication of the mutation's status.

See `template.md` for the mutation usage pattern and `examples/sample.md` for a complete example.

## Provide a default value for the query when the query hasnt resolved

This helps prevent rendering errors for when the API call hasn't succeeded yet. If the data is an object, provide a default object. If the data is a list, provide an empty array.

See `template.md` for default value patterns and `examples/sample.md` for complete examples.
