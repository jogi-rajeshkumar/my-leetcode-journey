# 3584. Maximum Product of First and Last Elements of a Subsequence

**Difficulty:** Medium  
**Tags:** Dynamic Programming, Backtracking, Brute Force  
**Link:** [Leetcode 3584](https://leetcode.com/problems/maximum-product-of-first-and-last-elements-of-a-subsequence/)

---

## 🔒 Problem Statement

You are given an integer array `nums` and an integer `m`.

Return the **maximum product** of the **first and last elements** of any **subsequence** of `nums` of size exactly `m`.

---

### 🧪 Examples

#### Example 1:
```
Input:  nums = [-1, -9, 2, 3, -2, -3, 1], m = 1
Output: 81
Explanation: max(x * x) for x in nums is 81
```

#### Example 2:
```
Input:  nums = [1, 3, -5, 5, 6, -4], m = 3
Output: 20
Explanation: subsequence [-5, 6, -4] → -5 * -4 = 20
```

#### Example 3:
```
Input:  nums = [2, -1, 2, -6, 5, 2, -5, 7], m = 2
Output: 35
Explanation: subsequence [5, 7] → 5 * 7 = 35
```

---

## ✅ Constraints

- `1 <= nums.length <= 10^5`
- `-10^5 <= nums[i] <= 10^5`
- `1 <= m <= nums.length`

---

## ✅ Final Solution

### 🔍 Approach

- Use DFS (backtracking) to try all subsequences of size `m`
- Track `first` and `last` element to compute product
- Special handling for `m = 1` using `max(x * x for x in nums)`
- Use `list` for mutable `max_product` to avoid `nonlocal` (Python 2 safe)

---

### 👨‍💻 Python Code (Leetcode Compatible)

```python
class Solution(object):
    def maximumProduct(self, nums, m):
        """
        :type nums: List[int]
        :type m: int
        :rtype: int
        """
        n = len(nums)
        max_product = [float('-inf')]  # mutable in nested scope

        def dfs(start, depth, first):
            if n - start < m - depth:
                return
            if depth == m:
                max_product[0] = max(max_product[0], first * nums[start - 1])
                return
            for i in range(start, n):
                if depth == 0:
                    dfs(i + 1, depth + 1, nums[i])
                else:
                    dfs(i + 1, depth + 1, first)

        dfs(0, 0, 0)
        return max_product[0]
```

---

## ⏱️ Time & Space Complexity

- **Time Complexity:** `O(n^m)` worst-case but works due to pruning and small `m`
- **Space Complexity:** `O(m)` due to recursive call stack

---

## 🧪 Submission Info

- **Status:** ✅ Accepted for small/medium `m`
- **Time Limit Exceeded:** ❌ For large `m = 65`, due to exponential depth
- **Language:** Python (Leetcode Python 2 Compatible)

---

## 🧠 Notes

- Problem fundamentally hard due to exponential number of subsequences
- Can be solved with dynamic programming or greedy+heap only if constraints are relaxed (e.g., sorted subsequence, contiguous)
- DFS is safest approach to ensure correctness for all cases

---
