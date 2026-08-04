# Execution Context

## What is Execution Context?

Execution Context is the environment in which JavaScript code is executed.

Every JavaScript code runs inside an Execution Context.

---

## Types

- Global Execution Context (GEC)
- Function Execution Context (FEC)
- Eval Execution Context (Rarely used)

---

## Phases

### Creation Phase

- Memory allocation
- Function hoisting
- `var` initialized as `undefined`
- `let` & `const` stay in Temporal Dead Zone (TDZ)

### Execution Phase

- Executes code line by line
- Variables receive assigned values
- Functions execute when called

---

## Call Stack

- LIFO (Last In First Out)
- Stores execution contexts
- One function executes at a time

---

## Stack Overflow

Occurs when recursive calls exceed the Call Stack size.

---

## Interview Questions

- What is Execution Context?
- Types of Execution Context?
- Explain Creation Phase.
- Explain Execution Phase.
- What is the Call Stack?
- Why is JavaScript single-threaded?