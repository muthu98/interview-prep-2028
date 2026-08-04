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