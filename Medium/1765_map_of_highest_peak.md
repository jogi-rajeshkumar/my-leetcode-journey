# 1765. Map of Highest Peak

**Difficulty:** Medium  
**Tags:** BFS, Graph, Matrix  
**Link:** [Leetcode 1765](https://leetcode.com/problems/map-of-highest-peak/)

---

## 🔒 Problem Statement

You are given an integer matrix `isWater` of size `m x n` that represents a map of land and water cells.

- If `isWater[i][j] == 0`, cell `(i, j)` is a **land** cell.
- If `isWater[i][j] == 1`, cell `(i, j)` is a **water** cell.

You must assign each cell a height such that:

- The height of each cell must be non-negative.
- If the cell is a **water** cell, its height must be `0`.
- Any two adjacent cells must have an absolute height difference of **at most 1**.

Return an integer matrix `height` of size `m x n` where `height[i][j]` is the height of cell `(i, j)`.  
If there are multiple valid assignments, return **any** of them.

---

### 🧪 Examples

#### Example 1:

Input: `isWater = [[0,1],[0,0]]`  
Output: `[[1,0],[2,1]]`

#### Example 2:

Input: `isWater = [[0,1,0],[1,0,0],[0,0,0]]`  
Output: `[[1,1,0],[0,1,1],[1,2,2]]`

---

### ✅ Constraints

- `1 <= m, n <= 1000`
- `isWater[i][j]` is `0` (land) or `1` (water)
- At least one water cell exists

---

## ✅ Solution

### 🔍 Approach

- Perform a **multi-source BFS** starting from all water cells.
- Initialize their height as `0` and use BFS to expand to adjacent land cells.
- Each step increases height by `1`, ensuring the absolute difference rule.

---

### 👨‍💻 Python Code

```python
from collections import deque

class Solution(object):
    def highestPeak(self, isWater):
        """
        :type isWater: List[List[int]]
        :rtype: List[List[int]]
        """
        m, n = len(isWater), len(isWater[0])
        height = [[-1 for _ in range(n)] for _ in range(m)]
        q = deque()

        # Step 1: Enqueue all water cells with height 0
        for i in range(m):
            for j in range(n):
                if isWater[i][j] == 1:
                    height[i][j] = 0
                    q.append((i, j))

        # Step 2: BFS in 4 directions
        directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]

        while q:
            i, j = q.popleft()
            for dx, dy in directions:
                ni, nj = i + dx, j + dy
                if 0 <= ni < m and 0 <= nj < n and height[ni][nj] == -1:
                    height[ni][nj] = height[i][j] + 1
                    q.append((ni, nj))

        return height
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(m * n)` — every cell is visited once in BFS
- **Space Complexity:** `O(m * n)` — for the height matrix and BFS queue

---

## 🧪 Submission Info

- **Status:** ✅ Accepted  
- **Language:** Python  
- **Runtime:** 988 ms  
- **Memory Usage:** 126 MB  
- **Notes:** Efficient multi-source BFS approach, ensures minimum height assignments with valid constraints.

---
