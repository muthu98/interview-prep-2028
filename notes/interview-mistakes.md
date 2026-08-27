# 🚨 Interview Mistakes

---

## Sliding Window

### Mistake

Initially scanned the entire window to find duplicates.

### Correct Approach

Use a Set to detect duplicates.

Move the left pointer while removing elements from the Set.

---

## Kadane's Algorithm

### Mistake

Initially focused only on the maximum sum.

### Learning

Also track the start and end indices if required.

---

## JavaScript

### Mistake

Forgot that const allows object and array mutation.

### Learning

const prevents reassignment, not mutation.

# Day 5

## LeetCode 567

### Mistakes

- Initially confused between `Map.size` and window length.
- Wanted to reset the window instead of sliding it.
- Tried to optimize before completing the correct solution.
- Forgot that only the entering and leaving characters change during each slide.

### Learning

Always write the correct solution first.

Optimize only after identifying repeated work.

# Day 6

## LeetCode 121

### Mistakes

- Initially thought `left++`.
- Learned `left` should always point to the minimum price seen so far.
- Understood why `left = right` is the correct update.

### Learning

Two Pointers is about tracking the best positions, not maintaining a window.

# Day 7

## Binary Search

### Mistakes

- Initially used `left < right`.
- Initially moved pointers to `mid`.
- Learned to use `left <= right`.
- Learned to update pointers with `mid + 1` and `mid - 1`.

---

## JavaScript

### Mistakes

- Initially thought `let` and `const` are not hoisted.
- Learned they are hoisted but remain uninitialized inside the Temporal Dead Zone.


# Day 8

## Binary Search

### Mistake

Initially tried to determine the insertion position using `mid`.

### Learning

Always return `left` after the loop.

---

### Mistake

Thought `left == right` required special handling.

### Learning

The standard Binary Search template handles it naturally.

---

## JavaScript

### Mistake

Defined Execution Context by describing its phases instead of defining it.

### Learning

Execution Context is the environment where JavaScript code executes.

---

### Mistake

Remembered only one Microtask and one Macrotask example.

### Learning

Microtasks:
- Promise.then()
- Promise.catch()
- Promise.finally()
- queueMicrotask()

Macrotasks:
- setTimeout()
- setInterval()
- DOM Events


# Day 9

## JavaScript

Mistake

Confused global scope with regular function under strict mode.

Correct

Global scope

Browser

this === window

Regular Function

Non strict

this === window

Strict

this === undefined

---

Improvement

Instead of saying

"this refers to window"

Say

"this depends on how the function is invoked."

---

Minor

Function declaration vs function expression does not affect `this`.

Function invocation does.

# Day 10

## DSA

Initial idea:

Maintain only one minimum value.

Issue:

Cannot restore the previous minimum after popping the current minimum.

Solution:

Maintain a second stack to track minimum values.

---

## JavaScript

Mistake

Said classes store their own methods.

Correct

Class methods are stored on the class prototype.

Classes are syntactic sugar over constructor functions.


# Day 11

## DSA

### Mistake

Concern:

> Moving all `stack2` elements to `stack1` is O(n), so won't the solution be inefficient?

### Correction

A single transfer is O(n), but each element is transferred at most once.

Therefore:

- `pop()` → O(1) amortized
- `peek()` → O(1) amortized

---

## JavaScript

### Mistake 1

❌ `var` is global.

✅ `var` is function-scoped.

### Mistake 2

❌ Higher-order function means a function that returns another function.

✅ A higher-order function can accept a function, return a function, or both.

### Mistake 3

Initially needed clarification on why:

```js
var
```

produces:

```text
3
3
3
```

while:

```js
let
```

produces:

```text
0
1
2
```

### Correct Understanding

`var` → shared binding.

`let` → separate binding for each loop iteration.

---

# Day 12

## DSA

### Mistake

Used new `ListNode` instances, and then object spread, to build the reversed list.

Both approaches produced the correct values but created one new object per node, so they used O(n) extra space and did not reverse the original nodes in place.

### Correction

Save the next node before changing the current link:

```js
const next = head.next;
head.next = previous;
```

Then advance `previous` and `head`. Reusing the existing nodes reduces extra space to O(1).

### Complexity Nuance

Linked-list insertion or deletion is not always O(1). The pointer change is O(1) when the relevant reference is already known, but locating a node, its predecessor, or the tail can require O(n) traversal.

---

# Day 13

## DSA

### Correction 1

Initially planned to store every node and its position in a `Map`.

The position is not needed for cycle detection. A `Set` of visited node references is sufficient and expresses the requirement more clearly.

### Correction 2

Cycle detection must compare node references, not node values. Two different nodes may contain the same value without forming a cycle.

---

# Day 14

## DSA

### Mistake

Used object spread to copy selected nodes while merging two sorted linked lists.

Renaming the result pointers to `mergedHead` and `tail` made their roles clearer, but the copied nodes still caused extra space usage.

### Correction

Connect the selected existing node directly to `tail.next`, advance `tail`, and then advance only the input list whose node was selected.

The final solution reuses the original nodes and achieves O(1) extra space.

---

# Day 15

## DSA

### Incomplete Optimization

The length-based solution was correct and had optimal Big-O complexity, but it used two passes and did not satisfy the one-pass follow-up.

### Correction

Use a dummy node and maintain an `n + 1` gap between fast and slow pointers. When `fast` reaches `null`, `slow` is immediately before the node to remove.

## JavaScript

### Mistake 1

Used `map` with an async callback and expected one combined Promise.

### Correction

Async `map` returns an array of Promises. Return one outer Promise and settle it explicitly.

### Mistake 2

Awaited an input and then attempted to call `.then()` on its resolved value.

### Correction

Normalize the original input with `Promise.resolve(value)` before attaching handlers.

### Mistake 3

Returned a results array from the Promise executor and stored rejection reasons as successful results.

### Correction

Returning from the executor does not settle the Promise. Call `resolve(results)` only after all inputs fulfill, and call `reject(error)` immediately when one input rejects.
