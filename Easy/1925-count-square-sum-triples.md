# 🟢 LeetCode 1925: Count Square Sum Triples

## 🔗 Problem Link

https://leetcode.com/problems/count-square-sum-triples/

------------------------------------------------------------------------

## 🧠 Problem Summary

You're given a number n, and you need to count how many Pythagorean-like triples ``(a,b,c)`` satisfy:
```a^2+b^2=c^2```
with the constraint:
```1 <= a,b,c <= n```
Each ordered pair counts separately — meaning ``(a,b,c)`` and ``(b,a,c)`` are two different triples.


------------------------------------------------------------------------

## 💭 My Thought Process

- My first instinct was brute force: try all `a,b,c` up to `n`.
But that’s ``O(n^3)`` — way too slow.
- Then I realized we only care about Pythagorean triples, which have a known formula using *Euclid’s parameters* s and t.
- That clicked: instead of checking all triples, I can *generate* them using the formula and scale them up.
- The tricky part was ensuring:
  - s and t have opposite parity
  - gcd (s,t)=1
  - Count multiples correctly
- Once that fell into place, the solution became extremely efficient.


------------------------------------------------------------------------

## ❌ Mistakes I Made

- I initially forgot that ordered pairs count separately, so I undercounted.
- I didn’t break - early when ``c>n``, causing unnecessary iterations.



------------------------------------------------------------------------

## ✔️ Final Approach

Use *Euclid’s formula* to generate primitive Pythagorean triples:
``a=s^2-t^2, b=2st, c=s^2+t^2``
Then count how many multiples of each primitive triple fit within the limit n.
Key ideas:
- Loop over valid `s,t` pairs.
- Ensure they generate primitive triples:
  - `gcd (s,t)=1`
  - `s` and `t` have opposite parity
- Compute `c=s^2+t^2`
- If `c>n`, break early.
- Count how many multiples fit:
   `` k = ( n / c )``
- Each triple contributes *2* (because `(a,b,c)` and `(b,a,c)` both count).


------------------------------------------------------------------------

## 🧾 Code (Python)

``` python
class Solution:
    def countTriples(self, n: int) -> int:
        count = 0
        nsqrt = int(sqrt(n))
        for s in range(2, nsqrt + 1):
            for t in range(( s & 1 )+1, s, 2):
                if gcd(s, t) != 1: continue
                c = s * s + t * t
                if c>n: break
                k=n//c
                count+=2*k
        return count

```

------------------------------------------------------------------------

## ⏱️ Complexity

-   **Time:** O(n^0.5) - - because we only iterate over valid s,t pairs

-   **Space:** O(1)

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Implement it in C++ or Java to strengthen multi-language mastery
- Try a brute-force version just to compare performance differences

