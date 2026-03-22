# LeetCode 75 — Sort Colors (Dutch National Flag Problem)

---

## 🟢 PART 1 — LEETCODE SUBMISSION (Copy-Paste Ready)

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int low = 0;               // boundary: everything before low is 0
        int mid = 0;               // current element under examination
        int high = nums.size() - 1; // boundary: everything after high is 2

        while (mid <= high) {
            if (nums[mid] == 0) {
                swap(nums[low], nums[mid]); // send 0 to the left zone
                low++;                      // expand 0-zone rightward
                mid++;                      // element at old low was 1 (safe to advance)
            } else if (nums[mid] == 2) {
                swap(nums[mid], nums[high]); // send 2 to the right zone
                high--;                      // shrink unknown zone from right
                // do NOT increment mid — newly swapped element is unexamined
            } else {
                mid++; // nums[mid] == 1, already in correct zone
            }
        }
    }
};
```

---

## 📄 PART 2 — README

---

## 1. Problem Analysis

- **Array size:** `1 ≤ n ≤ 300`; values are only `{0, 1, 2}` — no negatives, duplicates allowed, not pre-sorted
- **What's asked:** Sort the array **in-place** in a single pass so all 0s come before all 1s which come before all 2s; cannot use `std::sort`
- **Brute force in English:** Count how many 0s, 1s, and 2s exist, then overwrite the array from the front — simple two-pass counting sort
- **Pattern: Three Pointers — Dutch National Flag**
  - Why? We have exactly 3 distinct values to partition. Two pointers collapse the unsorted region from both ends while a third walks forward, achieving a **single O(n) pass with O(1) space**.

---

## 2. Visual Diagram

**Input:** `nums = [2, 0, 2, 1, 1, 0]`

```
Invariant at all times:
  [0...low-1]  = all 0s
  [low...mid-1] = all 1s
  [mid...high] = unknown
  [high+1...n-1] = all 2s

Initial state:
Index:  0    1    2    3    4    5
Value: [2,   0,   2,   1,   1,   0]
        ^L               ^H
        ^M

Step 1: nums[mid]=2 → swap(mid=0, high=5), high--
       [0,   0,   2,   1,   1,   2]
        ^L              ^H
        ^M

Step 2: nums[mid]=0 → swap(low=0, mid=0), low++, mid++
       [0,   0,   2,   1,   1,   2]
             ^L         ^H
             ^M

Step 3: nums[mid]=0 → swap(low=1, mid=1), low++, mid++
       [0,   0,   2,   1,   1,   2]
                  ^L    ^H
                  ^M

Step 4: nums[mid]=2 → swap(mid=2, high=4), high--
       [0,   0,   1,   1,   2,   2]
                  ^L  ^H
                  ^M

Step 5: nums[mid]=1 → mid++
       [0,   0,   1,   1,   2,   2]
                  ^L ^H
                       ^M

Step 6: mid > high → STOP ✅
Result: [0, 0, 1, 1, 2, 2]
```

| Step | low | mid | high | nums[mid] | Action |
|------|-----|-----|------|-----------|--------|
| 1    | 0   | 0   | 5    | 2         | swap(mid,high), high-- |
| 2    | 0   | 0   | 4    | 0         | swap(low,mid), low++, mid++ |
| 3    | 1   | 1   | 4    | 0         | swap(low,mid), low++, mid++ |
| 4    | 2   | 2   | 4    | 2         | swap(mid,high), high-- |
| 5    | 2   | 2   | 3    | 1         | mid++ |
| 6    | 2   | 3   | 3    | 1         | mid++ |
| Done | 2   | 4   | 3    | —         | mid > high, exit |

> **💡 Aha Moment:** When `nums[mid] == 2`, we do NOT advance `mid` after swapping — the element that just arrived at `mid` from the right is still unexamined!

---

## 3. All Approaches (Worst → Best)

### Approach 1 — Brute Force (std::sort)

**Explanation:** Simply call the library sort. It uses introsort (quicksort + heapsort hybrid) internally — works but ignores the constraint that values are only 0/1/2.

- **Time:** O(n log n) — general-purpose sort doesn't exploit the limited value range
- **Space:** O(log n) — recursion stack from introsort

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    void sortColors(vector<int>& nums) {
        sort(nums.begin(), nums.end()); // ignores the 0/1/2 constraint
    }
};

int main() {
    Solution sol;
    vector<int> nums1 = {2, 0, 2, 1, 1, 0};
    sol.sortColors(nums1);
    // Output: 0 0 1 1 2 2
    for (int x : nums1) cout << x << " ";
    cout << endl;

    vector<int> nums2 = {2, 0, 1};
    sol.sortColors(nums2);
    // Output: 0 1 2
    for (int x : nums2) cout << x << " ";
    cout << endl;

    return 0;
}
```

**Bottleneck:** O(n log n) is unnecessary when values are bounded to {0,1,2}. LeetCode problem explicitly discourages using built-in sort.

---

### Approach 2 — Better (Counting Sort / Two-Pass)

**Optimization:** Since values are only 0, 1, 2 — count each, then overwrite. Two passes, but O(n) time.

- **Time:** O(n) — one pass to count + one pass to fill = 2n ≈ O(n)
- **Space:** O(1) — only 3 counters needed

```cpp
#include <iostream>
#include <vector>
using namespace std;

class Solution {
public:
    void sortColors(vector<int>& nums) {
        int count0 = 0, count1 = 0, count2 = 0;

        // Pass 1: count occurrences
        for (int x : nums) {
            if (x == 0) count0++;
            else if (x == 1) count1++;
            else count2++;
        }

        int i = 0;
        // Pass 2: overwrite array in order
        while (count0--) nums[i++] = 0; // fill 0s
        while (count1--) nums[i++] = 1; // fill 1s
        while (count2--) nums[i++] = 2; // fill 2s
    }
};

int main() {
    Solution sol;

    vector<int> nums1 = {2, 0, 2, 1, 1, 0};
    sol.sortColors(nums1);
    // Output: 0 0 1 1 2 2
    for (int x : nums1) cout << x << " ";
    cout << endl;

    vector<int> nums2 = {0};
    sol.sortColors(nums2);
    // Output: 0
    for (int x : nums2) cout << x << " ";
    cout << endl;

    vector<int> nums3 = {1, 1, 1};
    sol.sortColors(nums3);
    // Output: 1 1 1
    for (int x : nums3) cout << x << " ";
    cout << endl;

    return 0;
}
```

**Limitation:** Requires two passes over the array. The follow-up challenge asks: can you do it in **one pass**?

---

### Approach 3 — Optimal (Dutch National Flag — One Pass, Three Pointers)

**Key Insight:** Maintain three regions simultaneously — [0s | 1s | unknown | 2s] — and shrink the unknown region one step at a time using three pointers.

- **Time:** O(n) — each element is visited at most twice (once by mid, once by a swap)
- **Space:** O(1) — three integer pointers only

```cpp
#include <iostream>
#include <vector>
using namespace std;

class Solution {
public:
    void sortColors(vector<int>& nums) {
        int low = 0;                    // next position for 0
        int mid = 0;                    // current pointer
        int high = nums.size() - 1;     // next position for 2

        while (mid <= high) {
            if (nums[mid] == 0) {
                swap(nums[low], nums[mid]); // place 0 in its region
                low++;
                mid++;
            } else if (nums[mid] == 2) {
                swap(nums[mid], nums[high]); // place 2 in its region
                high--;
                // mid stays — swapped-in element is unexamined
            } else {
                mid++; // 1 is already in the right place
            }
        }
    }
};

int main() {
    Solution sol;

    // Test 1: General case
    vector<int> nums1 = {2, 0, 2, 1, 1, 0};
    sol.sortColors(nums1);
    // Expected: 0 0 1 1 2 2
    for (int x : nums1) cout << x << " "; cout << "\n";

    // Test 2: Already sorted
    vector<int> nums2 = {0, 1, 2};
    sol.sortColors(nums2);
    // Expected: 0 1 2
    for (int x : nums2) cout << x << " "; cout << "\n";

    // Test 3: All same
    vector<int> nums3 = {1, 1, 1};
    sol.sortColors(nums3);
    // Expected: 1 1 1
    for (int x : nums3) cout << x << " "; cout << "\n";

    // Test 4: Single element
    vector<int> nums4 = {2};
    sol.sortColors(nums4);
    // Expected: 2
    for (int x : nums4) cout << x << " "; cout << "\n";

    // Test 5: Reverse sorted
    vector<int> nums5 = {2, 2, 1, 1, 0, 0};
    sol.sortColors(nums5);
    // Expected: 0 0 1 1 2 2
    for (int x : nums5) cout << x << " "; cout << "\n";

    // Test 6: All zeros
    vector<int> nums6 = {0, 0, 0};
    sol.sortColors(nums6);
    // Expected: 0 0 0
    for (int x : nums6) cout << x << " "; cout << "\n";

    return 0;
}
```

> ⚠️ NOTE: The code in Section 3 includes `main()` and `#include` for local testing.  
> For LeetCode submission, use the clean `class Solution {}` block from **PART 1** above.

---

## 4. Complexity Comparison

| Approach | Time | Space | Trade-off |
|----------|------|-------|-----------|
| Brute Force (`std::sort`) | O(n log n) | O(log n) | Simple but ignores value constraint |
| Counting Sort (Two-Pass) | O(n) | O(1) | Fast but needs 2 passes over array |
| Dutch National Flag (Optimal) | O(n) | O(1) | Single pass, in-place, truly optimal |

---

## 5. The Pattern Template (Reusable — Three Pointers / DNF)

```cpp
// Dutch National Flag / Three-Region Partition Template
// Use when: array has exactly 3 distinct values to partition in-place

void threeWayPartition(vector<int>& arr, int pivot) {
    int low = 0;
    int mid = 0;
    int high = arr.size() - 1;

    while (mid <= high) {
        if (arr[mid] < pivot) {
            swap(arr[low], arr[mid]);
            low++;
            mid++;
            // 🔧 customize: what "less than pivot" means for your problem
        } else if (arr[mid] > pivot) {
            swap(arr[mid], arr[high]);
            high--;
            // 🔧 customize: what "greater than pivot" means for your problem
            // NOTE: do NOT increment mid here
        } else {
            mid++;
            // 🔧 customize: what "equal to pivot" means for your problem
        }
    }
}

// Invariant maintained:
// arr[0..low-1]  < pivot
// arr[low..mid-1] == pivot
// arr[mid..high]  = unknown
// arr[high+1..n-1] > pivot
```

---

## 6. Similar Problems (Pattern Family)

| # | Problem | What's Similar | What's Different |
|---|---------|-----------------|------------------|
| [905](https://leetcode.com/problems/sort-array-by-parity/) | Sort Array By Parity | Two-region in-place partition with two pointers | Only 2 groups (even/odd), not 3 |
| [283](https://leetcode.com/problems/move-zeroes/) | Move Zeroes | In-place rearrangement, O(n) time O(1) space | Two groups, zeros to back, order preserved |
| [922](https://leetcode.com/problems/sort-array-by-parity-ii/) | Sort Array By Parity II | Two-pointer in-place partition | Even indices must hold even, odd indices odd |
| [215](https://leetcode.com/problems/kth-largest-element-in-an-array/) | Kth Largest Element | QuickSelect uses same 3-way partition | Finding kth element, not full sort |
| [912](https://leetcode.com/problems/sort-an-array/) | Sort an Array | General array sort | No value constraint; must implement full sort |

---

## 7. Interview Checklist

Before submitting in a Microsoft/FAANG interview, verify:

- [x] Handles empty array — `while (mid <= high)` exits immediately if size is 0
- [x] Handles single element — loop runs once and terminates correctly
- [x] Handles all same elements — e.g., all 1s: `mid` walks forward, no swaps needed
- [x] Handles all 0s — `low` and `mid` both advance together safely
- [x] Handles all 2s — `high` decrements until `high < mid`, loop exits
- [x] Correct return type — `void`, array modified in-place as required
- [x] No out-of-bounds access — `mid <= high` guard prevents any overflow
- [x] No integer overflow — only indices and swaps, no arithmetic on values
- [x] Does NOT increment `mid` after swapping with `high` — most common bug!
- [x] Works on already-sorted input without extra swaps

---

## 8. My Thought Process (Interview Script)

> Speak this out loud during a real interview:

"So I see we have an array with only three possible values — 0, 1, and 2 — and we need to sort it in-place.

My first instinct is counting sort: count each value, overwrite. That's O(n) time and O(1) space — pretty good. But I notice the follow-up says can we do it in one pass, which tells me there's a smarter approach hiding here.

I notice this is essentially a three-way partition problem — famously solved by Dijkstra's Dutch National Flag algorithm. The idea is to maintain three regions: confirmed 0s on the left, confirmed 2s on the right, and an unknown window in the middle. We shrink that window with three pointers.

The tricky part is: when we swap a 2 to the right, we don't advance `mid` — because what came back from the right hasn't been examined yet. But when we swap a 0 to the left, we DO advance `mid` — because whatever was at `low` must have been a 1 (it was in the already-processed zone).

This gives us O(n) time, O(1) space, single pass — which is optimal. Let me code it up."

---

*Generated for LeetCode 75 — Sort Colors | Pattern: Dutch National Flag / Three Pointers*
