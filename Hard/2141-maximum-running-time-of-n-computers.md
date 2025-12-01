# 🟢 LeetCode 2141: Maximum Running Time of N Computers

## 🔗 Problem Link

https://leetcode.com/problems/maximum-running-time-of-n-computers/

------------------------------------------------------------------------

## 🧠 Problem Summary

You are given `n` computers and an array `batteries` where `batteries[i]` is the runtime (in hours) of the i-th battery. You can use one battery per computer at a time and swap batteries between computers, but each battery can only supply power for its given runtime total. Determine the maximum number of hours all `n` computers can run simultaneously.

------------------------------------------------------------------------

## 💭 My Thought Process

- The total available runtime is `sum(batteries)`; if we can distribute this energy evenly across `n` machines, the upper bound per machine is `sum(batteries) // n`.
- Large batteries that individually exceed the current average are effectively reducible: if a battery has more capacity than the target per-machine runtime, its extra capacity can't help raise the target for other machines beyond the average, so we can remove (use fully) such batteries and reduce `n` accordingly.
- Sorting batteries and greedily removing the largest ones that exceed `total // n` gives a correct reduction process until all remaining batteries are at most the per-machine average, after which `total // n` is the achievable runtime.

------------------------------------------------------------------------

## ❌ Mistakes I Made

- Initially thinking binary search over time was necessary — while valid, a greedy sorting approach is simpler and uses O(m log m) time where m = len(batteries).
- Forgetting to handle the case where many batteries are extremely large and reduce `n` to 0 (should not happen for valid inputs but guard assumptions accordingly).

------------------------------------------------------------------------

## ✔️ Final Approach

- Compute `total = sum(batteries)` and sort `batteries` ascending.
- Iterate from the largest battery downward: if `batteries[i] > total // n`, subtract that battery from `total` and decrement `n` (we assign that battery to run alone and reduce the remaining computers to serve). Continue until the largest remaining battery is <= `total // n`.
- Return `total // n` as the maximum simultaneous runtime for the remaining `n` computers.

------------------------------------------------------------------------

## 🧾 Code (Python)

``` python
class Solution:
    def maxRunTime(self, n: int, batteries: List[int]) -> int:
        total = sum(batteries)
        batteries.sort()

        for i in range(len(batteries) -1, -1, -1):
            if batteries[i] > total // n:
                total -= batteries[i]
                n -= 1
            else:
                break
        return total // n
```

------------------------------------------------------------------------

## ⏱️ Complexity

- **Time:** O(m log m) where m = len(batteries) due to sorting.
- **Space:** O(1) extra space (sorting aside) or O(m) if the sorting implementation requires it.

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Implement the binary-search-on-time alternative (feasible/time-check function) to compare approaches.
- Provide a C++ implementation to compare performance and memory behavior.
- Add unit tests for edge cases: many small batteries, a battery much larger than the sum of others, and extreme `n` values.

