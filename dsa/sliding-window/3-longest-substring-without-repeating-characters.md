# 3. Longest Substring Without Repeating Characters

- **LeetCode:** 3
- **Difficulty:** Medium
- **Pattern:** Sliding Window
- **Importance:** ⭐⭐⭐⭐⭐

---

# Problem

Given a string `s`, find the length of the longest substring without repeating characters.

### Example

```text
Input: "abcabcbb"
Output: 3

Explanation:
The answer is "abc".
```

---

# My Thought Process

1. Traverse the string using `right`.
2. Use `left` to maintain the current window.
3. Compare the current character with previous characters inside the window.
4. If a duplicate is found:
   - Move `left`.
   - Update the current window length.
5. Track the maximum length.

---

# My Solution (First Attempt)

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
    let stringCount = 0;
    let stringMax = 0;

    for (let right = 0, left = 0; right < s.length; right++) {

        let temp = left;

        while (temp < right) {

            if (s[temp] == s[right]) {
                stringCount = right - temp - 1;
                left = temp + 1;
            }

            temp++;
        }

        stringCount++;
        stringMax = Math.max(stringCount, stringMax);
    }

    return stringMax;
};
```

---

# Complexity (My Solution)

Time Complexity

```text
O(n²)
```

Space Complexity

```text
O(1)
```

### Why?

For every character, I scan the current window again to find duplicates.

---

# Optimized Solution

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
    const window = new Set();

    let left = 0;
    let maxLength = 0;

    for (let right = 0; right < s.length; right++) {

        while (window.has(s[right])) {
            window.delete(s[left]);
            left++;
        }

        window.add(s[right]);

        maxLength = Math.max(maxLength, right - left + 1);
    }

    return maxLength;
};
```

---

# Complexity (Optimized)

Time Complexity

```text
O(n)
```

Space Complexity

```text
O(min(n, characterSet))
```

---

# Key Learning

### ❌ My Initial Mistake

I knew I should use a `Set` for detecting duplicates but wasn't sure how to remove duplicates efficiently.

So I scanned the window every time using another loop.

---

### ✅ Correct Sliding Window Approach

The `Set` is **only used to detect duplicates**.

The `left` pointer is responsible for **shrinking the window** until the duplicate is removed.

```javascript
while (window.has(s[right])) {
    window.delete(s[left]);
    left++;
}
```

---

# Sliding Window Template

```javascript
let left = 0;
const window = new Set();

for (let right = 0; right < arr.length; right++) {

    while (window.has(arr[right])) {
        window.delete(arr[left]);
        left++;
    }

    window.add(arr[right]);

    // Update answer
}
```

---

# Pattern Recognition

Use Sliding Window when the question mentions:

- Longest substring
- Smallest substring
- Consecutive elements
- At most K
- At least K
- Without repeating characters

---

# Interview Tips

### Set vs Map

Use **Set** when you need:

- Check existence
- Detect duplicates
- Ensure uniqueness

Use **Map** when you need:

- Frequency count
- Last seen index
- Extra information

---

# Common Mistakes

- Restarting the window instead of shrinking it.
- Scanning the entire window repeatedly.
- Using `if` instead of `while` when removing duplicates.
- Forgetting to update the maximum length after expanding the window.

---

# Revision Notes

✅ Sliding Window maintains a **valid window**.

✅ `right` expands the window.

✅ `left` shrinks the window.

✅ `Set` detects duplicates.

✅ Both pointers only move forward.

Therefore:

```text
Time Complexity = O(n)
```