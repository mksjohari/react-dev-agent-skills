# React repo structure templates

## Component folder template

```
components/
  └── MyAwesomeComponent/
    └── MyAwesomeComponent.tsx
    └── MyAwesomeComponent.test.tsx
    └── MyAwesomeComponent.service.ts
    └── MyAwesomeComponent.service.test.ts
    └── index.ts
  └── index.ts
```

## Hook folder template

```
hooks/
  └── myFirstHook/
    └── myFirstHook.ts
    └── myFirstHook.test.tsx
    └── myFirstHook.service.ts
    └── myFirstHook.service.test.ts
    └── index.ts
  └── index.ts
```

## Page folder template

```
pages/
  └── FirstPage/
    └── FirstPage.tsx
    └── FirstPage.test.tsx
    └── FirstPage.service.ts
    └── FirstPage.service.test.ts
    └── index.ts
  └── index.ts
```

## Barrel export pattern

```typescript
// index.ts
export * from "./MyAwesomeComponent";
```
