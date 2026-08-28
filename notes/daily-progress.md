# 📅 Daily Progress

---

## Day 1 ✅

### DSA

- LeetCode 217 - Contains Duplicate
- Pattern: Hashing

### JavaScript

- Set Basics

---

## Day 2 ✅

### DSA

- LeetCode 238 - Product of Array Except Self
- Pattern: Prefix & Suffix

### JavaScript

- Promise
- Async / Await

---

## Day 3 ✅

### DSA

- LeetCode 53 - Maximum Subarray
- Pattern: Kadane's Algorithm

### JavaScript

- Type Coercion
- == vs ===

---

## Day 4 ✅

### DSA

- LeetCode 3 - Longest Substring Without Repeating Characters
- Pattern: Sliding Window

### JavaScript

- var vs let vs const

## Day 5 ✅

### DSA

- LeetCode 567 - Permutation in String
- Fixed Sliding Window
- Frequency Map
- Window Maintenance
- Discussed optimized solution using Matches

### JavaScript

- Closures
- Lexical Scope
- Independent Closures
- Private Variables

## Day 6 ✅

### DSA

- LeetCode 121 - Best Time to Buy and Sell Stock
- Two Pointers
- Minimum Price Tracking
- Maximum Profit

### JavaScript

- Promises
- Promise States
- resolve()
- reject()
- then()
- catch()
- finally()
- Promise Chaining

## Day 7 ✅

### DSA

- Binary Search
- LeetCode 704 - Binary Search

### JavaScript

- Hoisting
- Temporal Dead Zone (TDZ)
- Function Declaration
- Function Expression

# Day 8

## DSA

- ✅ 35. Search Insert Position
- Pattern: Binary Search

## JavaScript

- ✅ Execution Context
- ✅ Call Stack
- ✅ Event Loop
- ✅ Web APIs
- ✅ Callback Queue
- ✅ Microtask Queue
- ✅ Macrotask Queue

## Learning

- Binary Search returns `left` when the target is not found.
- Event Loop executes all Microtasks before Macrotasks.
- Execution Context has Creation and Execution phases.

# Day 9

## DSA

✅ Pattern: Stack

Problem Solved

- 20. Valid Parentheses

Learnings

- Recognized Stack pattern immediately.
- Used expected closing brackets instead of opening brackets.
- Completed optimal solution in O(n).

---

## JavaScript

Completed

- this
- call()
- apply()
- bind()

Interview Score

DSA: 10/10

JavaScript: 9.3/10

Overall

Pattern recognition speed continues to improve.

# Day 10

## DSA

Pattern

- Stack

Problem

- 155. Min Stack

Highlights

- Initially considered tracking the minimum using a single variable.
- Identified why that approach fails after pop operations.
- Implemented the optimal two-stack solution.

---

## JavaScript

Completed

- Prototype
- Prototype Chain
- Object.create()
- prototype vs **proto**
- new keyword
- Constructor Function vs Class

Interview Scores

DSA: 9.9 / 10

JavaScript: 8.8 / 10



# Day 11

## DSA

### Problem

232. Implement Queue using Stacks

### Pattern

Queue + Two Stacks

### Key Learning

Initially questioned whether moving all elements from `stack2` to `stack1` would make the solution O(n).

Learned the difference between:

- Worst-case complexity of one operation
- Amortized complexity across many operations

Final understanding:

> Each element is transferred at most once, therefore `pop()` and `peek()` are O(1) amortized.

---

## JavaScript

### Topics

- Closures
- Lexical Environment
- First-Class Functions
- Higher-Order Functions
- `var` vs `let`
- Closure + Event Loop

### Output Question

```js
for (var i = 0; i < 3; i++) {
    setTimeout(() => {
        console.log(i);
    }, 0);
}
```

Output:

```text
3
3
3
```

Reason:

All callbacks close over the same `var` binding.

With `let`:

```text
0
1
2
```

because each iteration has a separate binding.

---

## Interview Mistakes

- Initially described `var` as global instead of function-scoped.
- Initially defined higher-order functions only as functions that return functions.
- Needed clarification on why transferring stack elements still gives O(1) amortized complexity.

---

# Day 12

## DSA

### Fundamentals

- A linked-list node stores a value and a `next` reference.
- Arrays support direct indexed access; linked lists require traversal, so access by position is O(n).
- Insertion or deletion is O(1) only when the needed node/reference is already available; finding it can still take O(n).
- Deleting the tail of a singly linked list is O(n) when its previous node must be found.

### Problem

- 206. Reverse Linked List
- Pattern: Linked List / Pointer Reversal

### Learning Progression

- First created new `ListNode` nodes, producing a correct reversed list with O(n) extra space.
- Then used object spread, but each spread still created a new object and therefore still used O(n) extra space.
- Finally reused the existing nodes: save `head.next`, reverse the current link, and advance both pointers.
- Final complexity: O(n) time and O(1) extra space.

## JavaScript

No JavaScript topic was completed for Day 12.

---

# Day 13

## DSA

### Problem

- 141. Linked List Cycle
- Pattern: Linked List + Hashing

### Learning Progression

- Initially described using a `Map` to store each node and its position.
- Correctly recognized that revisiting a node means the list contains a cycle.
- Simplified the implementation to a `Set` because the stored position was unnecessary.
- Completed the O(n)-time, O(n)-extra-space solution using node references.
- The O(1)-extra-space optimization remains pending.

## JavaScript

### Topic

- Debounce

### Key Learning

- Preserved the timer identifier with a closure.
- Cancelled the previous timer before scheduling a new call.
- Forwarded arguments with rest parameters.
- Preserved `this` using an arrow timer callback and `func.apply(this, args)`.

---

# Day 14

## DSA

### Problem

- 21. Merge Two Sorted Lists
- Pattern: Linked List / Pointer Merge

### Learning Progression

- Correctly compared the current nodes and tracked the merged head and tail.
- Initially copied selected nodes with object spread.
- Renamed the pointers more clearly, but recognized that renaming did not remove the node copies.
- Final solution connected the existing nodes directly.
- Completed the merge in O(n + m) time and O(1) extra space.

## JavaScript

### Topic

- Leading-edge throttle

### Key Learning

- Stored a waiting flag in a closure.
- Executed the first call immediately.
- Ignored calls received during the delay.
- Preserved arguments and `this` with `func.apply(this, args)`.
- The implementation intentionally does not perform a trailing call.
- A precise throttle-versus-debounce explanation remains to revise.

---

# Day 15

## DSA

### Problem

- 19. Remove Nth Node From End of List
- Pattern: Linked List / Fast and Slow Pointers

### Learning Progression

- First calculated the length and removed the target in a second traversal.
- Recognized that this was O(L) time and O(1) space but did not satisfy the one-pass follow-up.
- Learned to maintain an `n + 1` gap between fast and slow pointers.
- Used a dummy node to handle removing the head uniformly.
- Completed the one-pass O(L)-time, O(1)-space solution.

## JavaScript

### Topic

- Custom `Promise.all`

### Learning Progression

- Initially used an async `map`, which returned an array of Promises rather than one Promise.
- Learned to normalize inputs with `Promise.resolve`.
- Preserved input order by storing results at their original indexes.
- Used a completion counter and handled empty input.
- Implemented fail-fast rejection and understood that remaining operations are not cancelled.
- Compared `Promise.all` with `Promise.allSettled`; a custom `allSettled` implementation was not completed.

---

# Day 16

## DSA

### Problem

- 143. Reorder List
- Pattern: Linked List / Split, Reverse, and Merge

### Learning Progression

- First considered reversing the whole list and interleaving it with the original order.
- Recognized that reversing the entire list loses access to the original forward order.
- Switched to counting and splitting the list, then realized the second half must be reversed to obtain nodes from the end efficiently.
- Counted the nodes, split after `Math.ceil(count / 2)`, reversed the second half in place, and merged the two halves alternately.
- Completed the odd- and even-length cases in O(n) time and O(1) extra space.

## JavaScript

### Topic

- Custom EventEmitter

### Learning Progression

- Started with separate Maps for regular and once-only listeners.
- Corrected `Map.has()` versus `Map.get()`, array `push()` usage, targeted listener removal, and mixed regular/once emission.
- Removed once-only listeners before invoking them and emitted from a snapshot to handle reentrancy and mutation safely.
- Discovered that two Maps lose the registration order between `on()` and `once()` calls.
- Redesigned storage as one ordered array of `{ listener, once }` entries per event.
- Used the chosen duplicate-listener contract: `off()` removes the latest matching registration.
- Completed the implementation; repeated once-listener removal is a possible O(k²) optimization follow-up, not a correctness issue.

---

# Day 17

## DSA

### Problem

- 138. Copy List with Random Pointer
- Pattern: Linked List / Node Mapping and Interleaving

### Learning Progression

- First considered shallow and deep copying with object spread, then learned that `{ ...node }` creates only a new outer node while `next` and `random` still reference original nodes.
- Proposed the correct two-pass `Map` relationship: original node → copied node.
- In the first Map attempt, created a separate shallow-copied head and accidentally modified original nodes while wiring the second pass.
- Corrected the baseline by creating every copied node only through the Map, then translating each original `next` and `random` reference through that Map.
- Completed the Map solution in O(n) time and O(n) extra space.
- Optimized by interleaving copies with originals, assigning `copy.random = original.random.next`, and separating both lists while restoring the original.
- Replaced an initial flag-based random traversal with direct reference mapping; retained a valid dummy-tail separation before reaching the final O(1)-extra-space solution.

## JavaScript

### Topic

- Promise Concurrency Limiter / `promisePool(tasks, limit)`

### Learning Progression

- Started with a queue, running-task count, result index, outer Promise, and scheduler.
- Corrected an off-by-one concurrency condition, captured each task's index before async work, and preserved input order in a plain results array.
- Changed failure behavior from all-settled-style results to fail-fast rejection and stopped scheduling queued tasks after the first failure.
- Used `Promise.resolve().then(() => task())` so synchronous task throws become rejections.
- Moved completion checks to cleanup: decrement the running count, then resolve only when the queue is empty and no task remains active; otherwise restart the scheduler.
- Handled empty input with `resolve([])` and completed the required implementation.
- A non-positive-limit guard and avoiding `queue.shift()` overhead remain optional interview follow-ups.
