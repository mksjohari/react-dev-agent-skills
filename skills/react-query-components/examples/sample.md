# React Query Components - Examples

## Using a query in the component

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

## Default value for object data

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
```

## Default value for list data

```typescript
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
