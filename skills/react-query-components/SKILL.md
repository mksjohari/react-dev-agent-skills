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

```typescript
const MyComponent = () => {
  const { data: clientInfo, isLoading, isRefetching, isError } = useClientInfo(clientId);

  if (isLoading || isRefetching) {
    // handle loading state
    return <LoadingSpinner />;
  }

  if (isError) {
    // handle error state
    return <Error />;
  }

  return <div>Hello world</div>
};
```

## Using a mutation in the component

Always handle the success and error state of the mutation, giving the user some form of indication of the mutation's status.

```typescript
const MyComponent = () => {
  const updateClientInfoMutation = useUpdateClientInfo();

  const handleUpdateClientInfo = () => {
    updateClientInfoMutation.mutate({
      clientId,
      clientInfo
    }, {
      onSuccess: () => {
        console.log('success') // bare minimum
        // other notifications are preferred e.g. toast / UI state update
      }
      onError: () => {
        console.error('error') // bare minimum
        // other notifications preferred e.g. toast / UI state update
      }
    })
  }
};
```

## Provide a default value for the query when the query hasnt resolved

This helps prevent rendering errors for when the API call hasn't succeeded yet.

```typescript
const MyComponent = () => {
  // If the data is an object, provide a default object
  const {
    data: clientInfo = { name: "", username: "", createdDate: null },
    isLoading,
    isRefetching,
    isError,
  } = useClientInfo(clientId);
};

const MyOtherComponent = () => {
  // If the data is list, provide an empty array
  const {
    data: clientList = [],
    isLoading,
    isRefetching,
    isError,
  } = useClientList();
};
```
