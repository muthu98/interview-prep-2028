# TypeScript Type System Basics

## Day 21 — Introductory Coverage

Covered annotations, `unknown` vs `any`, `interface` vs `type`, union vs intersection, optional properties, and readonly objects/arrays/tuples.

```typescript
const count: number = 3;
function label(id: number): string { return String(id); }

let input: unknown = "task";
if (typeof input === "string") input.toUpperCase();
// unknown requires narrowing; any bypasses these checks.

interface Task {
  readonly id: number;
  title: string;
  description?: string;
}
type Status = "TODO" | "DONE"; // union: one of the alternatives
type TaskWithStatus = Task & { status: Status }; // intersection: both shapes

const tags: readonly string[] = ["study"];
const pair: readonly [number, string] = [1, "Task"];
```

- Annotations describe expected types at compile time; they do not validate incoming JSON at runtime.
- `unknown` accepts any value but requires narrowing before unsafe use. `any` disables checking and can spread unchecked values.
- Both interfaces and type aliases describe object shapes. Interfaces support declaration merging and extension; type aliases also name unions, primitives, and tuples. Neither is universally better.
- A union (`A | B`) accepts alternatives; narrow before accessing members not shared by all alternatives. An intersection (`A & B`) must satisfy both types; conflicting property requirements can make a type unusable.
- `description?` permits omission; reading it may yield `undefined`.
- `readonly` prevents reassignment through that typed reference. Readonly arrays/tuples prohibit mutations such as `push` or index assignment. These are compile-time restrictions, not runtime freezing or automatically deep immutability.

## Revision

Explain the difference between a const binding and readonly properties, and demonstrate safe narrowing of unknown input.

