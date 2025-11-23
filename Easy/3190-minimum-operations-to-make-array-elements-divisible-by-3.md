# 🟢 LeetCode 3190: Minimum Operations to Make Array Elements Divisible by 3

## 🔗 Problem Link
https://leetcode.com/problems/minimum-operations-to-make-array-elements-divisible-by-3/

------------------------------------------------------------------------

## 🧠 Problem Summary

You are given an array `nums`.  
In one operation, you can **increase or decrease any element by 1**.

Your goal is to make **every element divisible by 3** using the **minimum number of operations**.

Each element:
- If already divisible by 3 → needs 0 operations  
- If remainder is 1 → needs 1 operation (either +1 or -1)  
- If remainder is 2 → needs 1 operation (either +1 or -1)

So you just count how many numbers are **not divisible by 3**.

------------------------------------------------------------------------

## 💭 My Thought Process

At first, I wondered if some numbers require more than 1 operation or we need to adjust sequences.  
But after checking examples, the pattern became obvious:

Every number is at most **1 step** away from the nearest multiple of 3.

So instead of simulating adjustments, just count how many elements have a remainder of 1 or 2.

That's it.  
No greediness, no DP, no complex logic.

------------------------------------------------------------------------

## ❌ Mistakes I Made

- Initially overthought the problem as if adjustments may chain together  
- Forgot that every number is max 1 step from the nearest multiple of 3  

------------------------------------------------------------------------

## ✔️ Final Approach

For each number:
- If `num % 3 == 0`, ignore  
- Otherwise, add 1 to the operation count  

Return the count.

Clean. Fast. Straightforward.

------------------------------------------------------------------------

## 🧾 Code (Python)

```python
class Solution:
    def minimumOperations(self, nums: List[int]) -> int:
        count = 0
        for i in nums:
            if i % 3 != 0:
                count += 1
        return count
```
------------------------------------------------------------------------

## ⏱️ Complexity

-   **Time:** O(n) — just scanning the list once
-   **Space:** O(1) — constant extra memory

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- use Python list comprehensions for shorter code

- Try solving in one line

- Compare with the math trick of counting remainders directly

