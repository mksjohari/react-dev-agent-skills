---
name: ts-enums
description: TypeScript enum conventions. Use when doing string comparisons, working with finite value sets, magic strings, or defining enums in TypeScript code.
user-invocable: false
---

# TypeScript Enums

When there is a situation where you want to do string comparisons for a finite amount of known values, always prefer to use enums over using types or string literal comparisons.

## Rules

1. **Always use enums over magic strings.** Enums are easier to change and manage than raw string literals or union types.
2. **Place enums in an `enum.ts` file.** Keep enum definitions centralized and importable.

## When to Use

Use this skill when doing any form of string comparisons for a finite set of known values.

## Templates and Examples

- See `template.md` for the standard enum definition and usage pattern.
- See `examples/sample.md` for correct and incorrect usage examples.
