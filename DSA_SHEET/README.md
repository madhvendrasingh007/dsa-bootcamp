# 🚀 30-Day DSA Mastery Roadmap
### Crack MAANG Interviews with Pattern Recognition | Starting March 23, 2026

<div align="center">

![DSA Roadmap](https://img.shields.io/badge/Duration-30%20Days-blueviolet?style=for-the-badge)
![Problems](https://img.shields.io/badge/Problems-~87-orange?style=for-the-badge)
![Level](https://img.shields.io/badge/Level-Intermediate-green?style=for-the-badge)
![Target](https://img.shields.io/badge/Target-MAANG%2FMicrosoft-red?style=for-the-badge)

> **Stop restarting. Start pattern-matching.**  
> This roadmap rewires your brain to *see* patterns before touching code.

</div>

---

## 📌 The Universal Problem-Solving Framework

> Apply this **before writing a single line of code** for every problem.

```
1. READ CONSTRAINTS   → Array size? Sorted? Duplicates? Negatives?
2. IDENTIFY THE ASK   → Subarray? Pair? Index? Min/Max?
3. NAME THE PATTERN   → (use the table below)
4. WRITE SKELETON     → Function signature + base cases first
5. DRY RUN            → On 2 examples before coding full solution
```

---

## 🧠 Master Pattern Bible — All Topics

> Every DSA problem maps to one of these patterns. Learn the trigger, not the solution.

### 🟦 Array & String Patterns

| Pattern | Named Algorithm | Trigger Clue | Brute → Optimal |
|:---|:---|:---|:---|
| **Two Pointers** | — | Sorted, pairs, sum = target | O(n²) → **O(n)** |
| **Fast & Slow Pointers** | Floyd's Cycle Detection | Cycle, middle, palindrome LL | O(n) space → **O(1)** |
| **Sliding Window** | — | Subarray/substring, max/min length, "at most k" | O(n²) → **O(n)** |
| **Prefix Sum** | — | Range sum, subarray sum = k, "sum from l to r" | O(n²) → **O(n)** |
| **Hashing** | — | Count, check existence, first/only, duplicates | O(n²) → **O(n)** |
| **Kadane's Algorithm** | Kadane's | Max/min contiguous subarray sum | O(n²) → **O(n)** |
| **Carry Forward** | — | Running best (stock price, max so far) | O(n²) → **O(n)** |
| **Cyclic Sort** | — | Numbers 1 to n, missing/duplicate in range | O(n²) → **O(n)** |
| **Sorting-based** | Dutch National Flag | Rearrange, group by condition, 0s/1s/2s | Simplifies logic |

### 🟩 Binary Search Patterns

| Pattern | Named Algorithm | Trigger Clue | Brute → Optimal |
|:---|:---|:---|:---|
| **Binary Search** | — | Sorted array, "find in sorted", large constraints | O(n) → **O(log n)** |
| **Binary Search on Answer** | — | "Minimize the maximum", "maximize the minimum" | O(n²) → **O(n log n)** |

### 🟧 Linked List Patterns

| Pattern | Named Algorithm | Trigger Clue | Brute → Optimal |
|:---|:---|:---|:---|
| **In-place Reversal** | — | Reverse LL or a group, rotate list | O(n) space → **O(1)** |
| **Fast & Slow Pointers** | Floyd's Algorithm | Cycle detect, cycle start, nth from end | O(n) space → **O(1)** |

### 🟥 Stack & Queue Patterns

| Pattern | Named Algorithm | Trigger Clue | Brute → Optimal |
|:---|:---|:---|:---|
| **Monotonic Stack** | — | Next greater/smaller, histogram, temperatures | O(n²) → **O(n)** |
| **Monotonic Deque** | — | Sliding window max/min | O(n·k) → **O(n)** |
| **LRU Design** | HashMap + DLL | O(1) get + put with eviction | O(n) → **O(1)** |

### 🌳 Tree & Graph Patterns

| Pattern | Named Algorithm | Trigger Clue | Complexity |
|:---|:---|:---|:---|
| **DFS** | Depth-First Search | Path, subtree, connectivity, backtracking | O(V+E) / O(h) |
| **BFS** | Breadth-First Search | Level order, shortest path, word ladder | O(V+E) / O(w) |
| **Topological Sort** | Kahn's Algorithm | Dependencies, task scheduling, course order | O(V+E) / O(V) |
| **Union-Find** | DSU (Disjoint Set Union) | Connected components, detect cycle | **O(α(n)) ≈ O(1)** |
| **Shortest Path** | Dijkstra's / Bellman-Ford | Weighted shortest path | O(E log V) |
| **Two Heaps** | — | Median of stream, balance two halves | O(log n) insert |
| **Top-K Elements** | Heap (Priority Queue) | Kth largest/smallest, top K frequent | O(n log k) |

### 🟪 Dynamic Programming Patterns

| Pattern | Named Algorithm | Trigger Clue | Complexity |
|:---|:---|:---|:---|
| **1D DP** | — | Overlapping subproblems, "ways to reach", linear state | O(n) / O(1) |
| **2D DP** | Wagner-Fischer (Edit Distance) | LCS, Edit Distance, grid paths | O(m·n) / O(m·n) |
| **Unbounded Knapsack** | — | Coin Change, "infinite supply", rod cutting | O(n·W) / O(W) |
| **0/1 Knapsack** | — | Pick or skip each item, limited supply | O(n·W) / O(W) |
| **Interval DP** | — | Matrix Chain, Burst Balloons, ranges | O(n³) / O(n²) |
| **Backtracking** | — | All subsets/permutations/combinations | O(2^n) / O(n) |

### 🔤 String Matching Patterns

| Pattern | Named Algorithm | Trigger Clue | Complexity |
|:---|:---|:---|:---|
| **String Matching** | KMP Algorithm | Pattern in text, multiple occurrences | O(n+m) / O(m) |
| **String Hashing** | Rabin-Karp | Multiple pattern search | O(n+m) avg |
| **Trie** | — | Word search, prefix queries, autocomplete | O(n·L) |

---

## 🗓️ 30-Day Day-Wise Plan

### 📅 Week 1 — Arrays (Mar 23–29)
> **Goal:** Stop restarting. Own every array pattern cold.

---

#### Day 1 — Mar 23 | Sorting + Rearrangement
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Sort 0s, 1s, 2s | Two Pointers | **Dutch National Flag** | 3 pointers: lo, mid, hi — partition in one pass | O(n) / O(1) |
| 2 | Next Permutation | Sorting-based | — | Find rightmost dip, swap next greater, reverse suffix | O(n) / O(1) |
| 3 | Pascal's Triangle | Simulation | — | Each element = sum of two above | O(n²) / O(n²) |

#### Day 2 — Mar 24 | Subarray / Carry Forward
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Max Subarray Sum | **Kadane's** | Kadane's Algorithm | Drop subarray when sum goes negative | O(n) / O(1) |
| 2 | Max Product Subarray | Kadane's variant | — | Track both max AND min (negatives flip sign) | O(n) / O(1) |
| 3 | Best Time to Buy & Sell Stock | Carry Forward | — | Track running minimum, update max profit | O(n) / O(1) |

#### Day 3 — Mar 25 | Two Pointers
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Container With Most Water | Two Pointers | — | Move the pointer with smaller height inward | O(n) / O(1) |
| 2 | Trapping Rain Water ⭐ | Two Pointers | — | Water at i = min(maxL, maxR) − height[i] | O(n) / O(1) |
| 3 | 3Sum | Sorting + Two Pointers | — | Fix one element, two-pointer the rest; skip duplicates | O(n²) / O(1) |

#### Day 4 — Mar 26 | Hashing
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Two Sum | Hashing | — | Store complement in map, check existence in one pass | O(n) / O(n) |
| 2 | Longest Consecutive Sequence ⭐ | Hashing | — | Only start counting when (n−1) is NOT in set | O(n) / O(n) |
| 3 | Count Inversions | Divide & Conquer | **Merge Sort** | Count during merge when right element < left | O(n log n) / O(n) |

#### Day 5 — Mar 27 | Matrix
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Set Matrix Zeroes ⭐ | Matrix | — | Use first row/col as marker to avoid extra space | O(m·n) / O(1) |
| 2 | Spiral Matrix | Matrix Traversal | — | Shrink 4 boundaries after each direction pass | O(m·n) / O(1) |
| 3 | Rotate Image | Matrix | — | Transpose → reverse each row | O(n²) / O(1) |

#### Day 6 — Mar 28 | Binary Search
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Search in Rotated Sorted Array ⭐ | Binary Search | — | One half is always sorted — decide which half | O(log n) / O(1) |
| 2 | Find Minimum in Rotated Array | Binary Search | — | Min is the pivot — compare mid with rightmost | O(log n) / O(1) |
| 3 | Koko Eating Bananas | **BS on Answer** | — | Binary search on speed, check feasibility greedily | O(n log m) / O(1) |

#### Day 7 — Mar 29 | Prefix Sum + Revision
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Subarray Sum Equals K ⭐ | Prefix Sum + Hashing | — | prefixSum[j] − prefixSum[i] = k → map lookup | O(n) / O(n) |
| 2 | Product of Array Except Self ⭐ | Prefix + Suffix | — | Left product pass × right product pass, no division | O(n) / O(1) |
| 3 | **Revision** | — | — | Re-solve 2 problems you flagged 🔁 or ❌ from Week 1 | — |

---

### 📅 Week 2 — Strings + Linked List + Stack (Mar 30 – Apr 5)
> **Goal:** See Two Pointers evolve into Fast & Slow. See Stack unlock Monotonic power.

---

#### Day 8 — Mar 30 | Strings: Sliding Window
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Longest Substring Without Repeating ⭐ | Sliding Window | — | Shrink left window when duplicate enters | O(n) / O(1) |
| 2 | Minimum Window Substring ⭐ | Sliding Window | — | Expand right to satisfy, shrink left to minimize | O(n) / O(k) |
| 3 | Group Anagrams | Hashing | — | Sorted string = hashmap key | O(nk log k) / O(n) |

#### Day 9 — Mar 31 | Strings: Advanced
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Longest Palindromic Substring | Expand Around Center | — | Expand from each of 2n−1 centers | O(n²) / O(1) |
| 2 | String to Integer (atoi) | Simulation | — | Handle sign, overflow, non-digit chars explicitly | O(n) / O(1) |
| 3 | Pattern Matching | String Matching | **KMP Algorithm** | Failure function avoids re-matching prefix | O(n+m) / O(m) |

#### Day 10 — Apr 1 | Linked List: Basics
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Reverse Linked List | In-place Reversal | — | 3-pointer trick: prev → curr → next | O(n) / O(1) |
| 2 | Middle of Linked List | Fast & Slow | — | Slow ×1, fast ×2 — when fast ends, slow = mid | O(n) / O(1) |
| 3 | Merge Two Sorted Lists | Two Pointers on LL | — | Compare heads, link smaller, advance that pointer | O(n+m) / O(1) |

#### Day 11 — Apr 2 | Linked List: Cycle
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Detect Cycle ⭐ | Fast & Slow | **Floyd's Cycle Detection** | If they meet → cycle exists | O(n) / O(1) |
| 2 | Find Cycle Start | Fast & Slow | **Floyd's Algorithm** | Reset one to head; move both ×1 → meet at cycle start | O(n) / O(1) |
| 3 | Remove Nth From End | Fast & Slow | — | Advance fast by n first, then move both together | O(n) / O(1) |

#### Day 12 — Apr 3 | Linked List: Hard
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Reverse LL in K Groups ⭐ | In-place Reversal | — | Reverse k nodes, link reversed group to next | O(n) / O(1) |
| 2 | Merge K Sorted Lists ⭐ | Heap | — | Min-heap of size K; always extract minimum head | O(n log k) / O(k) |
| 3 | Palindrome Linked List | Fast & Slow + Reversal | — | Find mid → reverse second half → compare both halves | O(n) / O(1) |

#### Day 13 — Apr 4 | Stack: Basics + Monotonic
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Valid Parentheses | Stack | — | Push open bracket, pop and verify on close | O(n) / O(n) |
| 2 | Next Greater Element I & II ⭐ | Monotonic Stack | — | Maintain decreasing stack; pop when greater is found | O(n) / O(n) |
| 3 | Daily Temperatures | Monotonic Stack | — | Same as NGE but store index difference | O(n) / O(n) |

#### Day 14 — Apr 5 | Stack Hard + LRU
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Largest Rectangle in Histogram ⭐ | Monotonic Stack | — | Increasing stack; area = height × width on each pop | O(n) / O(n) |
| 2 | Sliding Window Maximum ⭐ | Monotonic Deque | — | Deque stores indices; front = max of current window | O(n) / O(k) |
| 3 | LRU Cache ⭐⭐ | HashMap + DLL | — | HashMap for O(1) lookup; DLL for O(1) insert/delete | O(1) all ops |

---

### 📅 Week 3 — Trees + Heap + Greedy (Apr 6–12)
> **Goal:** Make recursion feel natural. Every tree problem is just DFS with a decision.

---

#### Day 15 — Apr 6 | Tree Traversals
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Inorder/Preorder/Postorder (iterative) | DFS | Morris Traversal (opt.) | Use explicit stack to simulate call stack | O(n) / O(h) |
| 2 | Level Order Traversal ⭐ | BFS | — | Queue + level-size trick to separate levels | O(n) / O(w) |
| 3 | Zigzag Level Order | BFS | — | Alternate direction flag per level | O(n) / O(w) |

#### Day 16 — Apr 7 | Tree Properties
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Diameter of Binary Tree ⭐ | DFS | — | At each node: diameter = leftH + rightH; update global | O(n) / O(h) |
| 2 | Balanced Binary Tree | DFS | — | Return −1 upward if unbalanced (shortcut flag) | O(n) / O(h) |
| 3 | Binary Tree Max Path Sum ⭐ | DFS | — | At each node: choose best single path vs both children | O(n) / O(h) |

#### Day 17 — Apr 8 | Tree Hard
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | LCA of Binary Tree ⭐ | DFS | — | If p and q found in both subtrees → node is LCA | O(n) / O(h) |
| 2 | Serialize / Deserialize BT ⭐ | BFS/DFS | — | Encode null nodes explicitly to preserve structure | O(n) / O(n) |
| 3 | Construct BT from Pre+Inorder ⭐ | Divide & Conquer | — | Preorder root splits inorder into left/right | O(n) / O(n) |

#### Day 18 — Apr 9 | BST
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Validate BST ⭐ | DFS with range | — | Pass (min, max) bounds down recursion tree | O(n) / O(h) |
| 2 | Kth Smallest in BST | Inorder DFS | — | Inorder traversal of BST = sorted array | O(n) / O(h) |
| 3 | Sorted Array to BST | Divide & Conquer | — | Mid of array = root; recurse on both halves | O(n) / O(log n) |

#### Day 19 — Apr 10 | Heap
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Top K Frequent Elements ⭐ | Top-K / Heap | — | Min-heap of size K; evict smallest when K exceeded | O(n log k) / O(k) |
| 2 | Kth Largest in Array | Heap / QuickSelect | **QuickSelect (Hoare's)** | Partition like QuickSort — avg O(n) | O(n) avg / O(1) |
| 3 | Median from Data Stream ⭐ | Two Heaps | — | Max-heap (lower half) + min-heap (upper half) balanced | O(log n) insert |

#### Day 20 — Apr 11 | Greedy
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Meeting Rooms II ⭐ | Greedy + Heap | — | Sort by start; min-heap tracks earliest ending meeting | O(n log n) / O(n) |
| 2 | Jump Game I & II | Greedy | — | Track max reachable index; count jumps at boundary | O(n) / O(1) |
| 3 | Non-overlapping Intervals | Greedy | **Activity Selection** | Sort by end time; greedily keep non-overlapping | O(n log n) / O(1) |

#### Day 21 — Apr 12 | Revision
> Re-solve 3 problems tagged 🔁 from Trees/Stack. Verbalize one solution fully out loud as if in a real interview.

---

### 📅 Week 4 — Graphs + Backtracking + DP (Apr 13–21)
> **Goal:** Crack MAANG Round 2 & 3. Graphs + DP are where interviews are won or lost.

---

#### Day 22 — Apr 13 | Graph Basics
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Number of Islands ⭐ | DFS/BFS on Grid | **Flood Fill** | Sink visited land '1' → '0' to avoid extra visited array | O(m·n) / O(m·n) |
| 2 | Detect Cycle Undirected Graph | BFS/DFS | — | BFS: parent tracking; DFS: visited but not parent | O(V+E) / O(V) |
| 3 | Clone a Graph | BFS + Hashing | — | Map old→new node; BFS to replicate neighbor links | O(V+E) / O(V) |

#### Day 23 — Apr 14 | Graph Advanced
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Topological Sort ⭐ | BFS | **Kahn's Algorithm** | Enqueue in-degree 0 nodes; reduce neighbors | O(V+E) / O(V) |
| 2 | Number of Connected Components | Union-Find | **DSU** | Find + Union with path compression & rank | O(α(n)) ≈ O(1) |
| 3 | Pacific Atlantic Water Flow | Multi-source BFS | — | BFS inward from both oceans; find intersection | O(m·n) / O(m·n) |

#### Day 24 — Apr 15 | Backtracking
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Subsets I & II | Backtracking | — | Include/exclude each element; sort to skip duplicates | O(2^n) / O(n) |
| 2 | Permutations ⭐ | Backtracking | — | Swap current with each remaining; recurse; swap back | O(n!) / O(n) |
| 3 | N-Queens ⭐ | Backtracking | — | Track col + diagonal sets; prune invalid placements | O(n!) / O(n) |

#### Day 25 — Apr 16 | DP Foundations
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Climbing Stairs → House Robber → House Robber II | 1D DP | — | Build up: dp[i] = f(dp[i−1], dp[i−2]) family | O(n) / O(1) |
| 2 | Longest Increasing Subsequence ⭐ | 1D DP / BS | **Patience Sort** | BS on tails of active sequences for O(n log n) | O(n log n) / O(n) |
| 3 | 0/1 Knapsack ⭐ | 2D DP | — | dp[i][w] = max(include item i, exclude item i) | O(n·W) / O(W) |

#### Day 26 — Apr 17 | DP Strings
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Longest Common Subsequence ⭐ | 2D DP | — | Match: dp[i][j] = 1 + dp[i−1][j−1]; else take max | O(m·n) / O(m·n) |
| 2 | Edit Distance ⭐ | 2D DP | **Wagner-Fischer** | Min of 3 ops: insert, delete, replace | O(m·n) / O(m·n) |
| 3 | Word Break | 1D DP + Hashing | — | dp[i] = true if any dp[j] true AND s[j..i] in dict | O(n²) / O(n) |

#### Day 27 — Apr 18 | DP Hard
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Coin Change I & II ⭐ | Unbounded Knapsack | — | Coins reusable; inner loop over all denominations | O(n·amt) / O(amt) |
| 2 | Decode Ways | 1D DP | — | Track single digit + two-digit decode paths | O(n) / O(1) |
| 3 | Burst Balloons | Interval DP | — | Think backwards: which balloon burst LAST in range | O(n³) / O(n²) |

#### Day 28 — Apr 19 | Hard + Mixed
| # | Problem | Pattern | Named Algo | Key Insight | Time / Space |
|:---:|:---|:---|:---|:---|:---:|
| 1 | Median of Two Sorted Arrays ⭐ | Binary Search | — | BS on partition of smaller array | O(log(min(m,n))) / O(1) |
| 2 | Split Array Largest Sum | BS on Answer | — | BS on max subarray sum; verify feasibility greedily | O(n log(sum)) / O(1) |
| 3 | Word Search (Grid) | Backtracking + DFS | — | DFS from each cell; mark visited inline, restore after | O(m·n·4^L) / O(L) |

---

#### Day 29 — Apr 20 | 🎯 Full Timed Mock Interview
```
Pick 5 random problems (1 per topic below):
  ✅ 1 Array problem
  ✅ 1 Linked List / Stack problem
  ✅ 1 Tree problem
  ✅ 1 Graph problem
  ✅ 1 DP problem

Rules:
  ⏱ Time limit: 2.5 hours total
  🚫 No hints, no solutions
  🗣 Speak out loud as you solve (simulate real interview)
  📝 Log: Solved ✅ | Needed hint 🔁 | Couldn't do ❌
```

#### Day 30 — Apr 21 | 🔍 Gap Closer
```
  1. Re-solve every ❌ problem from your 30-day log
  2. Tag every unsolved problem with its pattern name
  3. You now have your REAL weak patterns — not assumed ones
  4. These are your Week 5 focus if you continue prep
```

---

## 📊 Plan at a Glance

| Week | Dates | Topics | Problems |
|:---:|:---:|:---|:---:|
| Week 1 | Mar 23–29 | Arrays (Two Pointers, Hashing, BS, Matrix, Prefix Sum) | ~21 |
| Week 2 | Mar 30–Apr 5 | Strings + Linked List + Stack | ~21 |
| Week 3 | Apr 6–12 | Trees + BST + Heap + Greedy | ~21 |
| Week 4 | Apr 13–21 | Graphs + Backtracking + DP + Mock | ~24 |
| **Total** | **30 days** | **All core DSA topics** | **~87** |

---

## 🔑 How to Read Complexity

| Notation | Meaning |
|:---|:---|
| `O(n) / O(1)` | Time / Space |
| `O(h)` | Height of tree — O(log n) balanced, O(n) skewed |
| `O(w)` | Width of tree (max nodes at any level) |
| `O(α(n))` | Inverse Ackermann — amortized nearly O(1) for DSU |
| `O(4^L)` | L = word length, 4 directions in grid backtracking |

---

## 🛠 How to Use the Problem Prompt

For every problem in this sheet, use this prompt template:

```
Problem: [NAME]

Solve in C++ and generate a README with:
1. Problem Analysis (constraints, pattern identification)
2. ASCII visual diagram with step-by-step dry run
3. All approaches (Brute → Better → Optimal) with complexity proof
4. Complexity comparison table
5. Reusable pattern skeleton in C++ with comments
6. 4-5 similar LeetCode problems using same pattern
7. Interview checklist (edge cases)
8. What to say out loud in a Microsoft interview (verbalize script)
```

---

## ⭐ Problem Priority Legend

| Symbol | Meaning |
|:---:|:---|
| ⭐ | High-frequency MAANG interview problem |
| ⭐⭐ | Must-know — asked in almost every company |
| 🔁 | Needed hint — revisit in 3 days |
| ❌ | Couldn't solve — revisit on Day 30 |
| ✅ | Solved independently |

---

<div align="center">

**Built with Striver's SDE Sheet + MAANG Most-Asked Questions**  
*Pattern recognition > memorization. Always.*

</div>
