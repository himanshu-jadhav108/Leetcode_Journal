# 🟢 LeetCode 2211: Count Collisions on a Road

## 🔗 Problem Link

https://leetcode.com/problems/count-collisions-on-a-road/

------------------------------------------------------------------------

## 🧠 Problem Summary

Given a string `directions` representing cars on a road, where 'L' means a car moving left, 'R' means a car moving right, and 'S' means a car staying still, count the number of collisions that occur. Cars collide when a faster car catches up to a slower car or a stationary car.

------------------------------------------------------------------------

## 💭 My Thought Process

- Cars moving left ('L') don't collide with anything to their left.
- Cars moving right ('R') don't collide with anything to their right.
- Collisions only happen in the middle region between leftmost 'L' cars and rightmost 'R' cars.
- After removing leading 'L's and trailing 'R's, every remaining 'R' will eventually collide with every 'L' to its right (directly or via a chain).
- Each collision between an 'R' and 'L' pair counts as one collision, so we count all 'R' and 'L' in the remaining string.

------------------------------------------------------------------------

## ❌ Mistakes I Made

- Initially thinking we need to simulate the collisions step-by-step, which is overly complex.
- Not recognizing that leading 'L's can't collide (they're moving away from the road start) and trailing 'R's can't collide (they're moving away from the road end).
- Overcounting by not realizing that between consecutive 'S' characters, 'R' and 'L' patterns still collide in a 1-to-1 manner.

------------------------------------------------------------------------

## ✔️ Final Approach

- Strip all leading 'L' characters (they move away from the start, no collisions).
- Strip all trailing 'R' characters (they move away from the end, no collisions).
- In the remaining string, every 'R' will collide with every 'L' to its right. Count all 'R' and 'L' occurrences in the stripped string as the collision count.

------------------------------------------------------------------------

## 🧾 Code (Python)

``` python
class Solution:
    def countCollisions(self, directions: str) -> int:
        directions = directions.lstrip("L")
        directions = directions.rstrip("R")

        return directions.count("R") + directions.count("L")
```

------------------------------------------------------------------------

## ⏱️ Complexity

- **Time:** O(n) — `lstrip` and `rstrip` scan the string linearly, and counting 'R' and 'L' is also linear.
- **Space:** O(n) in the worst case for the stripped string (though Python string operations may optimize this).

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Add unit tests for edge cases: all same character, alternating patterns, single character strings.
- Implement a simulation-based approach for comparison and to verify correctness.
- Provide C++/Java implementations and benchmark against the optimized string approach. 
