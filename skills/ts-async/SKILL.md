---
name: ts-async
description: TypeScript async/await conventions. Use when working with promises, async/await, callbacks, or asynchronous code patterns in TypeScript.
user-invocable: false
---

# Async/Await

Using the async/await syntax we get a cleaner solution without any `.then()` chains of functions.

## Rules

1. **Always prefer async/await over `.then()` chains and callbacks.** Async/await produces cleaner, more readable code that is easier to debug and reason about.

## When to Use

Use this skill when working with TypeScript promises and callbacks.

## Templates and Examples

- See `template.md` for the standard async/await with try/catch pattern.
- See `examples/sample.md` for correct and incorrect usage examples.

## Reference

[Clean code javascript](https://github.com/ryanmcdermott/clean-code-javascript?tab=readme-ov-file#concurrency)
