# 🟢 LeetCode 58: Length of Last Word

## 🔗 Problem Link

https://leetcode.com/problems/length-of-last-word/

------------------------------------------------------------------------

## 🧠 Problem Summary

Given a string `s` consisting of words and spaces, return the length of the last word in the string. A word is a maximal substring consisting of non-space characters only. Trailing and leading spaces may be present.

------------------------------------------------------------------------

## 💭 My Thought Process

- The simplest approach is to trim trailing spaces and then split the string by spaces; the last element of the split is the last word.
- Alternatively, for O(1) extra space we can scan from the end, skip trailing spaces, and count characters until the next space or the start of the string.
- The split-and-take method is concise and very readable in Python; for very long strings and strict memory constraints, prefer the backward scan.

------------------------------------------------------------------------

## ❌ Mistakes I Made

- Not trimming trailing spaces before splitting — this can cause an empty string at the end.
- Using `s.split(' ')` which may produce empty segments for consecutive spaces; `s.split()` without arguments handles multiple spaces gracefully.
- Forgetting to handle the case where the string contains only spaces (should return 0).

------------------------------------------------------------------------

## ✔️ Final Approach

- Use `s.strip()` to remove leading/trailing spaces, then `s.split()` to split on any whitespace and safely get the last word with `split()[-1]`.
- Return the length of that last word. For a memory-optimized version, scan from the end counting non-space characters after skipping trailing spaces.

------------------------------------------------------------------------

## 🧾 Code (Python)

``` python
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        s = s.strip()
        last_word = s.split()[-1]
        return len(last_word)
```

------------------------------------------------------------------------

## ⏱️ Complexity

- **Time:** O(n) where n = len(s) — trimming and splitting or scanning take linear time.
- **Space:** O(n) in the worst case for `s.split()` (if the split creates many pieces). The backward-scan alternative uses O(1) extra space.

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Add the O(1) extra-space backward scan implementation and compare runtime on long inputs.
- Provide C++/Java versions and small unit tests covering edge cases (only spaces, single word, trailing spaces).

