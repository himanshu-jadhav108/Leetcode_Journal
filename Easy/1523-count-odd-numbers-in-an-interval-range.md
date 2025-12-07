# 🟢 LeetCode 1523: Count Odd Numbers in an Interval Range


## 🔗 Problem Link

https://leetcode.com/problems/count-odd-numbers-in-an-interval-range/

------------------------------------------------------------------------

## 🧠 Problem Summary

Given two integers `low` and `high`, you must return how many odd numbers exist in the inclusive range [low,high].


------------------------------------------------------------------------

## 💭 My Thought Process

- First thought: loop from `low` to `high` and count odds — but that’s too slow for large ranges.
- Then realized: odd numbers follow a pattern — every second number is odd.
- The key insight:
  - Count how many odds exist from `0` to `high`.
  - Count how many odds exist from `0` to `low - 1`.
  - Subtract the two.


------------------------------------------------------------------------

## ❌ Mistakes I Made

- Tried brute force initially.
- Overcomplicated parity checks instead of using integer division.


------------------------------------------------------------------------

## ✔️ Final Approach

- Odd numbers appear at positions:
```1,3,5,7,...```

- So the count of odd numbers from 0 to x is:
``` x + 1 // 2 ```

- Thus, the number of odds in [low,high] is:
```(high + 1) / 2 - ( low ) / 2``` 

- This gives a constant-time solution.


------------------------------------------------------------------------

## 🧾 Code (Python)

``` python
class Solution:
    def countOdds(self, low: int, high: int) -> int:
        return ( high + 1 ) // 2 - ( low // 2 )
```

------------------------------------------------------------------------

## ⏱️ Complexity

-   **Time:** O(1) — pure math, no loops
-   **Space:** O(1)

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Solve it in C++ or Java to build multi-language fluency

