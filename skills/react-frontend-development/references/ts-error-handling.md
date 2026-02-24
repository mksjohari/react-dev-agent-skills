---
title: Typescript error handling
description: Functions or promises that may throw an error should always be handled
---

# Error handling

Never ignore handling of errors in a function or promise.

## When to use

Use this skill when working with a Typescript function or promise has a potential to throw an error.

## Don't ignore caught errors from functions or promises

Always wrap the bit of code that an error may occur with `try/catch` and fail gracefully.

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

## References

[Clean code javascript](https://github.com/ryanmcdermott/clean-code-javascript?tab=readme-ov-file#error-handling)
