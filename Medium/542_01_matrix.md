# 542. 01 Matrix

**Difficulty:** Medium  
**Tags:** BFS, Matrix, Dynamic Programming  
**Link:** [Leetcode 542](https://leetcode.com/problems/01-matrix/)

---

## 🔒 Problem Statement

Given an `m x n` binary matrix `mat`, return a matrix where each cell contains the **distance to the nearest 0**.

- The distance between two adjacent cells (up, down, left, right) is considered 1.
- The output matrix should maintain the same shape as the input.

---

### 🧪 Examples

#### Example 1:
```
Input:  mat = [[0,0,0],[0,1,0],[0,0,0]]
Output: [[0,0,0],[0,1,0],[0,0,0]]
```

#### Example 2:
```
Input:  mat = [[0,0,0],[0,1,0],[1,1,1]]
Output: [[0,0,0],[0,1,0],[1,2,1]]
```

---

### ✅ Constraints

- `1 <= m, n <= 10^4`
- `1 <= m * n <= 10^4`
- `mat[i][j]` is `0` or `1`
- There is at least one `0` in `mat`

---

## ✅ Solution

### 🔍 Approach

- Use **multi-source BFS** starting from all the `0`s.
- Set distance `0` to those cells, and initialize `-1` for all `1`s.
- Perform BFS from each zero simultaneously and update distance to neighbors.

---

### 👨‍💻 Python Code

```python
from collections import deque

class Solution(object):
    def updateMatrix(self, mat):
        """
        :type mat: List[List[int]]
        :rtype: List[List[int]]
        """
        m, n = len(mat), len(mat[0])
        q = deque()
        dist = [[-1 for _ in range(n)] for _ in range(m)]

        # Enqueue all 0s and mark their distance
        for i in range(m):
            for j in range(n):
                if mat[i][j] == 0:
                    dist[i][j] = 0
                    q.append((i, j))

        # BFS directions
        directions = [(0,1), (1,0), (0,-1), (-1,0)]

        while q:
            x, y = q.popleft()
            for dx, dy in directions:
                nx, ny = x + dx, y + dy
                if 0 <= nx < m and 0 <= ny < n and dist[nx][ny] == -1:
                    dist[nx][ny] = dist[x][y] + 1
                    q.append((nx, ny))

        return dist
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(m * n)` — every cell is visited once in BFS.
- **Space Complexity:** `O(m * n)` — queue and distance matrix.

---

## 🧪 Submission Info

- **Status:** ✅ Accepted  
- **Language:** Python  
- **Runtime:** 182 ms (⏱ Beats 74.86%)  
- **Memory Usage:** 16.08 MB (📦 Beats 45.36%)  
- **Submitted by:** Rajesh Kumar Jogi at Jun 19, 2025, 19:45

---

## 🧠 Notes

- Efficient BFS solution ideal for grid traversal with multiple sources.
- Greedy expansion ensures shortest path to nearest 0.
- Handles large input sizes effectively due to linear time complexity.

---
