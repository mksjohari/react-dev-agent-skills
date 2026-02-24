# React Query Components - Code Templates

## Query usage in component

Destructure the return, handle loading/refetching/error states.

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

## Mutation usage in component

Handle onSuccess and onError callbacks to indicate mutation status to the user.

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

## Default value patterns

Provide default values to prevent rendering errors before the API call resolves.

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
