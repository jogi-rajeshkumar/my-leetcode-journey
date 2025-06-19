# 2294. Partition Array Such That Maximum Difference Is K

**Difficulty:** Medium  
**Tags:** Greedy, Sorting  
**Link:** [Leetcode 2294](https://leetcode.com/problems/partition-array-such-that-maximum-difference-is-k/)

---

## 🔒 Problem Statement

You are given an integer array `nums` and an integer `k`.  
You may partition `nums` into one or more subsequences such that **each element in `nums` appears in exactly one** of the subsequences.

Return the **minimum number of subsequences** needed such that the **difference between the maximum and minimum values** in each subsequence is at most `k`.

A **subsequence** is a sequence that can be derived from another sequence by deleting some or no elements without changing the order of the remaining elements.

---

### 🧪 Examples

#### Example 1:
```
Input: nums = [3,6,1,2,5], k = 2  
Output: 2  
Explanation: [3,1,2] and [6,5] are two valid subsequences.
```

#### Example 2:
```
Input: nums = [1,2,3], k = 1  
Output: 2  
Explanation: [1,2] and [3] are two valid subsequences.
```

#### Example 3:
```
Input: nums = [2,2,4,5], k = 0  
Output: 3  
Explanation: [2,2], [4], and [5] are valid groups where max - min ≤ 0.
```

---

### ✅ Constraints

- `1 <= nums.length <= 10^5`
- `0 <= nums[i] <= 10^5`
- `0 <= k <= 10^5`

---

## ✅ Solution

### 🔍 Approach

- **Sort the array** so that elements close in value are adjacent.
- Use a **greedy approach**:
  - Start a new group from the current element.
  - Keep expanding the group while the maximum difference ≤ `k`.
  - Count how many such groups are needed.

---

### 💡 Intuition

Sorting ensures we consider the smallest possible valid subsequences first.  
Greedily expanding each group allows us to **minimize** the total number of subsequences.

---

### 👨‍💻 Python Code

```python
class Solution(object):
    def partitionArray(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        nums.sort()
        count = 0
        i = 0
        n = len(nums)

        while i < n:
            start = nums[i]
            count += 1  # Start a new group
            while i < n and nums[i] - start <= k:
                i += 1

        return count
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(n log n)`  
  - Sorting takes `O(n log n)`
  - Single pass after sorting is `O(n)`

- **Space Complexity:** `O(1)`  
  - Sorting can be in-place; otherwise `O(n)` for sorted copy (ignored in contest)

---

## 🧪 Submission Info

- **Status:** ✅ Accepted  
- **Language:** Python  
- **Runtime:** 150 ms  
- **Memory Usage:** 21.6 MB  
- **Notes:** Clean greedy approach with sort + linear scan. Handles edge cases efficiently.

---
