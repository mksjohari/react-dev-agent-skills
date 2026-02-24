---
name: ts-variables
description: TypeScript variable conventions. Use when declaring or naming TypeScript variables, including camelCase naming, meaningful names, explicit typing, searchable constants, explanatory variables, and default parameters.
user-invocable: false
---

# Variables

Variables names should have simple, meaningful and clear names that explain what they do. Variables names should also always be in camelCase.

## When to use

Use this skill when working with Typescript variables.

## Rules

- **Meaningful, pronounceable names in camelCase** -- Use descriptive, pronounceable variable names. Always use camelCase.
- **Explicit types when broader than inferred** -- Add explicit type annotations when the variable can hold more types than what TypeScript infers (e.g., `string | null`).
- **Consistent vocabulary** -- Use the same word for the same concept throughout the codebase. Do not mix synonyms like `getUser`, `getClientData`, `getCustomerRecord`.
- **Searchable names (named constants)** -- Replace magic numbers and strings with descriptively named constants (e.g., `MILLISECONDS_PER_DAY` instead of `86400000`). Use UPPER_SNAKE_CASE for constants.
- **Explanatory variables** -- Use intermediate variables with descriptive names to break down complex expressions, especially regex matches or computed values.
- **No mental mapping** -- Avoid single-letter variable names in callbacks and loops. Use full, descriptive names so readers do not have to mentally map abbreviations.
- **No unneeded context** -- If a class or object name already provides context, do not repeat it in property names (e.g., `car.color` not `car.carColor`).
- **Default parameters over short-circuiting** -- Use default parameter values instead of `||` short-circuiting. Default parameters only replace `undefined`, not other falsy values like `''`, `0`, or `null`.

See [template.md](template.md) for correct code patterns and [examples/](examples/) for detailed incorrect/correct comparisons.

## Reference

[Clean code javascript](https://github.com/ryanmcdermott/clean-code-javascript?tab=readme-ov-file#variables)
