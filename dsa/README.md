# 🧠 DSA Pattern Roadmap

> This repository is organized by **patterns**, not by LeetCode problem numbers.
>
> 🎯 **Goal**
>
> Learn:
>
> - How to recognize a pattern
> - When to apply it
> - Explain the solution clearly in interviews
> - Write optimized code with confidence

---

# 📊 Current Progress

## Overall Statistics

- ✅ Patterns Completed: **9 / 21**
- ✅ Problems Solved: **16**
- 📅 Current Day: **Day 16**

---

| Pattern               | Importance | Status | Problems |
| --------------------- | :--------: | :----: | :-------: |
| Arrays                | ⭐⭐⭐⭐⭐ | ⬜ | 0 |
| Hashing               | ⭐⭐⭐⭐⭐ | ✅ | 1 |
| Two Pointers          | ⭐⭐⭐⭐⭐ | ✅ | 1 |
| Sliding Window        | ⭐⭐⭐⭐⭐ | ✅ | 2 |
| Prefix Sum / Suffix   | ⭐⭐⭐⭐☆ | ✅ | 1 |
| Binary Search         | ⭐⭐⭐⭐⭐ | ✅ | 2 |
| Intervals             | ⭐⭐⭐⭐☆ | ⬜ | 0 |
| Stack                 | ⭐⭐⭐⭐⭐ | ✅ | 2 |
| Queue                 | ⭐⭐⭐☆☆ | ✅ | 1 |
| Linked List            | ⭐⭐⭐⭐☆ | ✅ | 5 |
| Trees                  | ⭐⭐⭐⭐⭐ | ⬜ | 0 |
| Heap / Priority Queue | ⭐⭐⭐⭐☆ | ⬜ | 0 |
| Graphs                | ⭐⭐⭐⭐⭐ | ⬜ | 0 |
| Union Find             | ⭐⭐⭐☆☆ | ⬜ | 0 |
| Backtracking           | ⭐⭐⭐⭐☆ | ⬜ | 0 |
| Dynamic Programming    | ⭐⭐⭐⭐⭐ | ⬜ | 0 |
| Greedy                 | ⭐⭐⭐⭐☆ | ⬜ | 0 |
| Trie                   | ⭐⭐⭐☆☆ | ⬜ | 0 |
| Bit Manipulation       | ⭐⭐⭐⭐☆ | ⬜ | 0 |
| Math                   | ⭐⭐⭐☆☆ | ⬜ | 0 |
| Kadane's Algorithm     | ⭐⭐⭐⭐⭐ | ✅ | 1 |

---

# 📌 Pattern Recognition Cheat Sheet

| If the problem mentions... | Think About |
| -------------------------- | ------------------- |
| Duplicate, Frequency | Hashing |
| Pair, Sorted Array | Two Pointers |
| Longest / Smallest Window | Sliding Window |
| Prefix / Suffix | Prefix Sum |
| Sorted Array | Binary Search |
| Merge Intervals | Intervals |
| Parentheses | Stack |
| FIFO, BFS, Scheduling | Queue |
| Reverse Linked List | Linked List |
| Cycle or repeated node reference | Linked List |
| Merge sorted linked lists | Linked List |
| Nth node from the end | Linked List / Two Pointers |
| Reorder a linked list from both ends | Linked List / Reverse and Merge |
| Tree Traversal | Trees |
| Top K | Heap |
| Shortest Path | Graphs |
| Connected Components | Union Find |
| All Possibilities | Backtracking |
| Optimize Repeated Work | Dynamic Programming |
| Best Local Choice | Greedy |
| Prefix Search | Trie |
| XOR | Bit Manipulation |
| Prime / GCD | Math |

---

# 1. Arrays

### Description

Basic array traversal and manipulation.

### Recognition Clues

- Traverse elements
- Rotate array
- Matrix traversal
- In-place modification

### Common Topics

- Traversal
- Rotation
- Matrix
- Simulation
- Prefix Sum

### Complexity

Time: **O(n)**

Space: **O(1)**

### Companies

Amazon, Google, Microsoft, Walmart

### Problems

- [ ]

---

# 2. Hashing

### Description

Use HashMap / HashSet for constant-time lookup.

### Recognition Clues

- Duplicate
- Frequency
- Lookup
- Pair Sum

### Complexity

Time: **O(n)**

Space: **O(n)**

### Problems

- [x] 217. Contains Duplicate

---

# 3. Two Pointers

### Description

Maintain two pointers moving together or toward each other.

### Recognition Clues

- Sorted array
- Pair Sum
- Remove duplicates
- Palindrome

### Complexity

Time: **O(n)**

Space: **O(1)**

### Problems

- [x] 121. Best Time to Buy and Sell Stock

---

# 4. Sliding Window

### Description

Maintain a moving window.

### Recognition Clues

- Longest substring
- Fixed window
- Consecutive elements

### Complexity

Time: **O(n)**

Space: **O(1)** / **O(n)**

### Problems

- [x] 3. Longest Substring Without Repeating Characters
- [x] 567. Permutation in String

---

# 5. Prefix Sum / Suffix

### Description

Reuse cumulative information.

### Recognition Clues

- Range Sum
- Product Except Self

### Complexity

Time: **O(n)**

Space: **O(n)**

### Problems

- [x] 238. Product of Array Except Self

---

# 6. Binary Search

### Description

Search in a sorted answer space.

### Recognition Clues

- Sorted array
- Search target
- O(log n)

### Complexity

Time: **O(log n)**

Space: **O(1)**

### Problems

- [x] 704. Binary Search
- [x] 35. Search Insert Position

---

# 7. Stack

### Description

Use the **Last-In-First-Out (LIFO)** principle to solve problems involving nested or ordered operations.

### Recognition Clues

- Matching parentheses
- Nested structures
- Undo operations
- Expression evaluation
- Next Greater Element

### Common Topics

- Parentheses validation
- Monotonic Stack
- Min Stack
- Expression Evaluation
- Decode String

### Complexity

Time: **O(n)**

Space: **O(n)**

### Problems

- [x] 20. Valid Parentheses
- [x] 155. Min Stack

---

# 8. Queue

### Description

Use the **First-In-First-Out (FIFO)** principle.

A queue can be implemented using two stacks by reversing the order of elements when required.

### Recognition Clues

- FIFO
- BFS
- Scheduling
- Processing in arrival order
- Stream processing

### Common Topics

- Queue implementation
- Queue using stacks
- Circular Queue
- BFS
- Deque

### Complexity

For a queue implemented using two stacks:

- `push()` → **O(1)**
- `pop()` → **O(1) amortized**
- `peek()` → **O(1) amortized**
- `empty()` → **O(1)**

### Key Insight

Use two stacks:

- `stack2` receives new elements.
- `stack1` provides elements for `pop()` and `peek()`.
- When `stack1` is empty, transfer all elements from `stack2` to `stack1`.

Although transferring elements can take **O(n)** for one operation, each element is transferred at most once.

Therefore, `pop()` and `peek()` are **O(1) amortized**.

### Problems

- [x] 232. Implement Queue using Stacks

---

# 9. Linked List

### Description

Store values in nodes connected by `next` references rather than contiguous indexes.

### Recognition Clues

- Reverse or reconnect nodes
- Traverse using `next`
- Insert or delete through references
- Slow and fast pointers

### Complexity

- Access by position: **O(n)**
- Insert/delete with the relevant node reference: **O(1)**
- Find a node or the tail without a stored reference: **O(n)**

### Problems

- [x] 206. Reverse Linked List
- [x] 141. Linked List Cycle
- [x] 21. Merge Two Sorted Lists
- [x] 19. Remove Nth Node From End of List
- [x] 143. Reorder List

---

# Remaining Patterns

- Intervals
- Trees
- Heap / Priority Queue
- Graphs
- Union Find
- Backtracking
- Dynamic Programming
- Greedy
- Trie
- Bit Manipulation
- Math

---

# 🎯 Interview Strategy

For every problem:

1. Understand the problem.
2. Identify the pattern.
3. Explain the approach in plain English.
4. Write the brute-force solution.
5. Optimize it.
6. Analyze Time & Space Complexity.
7. Consider follow-up questions.
8. Write revision notes.

---

# 📝 Problem Solving Template

Every problem in this repository follows:

- Pattern
- Recognition Clues
- Algorithm
- Dry Run
- Code
- Time Complexity
- Space Complexity
- Interview Notes
- Common Mistakes

---

# 🚀 Learning Roadmap

## Phase 1 — Foundation

- ⬜ Arrays
- ✅ Hashing
- ✅ Two Pointers
- ✅ Sliding Window
- ✅ Prefix Sum / Suffix
- ✅ Binary Search
- ✅ Stack
- ✅ Queue
- ✅ Linked List

---

## Phase 2 — Intermediate

- Linked List
- Trees
- Heap
- Intervals
- Greedy
- Kadane's Algorithm
- Bit Manipulation

---

## Phase 3 — Advanced

- Graphs
- Union Find
- Backtracking
- Dynamic Programming
- Trie
- Math

---

# 📚 Resources

- LeetCode
- NeetCode 150
- Blind 75
- Grind 75

---

⭐ The goal of this repository is not to memorize solutions, but to recognize patterns, explain approaches confidently, and become interview-ready.
