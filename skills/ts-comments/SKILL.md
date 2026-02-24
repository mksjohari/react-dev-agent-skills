---
name: ts-comments
description: TypeScript comment conventions. Use when writing comments in TypeScript code, including avoiding unnecessary comments, removing commented-out code, and only commenting business logic complexity.
user-invocable: false
---

# Comments

Comments are an apology, not a requirement. Good code should document itself.

## Rules

1. **Only comment things that have business logic complexity.** Comments should only explain business logic that others may not have prior knowledge of. Do not comment obvious operations -- let descriptive naming do the work.
2. **Never leave commented-out code in the codebase.** Version control exists for a reason. Delete unused code rather than commenting it out.

## When to Use

Use this skill when writing TypeScript comments.

## Templates and Examples

- See `template.md` for the pattern showing when and how to comment.
- See `examples/sample.md` for correct and incorrect usage examples.

## Reference

[Clean code javascript](https://github.com/ryanmcdermott/clean-code-javascript?tab=readme-ov-file#comments)
