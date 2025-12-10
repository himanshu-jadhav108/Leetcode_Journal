# 🟢 LeetCode 3577: Count Permutations That Meet Complexity Rules

## 🔗 Problem Link

https://leetcode.com/problems/count-the-number-of-computer-unlocking-permutations/

------------------------------------------------------------------------

## 🧠 Problem Summary

Given an array `complexity` representing unlocking complexities of computers, count the number of valid permutations where each computer (except the first) has a complexity strictly greater than the previous computer. Return the count modulo 10^9 + 7.

------------------------------------------------------------------------

## 💭 My Thought Process

- Key observation: the first computer's complexity is fixed (it remains first in any permutation).
- For a valid permutation, all remaining computers must have strictly increasing complexity from left to right.
- If any computer (index > 0) has complexity <= the first computer's complexity, no valid permutations exist (return 0).
- If a valid arrangement is possible, count the number of ways to arrange the remaining (n-1) computers in increasing order — this is (n-1)!.

------------------------------------------------------------------------

## ❌ Mistakes I Made

- Initially overthinking the problem — didn't realize the first element must remain first and the constraint is a strict increasing sequence for the rest.
- Off-by-one in factorial calculation — should compute (n-1)!, not n!.
- Not checking if it's impossible early (when some computer has complexity <= first).

------------------------------------------------------------------------

## ✔️ Final Approach

- Store the first computer's complexity.
- Check if all other computers have strictly greater complexity than the first; if not, return 0.
- Compute (n-1)! modulo 10^9 + 7 as the number of valid permutations (since the remaining n-1 computers can be arranged in any order and must satisfy the increasing constraint, there's exactly (n-1)! valid arrangements).

------------------------------------------------------------------------

## 🧾 Code (Python)

``` python
class Solution:
    MOD = 10**9 + 7

    def countPermutations(self, complexity: List[int]) -> int:
        n = len(complexity)
        first = complexity[0]

        for i in range(1, n):
            if complexity[i] <= first:
                return 0
        fact = 1
        
        for i in range(2, n):
            fact = (fact * i ) % self.MOD
        return fact

```

------------------------------------------------------------------------

## ⏱️ Complexity

- **Time:** O(n) — one pass to check validity, another to compute (n-1)!.
- **Space:** O(1) — only a few variables.

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Implement factorial using precomputation for multiple queries.
- Add unit tests for edge cases: all equal complexities, single element, sorted arrays.
- Provide C++/Java translations for consistency. 
