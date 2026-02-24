---
name: ts-error-handling
description: TypeScript error handling conventions. Use when writing try/catch blocks, handling errors from functions or promises, or implementing error reporting in TypeScript code.
user-invocable: false
---

# Error Handling

Never ignore handling of errors in a function or promise.

## Rules

1. **Never ignore caught errors.** Always handle errors with `console.error`, a user notification, or an error reporting service. Using `console.log` alone is insufficient -- use `console.error` at minimum.
2. **Wrap potentially throwing code with `try/catch`.** Always wrap code that may throw an error and fail gracefully.

## When to Use

Use this skill when working with a TypeScript function or promise that has the potential to throw an error.

## Templates and Examples

- See `template.md` for the standard try/catch with proper error handling pattern.
- See `examples/sample.md` for correct and incorrect usage examples.

## References

[Clean code javascript](https://github.com/ryanmcdermott/clean-code-javascript?tab=readme-ov-file#error-handling)
