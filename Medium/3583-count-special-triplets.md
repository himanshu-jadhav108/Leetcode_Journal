# 🟢 LeetCode 3583: Count Special Triplets

## 🔗 Problem Link

https://leetcode.com/problems/count-special-triplets/

------------------------------------------------------------------------

## 🧠 Problem Summary

Given an array `nums`, count the number of "special" triplets (i, j, k) where i < j < k and nums[i] * 2 = nums[j] and nums[j] * 2 = nums[k]. Return the count modulo 10^9 + 7.

------------------------------------------------------------------------

## 💭 My Thought Process

- Brute force would be O(n^3), checking all triplets — too slow.
- Key insight: for each middle element at index j, we can count how many valid left elements (nums[i] = nums[j] / 2) appear before it and how many valid right elements (nums[k] = nums[j] * 2) appear after it.
- Use a frequency counter for all elements and a "seen so far" counter to track elements before the current index efficiently.
- For each j, count pairs: (valid i's before j) * (valid k's after j).

------------------------------------------------------------------------

## ❌ Mistakes I Made

- Initially thinking O(n^3) brute force was necessary without recognizing the two-pointer opportunity.
- Not handling the special case where nums[j] is 0 (since 0/2 = 0, which creates double-counting issues).
- Forgetting to apply modulo at the end to handle large counts.

------------------------------------------------------------------------

## ✔️ Final Approach

- Precompute `freq` = frequency of all elements in nums.
- Use `prev` to track frequencies of elements seen so far (before the current index).
- For each middle index j (from 1 to n-2):
  - Compute x2 = nums[j] * 2 (target for right element).
  - Count triplets: (count of nums[j]/2 before j) * (count of x2 after j, excluding those already seen).
  - Handle the x == 0 edge case to avoid double-counting.
  - Update `prev` with the current element.
- Return the total count modulo 10^9 + 7.

------------------------------------------------------------------------

## 🧾 Code (Python)

``` python

class Solution:
    def specialTriplets(self, nums: List[int]) -> int:
        n, MOD=len(nums), 10**9+7
        freq, prev=Counter(nums), Counter()
        cnt=0
        prev[nums[0]]+=1
        for i in range(1, n-1):
            x=nums[i]
            x2=x<<1
            cnt+=prev[x2]*(freq[x2]-prev[x2]-(x==0))
            prev[x]+=1
        return cnt%MOD
        
```

------------------------------------------------------------------------

## ⏱️ Complexity

- **Time:** O(n) — single pass through the array with O(1) counter operations.
- **Space:** O(n) — for the frequency and "seen so far" counters.

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Implement with different multiplier ratios (e.g., 3x or k*x) and benchmark.
- Add unit tests for edge cases: arrays with zeros, single elements, all duplicates.
- Provide C++/Java implementations for cross-language practice. 
