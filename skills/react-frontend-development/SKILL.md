---
name: react-frontend-development
description: React frontend development guidelines. This skill should be used when writing, reveiewing or refactoring React code in Typescript and Javascript to ensure optimal coding style and patterns.
metadata:
  author: jasontslxd
  version: "1.0"
---

# React frontend development guidelines

Comprehensive development guidelines for React applications in Javascript or Typescript. Use this skill when the user needs to work with React code and/or Javascript and Typescript files, i.e. `.js`, `.jsx`, `.ts` and `.tsx` files.

## When to apply

Reference these guidelines when:

- Creating new React components
- Implementing data fetching
- Refactoring existing React code

## How to use

Read individual reference files for detailed explanations and code examples. The references are grouped in the following categories:

| Category                | Importance | Prefix |
| ----------------------- | ---------- | ------ |
| React coding style      | CRITICAL   | style  |
| React data fetching     | CRITICAL   | data   |
| Typescript coding style | HIGH       | ts     |

Each rule file contains:

- Brief explanation of why it matters
- Incorrect code example with explanation
- Correct code example with explanation
- Additional context and references

## Quick overview

### 1. React coding style

- [style-repo-structure](references/style-repo-structure.md) - How to structure React code in a repository
- [style-component-structure](references/style-component-structure.md) - How to create structured React components
- [style-hook-structure](references/style-hook-structure.md) - How to create structured React hooks

### 2. React data fetching

- [data-tanstack-query](references/data-tanstack-query.md) - How to make API calls in React using Tanstack Query
- [data-component-fetching](references/data-component-fetching.md) - How to use the Tanstack Query hooks inside a React component

### 3. Typescript coding style

- [ts-variables](references/ts-variables.md) - How to properly use Typescript variables
- [ts-interfaces](references/ts-interfaces.md) - How to properly use Typescript interfaces
- [ts-functions](references/ts-functions.md) - How to properly use Typescript functions
- [ts-concurrency](references/ts-concurrency.md) - How to properly use Typescript concurrency
- [ts-comments](references/ts-comments.md) - How to properly use Typescript comments
- [ts-error-handling](references/ts-error-handling.md) - How to properly handle Typescript errors
