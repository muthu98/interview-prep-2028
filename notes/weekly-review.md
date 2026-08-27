# 📅 Weekly Review

## Review Period

**Day 1 → Day 15**

---

## 🎯 Overall Progress

This period focused on building a strong foundation for technical interviews across:

- DSA pattern recognition
- DSA problem solving
- JavaScript fundamentals
- JavaScript internals
- Interview explanation skills

The main improvement has been moving from simply solving problems to understanding **why a particular approach works and how to explain it**.

---

# 📊 Progress Summary

## DSA

### Patterns Covered

- Hashing
- Two Pointers
- Sliding Window
- Prefix / Suffix
- Binary Search
- Stack
- Queue
- Linked List
- Kadane's Algorithm

### Problems Solved

**15 problems**

The focus was not only on getting accepted solutions, but also on:

- Identifying the underlying pattern
- Thinking about alternative approaches
- Understanding complexity
- Questioning whether an approach remains efficient with repeated operations
- Improving interview explanation

---

## JavaScript

### Topics Covered

- var / let / const
- Hoisting
- TDZ
- Execution Context
- Call Stack
- Event Loop
- Promises
- Async / Await
- Type Coercion
- Closures
- `this`
- `call()`
- `apply()`
- `bind()`
- Prototype
- Prototype Chain
- `Object.create()`
- `new`
- First-Class Functions
- Higher-Order Functions
- Debounce
- Throttle
- Custom `Promise.all`

The focus has gradually moved from JavaScript syntax toward **JavaScript runtime behavior and internals**.

---

# 💡 Biggest Learning This Period

## DSA

The biggest improvement is understanding that an operation being **O(n) once** does not automatically mean the entire algorithm is O(n) for every sequence of operations.

This became clear while learning Queue using Stacks and understanding **amortized complexity**.

The learning approach is becoming:

> Don't just ask "What is the complexity of this operation?"

Also ask:

> "How often can this expensive operation actually happen?"

---

## JavaScript

The biggest improvement is understanding relationships between concepts rather than learning them independently.

Examples:

```text
Lexical Scope
     ↓
Closures
     ↓
var / let behavior
     ↓
Async callbacks
     ↓
Event Loop
