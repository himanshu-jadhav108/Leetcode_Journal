# 🟢 LeetCode 1: Two Sum

## 🔗 Problem Link

https://leetcode.com/problems/two-sum/

------------------------------------------------------------------------

## 🧠 Problem Summary

Given an array of integers and a target value, we need to return the **indices of two numbers** such that they add up to the target.  
We cannot use the same element twice, and there is exactly one valid solution.


------------------------------------------------------------------------

## 💭 My Thought Process

At first, the brute-force approach came to mind (two loops), but that is slow and unnecessary.  
Then I realized the key idea: for every number, we only need to check if its **complement**  
(`target - number`) has already been seen.

A hashmap lets us check that in O(1).  
Once I saw this pattern, the solution clicked immediately.


------------------------------------------------------------------------

## ❌ Mistakes I Made

- Thinking too much about edge cases instead of focusing on the core pattern  
- Initially storing indices before checking the complement (wrong order)


------------------------------------------------------------------------

## ✔️ Final Approach

Iterate through the list once.  
Keep a dictionary that maps each number to its index.  
For every number `n`, check if `target - n` exists in the dictionary:  
- If yes → return the pair of indices  
- If no → store `n` in the dictionary and continue  

This gives a clean O(n) solution.

------------------------------------------------------------------------

## 🧾 Code (Python)

``` python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        idx = {}

        for i, n in enumerate(nums):
            if target - n in idx:
                return [i, idx[target - n]]
            idx[n] = i 
```

------------------------------------------------------------------------

## ⏱️ Complexity

-   **Time:** O(n) — we scan the list once
-   **Space:** O(n) — dictionary for storing visited numbers

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Solve it in C++ or Java to build multi-language fluency
- Try solving without extra space (two-pointer on sorted array, but that ruins original indices)

