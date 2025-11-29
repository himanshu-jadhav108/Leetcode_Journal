# 🟢 LeetCode 3512: Minimum Operations to Make Array Sum Divisible by K

## 🔗 Problem Link

https://leetcode.com/problems/minimum-operations-to-make-array-sum-divisible-by-k/

------------------------------------------------------------------------

## 🧠 Problem Summary

Given an integer array `nums` and an integer `k`, you may perform operations that remove exactly one element from the array. The task is to find the minimum number of operations needed so that the sum of the remaining elements is divisible by `k`. If it is impossible to achieve, return -1.

------------------------------------------------------------------------

## 💭 My Thought Process

- The total sum modulo `k` determines how much we need to remove (let's call it `need = total_sum % k`).
- If `need == 0`, no operations are required.
- A valid removal is any subarray (contiguous sequence) whose sum % `k` == `need`; removing such a subarray will leave the remaining sum divisible by `k`.
- The problem reduces to finding the shortest subarray with sum % `k` == `need` (or determining that none exists). Typical approaches use prefix sums and a hash map that records indices by prefix sum modulo `k` to find candidates in O(n) time.

------------------------------------------------------------------------

## ❌ Mistakes I Made

- Treating removal of single elements only; the correct formulation allows removing any subarray, so single-element heuristics can be insufficient.
- Forgetting to handle the `need == 0` early exit (zero operations required).
- Overlooking edge cases where the only valid subarray is the entire array (then removing it would leave an empty array — check problem statement for whether empty is allowed; if not allowed, answer may be -1).

------------------------------------------------------------------------

## ✔️ Final Approach

- Compute `total = sum(nums)`; let `need = total % k`.
- If `need == 0`, return 0.
- Use prefix sum modulo `k`: maintain a map `last_index[mod]` storing the latest index where a prefix had remainder `mod` (initialize `last_index[0] = -1` for prefix sum 0 at index -1).
- For each index `i`, compute `pref = (pref + nums[i]) % k`. We want a prior prefix with remainder `(pref - need) % k`; if found at index `j`, then subarray `(j+1..i)` has sum % `k` == `need`, and its length is `i - j`. Track the minimal such length. The answer is that minimal length (number of elements removed); if no such subarray exists or it equals `n` (removing whole array not allowed in some statements), return -1.

------------------------------------------------------------------------

## 🧾 Code (Python)

``` python
class Solution:
    def minOperations(self, nums: List[int], k: int) -> int:
        return sum(nums) % k
```

------------------------------------------------------------------------

## ⏱️ Complexity

- **Time:** O(n) for the optimal sliding/prefix-sum solution using a hashmap.
- **Space:** O(k) or O(n) depending on implementation (hashmap of prefix remainders or storing indices).

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Implement the full O(n) prefix-sum + hashmap solution and add unit tests.
- Provide a C++/Java version and compare speed/memory trade-offs.
- Add example cases (edge cases: need == 0, impossible cases, single-element arrays).

