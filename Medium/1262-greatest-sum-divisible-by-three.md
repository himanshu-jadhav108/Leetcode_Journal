# 🟢 LeetCode 1262: Greatest Sum Divisible By Three

## 🔗 Problem Link

https://leetcode.com/problems/greatest-sum-divisible-by-three


------------------------------------------------------------------------

## 🧠 Problem Summary

In the Problem , there was the array of integer, I need to select **any subset** of numbers such that:
- Their **sum is maximum** , and 
- That sum should be **divisible by 3**
  
This is not a simple greedy problem because removing the smallest remainder item is not always optimal.  
I need a controlled dynamic update of possible sums based on remainders.

------------------------------------------------------------------------

## 💭 My Thought Process

- First thought:  
  Just take the total sum and if `sum % 3 != 0`, remove the smallest element with the right remainder.  
  This works for some cases but fails when multiple removals are needed.

- Then I realized:  
  This is basically a DP problem where states track:
  - Maximum sum with remainder **0**
  - Maximum sum with remainder **1**
  - Maximum sum with remainder **2**

- The “click moment”:  
  Updating DP using a copy (`g = f[:]`) is required so that I don’t corrupt the current iteration state.

------------------------------------------------------------------------

## ❌ Mistakes I Made

- Ignored cases where two small remainder-1 items beat one remainder-2 item (and vice-versa).
- Tried greedy removal logic — fails for tricky combinations.

------------------------------------------------------------------------

## ✔️ Final Approach

Use **DP with 3 states** representing:

- `f[0]` → max sum divisible by 3  
- `f[1]` → max sum that leaves remainder 1  
- `f[2]` → max sum that leaves remainder 2  

For every number:
- Find its remainder `num % 3`
- Try adding it to each DP bucket and update the new DP array `g`
- Replace `f` with `g`

Final answer = `f[0]` (maximum sum divisible by 3)

This guarantees checking all valid combinations without brute force.

------------------------------------------------------------------------

## 🧾 Code (Python)

``` python
class Solution:
    def maxSumDivThree(self, nums: List[int]) -> int:
        f = [0, float('-inf'), float("-inf")]

        for num in nums:
            g = f [:]
            rem = num % 3
            for r in range(3):
                sum1 = f[r]
                if sum1 == float("-inf"):
                    continue
                rem2 = (r + rem) % 3
                sum2 = sum1 + num
                g[rem2] = max(g[rem2],sum2)
            f = g
        return f[0]



```

------------------------------------------------------------------------

## ⏱️ Complexity

-   **Time:** O(n)
-   **Space:** O(1) (Only for 3 DP states)

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Solve it in C++ or Java to build multi-language fluency
- Implement a bottom-up table version for clarity
