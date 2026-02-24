---
name: ts-async
description: TypeScript async/await conventions. Use when working with promises, async/await, callbacks, or asynchronous code patterns in TypeScript.
user-invocable: false
---

# Always prefer async/await over callbacks and promises

Using the async await syntax we get a cleaner solution without any `then` chains of functions.

**Incorrect:**

```typescript
import { get } from "request-promise";
import { writeFile } from "fs-extra";

get("https://en.wikipedia.org/wiki/Robert_Cecil_Martin")
  .then((body) => {
    return writeFile("article.html", body);
  })
  .then(() => {
    console.log("File written");
  })
  .catch((err) => {
    console.error(err);
  });
```

**Correct:**

```typescript
import { get } from "request-promise";
import { writeFile } from "fs-extra";

const getCleanCodeArticle = async () => {
  try {
    const body = await get("https://en.wikipedia.org/wiki/Robert_Cecil_Martin");
    await writeFile("article.html", body);
    console.log("File written");
  } catch (err) {
    console.error(err);
  }
};

getCleanCodeArticle();
```

## When to use

Use this skill when working with Typescript promises and callbacks.

## Reference

[Clean code javascript](https://github.com/ryanmcdermott/clean-code-javascript?tab=readme-ov-file#concurrency)
