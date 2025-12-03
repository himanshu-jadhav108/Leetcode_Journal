# 🟢 LeetCode 3625: Count Number Of Trapezoids II

## 🔗 Problem Link

https://leetcode.com/problems/count-number-of-trapezoids-ii/

------------------------------------------------------------------------

## 🧠 Problem Summary

Given a list of 2D points, count the number of trapezoids that can be formed where a trapezoid is defined by four distinct points such that one pair of opposite sides is parallel (the two lines formed by the point pairs have the same slope). Return the count modulo 10^9 + 7.

------------------------------------------------------------------------

## 💭 My Thought Process

- A trapezoid has one pair of parallel sides: we need to find all pairs of line segments (formed by choosing 4 distinct points: 2 for each segment) that share the same slope.
- Two segments have the same slope if their direction vectors (dx, dy) have the same normalized form (reduced by their GCD and canonicalized for direction).
- For each unique normalized slope, count how many segments share that slope. If there are `c` segments with the same slope, the number of trapezoid combinations is comb(c, 2) — but we must exclude degenerate cases where the four points are collinear (all on a single line).
- Key insight: count all pairs of parallel segments, then subtract pairs that are collinear (same descartes intercept = c in y = mx + c, after normalization). This requires careful handling of slope representation and line intercepts.

------------------------------------------------------------------------

## ❌ Mistakes I Made

- Initially not canonicalizing slopes correctly — slopes must be normalized and directional (avoid (dx, dy) and (-dx, -dy) being considered different).
- Forgetting to subtract collinear cases — pairs of segments on the same line do not form valid trapezoids.
- Using floating-point arithmetic for slopes and intercepts, causing precision errors; switched to integer-only using GCD and scaled coordinates.

------------------------------------------------------------------------

## ✔️ Final Approach

- For each pair of points (i, j), compute the normalized slope (sx, sy) by reducing (dx, dy) with GCD and ensuring a canonical direction.
- Compute the normalized "line intercept" des = sx * y1 - sy * x1 (a value invariant along the line with slope (sx, sy)).
- Use two dictionaries: `t` counts segments grouped by normalized slope and intercept (to find parallel and collinear pairs), and `v` counts segments grouped by actual (dx, dy) and intercept (for collinearity check across all scales).
- For each slope group in `t`, count pairs of distinct segments: sum over all pairs (a,b) with a < b where both belong to the same slope but different intercepts. This is done via the `count` helper: for each intercept value in a slope group, multiply its count by the sum of all remaining segments in that slope group.
- Subtract the collinear cases (pairs on the same line) which come from the `v` dictionary divided by 2 (since each collinear pair is counted twice in `v` due to direction canonicalization).

------------------------------------------------------------------------

## 🧾 Code (Python)

``` python
from math import gcd
from collections import defaultdict
from typing import List

class Solution:
    def countTrapezoids(self, points: List[List[int]]) -> int:
        t = defaultdict(lambda: defaultdict(int))
        v = defaultdict(lambda: defaultdict(int))

        n = len(points)

        for i in range(n):
            x1, y1 = points[i]
            for j in range(i + 1, n):
                x2, y2 = points[j]
                dx = x2 - x1
                dy = y2 - y1

                if dx < 0 or (dx == 0 and dy < 0):
                    dx = -dx
                    dy = -dy

                g = gcd(dx, abs(dy))
                sx = dx // g
                sy = dy // g

                des = sx * y1 - sy * x1

                key1 = (sx << 12) | (sy + 2000)
                key2 = (dx << 12) | (dy + 2000)

                t[key1][des] += 1
                v[key2][des] += 1

        return self.count(t) - self.count(v) // 2

    def count(self, mp):
        ans = 0

        for inner in mp.values():
            total = sum(inner.values())
            remaining = total

            for val in inner.values():
                remaining -= val
                ans += val * remaining

        return ans
```

------------------------------------------------------------------------

## ⏱️ Complexity

- **Time:** O(n^2) to iterate all pairs of points and compute slopes; O(n^2 log n) when considering GCD computation and the counting step over all slope/intercept groups.
- **Space:** O(n^2) in the worst case for storing all point-pair segments in the dictionaries.

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Add unit tests for edge cases: collinear points, duplicate points, very close slopes.
- Optimize the implementation using a more efficient slope representation (e.g., Stern-Brocot tree or continued fractions for rational slopes).
- Provide C++/Java translations and benchmark performance on large inputs. 
