# 🟢 LeetCode 3381 : Maximum Subarray Sum With Length Divisible By K

## 🔗 Problem Link

https://leetcode.com/problems/maximum-subarray-sum-with-length-divisible-by-k/

------------------------------------------------------------------------

## 🧠 Problem Summary

Given an integer array `nums` and an integer `k`, find the maximum sum of any subarray whose length is divisible by `k`. Return the maximum sum (subarray must be contiguous). If all sums are negative, return the largest (least negative) sum.

------------------------------------------------------------------------

## 💭 My Thought Process

- Use prefix sums: prefix[p] = sum(nums[:p]) for p from 0..n.
- A subarray from l..r (inclusive) has sum = prefix[r+1] - prefix[l] and length = r-l+1. The length is divisible by `k` iff `(r+1) % k == l % k`.
- For each prefix index p (which corresponds to r+1), the best partner `l` must have the same `p % k`. So maintain the minimum prefix sum seen for each remainder class mod `k` and compute candidate sums as current_prefix - min_prefix[rem].
- Initialize `min_prefix[0] = 0` (empty prefix at index 0). Iterate once over the array updating prefix and min_prefix for prefix index `(i+1) % k`.

------------------------------------------------------------------------

## ❌ Mistakes I Made

- Using `i % k` (index of element) instead of `(i+1) % k` (prefix index) when mapping prefix sums to remainders.
- Initializing the wrong remainder in `min_prefix` (should set remainder 0 to 0, not `(k-1) % k`).
- Overlooking prefix-index vs element-index off-by-one differences when reasoning about lengths.

------------------------------------------------------------------------

## ✔️ Final Approach

- Compute a running prefix sum while tracking `min_prefix[rem]` = minimal prefix sum observed for prefix indices with remainder `rem` (mod `k`).
- At each step (prefix index `p = i+1`), compute `rem = p % k` and candidate max = `prefix_sum - min_prefix[rem]`.
- Update `min_prefix[rem]` with the current prefix sum for future candidates.
- This is a single pass O(n) algorithm using O(k) extra space.

------------------------------------------------------------------------

## 🧾 Code (Python)

```python

class Solution:
    def maxSubarraySum(self, nums: List[int], k: int) -> int:
        prefix_sum = 0
        max_sum = float('-inf')
        min_prefix = [float('inf')]*k
        min_prefix[(k - 1)% k] = 0

        for i, num in enumerate(nums):
            prefix_sum += num
            idx = i % k
            max_sum = max(max_sum, prefix_sum - min_prefix[idx])
            min_prefix[idx] = min(min_prefix[idx], prefix_sum)
            
        return max_sum
```

------------------------------------------------------------------------

## ⏱️ Complexity

- **Time:** O(n) — single pass over `nums`.
- **Space:** O(k) — store one minimum prefix per remainder class.

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Add explicit unit tests covering edge cases: small arrays, single element, k=1, negative-only arrays, and arrays with zeros.
- Implement the solution in C++/Java to compare performance and memory footprint.
- Consider modifications for maximum average subarray with length divisible by k (different problem).

