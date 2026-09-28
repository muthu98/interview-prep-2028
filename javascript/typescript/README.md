# TypeScript Interview Notes

## Day 20 — Generics vs `any` Basics

Initial explanation: a generic adapts to the type passed in. The key refinement is that it preserves type information and the relationship between input and output at compile time.

```ts
function identity<T>(value: T): T {
    return value;
}

const text = identity("hello");
const number = identity(123);
```

TypeScript infers the return types from the arguments. A signature such as `identity(value: any): any` loses that relationship; `any` bypasses checking on the value and can allow invalid method calls to reach runtime.

Interview answer: "Generics let reusable code work with different types while preserving type safety; `any` gives up that checking."

- [x] Explain basic generic input/output relationships and inference.
- [x] Explain why `any` weakens type safety.
- [ ] Re-explain the distinction without notes.

Scope: basics only; advanced generics are not marked complete.
