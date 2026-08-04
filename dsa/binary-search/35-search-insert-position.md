# 35. Search Insert Position

## Pattern

Binary Search

## Difficulty

Easy

---

## Problem

Given a sorted array of distinct integers and a target value, return the index if the target exists.

If not found, return the index where it should be inserted to maintain sorted order.

---

## Recognition

- Sorted array
- Search target
- Need O(log n)
- Return insertion index

---

## Algorithm

1. Initialize `left = 0` and `right = nums.length - 1`.
2. While `left <= right`
   - Calculate `mid`
   - If target equals `nums[mid]`, return `mid`
   - If target is greater, move `left`
   - Otherwise move `right`
3. Return `left`

---

## Code

```js
var searchInsert = function(nums, target) {

    let left = 0;
    let right = nums.length - 1;

    while (left <= right) {

        const mid = Math.floor((left + right) / 2);

        if (nums[mid] === target) {
            return mid;
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    return left;
};
```

---

## Complexity

Time: **O(log n)**

Space: **O(1)**

---

## Interview Notes

- Binary Search always compares with `nums[mid]`.
- No need for `left == right` special handling.
- If target is not found, `left` is the insertion position.