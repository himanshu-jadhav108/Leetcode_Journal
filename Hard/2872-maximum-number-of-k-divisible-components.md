# 🟢 LeetCode 2872: Maximum Number of K-Divisible Components

## 🔗 Problem Link

https://leetcode.com/problems/maximum-number-of-k-divisible-components

------------------------------------------------------------------------

## 🧠 Problem Summary

Given an undirected tree with `n` nodes (0-indexed), an array `edges` describing the tree edges, and a `values` array where `values[i]` is the value at node `i`, you may remove edges to split the tree into components. The goal is to maximize the number of components whose total sum of node values is divisible by `k`. Return that maximum count.

------------------------------------------------------------------------

## 💭 My Thought Process

- The tree structure suggests a DFS post-order traversal to compute subtree sums.
- For each node, compute the total sum of its subtree (including the node itself). If a subtree sum is divisible by `k`, we can cut the connection above it (or treat it as a completed component) and count one component; then the parent should see that subtree as contributing 0 to its own sum.
- Using recursion, a DFS call returns two pieces of information: the remaining sum modulo arithmetic (or the raw remaining sum) that should be passed upward, and the number of divisible components found in that subtree.
- The answer is the total count of divisible subtrees found across the whole tree.

------------------------------------------------------------------------

## ❌ Mistakes I Made

- Initially forgetting that when a subtree sum is divisible by `k` we should not pass that sum upward (it becomes 0 contribution for ancestors).
- Not handling recursion base cases carefully (e.g., leaf nodes) when summing values and counting components.

------------------------------------------------------------------------

## ✔️ Final Approach

- Build adjacency list from `edges`.
- Run DFS from node 0 (any node is fine since the graph is a tree) computing subtree sums and counts of k-divisible components.
- In DFS: accumulate the sum of current node plus returned subtree sums from children. If the total % `k` == 0, increment component count and return (0, count) to parent; otherwise return (total, count).
- The final answer is the count returned for the root DFS traversal.

------------------------------------------------------------------------

## 🧾 Code (Python)

``` python
class Solution:
    def maxKDivisibleComponents(self, n: int, edges: List[List[int]], values: List[int], k: int) -> int:
        adj = [[] for _ in range(n)]
        for u,v in edges :
            adj[u].append(v)
            adj[v].append(u)
        
        def dfs(node : int, parent : int) -> (int, int):
            total = values [node]
            count = 0
            for nei in adj[node]:
                if nei != parent:
                    sub_total , sub_count = dfs(nei, node)
                    total += sub_total
                    count += sub_count
            if total % k == 0:
                count += 1
                return 0, count
            return total , count
        return dfs(0, -1)[1]
```

------------------------------------------------------------------------

## ⏱️ Complexity

- **Time:** O(n) — each node and edge is visited once in the DFS.
- **Space:** O(n) — adjacency list plus recursion stack (height up to n in worst case).

------------------------------------------------------------------------

## 🔁 If I Revisit Later, I'll Try

- Provide an iterative DFS implementation to avoid recursion depth issues on very deep trees.
- Implement and compare a C++ version to verify performance and stack safety.
- Add small tests (including edge cases where `k = 1`, negative values, and single-node trees) to validate correctness.

