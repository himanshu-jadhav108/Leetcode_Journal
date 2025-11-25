# 🟢 LeetCode 1015: Smallest Integer Divisible by K

## 🔗 Problem Link
https://leetcode.com/problems/smallest-integer-divisible-by-k/

---

## 🧠 Problem Summary

You need to find the **smallest number of 1's** (like 1, 11, 111, 1111...) such that this number is divisible by `k`.

Example:
- If k = 3 → 111 is divisible by 3 → answer = 3
- If k = 2 or k = 5 → impossible (because numbers made of only '1's never end with even digit or 5)

You aren’t allowed to actually build the number (it gets too large).  
You must work only with **remainders**.

---

## 💭 My Thought Process

- First attempt:  
  Tried constructing the number as integer → quickly realized it will explode in size. Useless.

- Then understood:  
  You only need the remainder at each step:
  - `(previous_remainder * 10 + 1) % k`
  
  This simulates adding another “1” digit without creating huge numbers.

- Realization that fixed the logic:  
  For k divisible by 2 or 5, no number full of 1s can ever be divisible by k → instantly return -1.

---

## ❌ Mistakes I Made

- Initially forgot the edge case for k divisible by 5.
- Tried brute force generating the number → overflow / time issues.

---

## ✔️ Final Approach

- If k is divisible by 2 or 5 ⇒ immediately impossible.
- Otherwise, simulate adding digits `1` using a running remainder.
- If remainder becomes 0 at step `i`, then `i` is the number of 1's needed.

We are guaranteed that repeating remainders means we’re stuck, so we only loop up to `k`.

---

## 🧾 Code (Python)

```python
class Solution:
    def smallestRepunitDivByK(self, k: int) -> int:
        if k == 1:
            return 1
        if k % 2 == 0 or k % 5 == 0:
            return -1

        rem = 0
        for i in range(1, k + 1):
            rem = (rem * 10 + 1) % k
            if rem == 0:
                return i
        return -1
```

------------------------------------------------------------------------

## ⏱️ Complexity

-   **Time:** O(n)
-   **Space:** O(1)

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Solve it in C++ or Java to build multi-language fluency
- Try to visualize remainder cycles to understand modulo patterns more deeply
