# 🟢 LeetCode 020: Valid Parentheses

## 🔗 Problem Link

https://leetcode.com/problems/valid-parentheses/

------------------------------------------------------------------------

## 🧠 Problem Summary

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid. A string is valid if all open brackets are closed by the correct closing bracket in the correct order.

------------------------------------------------------------------------

## 💭 My Thought Process

- This is a classic stack problem: each opening bracket pushes onto the stack, and each closing bracket must match and pop the top of the stack.
- If the stack is empty when we encounter a closing bracket, or the top doesn't match, the string is invalid.
- After processing all characters, the stack must be empty for a valid string.
- Use a hashmap to map closing brackets to their corresponding opening brackets for clean matching.

------------------------------------------------------------------------

## ❌ Mistakes I Made

- Not handling an empty string correctly (an empty string is technically valid with an empty stack).
- Forgetting to check if the stack is empty before popping when encountering a closing bracket.
- Not returning `not stack` at the end to ensure all brackets were closed.

------------------------------------------------------------------------

## ✔️ Final Approach

- Create a hashmap `mapping` that maps each closing bracket to its corresponding opening bracket.
- Use a stack to track opening brackets as we iterate through the string.
- When we encounter an opening bracket, push it onto the stack.
- When we encounter a closing bracket, check if the stack is non-empty and the top matches the mapped opening bracket. If so, pop; otherwise, return `False`.
- After the loop, return `True` only if the stack is empty (all brackets matched and closed).

------------------------------------------------------------------------

## 🧾 Code (Python)

``` python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        mapping = {')': '(', '}': '{', ']':'['}

        for ch in s:
            if ch in mapping.values():
                stack.append(ch)
            else:
                if not stack or stack[-1] != mapping[ch]:
                    return False
                stack.pop()
       
        return not stack
```

------------------------------------------------------------------------

## ⏱️ Complexity

- **Time:** O(n) — single pass through the string with stack operations (push/pop) each O(1).
- **Space:** O(n) in the worst case — if the string is all opening brackets, the stack grows to size n.

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Implement a solution using character counting (for problems with multiple bracket types) and compare performance.
- Add unit tests covering edge cases: empty string, single bracket, nested brackets, and mismatched brackets.
- Provide C++/Java implementations for consistency. 
