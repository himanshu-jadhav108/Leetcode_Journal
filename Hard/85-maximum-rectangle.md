# 🟢 LeetCode 85: Maximum Rectangle

## 🔗 Problem Link

https://leetcode.com/problems/maximal-rectangle/

------------------------------------------------------------------------

## 🧠 Problem Summary

Given a 2D binary matrix filled with '0' and '1', find the largest rectangle containing only '1's and return its area.

------------------------------------------------------------------------

## 💭 My Thought Process

- Treat each row as the base of a histogram where the height of each bar is the number of consecutive '1's above (including current row).
- For every row build/update this histogram and compute the largest rectangle area in the histogram using a monotonic stack (classic Largest Rectangle in Histogram problem).
- Take the maximum area across all rows.

Key insights:
- Reusing histogram heights across rows makes the algorithm efficient (O(rows * cols)).
- Use a sentinel (0) at the end of heights to flush remaining stack entries and avoid extra checks.

------------------------------------------------------------------------

## ❌ Mistakes I Made

- Forgetting to append a sentinel 0 to the histogram when computing largest-rectangle-histogram, which caused remaining bars to not be processed.
- Off-by-one errors when computing width; ensure width = i if stack empty else i - stack[-1] - 1.

------------------------------------------------------------------------

## ✔️ Final Approach

1. If matrix empty, return 0.
2. Maintain an array `histogram` of length = number of columns; for each row, update:
   - histogram[j] = histogram[j] + 1 if row[j] == '1' else 0
3. For each updated histogram, compute largest rectangle area using a monotonic increasing stack:
   - Iterate with a sentinel 0 appended; when current bar < stack top bar height, pop and compute area.
4. Track the global maximum area and return it after processing all rows.

This gives O(rows * cols) time and O(cols) extra space.

------------------------------------------------------------------------

## 🧾 Code (Python)

```python
from typing import List

class Solution:
    def largestRectangleHistogram(self, heights: List[int]) -> int:
        stack: List[int] = []
        max_area = 0
        heights.append(0)

        for i, h in enumerate(heights):
            while stack and heights[stack[-1]] > h:
                height = heights[stack.pop()]
                width = i if not stack else i - stack[-1] - 1
                max_area = max(max_area, height * width)
            stack.append(i)

        heights.pop()
        return max_area

    def maximalRectangle(self, matrix: List[List[str]]) -> int:
        if not matrix or not matrix[0]:
            return 0

        rows, cols = len(matrix), len(matrix[0])
        histogram = [0] * cols
        max_rect = 0

        for row in matrix:
            for j in range(cols):
                histogram[j] = histogram[j] + 1 if row[j] == '1' else 0

            max_rect = max(max_rect, self.largestRectangleHistogram(histogram))

        return max_rect

```

------------------------------------------------------------------------

## ⏱️ Complexity

- **Time:** O(rows * cols) — we update the histogram for each row (O(cols)) and compute largest-rectangle-in-histogram in O(cols) per row.
- **Space:** O(cols) — the histogram and stack sizes are proportional to the number of columns.

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Implement in C++/Java to build multi-language fluency.
- Add a small test harness and examples to verify edge cases (all zeros, all ones, single row/col).
