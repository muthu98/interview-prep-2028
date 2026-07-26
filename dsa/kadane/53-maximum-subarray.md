# 53. Maximum Subarray

## Difficulty

Medium

## Pattern

Kadane's Algorithm (Dynamic Programming)

## Problem

Given an integer array, find the contiguous subarray with the largest sum and return its sum.

## My Algorithm

1. Traverse the array once.
2. Maintain a running sum (`currentSum`).
3. At each element, decide whether to:

   * Continue the current subarray.
   * Start a new subarray from the current element.
4. Update `maxSum` whenever a better sum is found.
5. Return `maxSum`.

## My Solution

```javascript
var maxSubArray = function(nums) {
    let currentSum = 0, maxSum = -Infinity;

    for (let i = 0; i < nums.length; i++) {
        if (nums[i] > currentSum + nums[i]) {
            currentSum = 0;
            // tempStart=i
        }

        currentSum += nums[i];

        if (maxSum < currentSum) {
            maxSum = currentSum;
        }
    }

    return maxSum;
};
```

## Time Complexity

O(n)

## Space Complexity

O(1)

## Interview Follow-up

How would you return the start and end indices of the maximum subarray?

### Idea

Maintain:

* `tempStart`
* `startIndex`
* `endIndex`

When starting a new subarray:

* Update `tempStart`.

When `currentSum` becomes the new `maxSum`:

* `startIndex = tempStart`
* `endIndex = current index`

## What I Learned

* Kadane's Algorithm is based on making a local decision at each index.
* At every element, choose whether to continue the current subarray or start a new one.
* Solving the basic version first makes interview follow-up questions easier.
