# 🟢 LeetCode 9: Palindrome Number

## 🔗 Problem Link
https://leetcode.com/problems/palindrome-number/

------------------------------------------------------------------------

## 🧠 Problem Summary

You are given an integer `x` and you need to check whether it reads the same forward and backward — just like a palindrome string, but here it's a **number**.

Key points:
- Negative numbers can never be palindromes because of the minus sign.
- A number ending with `0` (like 10, 20, 30) cannot be a palindrome unless the number is exactly `0`.

------------------------------------------------------------------------

## 💭 My Thought Process

At first, it seems obvious to convert the number to a string and compare it with its reverse.  
But that’s a lazy approach and not memory-efficient.

So I looked for a mathematical way:
- Reverse the number **digit by digit**, but that’s wasteful.
- Then I realized:  
  **I don’t need to reverse the whole number — only half of it.**

The moment the reversed half becomes greater than or equal to the remaining half, I can stop.  
This saves time and avoids overflow issues.

That trick made everything click.

------------------------------------------------------------------------

## ❌ Mistakes I Made

- Initially tried to reverse the whole number, which was unnecessary  
- Forgot about edge cases:  
  - Negative numbers  
  - Numbers ending in zero  

------------------------------------------------------------------------

## ✔️ Final Approach

Reverse only the **last half** of the digits of the number and compare the two halves.

Steps:
1. If `x` is negative → return False  
2. If `x` ends with `0` but is not `0` → return False  
3. Build `rev` by extracting digits from the end  
4. Stop when `rev >= x`  
5. Check:
   - `x == rev` (even number of digits)  
   - OR `x == rev // 10` (odd number of digits, middle digit removed)

Clean, fast, and avoids extra memory.

------------------------------------------------------------------------

## 🧾 Code (Python)

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        if x < 0 or (x % 10 == 0 and x != 0):  # Handles the edge cases
            return False
        rev = 0  # Initialise the variable for reverse the order 
        while x > rev:
            rev = rev * 10 + x % 10
            x //= 10
        return x == rev or x == rev // 10  # Compare the halves for the final output
```

------------------------------------------------------------------------

## ⏱️ Complexity

-   **Time:** O(log₁₀(n)) — we process half the digits
-   **Space:** O(1) — no extra memory used

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- The full-string approach just for comparison
- A C++ implementation for practice
