# 💬 Interview Questions

## Sliding Window

- Why use while instead of if?
- Can this be solved using Map?
- Why is the complexity O(n)?
- Why doesn't the nested loop make it O(n²)?

---

## JavaScript

- Difference between var, let and const?
- What is the Temporal Dead Zone?
- Why does var print 3 3 3?
- Can a const object be modified?
- Difference between const and immutable?

# Sliding Window

## Q1

Why compare the frequency map for every window?

Answer:
Every window represents a different substring. Since one character enters and one leaves, the window contents change and must be validated.

---

## Q2

Can this be optimized?

Answer:
Yes.

Instead of comparing the whole frequency map every time, maintain a match counter or use a fixed-size frequency array.

---

## Q3

Difference between Variable and Fixed Sliding Window?

Variable:
Window size changes.

Fixed:
Window size remains constant.

## Two Pointers

### Q1

Why move `left = right` instead of `left++`?

Answer:

Because `left` represents the best buying day (minimum price). When a lower price is found, it becomes the new buying day.

---

### Q2

Difference between Sliding Window and Two Pointers?

Sliding Window maintains a contiguous window.

Two Pointers tracks two positions that move according to the problem.

## Binary Search

### Q1

Why do we use `left <= right`?

### Q2

Why do we use `mid + 1` and `mid - 1`?

### Q3

Why is Binary Search `O(log n)`?

---

## JavaScript

### Q1

What is Hoisting?

### Q2

Are `let` and `const` hoisted?

### Q3

What is the Temporal Dead Zone?

### Q4

Difference between Function Declaration and Function Expression?

### Q5

Why does `var` print `undefined`?


## Binary Search

- Why return `left` instead of `right`?
- Why compare with `nums[mid]`?
- Why use `left <= right`?

---

## JavaScript

- What is Execution Context?
- Explain Creation Phase.
- Explain Execution Phase.
- What is the Call Stack?
- What is the Event Loop?
- Difference between Microtask and Macrotask?
- Why does Promise execute before setTimeout()?
- Does setTimeout(fn, 0) execute immediately?