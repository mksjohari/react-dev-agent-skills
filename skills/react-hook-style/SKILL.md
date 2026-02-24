---
name: react-hook-style
description: React hook structure conventions. Use when creating or modifying React custom hooks (use*.ts files), including hook props interfaces and return types.
user-invocable: false
---

# React hook structure

These guidelines standardise the implementation details of React hooks, ensuring clean code, reusability and readability for the maintainer.

## When to use

Use this skill when implementing any React hook.

## Use interfaces to define hook props

Always use interfaces with strict typing to define hook props. The interface name should follow the pattern `IUse<HookName>Props`. Destructure props in the function signature rather than accessing them via `props.`.

See `template.md` for the hook with props interface template and `examples/sample.md` for incorrect/correct comparisons.
