---
name: ts-interfaces
description: TypeScript interface conventions. Use when defining TypeScript interfaces or type aliases, including preferring interfaces over types, using the "I" prefix for interface names, and extending interfaces.
user-invocable: false
---

# TypeScript Interfaces

Type aliases and interfaces are very similar, and in many cases you can choose between them freely. Almost all features of an interface are available in type, the key distinction is that a type cannot be re-opened to add new properties vs an interface which is always extendable. Furthermore, TypeScript recommends using interfaces over type aliases because of performance and display gains.

## Rules

1. **Always use interfaces over type aliases.** Interfaces are extendable, perform better at compile time, and produce cleaner error messages.
2. **Prefix interface names with "I".** This makes interfaces immediately identifiable when reading code (e.g., `ISomeInterface`).
3. **Use `extends` for composition.** When combining multiple interfaces, use the `extends` keyword rather than intersection types (`&`).

## When to Use

Use this skill when creating TypeScript interface or type definitions.

## Templates and Examples

- See `template.md` for the standard interface definition and composition patterns.
- See `examples/sample.md` for correct and incorrect usage examples.

## Reference

[TypeScript documentation on performance](https://github.com/microsoft/TypeScript/wiki/Performance#preferring-interfaces-over-intersections)
