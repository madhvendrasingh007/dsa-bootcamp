# LeetCode 118 — Pascal's Triangle

---

## 🟢 PART 1 — LEETCODE SUBMISSION (Copy-Paste Ready)

```cpp
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> triangle;
        triangle.push_back({1}); // first row is always [1]

        for (int i = 1; i < numRows; i++) {
            vector<int> row;
            vector<int>& prev = triangle[i - 1]; // reference to previous row

            row.push_back(1); // every row starts with 1

            // each interior element = sum of two elements directly above it
            for (int j = 1; j < i; j++) {
                row.push_back(prev[j - 1] + prev[j]);
            }

            row.push_back(1); // every row ends with 1
            triangle.push_back(row);
        }

        return triangle;
    }
};
```

---
---

# 📄 PART 2 — README

---

## 1. Problem Analysis

- **Input:** `numRows` — integer from `1` to `30`; no array input, purely generative
- **Output:** `vector<vector<int>>` — the full triangle with `numRows` rows
- **What's asked:** Build Pascal's triangle row by row; each inner element = sum of two elements directly above it; all edges are `1`
- **No negatives, no duplicates concern** — all values are positive binomial coefficients `C(n, k)`
- **Brute force in English:** For each row, compute every element using the combinatorial formula `C(n, k) = n! / (k! * (n-k)!)` — requires factorial computation per element
- **Pattern: Dynamic Programming (Tabulation / Row-by-Row Construction)**
  - Why? Each row depends only on the previous row. We build the answer iteratively, storing each completed row, and use it to compute the next — a classic bottom-up DP pattern.

---

## 2. Visual Diagram

**Input:** `numRows = 5`

```
Building row by row:

Row 0:           [1]
Row 1:          [1, 1]
Row 2:         [1, 2, 1]
Row 3:        [1, 3, 3, 1]
Row 4:       [1, 4, 6, 4, 1]

How Row 3 is built from Row 2 = [1, 2, 1]:

prev:  [ 1,   2,   1 ]
         \  / \  /
          \/   \/
          3    3
row:   [ 1,   3,   3,   1 ]
        ^^^             ^^^
       always 1       always 1

Interior element at position j:
  row[j] = prev[j-1] + prev[j]
```

Step-by-step table for `numRows = 5`:

| Row i | prev row         | Interior calc              | New row              |
|-------|------------------|----------------------------|----------------------|
| 0     | —                | —                          | [1]                  |
| 1     | [1]              | (none)                     | [1, 1]               |
| 2     | [1, 1]           | 1+1=2                      | [1, 2, 1]            |
| 3     | [1, 2, 1]        | 1+2=3, 2+1=3               | [1, 3, 3, 1]         |
| 4     | [1, 3, 3, 1]     | 1+3=4, 3+3=6, 3+1=4        | [1, 4, 6, 4, 1]      |

> **💡 Aha Moment:** Each interior element at column `j` in row `i` is exactly `prev[j-1] + prev[j]`. The edges never need computation — they're always `1`. This means the inner loop runs from `j=1` to `j=i-1`, which is exactly `i-1` iterations for row `i`.

---

## 3. All Approaches (Worst → Best)

### Approach 1 — Brute Force (Combinatorial Formula)

**Explanation:** Use the mathematical formula: element at row `n`, column `k` is `C(n,k) = n! / (k! * (n-k)!)`. Compute each element independently using factorial calculation.

- **Time:** O(numRows² × numRows) — for each of the `numRows²/2` elements, factorial computation takes O(n)
- **Space:** O(numRows²) — output storage only; factorial computation is O(1) auxiliary if done iteratively

```cpp
#include <iostream>
#include <vector>
using namespace std;

long long factorial(int n) {
    long long result = 1;
    for (int i = 2; i <= n; i++) result *= i;
    return result;
}

long long combination(int n, int k) {
    // C(n, k) = n! / (k! * (n-k)!)
    return factorial(n) / (factorial(k) * factorial(n - k));
}

class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> triangle;

        for (int i = 0; i < numRows; i++) {
            vector<int> row;
            for (int j = 0; j <= i; j++) {
                row.push_back((int)combination(i, j)); // C(i, j) for each element
            }
            triangle.push_back(row);
        }

        return triangle;
    }
};

int main() {
    Solution sol;

    auto result = sol.generate(5);
    // Expected: [1] [1,1] [1,2,1] [1,3,3,1] [1,4,6,4,1]
    for (auto& row : result) {
        for (int x : row) cout << x << " ";
        cout << "\n";
    }

    return 0;
}
```

**Bottleneck:** Factorial overflow risk for large n; redundant recomputation of factorials for every element — completely ignores the additive structure of Pascal's triangle.

---

### Approach 2 — Better (Optimized Combinatorial — Multiplicative Formula)

**Optimization:** Use the recurrence `C(n, k) = C(n, k-1) * (n-k+1) / k` to compute each element in O(1) from the previous one in the same row, avoiding repeated factorial calls.

- **Time:** O(numRows²) — each row element computed in O(1) from the previous
- **Space:** O(numRows²) — output only

```cpp
#include <iostream>
#include <vector>
using namespace std;

class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> triangle;

        for (int i = 0; i < numRows; i++) {
            vector<int> row(i + 1);
            row[0] = row[i] = 1; // edges are always 1

            long long val = 1;
            for (int j = 1; j < i; j++) {
                // C(i,j) = C(i, j-1) * (i - j + 1) / j
                val = val * (i - j + 1) / j;
                row[j] = (int)val;
            }
            triangle.push_back(row);
        }

        return triangle;
    }
};

int main() {
    Solution sol;

    auto result = sol.generate(6);
    // Expected: [1] [1,1] [1,2,1] [1,3,3,1] [1,4,6,4,1] [1,5,10,10,5,1]
    for (auto& row : result) {
        for (int x : row) cout << x << " ";
        cout << "\n";
    }

    return 0;
}
```

**Limitation:** Integer division must happen in exact order (numerator divisible by denominator) — subtle edge case. The DP approach below is simpler, equally fast, and more intuitive.

---

### Approach 3 — Optimal (Bottom-Up DP — Row Construction)

**Key Insight:** Each row is completely determined by the previous row using a simple addition rule. Build iteratively, carry only the previous row at any time.

- **Time:** O(numRows²) — row `i` has `i+1` elements; total = 1+2+...+numRows = numRows*(numRows+1)/2
- **Space:** O(numRows²) — output itself; O(1) auxiliary space (only prev row reference)

```cpp
#include <iostream>
#include <vector>
using namespace std;

class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> triangle;
        triangle.push_back({1}); // row 0 is always [1]

        for (int i = 1; i < numRows; i++) {
            vector<int> row;
            vector<int>& prev = triangle[i - 1]; // reference to previous row (no copy)

            row.push_back(1); // left edge always 1

            // interior elements: sum of two elements directly above
            for (int j = 1; j < i; j++) {
                row.push_back(prev[j - 1] + prev[j]);
            }

            row.push_back(1); // right edge always 1
            triangle.push_back(row);
        }

        return triangle;
    }
};

int main() {
    Solution sol;

    // Test 1: numRows = 5
    cout << "numRows = 5:\n";
    auto r1 = sol.generate(5);
    for (auto& row : r1) {
        for (int x : row) cout << x << " ";
        cout << "\n";
    }
    // Expected:
    // 1
    // 1 1
    // 1 2 1
    // 1 3 3 1
    // 1 4 6 4 1

    // Test 2: numRows = 1 (single row)
    cout << "\nnumRows = 1:\n";
    auto r2 = sol.generate(1);
    for (auto& row : r2) {
        for (int x : row) cout << x << " ";
        cout << "\n";
    }
    // Expected: 1

    // Test 3: numRows = 2
    cout << "\nnumRows = 2:\n";
    auto r3 = sol.generate(2);
    for (auto& row : r3) {
        for (int x : row) cout << x << " ";
        cout << "\n";
    }
    // Expected: 1 / 1 1

    // Test 4: numRows = 6 (verify 5th row = [1,5,10,10,5,1])
    cout << "\nnumRows = 6:\n";
    auto r4 = sol.generate(6);
    for (auto& row : r4) {
        for (int x : row) cout << x << " ";
        cout << "\n";
    }

    // Test 5: Max constraint numRows = 30
    cout << "\nnumRows = 30, last row first 3 elements: ";
    auto r5 = sol.generate(30);
    cout << r5[29][0] << " " << r5[29][1] << " " << r5[29][2] << " ...\n";
    // Expected: 1 29 406 ...

    return 0;
}
```

> ⚠️ NOTE: Code in Section 3 includes `main()` and `#include` for local testing.
> For LeetCode submission, use the clean `class Solution {}` block from **PART 1** above.

---

## 4. Complexity Comparison

| Approach | Time | Space | Trade-off |
|----------|------|-------|-----------|
| Brute Force (Factorials) | O(numRows³) | O(numRows²) | Simple math but factorial overflow and redundant work |
| Optimized Combinatorial | O(numRows²) | O(numRows²) | Avoids factorial but integer division order is tricky |
| Bottom-Up DP (Optimal) | O(numRows²) | O(numRows²) | Cleanest, most intuitive, no overflow risk |

> Note: O(numRows²) space is unavoidable — we must return the entire triangle as output.

---

## 5. The Pattern Template (Reusable — Bottom-Up DP / Row Construction)

```cpp
// Bottom-Up DP: Build 2D result row-by-row
// Use when: each row depends only on the previous row, with boundary conditions

vector<vector<int>> buildRowByRow(int n) {
    vector<vector<int>> result;

    // 🔧 Define and push the base case (row 0)
    result.push_back({ /* base row */ });

    for (int i = 1; i < n; i++) {
        vector<int> row;
        vector<int>& prev = result[i - 1]; // reference previous row

        // 🔧 Left boundary condition
        row.push_back(/* left edge value */);

        // 🔧 Interior elements — computed from prev row
        for (int j = 1; j < i; j++) {
            row.push_back(/* transition: prev[j-1] op prev[j] */);
        }

        // 🔧 Right boundary condition
        row.push_back(/* right edge value */);

        result.push_back(row);
    }

    return result;
}
```

---

## 6. Similar Problems (Pattern Family)

| # | Problem | What's Similar | What's Different |
|---|---------|----------------|-----------------|
| [119](https://leetcode.com/problems/pascals-triangle-ii/) | Pascal's Triangle II | Same triangle structure and row-building logic | Return only the k-th row using O(k) space |
| [120](https://leetcode.com/problems/triangle/) | Triangle | 2D triangle DP, each row depends on prev | Minimize path sum from top to bottom |
| [338](https://leetcode.com/problems/counting-bits/) | Counting Bits | Build array where each value uses a previous result | 1D DP, not 2D; count set bits using recurrence |
| [746](https://leetcode.com/problems/min-cost-climbing-stairs/) | Min Cost Climbing Stairs | Each state built from previous states | 1D DP on costs, not a triangle |
| [1137](https://leetcode.com/problems/n-th-tribonacci-number/) | N-th Tribonacci Number | Row-by-row (step-by-step) construction from prior values | Single value output, not full triangle |

---

## 7. Interview Checklist

Before submitting in a Microsoft/FAANG interview, verify:

- [x] `numRows = 1` — only `[[1]]` returned; inner loop doesn't execute
- [x] `numRows = 2` — `[[1],[1,1]]`; second row has no interior elements (loop `j=1` to `j<1` → skipped)
- [x] Interior loop bounds correct — `j` from `1` to `i-1` (not `0` to `i`), otherwise edges are double-pushed
- [x] Using `vector<int>&` reference for `prev` — avoids unnecessary copy of previous row
- [x] No integer overflow — numRows ≤ 30; C(30,15) = 155,117,520 fits safely in `int`
- [x] No out-of-bounds — `prev[j-1]` and `prev[j]` both valid since `j` ranges `1..i-1` and `prev.size() = i`
- [x] Correct return type — `vector<vector<int>>`
- [x] Output includes ALL rows from row 0 to row numRows-1 (not 1-indexed)

---

## 8. My Thought Process (Interview Script)

"So I need to generate Pascal's triangle for a given number of rows. Each element is the sum of the two directly above it, and every edge is 1.

My first instinct is the combinatorial formula — C(n, k) — since that's the mathematical definition. But computing factorials repeatedly is wasteful and risks overflow for larger values.

I notice that each row is entirely derivable from the previous row with a simple addition. That's a classic bottom-up DP signal — I don't need to go back further than one step.

So my plan: start with `[1]`, then for each new row, push `1`, compute interior elements as `prev[j-1] + prev[j]`, then push `1` again. The inner loop only runs for interior positions — rows 0 and 1 have no interior elements at all, which is naturally handled by the loop bounds.

Time is O(n²) because the total number of elements across all rows is n*(n+1)/2. Space is also O(n²) — unavoidable since we're returning the full triangle. This is as good as it gets."

---

*Generated for LeetCode 118 — Pascal's Triangle | Pattern: Bottom-Up Dynamic Programming / Row Construction*
