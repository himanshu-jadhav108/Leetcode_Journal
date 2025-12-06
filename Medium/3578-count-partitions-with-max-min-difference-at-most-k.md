# 🟢 LeetCode 3578: Count Partitions With Max-Min Difference At Most K

## 🔗 Problem Link

https://leetcode.com/problems/count-partitions-with-max-min-difference-at-most-k/

------------------------------------------------------------------------

## 🧠 Problem Summary

Given an array `nums` and an integer `k`, count the number of ways to partition the array into non-empty contiguous subarrays such that for every subarray in the partition, the difference between its maximum and minimum element is at most `k`. Return the number of valid partitions modulo 10^9 + 7.

------------------------------------------------------------------------

## 💭 My Thought Process

- The constraint on max-min per subarray suggests a sliding-window approach: for each right endpoint `r`, find the leftmost `l` such that the window `nums[l..r]` satisfies `max - min <= k`.
- Use monotonic deques to maintain max and min in the current window; adjust `l` as needed when the window violates the constraint.
- Once we know valid left boundaries for each `r`, dynamic programming can count partitions: `dp[i]` = number of ways to partition the prefix `nums[:i]`.
- Maintain a running sum `s` of valid `dp` values in the current window to compute `dp[r+1]` efficiently.

------------------------------------------------------------------------

## ❌ Mistakes I Made

- Not using monotonic deques initially and trying to recompute max/min for each window, which is O(n^2).
- Off-by-one errors in window boundaries when transitioning indices between `dp` and array indices.
- Not taking modulo at every addition/subtraction in the DP transitions, which can cause overflow.

------------------------------------------------------------------------

## ✔️ Final Approach

- Use two monotonic deques `mx` and `mn` to maintain indices of decreasing and increasing values respectively so we can get the window's max and min in O(1).
- Maintain `l` as the smallest index such that `nums[l..r]` satisfies `max - min <= k`. When the window violates the constraint, advance `l` while popping from deques and subtracting `dp[l]` from the running sum `s`.
- Let `dp[i]` be the number of valid partitions of the prefix `nums[:i]`; initialize `dp[0] = 1`. For each `r`, after adjusting `l`, `dp[r+1] = s + dp[r]` accumulation as shown in the code — the provided implementation does the accumulation carefully using `s`.

------------------------------------------------------------------------

## 🧾 Code (Python)

``` python
class Solution:
    def countPartitions(self, nums: List[int], k: int) -> int:
        n = len(nums)
        MOD = 10**9 + 7
        
        dp = [0] * (n + 1)
        dp[0] = 1
        
        from collections import deque
        mx, mn = deque(), deque()
        
        l = 0
        s = 0
        
        for r in range(n):
            while mx and nums[mx[-1]] <= nums[r]:
                mx.pop()
            while mn and nums[mn[-1]] >= nums[r]:
                mn.pop()
            mx.append(r)
            mn.append(r)
            
            while nums[mx[0]] - nums[mn[0]] > k:
                if mx[0] == l:
                    mx.popleft()
                if mn[0] == l:
                    mn.popleft()
                s = (s - dp[l]) % MOD
                l += 1
            
            s = (s + dp[r]) % MOD
            dp[r + 1] = s
        
        return dp[n]
        
```

------------------------------------------------------------------------

## ⏱️ Complexity

- **Time:** O(n) amortized — each index enters/exits deques at most once and DP updates are O(1) per element.
- **Space:** O(n) for the `dp` array and deques.

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Implement the same using prefix-sum Fenwick/Segment tree to compare performance.
- Add unit tests and provide a C++ translation for performance comparisons.
