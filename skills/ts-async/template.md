# Async/Await Templates

## Async Function with Try/Catch

```typescript
const fetchData = async () => {
  try {
    const result = await someAsyncOperation();
    return result;
  } catch (error) {
    console.error(error);
  }
};
```

## Multiple Async Operations

```typescript
const processData = async () => {
  try {
    const data = await fetchFromApi();
    await writeToFile("output.json", data);
    console.log("Done");
  } catch (error) {
    console.error(error);
  }
};
```
