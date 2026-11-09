# TypeScript Generic Constraints and `keyof`

## Day 22

### `keyof`

For:

```ts
type User = {
  id: number;
  name: string;
  active: boolean;
};
```

`keyof User` produces:

```ts
"id" | "name" | "active"
```

### Generic Constraint

```ts
function getValue<T, K extends keyof T>(
  obj: T,
  key: K
): T[K] {
  return obj[key];
}
```

`K extends keyof T` means the key must be one of the keys that actually exists in `T`.

### Object Constraint

```ts
function getValue<
  T extends object,
  K extends keyof T
>(obj: T, key: K): T[K] {
  return obj[key];
}
```

`T extends object` restricts `T` to object-like values.

## Interview Takeaway

- `keyof T` gives the valid property keys of `T`.
- `K extends keyof T` makes property access type-safe.
- `T extends object` can be used when a generic should accept only objects.
