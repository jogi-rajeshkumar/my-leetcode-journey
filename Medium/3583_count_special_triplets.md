# 3583. Count Special Triplets

**Difficulty:** Medium  
**Tags:** Hash Map, Prefix Count, Frequency Counter  
**Link:** [Leetcode 3583](https://leetcode.com/problems/count-special-triplets/)

---

## 🔒 Problem Statement

You are given an integer array `nums`.

A **special triplet** is a triplet of indices `(i, j, k)` satisfying:

- `0 <= i < j < k < n`, where `n = nums.length`
- `nums[i] == nums[j] * 2`
- `nums[k] == nums[j] * 2`

Return the total number of **special triplets** in the array.  
Since the answer may be large, return it **modulo 10^9 + 7**.

---

### 🧪 Examples

#### Example 1:
```
Input:  nums = [6,3,6]
Output: 1
Explanation: (i=0, j=1, k=2) is a valid triplet
```

#### Example 2:
```
Input:  nums = [0,1,0,0]
Output: 1
Explanation: (i=0, j=2, k=3)
```

#### Example 3:
```
Input:  nums = [8,4,2,8,4]
Output: 2
Explanation:
- (i=0, j=1, k=3)
- (i=1, j=2, k=4)
```

---

### ✅ Constraints

- `3 <= nums.length <= 10^5`
- `0 <= nums[i] <= 10^5`

---

## ✅ Solution

### 🔍 Approach

- Use **prefix and suffix counters**:
  - `prefix` counts frequencies of `nums[i]` values **before** index `j`
  - `suffix` counts frequencies of `nums[k]` values **after** index `j`
- For each `j`, find `nums[i] = nums[j] * 2` and `nums[k] = nums[j] * 2`
- Multiply counts of such `i` and `k` to get the number of valid triplets for that `j`

---

### 👨‍💻 Python Code

```python
class Solution(object):
    def specialTriplets(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        from collections import Counter

        MOD = 10**9 + 7
        count = 0

        # Frequency of elements after the current index
        suffix = Counter(nums)
        prefix = Counter()

        for j in range(len(nums)):
            suffix[nums[j]] -= 1  # This is the current middle element

            # We're checking nums[i] == nums[j] * 2
            left = prefix[nums[j] * 2]
            right = suffix[nums[j] * 2]

            count = (count + (left * right)) % MOD

            # Move nums[j] into prefix for next round
            prefix[nums[j]] += 1

        return count
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(n)` — each index visited once, constant-time hash lookups
- **Space Complexity:** `O(n)` — for storing prefix and suffix counters

---

## 🧪 Submission Info

- **Status:** ✅ Accepted  
- **Language:** Python  
- **Runtime:** 1531 ms (Beats 21.01%)  
- **Memory Usage:** 30.14 MB (Beats 42.71%)  
- **Submitted by:** Rajesh Kumar Jogi at Jun 19, 2025, 17:40

---

## 🧠 Notes

- Hash counting avoids brute-force triple loops
- Efficient for large inputs up to 10^5 due to linear complexity
- Good example of using prefix/suffix patterns in frequency-based problems

---
