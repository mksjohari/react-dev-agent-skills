---
title: Typescript variable conventions
description: Variables names should be simple, meaningful and clear that explain what they do
---

# Variables

Variables names should have simple, meaningful and clear names that explain what they do. Variables names should also always be in camelCase.

## When to use

Use this skill when working with Typescript variables.

## Use meaningful and ponounceable variable names

**Incorrect:**

```typescript
const yyyymmddstr = moment().format("YYYY/MM/DD");
```

**Correct:**

```typescript
const currentDate = moment().format("YYYY/MM/DD");
```

## Always type the variables if they can be more than the inferred type

**Incorrect:**

```typescript
const nullableString = null;
```

**Correct:**

```typescript
const nullableString: string | null = null;
```

## Use the same vocabulary for the variables describing the same thing

**Incorrect:**

```typescript
getUserInfo();
getClientData();
getCustomerRecord();
```

**Correct:**

```typescript
getUser();
```

## Use searchable names

**Incorrect:**

```typescript
// What the heck is 86400000 for?
setTimeout(blastOff, 86400000);
```

**Correct:**

```typescript
// Declare them as capitalized named constants.
const MILLISECONDS_PER_DAY = 60 * 60 * 24 * 1000; //86400000;

setTimeout(blastOff, MILLISECONDS_PER_DAY);
```

## Use explanatory variables

**Incorrect:**

```typescript
const address = "One Infinite Loop, Cupertino 95014";
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
saveCityZipCode(
  address.match(cityZipCodeRegex)[1],
  address.match(cityZipCodeRegex)[2],
);
```

**Correct:**

```typescript
const address = "One Infinite Loop, Cupertino 95014";
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
const [_, city, zipCode] = address.match(cityZipCodeRegex) || [];
saveCityZipCode(city, zipCode);
```

## Avoid mental mapping

Explicit creates readable code

**Incorrect:**

```typescript
const locations = ["Austin", "New York", "San Francisco"];
locations.forEach((l) => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  // Wait, what is `l` for again?
  dispatch(l);
});
```

**Correct:**

```typescript
const locations = ["Austin", "New York", "San Francisco"];
locations.forEach((location) => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  dispatch(location);
});
```

## Don't add unneeded context

If your class / object name provides some context, no need to repeat that in the variable name.

**Incorrect:**

```typescript
const Car = {
  carMake: "Honda",
  carModel: "Accord",
  carColor: "Blue",
};

const paintCar = (car, color) => {
  car.carColor = color;
};
```

**Correct:**

```typescript
const Car = {
  make: "Honda",
  model: "Accord",
  color: "Blue",
};

const paintCar = (car, color) => {
  car.color = color;
};
```

## Use default parameters instead of short circuiting or conditionals

Default parameters are often cleaner than short circuiting. Be aware that if you use them, your function will only provide default values for undefined arguments. Other "falsy" values such as '', "", false, null, 0, and NaN, will not be replaced by a default value.

**Incorrect:**

```typescript
const createMicrobrewery = (name?: string) => {
  const breweryName = name || "Hipster Brew Co.";
  // ...
};
```

**Correct:**

```typescript
const createMicrobrewery = (name?: string = "Hipster Brew Co.") {
  // ...
}
```

## Reference

[Clean code javascript](https://github.com/ryanmcdermott/clean-code-javascript?tab=readme-ov-file#variables)
