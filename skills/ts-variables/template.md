# Variable Templates

## Meaningful, pronounceable name

```typescript
const currentDate = moment().format("YYYY/MM/DD");
```

## Explicit type annotation for broader types

```typescript
const nullableString: string | null = null;
```

## Consistent vocabulary

```typescript
getUser();
```

## Searchable named constants

```typescript
// Declare them as capitalized named constants.
const MILLISECONDS_PER_DAY = 60 * 60 * 24 * 1000; //86400000;

setTimeout(blastOff, MILLISECONDS_PER_DAY);
```

## Explanatory variables

```typescript
const address = "One Infinite Loop, Cupertino 95014";
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
const [_, city, zipCode] = address.match(cityZipCodeRegex) || [];
saveCityZipCode(city, zipCode);
```

## Descriptive callback variable names

```typescript
const locations = ["Austin", "New York", "San Francisco"];
locations.forEach((location) => {
  doStuff();
  doSomeOtherStuff();
  // ...
  dispatch(location);
});
```

## No unneeded context in object properties

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

## Default parameters

```typescript
const createMicrobrewery = (name?: string = "Hipster Brew Co.") {
  // ...
}
```
