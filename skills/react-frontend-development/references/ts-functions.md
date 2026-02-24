---
title: Typescript function conventions
description: Functions should be simple, straightforward and have clear separation of concerns
---

# Functions

Functions should be simple, straightforward and have clear separation of concerns. All function names should be in camelCase.

## When to use

Use this skill when working with Typescript functions.

## Functions should always be defined using the arrow syntax

Arrow functions provide a more precise syntax, a more predictable `this` binding and seamless integration with Typescript's type annotations.

**Incorrect:**

```typescript
function foo(bar) {
  // do something
}
```

**Correct:**

```typescript
const foo = (bar: string) => {
  // do something
};
```

## Explicit types the function signatures

Always use explicit types for function signatures and avoid the any type. Explicitly type the return as well.

**Incorrect:**

```typescript
const combine = (val1: any, val2: any): any => {
  if (
    (typeof val1 === "number" && typeof val2 === "number") ||
    (typeof val1 === "string" && typeof val2 === "string")
  ) {
    return val1 + val2;
  }

  throw new Error("Must be of type String or Number");
};
```

**Correct:**

```typescript
const combine = (val1: number, val2: number): number => {
  return val1 + val2;
};
```

## Prefer early returns over if else

This reduces the number of nested layers

**Incorrect:**

```typescript
const someCondition = (condition1: boolean, condition2: boolean) => {
  if (condition1) {
    if (condition2) {
      // do something
    }
  }
};
```

**Correct:**

```typescript
const someCondition = (condition1: boolean, condition2: boolean) => {
  if (!condition1) return;
  if (!condition2) return;
  // do something
};
```

## Function arguments should have 2 or fewer arguments (ideally)

Limiting the amount of function parameters is incredibly important because it makes testing your function easier. Having more than three leads to a combinatorial explosion where you have to test tons of different cases with each separate argument. Usually, if you have more than two arguments then your function is trying to do too much. In cases where it's not, most of the time an object will suffice as an argument.

To make it obvious what properties the function expects, you can use the ES2015/ES6 destructuring syntax. This has a few advantages:

1. When someone looks at the function signature, it's immediately clear what properties are being used.
2. It can be used to simulate named parameters.
3. Destructuring also clones the specified primitive values of the argument object passed into the function. This can help prevent side effects. Note: objects and arrays that are destructured from the argument object are NOT cloned.
4. Linters can warn you about unused properties, which would be impossible without destructuring.

**Incorrect:**

```typescript
const createMenu = (title, body, buttonText, cancellable) => {
  // ...
};
```

**Correct:**

```typescript
interface ICreateMenuProps {
  title: string;
  body: string;
  buttonText: string;
  cancellable: boolean;
}

const createMenu = ({
  title,
  body,
  buttonText,
  cancellable,
}: ICreateMenuProps) => {
  // ...
};
```

## Functions should do one thing

This is by far the most important rule in software engineering. When functions do more than one thing, they are harder to compose, test, and reason about. When you can isolate a function to just one action, it can be refactored easily and your code will read much cleaner.

**Incorrect:**

```typescript
const emailClients = (clients) => {
  clients.forEach((client) => {
    const clientRecord = database.lookup(client);
    if (clientRecord.isActive()) {
      email(client);
    }
  });
};
```

**Correct:**

```typescript
const emailActiveClients = (clients) => {
  clients.filter(isActiveClient).forEach(email);
};

const isActiveClient = (client) => {
  const clientRecord = database.lookup(client);
  return clientRecord.isActive();
};
```

## Function names should say what they do

**Incorrect:**

```typescript
const addToDate = (date, month) => {
  // ...
};

const date = new Date();

// It's hard to tell from the function name what is added
addToDate(date, 1);
```

**Correct:**

```typescript
const addMonthToDate = (month, date) {
  // ...
}

const date = new Date();
addMonthToDate(1, date);
```

## Functions should only be one level of abstraction

When you have more than one level of abstraction your function is usually doing too much. Splitting up functions leads to reusability and easier testing.

**Incorrect:**

```typescript
const parseBetterJSAlternative = (code) => {
  const REGEXES = [
    // ...
  ];

  const statements = code.split(" ");
  const tokens = [];
  REGEXES.forEach((REGEX) => {
    statements.forEach((statement) => {
      // ...
    });
  });

  const ast = [];
  tokens.forEach((token) => {
    // lex...
  });

  ast.forEach((node) => {
    // parse...
  });
};
```

**Correct:**

```typescript
const parseBetterJSAlternative = (code) => {
  const tokens = tokenize(code);
  const syntaxTree = parse(tokens);
  syntaxTree.forEach((node) => {
    // parse...
  });
};

const tokenize = (code) => {
  const REGEXES = [
    // ...
  ];

  const statements = code.split(" ");
  const tokens = [];
  REGEXES.forEach((REGEX) => {
    statements.forEach((statement) => {
      tokens.push(/* ... */);
    });
  });

  return tokens;
};

const parse = (tokens) => {
  const syntaxTree = [];
  tokens.forEach((token) => {
    syntaxTree.push(/* ... */);
  });

  return syntaxTree;
};
```

## Remove duplicate code

Do your absolute best to avoid duplicate code. Duplicate code is bad because it means that there's more than one place to alter something if you need to change some logic.

Oftentimes you have duplicate code because you have two or more slightly different things, that share a lot in common, but their differences force you to have two or more separate functions that do much of the same things. Removing duplicate code means creating an abstraction that can handle this set of different things with just one function/module/class.

**Incorrect:**

```typescript
const showDeveloperList = (developers) => {
  developers.forEach((developer) => {
    const expectedSalary = developer.calculateExpectedSalary();
    const experience = developer.getExperience();
    const githubLink = developer.getGithubLink();
    const data = {
      expectedSalary,
      experience,
      githubLink,
    };

    render(data);
  });
};

const showManagerList = (managers) => {
  managers.forEach((manager) => {
    const expectedSalary = manager.calculateExpectedSalary();
    const experience = manager.getExperience();
    const portfolio = manager.getMBAProjects();
    const data = {
      expectedSalary,
      experience,
      portfolio,
    };

    render(data);
  });
};
```

**Correct:**

```typescript
const showEmployeeList = (employees) => {
  employees.forEach((employee) => {
    const expectedSalary = employee.calculateExpectedSalary();
    const experience = employee.getExperience();

    const data = {
      expectedSalary,
      experience,
    };

    switch (employee.type) {
      case "manager":
        data.portfolio = employee.getMBAProjects();
        break;
      case "developer":
        data.githubLink = employee.getGithubLink();
        break;
    }

    render(data);
  });
};
```

## Set default objects with Object.assign

**Incorrect:**

```typescript
const menuConfig = {
  title: null,
  body: "Bar",
  buttonText: null,
  cancellable: true,
};

const createMenu = (config) => {
  config.title = config.title || "Foo";
  config.body = config.body || "Bar";
  config.buttonText = config.buttonText || "Baz";
  config.cancellable =
    config.cancellable !== undefined ? config.cancellable : true;
};

createMenu(menuConfig);
```

**Correct:**

```typescript
const menuConfig = {
  title: "Order",
  // User did not include 'body' key
  buttonText: "Send",
  cancellable: true,
};

function createMenu(config) {
  let finalConfig = Object.assign(
    {
      title: "Foo",
      body: "Bar",
      buttonText: "Baz",
      cancellable: true,
    },
    config,
  );
  return finalConfig;
}

// config now equals: {title: "Order", body: "Bar", buttonText: "Send", cancellable: true}
createMenu(menuConfig);
```

## Don't use flags as function parameters

Flags tell your user that this function does more than one thing. Functions should do one thing. Split out your functions if they are following different code paths based on a boolean.

**Incorrect:**

```typescript
const createFile = (name, temp) => {
  if (temp) {
    fs.create(`./temp/${name}`);
  } else {
    fs.create(name);
  }
};
```

**Correct:**

```typescript
const createFile = (name) => {
  fs.create(name);
};

const createTempFile = (name) => {
  createFile(`./temp/${name}`);
};
```

## Avoid side effects (part 1)

A function produces a side effect if it does anything other than take a value in and return another value or values. You do need to have side effects in a program on occasion. Like the previous example, you might need to write to a file. What you want to do is to centralize where you are doing this. Don't have several functions and classes that write to a particular file. Have one service that does it. One and only one.

**Incorrect:**

```typescript
// Global variable referenced by following function.
// If we had another function that used this name, now it'd be an array and it could break it.
let name = "Ryan McDermott";

const splitIntoFirstAndLastName = () => {
  name = name.split(" ");
};

splitIntoFirstAndLastName();

console.log(name); // ['Ryan', 'McDermott'];
```

**Correct:**

```typescript
const splitIntoFirstAndLastName = (name) => {
  return name.split(" ");
};

const name = "Ryan McDermott";
const newName = splitIntoFirstAndLastName(name);

console.log(name); // 'Ryan McDermott';
console.log(newName); // ['Ryan', 'McDermott'];
```

## Avoid side effects (part 2)

In Typescript, some values are unchangeable (immutable) and some are changeable (mutable). Objects and arrays are two kinds of mutable values so it's important to handle them carefully when they're passed as parameters to a function. A function can change an object's properties or alter the contents of an array which could easily cause bugs elsewhere.

A solution would be for the function to always clone the array or object, edit it, and return the clone. This would ensure that functions that are still using the old object or array wouldn't be affected by the changes.

**Incorrect:**

```typescript
const addItemToCart = (cart, item) => {
  cart.push({ item, date: Date.now() });
};
```

**Correct:**

```typescript
const addItemToCart = (cart, item) => {
  return [...cart, { item, date: Date.now() }];
};
```

## Dont write to global functions

Polluting globals is a bad practice because you could clash with another library and the user of your API would be none-the-wiser until they get an exception in production.

**Incorrect:**

```typescript
Array.prototype.diff = (comparisonArray) => {
  const hash = new Set(comparisonArray);
  return this.filter((elem) => !hash.has(elem));
};
```

**Correct:**

```typescript
class SuperArray extends Array {
  diff(comparisonArray) {
    const hash = new Set(comparisonArray);
    return this.filter((elem) => !hash.has(elem));
  }
}
```

## Favor functional programming over imperative programming

Functional programming styles are easier to read and test.

**Incorrect:**

```typescript
const programmerOutput = [
  {
    name: "Uncle Bobby",
    linesOfCode: 500,
  },
  {
    name: "Suzie Q",
    linesOfCode: 1500,
  },
];

let totalOutput = 0;

for (let i = 0; i < programmerOutput.length; i++) {
  totalOutput += programmerOutput[i].linesOfCode;
}
```

**Correct:**

```typescript
const programmerOutput = [
  {
    name: "Uncle Bobby",
    linesOfCode: 500,
  },
  {
    name: "Suzie Q",
    linesOfCode: 1500,
  },
];

const totalOutput = programmerOutput.reduce(
  (totalLines, output) => totalLines + output.linesOfCode,
  0,
);
```

## Encapsulate conditionals

**Incorrect:**

```typescript
if (fsm.state === "fetching" && isEmpty(listNode)) {
  // ...
}
```

**Correct:**

```typescript
const shouldShowSpinner = (fsm, listNode) => {
  return fsm.state === "fetching" && isEmpty(listNode);
};

if (shouldShowSpinner(fsmInstance, listNodeInstance)) {
  // ...
}
```

## Avoid negative conditionals

**Incorrect:**

```typescript
const isDOMNodeNotPresent = (node) => {
  // ...
};

if (!isDOMNodeNotPresent(node)) {
  // ...
}
```

**Correct:**

```typescript
const isDOMNodePresent = (node) => {
  // ...
};

if (isDOMNodePresent(node)) {
  // ...
}
```

## Remove dead code

Dead code is just as bad as duplicate code. There's no reason to keep it in your codebase with tools for version control.

**Incorrect:**

```typescript
const oldRequestModule = (url) => {
  // ...
};

const newRequestModule = (url) => {
  // ...
};

const req = newRequestModule;
inventoryTracker("apples", req, "www.inventory-awesome.io");
```

**Correct:**

```typescript
const newRequestModule = (url) => {
  // ...
};

const req = newRequestModule;
inventoryTracker("apples", req, "www.inventory-awesome.io");
```

## References

[Clean code javascript](https://github.com/ryanmcdermott/clean-code-javascript?tab=readme-ov-file#functions)
