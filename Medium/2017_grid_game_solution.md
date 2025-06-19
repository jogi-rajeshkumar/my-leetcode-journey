# 2017. Grid Game

**Difficulty:** Medium  
**Tags:** Greedy, Prefix Sum, Dynamic Programming  
**Link:** [Leetcode 2017](https://leetcode.com/problems/grid-game/)

---

## 🔒 Problem Summary

Two robots play a game on a 2xN grid. Both start at `(0,0)` and want to reach `(1,n-1)` by moving only right or down.

- **Robot 1** moves first and sets all visited cells to `0`
- **Robot 2** then plays optimally to **maximize** the points it collects
- **Robot 1** wants to **minimize** Robot 2’s maximum collectible score

🧮 Return the number of points collected by the second robot if both play optimally.

---

## ✅ Constraints

- `grid.length == 2`
- `1 <= n == grid[0].length <= 5 * 10^4`
- `1 <= grid[r][c] <= 10^5`

---

## 🧠 Approach

Let the first robot choose a column `i` where it switches from top to bottom row.  
- Before `i`: collect from top
- After `i`: collect from bottom

Robot 2 will pick the worse of:
- **Top row right** from `i+1` to `n-1`
- **Bottom row left** from `0` to `i-1`

We try all `i` and minimize Robot 2’s **maximum gain**.

---

## 👨‍💻 Code (Python)

```python
class Solution(object):
    def gridGame(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        n = len(grid[0])

        top_prefix = [0] * (n + 1)
        bottom_prefix = [0] * (n + 1)

        for i in range(n):
            top_prefix[i + 1] = top_prefix[i] + grid[0][i]
            bottom_prefix[i + 1] = bottom_prefix[i] + grid[1][i]

        result = float('inf')
        for i in range(n):
            top_remaining = top_prefix[n] - top_prefix[i + 1]
            bottom_remaining = bottom_prefix[i]
            result = min(result, max(top_remaining, bottom_remaining))

        return result
```

---

## 🧪 Test Cases

### ✅ Example 1:
```
Input:  grid = [[2,5,4],[1,5,1]]
Output: 4
```

### ✅ Example 2:
```
Input:  grid = [[3,3,1],[8,5,2]]
Output: 4
```

### ✅ Example 3:
```
Input:  grid = [[1,3,1,15],[1,3,3,1]]
Output: 7
```

---

## ⏱️ Time and Space Complexity

- **Time Complexity:** `O(n)`  
- **Space Complexity:** `O(n)` for prefix sums

---

## ✅ Submission Results

- **Runtime:** 148 ms — Beats 25%
- **Memory:** 21.80 MB — Beats 53%
- **Status:** ✅ Accepted

---

## 🔍 Notes

- Prefix sums help compute segment sums efficiently
- Greedy choice to minimize second robot's gain
- Classic adversarial optimization using prefix arrays

