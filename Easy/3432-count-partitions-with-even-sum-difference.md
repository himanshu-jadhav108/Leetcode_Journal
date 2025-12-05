# 🟢 LeetCode 3432: Count Partitions With Even Sum Difference

## 🔗 Problem Link

https://leetcode.com/problems/count-partitions-with-even-sum-difference/

------------------------------------------------------------------------

## 🧠 Problem Summary

Given an array `nums`, count the number of ways to partition the array into two non-empty subarrays such that the difference between the sum of the left partition and the sum of the right partition is even. A partition at index `i` means the left partition is `nums[0..i]` and the right partition is `nums[i+1..n-1]`.

------------------------------------------------------------------------

## 💭 My Thought Process

- For each valid partition point (indices 0 to n-2), compute `left_sum` (sum of left partition) and `right_sum` (sum of right partition).
- The difference is `left_sum - right_sum`, which is even iff both `left_sum` and `right_sum` have the same parity (both odd or both even).
- Rather than computing `right_sum` from scratch each time, use `total_sum` and compute `right_sum = total_sum - left_sum`.
- Since `total_sum` is constant, checking parity equivalence is equivalent to checking if `left_sum % 2 == right_sum % 2`.

------------------------------------------------------------------------

## ❌ Mistakes I Made

- Initially computing `right_sum` separately, which was inefficient; realized we can derive it from `total_sum`.
- Confusing the parity condition: the difference is even iff the two sums have the same parity.
- Forgetting that we can only partition at indices 0 to n-2 (not at n-1, which would make the right partition empty).

------------------------------------------------------------------------

## ✔️ Final Approach

- Compute `total_sum = sum(nums)`.
- Iterate through indices 0 to n-2 (valid partition points).
- For each index, maintain a running `left_sum` and compute `right_sum = total_sum - left_sum`.
- Check if `left_sum % 2 == right_sum % 2`; if so, increment the count.
- Return the total count.

------------------------------------------------------------------------

## 🧾 Code (Python)

``` python
class Solution:
    def countPartitions(self, nums: List[int]) -> int:
        total_sum = sum(nums)
        left_sum = 0
        count = 0

        for x in range(len(nums) - 1):
            left_sum += nums[x]
            right_sum = total_sum - left_sum

            if left_sum % 2 == (right_sum % 2):
                count += 1
                
        return count
```

------------------------------------------------------------------------

## ⏱️ Complexity

- **Time:** O(n) — one pass to compute total sum, then one pass through the array to count valid partitions.
- **Space:** O(1) — only using a few variables for tracking.

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Add unit tests covering edge cases: arrays with all even/odd numbers, single element array, two-element array.
- Implement variations where the partition threshold is different (e.g., difference divisible by k).
- Provide C++/Java implementations for cross-language practice. 
