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