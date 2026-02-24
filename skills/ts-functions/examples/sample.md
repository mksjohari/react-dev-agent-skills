# Function Examples

## Arrow function syntax

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

## Explicit type signatures

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

## Early returns over nested if/else

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

## 2 or fewer arguments (destructured object)

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

## Single responsibility

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

## Descriptive names

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

## One level of abstraction

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

## No duplicate code

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

## Default objects with Object.assign

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

## No boolean flag parameters

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

## Avoid side effects (part 1 - global state)

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

## Avoid side effects (part 2 - immutability)

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

## No global function pollution

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

## Functional over imperative

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
