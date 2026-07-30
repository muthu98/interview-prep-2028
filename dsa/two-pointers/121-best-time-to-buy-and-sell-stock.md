# 121. Best Time to Buy and Sell Stock

## Difficulty
Easy

## Pattern
Two Pointers

---

## Problem

Given an array `prices`, where `prices[i]` is the stock price on the `i`th day, return the maximum profit you can achieve by buying once and selling once.

---

## Thought Process

```text
left  -> Buying Day
right -> Selling Day

Traverse using right pointer.

If current price is smaller than buying price,
move left = right.

Otherwise,
calculate current profit.

Update maximum profit.

Return maximum profit.
```

---

## Algorithm

1. Initialize `left = 0` and `profit = 0`.
2. Traverse using `right` from index `1`.
3. If `prices[right] < prices[left]`
   - Update `left = right`.
4. Else
   - Calculate profit.
   - Update maximum profit.
5. Return profit.

---

## My Solution

```javascript
var maxProfit = function(prices) {
    let profit = 0;

    for (let left = 0, right = 1; right < prices.length; right++) {
        profit = Math.max(profit, prices[right] - prices[left]);

        if (prices[left] > prices[right]) {
            left = right;
        }
    }

    return profit;
};
```

---

## Time Complexity

```
O(n)
```

---

## Space Complexity

```
O(1)
```

---

## Learning

- Two Pointers
- Track Minimum Value
- Greedy Thinking
- Maximum Profit Calculation

---

## Mistakes

- Initially thought `left++`.
- Learned that `left` should always point to the minimum price seen so far.