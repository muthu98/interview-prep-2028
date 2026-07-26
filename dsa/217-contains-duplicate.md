## Pattern
Hash Set / Hash Map

## Difficulty
Easy

## My Solution
- Used Object as frequency map
var containsDuplicate = function(nums) {
    let feq={}

    for(let val of nums){
        feq[val]=feq[val]+1 || 1
        if(feq[val]>1)return true
    }
    
    return false
};


## Optimal Solution
- Set
var containsDuplicate = function(nums) {
 const seen = new Set();

    for (const num of nums) {
        if (seen.has(num)) return true;
        seen.add(num);
    }

    return false;
};

## Time Complexity
O(n)

## Space Complexity
O(n)

## Mistakes
None

## What I Learned
- Object and Set both work.
- Set is cleaner for duplicate checking.