# 238. Product of Array Except Self

## Pattern
Prefix Product + Suffix Product

## Difficulty
Medium

## My Approach
- Created a suffix (right product) array.
- Traversed from left while maintaining a running prefix product.
- Multiplied prefix × suffix.
- Reused the input array for the output.

/**
 * @param {number[]} nums
 * @return {number[]}
 */
var productExceptSelf = function(nums) {
    let rightProduct=[...nums],product=1;
    for (let initial=nums.length-1;initial>=0;initial--){
        let temp=rightProduct[initial];
        rightProduct[initial]=product;
        product*=temp;
    }
    product=1;

    for(let initial=0;initial<nums.length;initial++){
        let temp=nums[initial];
        nums[initial]=product*rightProduct[initial]
        product*=temp
    }

    return nums

};

## Time Complexity
O(n)

## Space Complexity
O(n)

## Interview Follow-up
Can this be optimized to O(1) extra space?

## What I Learned
- Prefix and suffix product is an important interview pattern.
- First solve the correct solution, then optimize.
- Division is avoided because of zero handling.