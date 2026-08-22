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
