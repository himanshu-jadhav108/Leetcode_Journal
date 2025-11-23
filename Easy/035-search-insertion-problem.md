# 🟢 LeetCode 35: Search Insert Position

## 🔗 Problem Link  
https://leetcode.com/problems/search-insert-position/

---

## 🧠 Problem Summary

You’re given a sorted array and a target value.  
Your task is to return the index where the target exists, or the index where it should be inserted to maintain sorted order.  
Basically: binary search with an insertion fallback.

---

## 💭 My Thought Process

- First idea: loop through everything — pointless because the array is already sorted.
- Realized binary search is the correct tool for this.
- The key insight: when the loop ends, the `left` pointer automatically points to the correct insert position.

---

## ❌ Mistakes I Made

- Messed up the mid calculation once by forgetting parentheses.
- Used `right` as the fallback return instead of `left` (wrong logic).

---

## ✔️ Final Approach

Use binary search to narrow down the position.  
If the target is found, return its index.  
If not, `left` becomes the correct insert position because it represents the first index greater than the target.

---

## 🧾 Code (Python)

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1

        while left <= right:
            mid = (left + right) // 2

            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                left = mid + 1
            else:
                right = mid - 1
            
        return left
```
------------------------------------------------------------------------

## ⏱️ Complexity

-   **Time:** O(log n)
-   **Space:** o(1)

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Using bisect_left to simplify the logic.
- Implementing a recursive binary search version.
