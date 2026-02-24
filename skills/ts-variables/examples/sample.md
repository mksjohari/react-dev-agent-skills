# Variable Examples

## Meaningful, pronounceable names

**Incorrect:**

```typescript
const yyyymmddstr = moment().format("YYYY/MM/DD");
```

**Correct:**

```typescript
const currentDate = moment().format("YYYY/MM/DD");
```

## Explicit types when broader than inferred

**Incorrect:**

```typescript
const nullableString = null;
```

**Correct:**

```typescript
const nullableString: string | null = null;
```

## Consistent vocabulary

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

## Searchable names (named constants)

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

## Explanatory variables

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

## No mental mapping

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

## No unneeded context

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

## Default parameters over short-circuiting

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
