# Interface Templates

## Basic Interface Definition

```typescript
interface IMyInterface {
  propertyOne: string;
  propertyTwo: number;
  optionalProperty?: boolean;
}
```

## Interface Composition with Extends

```typescript
interface IBase {
  id: string;
}

interface IExtended extends IBase {
  name: string;
}

interface ICombined extends IBase, IExtended {
  additionalProp: boolean;
}
```
