# Async/Await Examples

## Prefer async/await over .then() chains

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
