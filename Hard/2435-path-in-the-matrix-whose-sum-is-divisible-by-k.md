# 🟢 LeetCode 2435: Path In the Matrix Whose Sum Is Divisible By K

## 🔗 Problem Link

https://leetcode.com/problems/path-in-the-matrix-whose-sum-is-divisible-by-k/

------------------------------------------------------------------------

## 🧠 Problem Summary

Given an m x n integer grid and an integer k, count the number of paths from the top-left cell (0,0) to the bottom-right cell (m-1,n-1) where you can only move right or down and the sum of the values along the path is divisible by k. Return the count modulo 10^9 + 7.

------------------------------------------------------------------------

## 💭 My Thought Process

- Observed that at each cell, only the current sum modulo `k` matters for future decisions, so we can use dynamic programming where the state stores counts per remainder.
- Let `dp[i][j][r]` be the number of ways to reach cell `(i,j)` with path sum % `k` == `r`.
- Transitions come from top `(i-1,j)` and left `(i,j-1)`: add current cell value to each previous remainder and accumulate counts into the new remainder.
- The base case is the first row and first column, which can be initialized by accumulating the prefix sums modulo `k` or by the general transition using only one source for those edges.
- Time complexity will be `O(m * n * k)` and we can reduce space to `O(n * k)` by keeping only the previous row.

------------------------------------------------------------------------

## ❌ Mistakes I Made

- Overwriting counts when updating the remainder bucket instead of adding to the existing bucket (lost contributions).
- Trying to maintain a running prefix `s` inconsistently across nested loops; clearer to use the standard DP transition per cell.

------------------------------------------------------------------------

## ✔️ Final Approach

- Use a row-wise DP with `prev[j][r]` = number of ways to reach cell `(current_row-1, j)` with remainder `r`.
- For each row `i`, build `curr[j][*]` from `prev[j][*]` (coming from top) and `curr[j-1][*]` (coming from left). For each remainder `r` from a predecessor, compute `nr = (r + grid[i][j]) % k` and add the predecessor count to `curr[j][nr]`.
- Initialize `prev` using the first row by accumulating the first-row prefixes (or equivalently by applying the same transitions starting from `(0,0)`).
- Return `prev[n-1][0]` after processing all rows (the number of ways to reach bottom-right with remainder 0).

------------------------------------------------------------------------

## 🧾 Code (Python)

```python
class Solution:
    def numberOfPaths(self, grid: List[List[int]], k: int) -> int:
        MOD = 10**9 + 7
        m,n = len(grid), len(grid[0])

        prev = [[0] * k for _ in range(n)]
        curr = [[0] * k for _ in range(n)]

        s = 0
        for j in range(n):
            s = (s + grid[0][j]) % k
            prev[j][s] = 1

        s = grid[0][0] % k

        for i in range(1, m):
            s = (s + grid[i][0]) % k
            curr[0] = [0] * k
            curr[0][s] = 1

            for j in range(1,n):
                curr[j] = [0]*k
                val = grid[i][j]

                for r in range(k):
                    nr = (r + val) % k
                    curr[j][nr] = (prev[j][r] + curr[j - 1][r]) % MOD
            
            prev, curr = curr, prev

        return prev[n - 1][0]
```

------------------------------------------------------------------------

## ⏱️ Complexity

- **Time:** O(m * n * k) — for each of the m*n cells we iterate over k remainders.
- **Space:** O(n * k) — we store two rows of size `n` each with `k` remainder buckets (here we reuse `prev`/`curr` so only one extra row is active).

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Implement the same solution in C++/Java to compare constant factors and memory layout.
- Add unit tests and small examples in the repo to validate edge cases (single row/column, k=1, large k, zeros in grid).
- Explore further micro-optimizations if `k` is large but values have special structure.

