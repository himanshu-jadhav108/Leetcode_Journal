# 🟢 LeetCode 1590: Make Sum Divisible by P

## 🔗 Problem Link

https://leetcode.com/problems/make-sum-divisible-by-p/

------------------------------------------------------------------------

## 🧠 Problem Summary

Given an integer array `nums` and an integer `p`, remove a (possibly empty) subarray from `nums` such that the sum of the remaining elements is divisible by `p`. Return the length of the shortest subarray you need to remove; if it's impossible, return `-1`.

------------------------------------------------------------------------

## 💭 My Thought Process

- Let `total = sum(nums)` and `target = total % p`. If `target == 0`, the array is already divisible by `p` and we return `0`.
- Removing a subarray with sum % `p` == `target` will make the remaining sum divisible by `p`.
- Use prefix sums modulo `p`: store the latest index where a particular prefix remainder occurred in a hashmap `mp`. For the current prefix remainder `prefix`, we need to find a previous prefix remainder equal to `(prefix - target) % p` so that the subarray between them has remainder `target`.
- Track the minimum length `res` of such subarrays. If no valid subarray shorter than `n` is found, return `-1`.

------------------------------------------------------------------------

## ❌ Mistakes I Made

- Forgetting the early return when `target == 0` (zero removals needed).
- Using raw prefix sums rather than prefix modulo `p` causing modulus arithmetic errors.
- Not initializing the hashmap with `{0: -1}` to handle subarrays starting at index 0.

------------------------------------------------------------------------

## ✔️ Final Approach

- Compute `total = sum(nums)` and `target = total % p`. If `target == 0`, return `0`.
- Iterate through `nums`, maintaining `prefix = (prefix + nums[i]) % p` and a map `mp` mapping prefix remainders to their latest indices (initialize `mp = {0: -1}`).
- For each index `i`, compute `need = (prefix - target) % p`. If `need` exists in `mp`, the subarray `(mp[need] + 1 .. i)` has remainder `target` and is a candidate for removal; update `res` with its length `i - mp[need]`.
- After the loop, return `-1` if the shortest length equals `n` (can't remove entire array), otherwise return `res`.

------------------------------------------------------------------------

## 🧾 Code (Python)

``` python
class Solution:
    def minSubarray(self, nums: List[int], p: int) -> int:
        total = sum(nums)
        target = total % p

        if target == 0:
            return 0

        mp = {0: -1}
        prefix = 0
        res = len(nums)

        for i, x in enumerate(nums):
            prefix = ( prefix + x ) % p
            need = ( prefix - target ) % p
            if need in mp:
                res = min(res, i - mp[need])
            mp[prefix] = i
            
        return -1 if res == len(nums) else res
```

------------------------------------------------------------------------

## ⏱️ Complexity

- **Time:** O(n) — single pass using hashmap lookups.
- **Space:** O(p) (at most), or O(n) in worst case if many distinct remainders appear.

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Add unit tests covering edge cases: `target == 0`, impossible cases, arrays with negative numbers (if allowed), and single-element arrays.
- Implement a C++/Java version and add a small runner to validate performance.
- Explore variations: shortest subarray with sum equal to a given value (without modulo).

