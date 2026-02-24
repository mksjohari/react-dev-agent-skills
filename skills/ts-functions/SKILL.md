---
name: ts-functions
description: TypeScript function conventions. Use when writing or refactoring TypeScript functions, including arrow function syntax, explicit typing, early returns, parameter destructuring, single responsibility, avoiding side effects, and removing duplicate code.
user-invocable: false
---

# Functions

Functions should be simple, straightforward and have clear separation of concerns. All function names should be in camelCase.

## When to use

Use this skill when working with Typescript functions.

## Rules

- **Arrow function syntax** -- Always define functions using arrow syntax for concise syntax, predictable `this` binding, and seamless TypeScript type annotations.
- **Explicit type signatures** -- Always use explicit types for function parameters and return values. Never use `any`.
- **Early returns over nested if/else** -- Use early returns to reduce nesting depth and improve readability.
- **2 or fewer arguments** -- Limit function parameters to 2 or fewer. For more, use a destructured object with an interface to make expected properties clear, simulate named parameters, and enable linter warnings for unused properties.
- **Single responsibility** -- Each function should do one thing only. Functions that do more than one thing are harder to compose, test, and reason about.
- **Descriptive names** -- Function names should clearly communicate what the function does.
- **One level of abstraction** -- Functions with more than one level of abstraction are doing too much. Split them for reusability and easier testing.
- **No duplicate code** -- Avoid duplicate code by creating abstractions that handle variations with a single function/module/class.
- **Default objects with Object.assign** -- Use `Object.assign` to set default values on config objects instead of manual fallback assignments.
- **No boolean flag parameters** -- Flags indicate a function does more than one thing. Split into separate functions instead.
- **Avoid side effects** -- Functions should take values in and return values out. Avoid mutating global state, and clone objects/arrays before modifying them to prevent bugs elsewhere.
- **No global function pollution** -- Never pollute global prototypes (e.g., `Array.prototype`). Extend via subclassing instead.
- **Functional over imperative** -- Prefer functional programming patterns (e.g., `map`, `filter`, `reduce`) over imperative loops. They are easier to read and test.
- **Encapsulate conditionals** -- Extract complex conditional expressions into descriptively named functions.
- **Avoid negative conditionals** -- Use positive function names (e.g., `isDOMNodePresent`) rather than negated ones (e.g., `isDOMNodeNotPresent`).
- **Remove dead code** -- Delete unused code. Version control preserves history if it is ever needed again.

See [template.md](template.md) for correct code patterns and [examples/](examples/) for detailed incorrect/correct comparisons.

## References

[Clean code javascript](https://github.com/ryanmcdermott/clean-code-javascript?tab=readme-ov-file#functions)
