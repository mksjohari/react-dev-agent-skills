---
name: ts-comments
description: TypeScript comment conventions. Use when writing comments in TypeScript code, including avoiding unnecessary comments, removing commented-out code, and only commenting business logic complexity.
user-invocable: false
---

# Comments

Comments are an apology, not a requirement. Good code should document itself.

## When to use

Use this skill when writing Typescript comments.

## Only comment things that have business logic complexity

Good code should document itself. Comments should only explain business logic that others may not have prior knowledge of.

**Incorrect:**

```typescript
/** Hashes a string to an integer **/
const hashIt = (data: string) => {
  // The hash
  let hash = 0;

  // Length of string
  const length = data.length;

  // Loop through every character in data
  for (let i = 0; i < length; i++) {
    // Get character code.
    const char = data.charCodeAt(i);
    // Make the hash
    hash = (hash << 5) - hash + char;
    // Convert to 32-bit integer
    hash &= hash;
  }
};
```

**Correct:**

```typescript
const hashStringToInt = (data) => {
  let hash = 0;
  const length = data.length;

  for (let i = 0; i < length; i++) {
    const char = data.charCodeAt(i);
    hash = (hash << 5) - hash + char;

    // Convert to 32-bit integer
    hash &= hash;
  }
};
```

## Don't leave commented out code in the codebase

Version control exists for a reason.

**Incorrect:**

```typescript
doStuff();
// doOtherStuff();
// doSomeMoreStuff();
// doSoMuchStuff();
```

**Correct:**

```typescript
doStuff();
```

## Reference

[Clean code javascript](https://github.com/ryanmcdermott/clean-code-javascript?tab=readme-ov-file#comments)
