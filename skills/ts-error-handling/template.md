# Error Handling Templates

## Try/Catch with Proper Error Handling

```typescript
try {
  functionThatMightThrow();
  await promiseThatMightThrow();
} catch (error) {
  // Use one or more of these approaches:
  console.error(error);
  notifyUserOfError(error);
  reportErrorToService(error);
}
```

## Async Function with Error Handling

```typescript
const fetchData = async () => {
  try {
    const response = await apiCall();
    return response.data;
  } catch (error) {
    console.error(error);
    notifyUserOfError(error);
  }
};
```
