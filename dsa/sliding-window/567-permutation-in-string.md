# 567. Permutation in String

## Difficulty
Medium

## Pattern
Sliding Window (Fixed Size)

---

## Problem

Given two strings `s1` and `s2`, return `true` if `s2` contains a permutation of `s1`.

---

## Thought Process

1. Create a frequency map of `s1`.
2. Maintain a fixed-size sliding window of length `s1.length`.
3. Update the window frequency as the window slides.
4. Compare the window frequency with `s1` frequency.
5. Return `true` if they match.

---

## My Initial Approach

- Used a frequency map.
- Compared frequencies for every valid window.

---

## Optimized Solution

- Maintain the sliding window.
- Update only the entering and leaving characters.
- Can further optimize using a `matches` counter or a 26-element frequency array.

---

## Time Complexity

O(n × k)

where

- n = length of s2
- k = distinct characters in s1

---

## Space Complexity

O(k)

---

## Learning

- Fixed Sliding Window
- Frequency Map
- Window Maintenance
- Difference between Window Length and Map Size

---

## Mistakes

- Used `Map.size` instead of window length.
- Initially tried to reset the window.
- Confused unique character count with total window size.

---

## Final Code

```javascript
const isEqual=(map1, map2)=> {
    for (const [key, value] of map1) {
        if (map2.get(key) !== value) {
            return false;
        }
    }
    return true;
}
var checkInclusion = function(s1, s2) {
    const s1Feq = new Map(), windowFeq= new Map();

    for(let value of s1){
        s1Feq.set(value,s1Feq.get(value)+1 ||1)
    }

    for(let left=0,right=0;right<s2.length ; right++){
         windowFeq.set(s2[right],windowFeq.get(s2[right])+1 ||1)
         if(right-left+1>s1.length){
           windowFeq.set(s2[left],windowFeq.get(s2[left])-1)
           if(windowFeq.get(s2[left])===0){
            windowFeq.delete(s2[left])
           }
            left++
         }
         if(right-left+1==s1.length && isEqual(s1Feq,windowFeq)){
            return true
         }

    }
    
    return false
};
```