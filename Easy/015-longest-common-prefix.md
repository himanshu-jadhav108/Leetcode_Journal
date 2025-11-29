# 🟢 LeetCode 15: Longest Common Prefix

## 🔗 Problem Link

https://leetcode.com/problems/longest-common-prefix/

------------------------------------------------------------------------

## 🧠 Problem Summary

Given an array of strings `strs`, find the longest common prefix string shared by all the strings in the array. If there is no common prefix, return an empty string.

------------------------------------------------------------------------

## 💭 My Thought Process

- A simple approach is to sort the strings lexicographically and then compare only the first and last strings: the common prefix of the whole list must be a prefix of both the first and last strings after sorting.
- Another straightforward method is vertical scanning: compare characters column by column across all strings until a mismatch is found.
- Sorting-based approach reduces comparisons because you only compare two strings instead of all pairs, and it is easy to implement correctly.

------------------------------------------------------------------------

## ❌ Mistakes I Made

- Not handling empty input (`strs == []`) which would cause `sorted(strs)[0]` to fail.
- Forgetting to check for empty strings inside the input list which may make the common prefix empty.
- Assuming all strings have equal lengths — must guard by using `min(len(first), len(last))` when iterating.

------------------------------------------------------------------------

## ✔️ Final Approach

- Sort the list of strings. Let `first` be the first string and `last` be the last string in sorted order.
- The longest common prefix of the whole list is the common prefix of `first` and `last`.
- Compare characters of `first` and `last` up to the length of the shorter string; append matching characters to the answer and stop at the first mismatch.
- Handle edge cases: empty `strs` or empty strings in the list.

------------------------------------------------------------------------

## 🧾 Code (Python)

``` python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        ans = ""
        strs = sorted(strs)
        first = strs[0]
        last = strs[-1]

        for i in range(min(len(first), len(last))):
            if (first[i] != last[i]):
                return ans
            ans += first[i]
        return ans 
```

------------------------------------------------------------------------

## ⏱️ Complexity

- **Time:** O(n * m * log n) when sorting is considered, where `n` is number of strings and `m` is average string length. After sorting, comparing first and last takes O(m).
- **Space:** O(n * m) for the sorted list copy in the worst case (language dependent). In-place sort may reduce extra space.

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Implement the vertical scanning and divide-and-conquer approaches and compare performance.
- Add input validation and unit tests for edge cases (empty list, single string, strings with no common prefix).
- Provide C++/Java implementations for familiarity with language-specific string handling.

