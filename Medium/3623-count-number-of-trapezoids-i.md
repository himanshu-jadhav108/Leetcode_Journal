# 🟢 LeetCode 3623: Count Number Of Trapezoids I

## 🔗 Problem Link

https://leetcode.com/problems/count-number-of-trapezoids-i/

------------------------------------------------------------------------

## 🧠 Problem Summary

Given a list of 2D points (integer coordinates), count the number of trapezoids that can be formed following the problem's definition. The provided solution groups points by their y-coordinate (horizontal lines) and counts combinations of point-pairs on distinct horizontal lines to form trapezoids, using combinatorics and modulo arithmetic to return the final count.

------------------------------------------------------------------------

## 💭 My Thought Process

- Observed that trapezoids in this problem can be formed by selecting two distinct horizontal lines and choosing two distinct points on each line (forming the pairs for the parallel sides).
- For each horizontal line (same y), the number of ways to choose a pair of points on that line is comb(c, 2) = c * (c-1) / 2 where c is the number of points sharing that y.
- If we let p_i be the number of point-pairs on line i, then for any unordered pair of distinct lines (i, j) there are p_i * p_j trapezoids formed by choosing one pair from each line. Summing p_i * p_j over i < j gives the total count.
- The sum over all i<j of p_i * p_j can be computed efficiently using the identity: (sum p_i)^2 - sum (p_i^2) all divided by 2.

------------------------------------------------------------------------

## ❌ Mistakes I Made

- Initially thinking in terms of individual points combinatorics directly across lines — grouping by y simplifies the counting.
- Forgetting to apply modulo at the end (important when counts are large), and ensuring integer division is safe when using the combinatorial identity.

------------------------------------------------------------------------

## ✔️ Final Approach

- Group points by y-coordinate and compute `c = count of points` per y.
- For each y with c > 1, compute `p = c * (c-1) // 2` (number of unordered point-pairs on that horizontal line).
- Let `total_pairs = sum(p)` and `squared_pairs = sum(p*p)`.
- The total number of trapezoids equals `(total_pairs^2 - squared_pairs) // 2` (sum over i<j p_i * p_j). Return that value modulo 10^9+7.

------------------------------------------------------------------------

## 🧾 Code (Python)

``` python

MOD = 10**9 + 7
class Solution:
    def countTrapezoids(self, points: List[List[int]]) -> int:
        pairs = [c * (c - 1) // 2 for c in Counter(y for _, y in points).values() if c > 1]
        total_pairs = sum(pairs)
        squared_pairs = sum(p*p for p in pairs)
        return ((total_pairs * total_pairs - squared_pairs) // 2) % MOD
        
```

------------------------------------------------------------------------

## ⏱️ Complexity

- **Time:** O(n) to count occurrences per y and compute the sums, where n = number of points (grouping step dominates).
- **Space:** O(u) where u is the number of distinct y-coordinates (for the counter and intermediate pair counts).

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Implement an explicit check for degenerate cases (few points, all points on a single line).
- Add unit tests and a small runner to validate results against brute-force for small inputs.
- Provide C++/Java translations to compare performance.

