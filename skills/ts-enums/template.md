# Enum Templates

## Enum Definition (in enum.ts)

```typescript
// enum.ts
export enum MyEnum {
  ValueOne = "valueOne",
  ValueTwo = "valueTwo",
  ValueThree = "valueThree",
}
```

## Enum Usage

```typescript
import { MyEnum } from "./enum";

const currentValue = MyEnum.ValueOne;

if (currentValue === MyEnum.ValueOne) {
  // handle ValueOne
} else if (currentValue === MyEnum.ValueTwo) {
  // handle ValueTwo
} else if (currentValue === MyEnum.ValueThree) {
  // handle ValueThree
}
```
