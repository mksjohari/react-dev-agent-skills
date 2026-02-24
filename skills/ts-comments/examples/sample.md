# Comment Examples

## Only comment things that have business logic complexity

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
