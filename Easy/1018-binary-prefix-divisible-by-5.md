# 🟢 LeetCode 1018: Binary Prefix Divisible By 5

## 🔗 Problem Link

https://leetcode.com/problems/binary-prefix-divisible-by-5

------------------------------------------------------------------------

## 🧠 Problem Summary

- I was given a binary array **nums** (each element is either `0` or `1`).
- For each prefix of the array , I had to determine whether the binary number represented by that prefix is divisible by 5 

- Example:
  - Input: nums = [1,0,1,0]
  - Prefixes:
    - 1 → decimal 1 → not divisible
    - 10 → decimal 2 → not divisible
    - 101 → decimal 5 → divisible
    - 1010 → decimal 10 → divisible
  - Output: [False, False, True, True]




------------------------------------------------------------------------

## 💭 My Thought Process

- At first , I thought I need to convert each prefix into its decimal form, which would be inefficient for large inputs.
- I realized then that I don't need the full number - just the remender % 5 I required

------------------------------------------------------------------------

## ❌ Mistakes I Made

- Tried to build the entire integer for each prefix → caused overflow and inefficiency.
- Forgot to use modulo at each step → numbers grew unnecessarily large.


------------------------------------------------------------------------

## ✔️ Final Approach

1. Keep a running remainder `(cur)` modulo 5
2. For each `bit` in `nums:`
    - Update `cur = ( cur * 2 + bit ) % 5`
    - Append `True` if ` cur == 0 ` else `False`
3. Return the result List.
   
This way, we never deal with huge numbers — only remainders between 0 and 4.

------------------------------------------------------------------------

## 🧾 Code (Python)

``` python

from typing import List

class Solution:
    def prefixesDivBy5(self, nums: List[int]) -> List[bool]:
        res = []
        cur = 0
        for bit in nums:
            cur = (cur * 2 + bit) % 5
            res.append(cur == 0)
        return res
        
```

------------------------------------------------------------------------

## ⏱️ Complexity

-   **Time:** o(n) (One pass through the array.)
-   **Space:** O(n) (result list of booleans.)


------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Solve it in C++ or Java to build multi-language fluency
- Write a reusable helper function for “prefix divisibility by k” problems.

