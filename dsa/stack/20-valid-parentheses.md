# 20. Valid Parentheses

**Difficulty:** Easy

**Pattern:** Stack

**LeetCode:** https://leetcode.com/problems/valid-parentheses/

---

# Problem

Given a string `s` containing only:

`()`, `{}`, `[]`

Determine if the string is valid.

A string is valid if:

- Every opening bracket has a matching closing bracket.
- Brackets are closed in the correct order.

---

# Recognition

- Matching symbols
- Nested structures
- Need to validate order
- Last opened should close first

➡️ Pattern: **Stack**

---

# Initial Thought Process

- Use an array as a stack.
- Traverse each character.
- Push the expected closing bracket whenever an opening bracket is found.
- On encountering a closing bracket, compare it with the top of the stack.
- If they don't match, return `false`.
- Finally, ensure the stack is empty.

---

# Algorithm

1. Create an empty stack.
2. Store opening → closing bracket mapping.
3. Iterate through the string.
4. Push expected closing brackets.
5. Compare closing brackets with stack top.
6. Return false if mismatch.
7. Return `stack.length === 0`.

---

# JavaScript

```javascript
var isValid = function(s) {
    let stack = [];
    const matches = {
        "{": "}",
        "[": "]",
        "(": ")"
    };

    for (const value of s) {
        if (matches[value]) {
            stack.push(matches[value]);
        } else if (value !== stack.pop()) {
            return false;
        }
    }

    return stack.length === 0;
};
```

---

# Complexity

Time: **O(n)**

Space: **O(n)**

---

# Interview Notes

- Recognize Stack immediately for matching symbols.
- Pushing expected closing brackets simplifies comparison.
- Always verify the stack is empty after traversal.

---

# Similar Problems

- 155. Min Stack
- 232. Implement Queue using Stacks
- 394. Decode String
- 71. Simplify Path