# Error Handling Examples

## Don't ignore caught errors from functions or promises

**Incorrect:**

```typescript
try {
  functionThatMightThrow();
  await promiseThatMightThrow();
} catch (error) {
  console.log(error);
}
```

**Correct:**

```typescript
try {
  functionThatMightThrow();
  await promiseThatMightThrow();
} catch (error) {
  // One option (more noisy than console.log):
  console.error(error);
  // Another option:
  notifyUserOfError(error);
  // Another option:
  reportErrorToService(error);
  // OR do all three!
}
```
