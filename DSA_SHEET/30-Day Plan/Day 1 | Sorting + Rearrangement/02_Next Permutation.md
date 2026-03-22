# LeetCode 31 — Next Permutation

---

## 🟢 PART 1 — LEETCODE SUBMISSION (Copy-Paste Ready)

```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int n = nums.size();
        int pivot = -1;

        // Step 1: Find rightmost index where nums[i] < nums[i+1] (the "dip")
        for (int i = n - 2; i >= 0; i--) {
            if (nums[i] < nums[i + 1]) {
                pivot = i;
                break;
            }
        }

        // Step 2: If pivot exists, find rightmost element > nums[pivot] and swap
        if (pivot != -1) {
            for (int j = n - 1; j > pivot; j--) {
                if (nums[j] > nums[pivot]) {
                    swap(nums[pivot], nums[j]); // smallest possible upgrade at pivot
                    break;
                }
            }
        }

        // Step 3: Reverse everything after pivot to get smallest suffix
        // (suffix is guaranteed descending after the swap)
        reverse(nums.begin() + pivot + 1, nums.end());
    }
};
```

---
---

# 📄 PART 2 — README

---

## 1. Problem Analysis

- **Array size:** `1 ≤ n ≤ 100`; values in `[0, 100]` — no negatives, duplicates allowed, not necessarily sorted
- **What's asked:** Rearrange the array **in-place** into its lexicographically next greater permutation; if it is already the largest (fully descending), wrap around to the smallest (fully ascending)
- **Brute force in English:** Generate all permutations of the array, sort them lexicographically, find the current one, return the next — or wrap to the first if at the end
- **Pattern: Two Pointers + Greedy (Suffix Reversal)**
  - Why? We want the *smallest* increase possible. The key insight is: the suffix that is **strictly descending** from the right is already "maximally used" — we need to find the first element that *breaks* that descent (the pivot), make the smallest possible swap there, then reset the suffix to ascending order by reversing it.

---

## 2. Visual Diagram

**Input:** `nums = [1, 3, 5, 4, 2]`

```
All permutations in order around our input:
... → [1,3,4,5,2] → [1,3,5,2,4] → [1,3,5,4,2] → [1,3,5,4,2]→NEXT→[1,4,2,3,5] ...
                                         ^^ we are here

Step 1: Find pivot — scan right-to-left for first nums[i] < nums[i+1]

Index:   0    1    2    3    4
Value:  [1,   3,   5,   4,   2]
                   ^    ↓    ↓
              suffix [5,4,2] is descending — fully used
              nums[1]=3 < nums[2]=5  →  pivot = 1? NO
              Wait: scan from right:
                i=3: nums[3]=4 > nums[4]=2 → skip
                i=2: nums[2]=5 > nums[3]=4 → skip
                i=1: nums[1]=3 < nums[2]=5 → PIVOT FOUND at i=1 ✅

Step 2: Find rightmost element > nums[pivot=1]=3 from the right

Index:   0    1    2    3    4
Value:  [1,   3,   5,   4,   2]
              ^              ← scan right-to-left
        j=4: nums[4]=2 > 3? NO
        j=3: nums[3]=4 > 3? YES → swap(pivot, j=3) ✅

After swap:
        [1,   4,   5,   3,   2]
              ^    ↑---------↑ this suffix is still descending

Step 3: Reverse suffix after pivot (index 2 to 4)

Before: [1,   4,   5,   3,   2]
After:  [1,   4,   2,   3,   5]  ✅ ANSWER
```

| Step | pivot | j  | Action              | Array State         |
|------|-------|----|---------------------|---------------------|
| 1    | 1     | —  | Find dip at idx 1   | [1, 3, 5, 4, 2]     |
| 2    | 1     | 3  | swap(idx1, idx3)    | [1, 4, 5, 3, 2]     |
| 3    | 1     | —  | reverse(idx2..end)  | [1, 4, 2, 3, 5] ✅  |

> **💡 Aha Moment:** The suffix to the right of the pivot is *always descending* after the swap. Reversing a descending array gives the smallest ascending arrangement — that's why `reverse` gives us the *next* permutation, not some arbitrary one.

---

## 3. All Approaches (Worst → Best)

### Approach 1 — Brute Force (Generate All Permutations)

**Explanation:** Generate every permutation of the array, sort them lexicographically, find the current permutation's position, and return the next one. If it's last, return the first.

- **Time:** O(n! × n) — there are n! permutations, each comparison is O(n)
- **Space:** O(n! × n) — storing all permutations

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        vector<int> sorted_nums = nums;
        sort(sorted_nums.begin(), sorted_nums.end()); // start from smallest permutation

        vector<vector<int>> all_perms;
        // Generate all permutations
        do {
            all_perms.push_back(sorted_nums);
        } while (next_permutation(sorted_nums.begin(), sorted_nums.end()));

        // Find current permutation and return the next
        for (int i = 0; i < (int)all_perms.size(); i++) {
            if (all_perms[i] == nums) {
                // wrap around if last permutation
                nums = all_perms[(i + 1) % all_perms.size()];
                return;
            }
        }
    }
};

int main() {
    Solution sol;

    vector<int> nums1 = {1, 2, 3};
    sol.nextPermutation(nums1);
    // Expected: 1 3 2
    for (int x : nums1) cout << x << " "; cout << "\n";

    vector<int> nums2 = {3, 2, 1};
    sol.nextPermutation(nums2);
    // Expected: 1 2 3 (wrap around)
    for (int x : nums2) cout << x << " "; cout << "\n";

    return 0;
}
```

**Bottleneck:** Completely infeasible for large n — 10! = 3,628,800 permutations. We're throwing away all structural insight.

---

### Approach 2 — Better (Using STL `next_permutation`)

**Optimization:** C++ STL already implements next_permutation internally using the same 3-step algorithm. Calling it directly is O(n) time — but it's cheating the interview intent.

- **Time:** O(n) — internally does the same pivot+swap+reverse logic
- **Space:** O(1)

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        // STL next_permutation returns false if it wraps to smallest permutation
        next_permutation(nums.begin(), nums.end());
    }
};

int main() {
    Solution sol;

    vector<int> nums1 = {1, 3, 5, 4, 2};
    sol.nextPermutation(nums1);
    // Expected: 1 4 2 3 5
    for (int x : nums1) cout << x << " "; cout << "\n";

    vector<int> nums2 = {3, 2, 1};
    sol.nextPermutation(nums2);
    // Expected: 1 2 3
    for (int x : nums2) cout << x << " "; cout << "\n";

    return 0;
}
```

**Limitation:** Interviews expect you to implement this from scratch. Using STL `next_permutation` signals you don't understand the underlying algorithm.

---

### Approach 3 — Optimal (Pivot + Swap + Reverse — 3-Step Algorithm)

**Key Insight:** The rightmost descending suffix is "maxed out." Find the element just before it (pivot), swap it with the smallest element in the suffix that's still greater than it, then reverse the suffix to reset it to ascending (minimum) order.

- **Time:** O(n) — three linear scans at most (find pivot + find swap + reverse)
- **Space:** O(1) — pure in-place, no extra storage

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int n = nums.size();
        int pivot = -1;

        // Step 1: Find rightmost i where nums[i] < nums[i+1]
        // Everything to the right of pivot is descending (already maximal)
        for (int i = n - 2; i >= 0; i--) {
            if (nums[i] < nums[i + 1]) {
                pivot = i;
                break;
            }
        }

        // Step 2: If pivot found, swap it with rightmost element greater than it
        // Scanning from right ensures we pick the SMALLEST such element
        if (pivot != -1) {
            for (int j = n - 1; j > pivot; j--) {
                if (nums[j] > nums[pivot]) {
                    swap(nums[pivot], nums[j]);
                    break;
                }
            }
        }

        // Step 3: Reverse the suffix after pivot
        // Suffix is descending (after swap), reversing makes it ascending (minimum)
        // If pivot == -1 (entire array descending), this reverses the whole array
        reverse(nums.begin() + pivot + 1, nums.end());
    }
};

int main() {
    Solution sol;

    // Test 1: General case
    vector<int> nums1 = {1, 3, 5, 4, 2};
    sol.nextPermutation(nums1);
    // Expected: 1 4 2 3 5
    for (int x : nums1) cout << x << " "; cout << "\n";

    // Test 2: Last permutation — wrap to first
    vector<int> nums2 = {3, 2, 1};
    sol.nextPermutation(nums2);
    // Expected: 1 2 3
    for (int x : nums2) cout << x << " "; cout << "\n";

    // Test 3: Simple ascending
    vector<int> nums3 = {1, 2, 3};
    sol.nextPermutation(nums3);
    // Expected: 1 3 2
    for (int x : nums3) cout << x << " "; cout << "\n";

    // Test 4: Duplicates
    vector<int> nums4 = {1, 1, 5};
    sol.nextPermutation(nums4);
    // Expected: 1 5 1
    for (int x : nums4) cout << x << " "; cout << "\n";

    // Test 5: Single element
    vector<int> nums5 = {1};
    sol.nextPermutation(nums5);
    // Expected: 1 (no change)
    for (int x : nums5) cout << x << " "; cout << "\n";

    // Test 6: Two elements
    vector<int> nums6 = {1, 2};
    sol.nextPermutation(nums6);
    // Expected: 2 1
    for (int x : nums6) cout << x << " "; cout << "\n";

    // Test 7: All same elements
    vector<int> nums7 = {2, 2, 2};
    sol.nextPermutation(nums7);
    // Expected: 2 2 2 (no next permutation)
    for (int x : nums7) cout << x << " "; cout << "\n";

    return 0;
}
```

> ⚠️ NOTE: Code in Section 3 includes `main()` and `#include` for local testing.  
> For LeetCode submission, use the clean `class Solution {}` block from **PART 1** above.

---

## 4. Complexity Comparison

| Approach | Time | Space | Trade-off |
|----------|------|-------|-----------|
| Brute Force (Generate All) | O(n! × n) | O(n! × n) | Correct but completely infeasible for n > 8 |
| STL `next_permutation` | O(n) | O(1) | Optimal speed, but not acceptable in interviews |
| Pivot + Swap + Reverse (Optimal) | O(n) | O(1) | Best — implements the exact insight interviewers want |

---

## 5. The Pattern Template (Reusable — Suffix Manipulation)

```cpp
// Next Permutation / Suffix Greedy Template
// Use when: find next lexicographic arrangement of elements in-place

void nextPermutationTemplate(vector<int>& arr) {
    int n = arr.size();
    int pivot = -1;

    // Step 1: Find rightmost "dip" — first element from right that can be increased
    for (int i = n - 2; i >= 0; i--) {
        if (arr[i] < arr[i + 1]) { // 🔧 customize comparison for your ordering
            pivot = i;
            break;
        }
    }

    // Step 2: Find the best candidate to swap with pivot
    if (pivot != -1) {
        for (int j = n - 1; j > pivot; j--) {
            if (arr[j] > arr[pivot]) { // 🔧 customize: smallest value > pivot element
                swap(arr[pivot], arr[j]);
                break;
            }
        }
    }

    // Step 3: Reset the suffix to its minimum arrangement
    reverse(arr.begin() + pivot + 1, arr.end()); // 🔧 always reverse to get minimum suffix
    // Note: if pivot == -1, this reverses the entire array (wrap-around case)
}
```

---

## 6. Similar Problems (Pattern Family)

| # | Problem | What's Similar | What's Different |
|---|---------|----------------|-----------------|
| [46](https://leetcode.com/problems/permutations/) | Permutations | Generate all permutations of an array | Returns all permutations, not just the next one |
| [47](https://leetcode.com/problems/permutations-ii/) | Permutations II | Permutations with duplicates | Handle repeated elements, return all unique |
| [60](https://leetcode.com/problems/permutation-sequence/) | Permutation Sequence | k-th permutation in lexicographic order | Find kth directly using factorial math, not step-by-step |
| [556](https://leetcode.com/problems/next-greater-element-iii/) | Next Greater Element III | Same exact 3-step algorithm on digits of a number | Input is an integer, must handle 32-bit overflow |
| [1850](https://leetcode.com/problems/minimum-adjacent-swaps-to-reach-the-kth-smallest-number/) | Min Swaps to Kth Smallest | Uses next permutation repeatedly k times | Count adjacent swaps to reach result |

---

## 7. Interview Checklist

Before submitting in a Microsoft/FAANG interview, verify:

- [x] Handles single element — `pivot` stays -1, `reverse` on entire array is a no-op for size 1
- [x] Handles fully descending array (last permutation) — `pivot = -1`, entire array gets reversed → first permutation
- [x] Handles fully ascending array — `pivot = n-2`, swap last two elements
- [x] Handles all same elements — `pivot = -1` (no `nums[i] < nums[i+1]` found), reverse is a no-op
- [x] Handles duplicates correctly — scanning from right for swap finds the *rightmost* valid candidate, not a duplicate
- [x] Does NOT skip `reverse` when pivot is -1 — `reverse(begin + 0, end)` handles wrap-around
- [x] No out-of-bounds — loop starts at `n-2`, `pivot+1` is valid even when `pivot = -1` (index 0)
- [x] Correct return type — `void`, modifies in-place
- [x] No integer overflow — only index arithmetic

---

## 8. My Thought Process (Interview Script)

"So I need to find the next lexicographically greater permutation — basically, the next arrangement if I listed all permutations in sorted order.

I notice that brute-forcing all permutations is factorial time which obviously won't work. Let me think about what 'next' means structurally.

My instinct is: I want to change as little as possible, as far to the right as possible. The rightmost chunk of the array that's descending is already 'maxed out' — there's no next permutation for that suffix. So I need to find the element just before that suffix — the pivot — and bump it up slightly.

The smallest bump I can make is to swap the pivot with the smallest element in the suffix that's still greater than it. Since the suffix is descending, scanning from the right gives me exactly that.

After the swap, the suffix is still descending — and I want the *minimum* arrangement for it, which is ascending. Reversing a descending array gives ascending — so I just reverse the suffix.

Three steps: find pivot, swap with successor, reverse suffix. O(n) time, O(1) space. Let me code it."

---

*Generated for LeetCode 31 — Next Permutation | Pattern: Greedy Suffix Manipulation / Two Pointers*
