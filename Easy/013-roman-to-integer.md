# 🟢 LeetCode 13: Roman to Integer

## 🔗 Problem Link
https://leetcode.com/problems/roman-to-integer/

---

## 🧠 Problem Summary

Convert a Roman numeral string into an integer.  
Each Roman character has a value, but the twist is the **subtractive pairs**:  
- IV = 4 (because I < V → subtract)  
- IX = 9  
- XL = 40  
- etc.

So the logic becomes:
- If current value < next value → subtract  
- Else → add  

---

## 💭 My Thought Process

- At first, mapping each symbol to its value was easy.  
- The confusion came from the subtractive rule — I initially thought I needed to manually check all special cases (IV, IX, etc.).  
- Clean realization:  
  **Just compare current and next symbol. If the next is bigger → subtract. Otherwise → add.**  
  This simplifies everything.

---

## ❌ Mistakes I Made

- Tried to handle every special case separately → overcomplicated.  
- Forgot to handle the “last character” safely when looking ahead.

---

## ✔️ Final Approach

- Create a dictionary mapping Roman characters to integers.  
- Loop through the string:
  - Look at current value and next value.
  - If current < next → subtract current.
  - Else → add current.
- This handles all cases naturally.

---

## 🧾 Code (Python)

```python
class Solution:
    def romanToInt(self, s: str) -> int:
        roman_dict = {
            'I' : 1,
            'V' : 5,
            'X' : 10,
            'L' : 50,
            'C' : 100,
            'D' : 500,
            'M' : 1000
        }
        result = 0

        for i in range(len(s)):
            cur_val = roman_dict[s[i]]
            nxt_val = roman_dict[s[i + 1]] if i + 1 < len(s) else 0

            if cur_val < nxt_val:
                result -= cur_val
            else:
                result += cur_val

        return result
```

------------------------------------------------------------------------

## ⏱️ Complexity

-   **Time:** O(n) (single pass through the string)
-   **Space:**O(1) (The size of the dictionary is fixed)

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Solve it in C++ or Java to build multi-language fluency
- Implement a more optimized version using reverse iteration
