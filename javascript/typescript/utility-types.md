# TypeScript Utility Types

## Day 23

### `Partial<T>`

Makes every property optional.

### `Required<T>`

Makes every property required.

### `Pick<T, K>`

Keeps only the selected keys.

### `Omit<T, K>`

Removes the selected keys.

### `Record<K, T>`

Creates an object type whose keys are `K` and whose values are `T`.

Example:

```ts
type User = {
  id: number;
  name: string;
  email: string;
};

type UpdateUser = Partial<User>;
type RequiredUser = Required<UpdateUser>;
type UserPreview = Pick<User, "id" | "name">;
type PublicUser = Omit<User, "email">;
type UserMap = Record<string, User>;
```

## Interview Shortcut

- Partial = optional
- Required = mandatory
- Pick = keep
- Omit = remove
- Record = key/value object type
