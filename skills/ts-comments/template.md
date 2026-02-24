# Comment Templates

## When to Comment: Business Logic Complexity

Only add comments when there is non-obvious business logic that requires context.

```typescript
const processOrder = (order: IOrder) => {
  const total = calculateTotal(order.items);

  // Discount of 15% is applied for orders over $100 per business rule BR-2041
  const discount = total > 100 ? total * 0.15 : 0;

  return total - discount;
};
```

## When NOT to Comment

Do not comment self-explanatory code. Use descriptive variable and function names instead.

```typescript
// Let the code speak for itself
const userFullName = `${firstName} ${lastName}`;
const isEligibleForDiscount = orderTotal > MINIMUM_DISCOUNT_THRESHOLD;
```
