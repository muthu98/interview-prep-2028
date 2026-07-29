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