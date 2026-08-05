# 155. Min Stack

**Difficulty:** Medium

**Pattern:** Stack

**LeetCode:** https://leetcode.com/problems/min-stack/

---

# Problem

Design a stack that supports:

- push(val)
- pop()
- top()
- getMin()

All operations must run in **O(1)** time.

---

# Pattern Recognition

### Recognition Clues

- Maintain stack operations
- Retrieve minimum element instantly
- O(1) retrieval
- Additional state required

Pattern:

**Stack**

---

# Initial Thought Process

Initially, I planned to store all values in a single stack and compute the minimum whenever `getMin()` was called.

Problem:

- `getMin()` becomes **O(n)** because it requires scanning the stack.

---

# Optimized Idea

Maintain two stacks:

- `stack`
- `minStack`

`minStack` stores the minimum value seen so far.

Whenever a new value is smaller than or equal to the current minimum, push it into `minStack`.

Whenever popping, if the popped value equals the current minimum, remove it from `minStack` as well.

---

# Algorithm

1. Push value into `stack`.
2. If `minStack` is empty or value <= current minimum, push into `minStack`.
3. During pop:
   - Remove from `stack`.
   - If popped value equals top of `minStack`, pop `minStack`.
4. `top()` returns last element of `stack`.
5. `getMin()` returns last element of `minStack`.

---

# JavaScript

```javascript
var MinStack = function () {
    this.stack = [];
    this.minStack = [];
};

MinStack.prototype.push = function (val) {
    this.stack.push(val);

    if (
        this.minStack.length === 0 ||
        val <= this.minStack[this.minStack.length - 1]
    ) {
        this.minStack.push(val);
    }
};

MinStack.prototype.pop = function () {
    const value = this.stack.pop();

    if (value === this.minStack[this.minStack.length - 1]) {
        this.minStack.pop();
    }
};

MinStack.prototype.top = function () {
    return this.stack[this.stack.length - 1];
};

MinStack.prototype.getMin = function () {
    return this.minStack[this.minStack.length - 1];
};
```

---

# Complexity

| Operation | Time |
|-----------|------|
| push | O(1) |
| pop | O(1) |
| top | O(1) |
| getMin | O(1) |

Space: **O(n)**

---

# Interview Notes

- A single stack is insufficient for O(1) minimum retrieval.
- Use a second stack to track minimum values.
- Use `<=` instead of `<` to correctly handle duplicate minimum values.

---

# Common Mistakes

❌ Using `Math.min(...stack)`

Time Complexity becomes O(n).

❌ Using `<` instead of `<=`

Fails for duplicate minimum values.