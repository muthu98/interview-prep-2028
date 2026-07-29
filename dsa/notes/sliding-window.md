---

# Fixed Sliding Window

Used when the window size is predetermined.

Example:

- LeetCode 567
- Find All Anagrams
- Maximum Average Subarray

## Algorithm

```text
Expand Right

↓

Window Size > k

↓

Remove Left

↓

Window Size == k

↓

Check Answer

↓

Continue
```

where

```
k = target window size
```

## Variable vs Fixed

| Variable Window | Fixed Window |
|-----------------|--------------|
| Window size changes | Window size stays constant |
| Longest Substring | Permutation in String |
| Minimum Window | Find All Anagrams |