# 704. Binary Search

## Difficulty

Easy

## Pattern

Binary Search

---

## Problem

Given a sorted array of integers `nums` and an integer `target`, return the index of `target` if it exists, otherwise return `-1`.

---

## My Thought Process

```text
left = 0
right = nums.length - 1

While left <= right

Find middle index

If target > nums[mid]
    move left = mid + 1

Else if target < nums[mid]
    move right = mid - 1

Else
    return mid

Return -1
```

---

## My Solution

```javascript
var search = function(nums, target) {

    let left = 0,
        right = nums.length - 1,
        mid;

    while (left <= right) {
        mid = Math.floor((left + right) / 2);

        if (nums[mid] > target) {
            right = mid - 1;
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else {
            return mid;
        }
    }

    return -1;
};
```

---

## Time Complexity

```
O(log n)
```

---

## Space Complexity

```
O(1)
```

---

## Learning

- Binary Search works only on sorted data.
- Eliminate half of the search space every iteration.
- Use `left <= right`.
- Update pointers using `mid + 1` and `mid - 1`.

---

## Mistakes

- Initially used `left < right`.
- Initially updated pointers to `mid` instead of `mid ± 1`.