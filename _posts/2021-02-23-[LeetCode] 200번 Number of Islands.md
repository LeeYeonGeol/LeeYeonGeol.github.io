---
title: "[LeetCode] 200번 Number of Islands"
categories: 
- LeetCode
tags:
- DFS/BFS
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given an `m x n` 2d `grid` map of `'1'`s (land) and `'0'`s (water), return *the number of islands*.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

## 예제

**Example 1:**

```
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
```

**Example 2:**

```
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
```

## 조건

> **Constraints:**
>
> - `m == grid.length`
> - `n == grid[i].length`
> - `1 <= m, n <= 300`
> - `grid[i][j]` is `'0'` or `'1'`.

## 답

### BFS를 활용한 풀이

전형적인 DFS/BFS문제이다. BFS를 통해 해결하였다.

```python
from collections import deque
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        n, m = len(grid), len(grid[0])
        
        dx = [-1, 0, 1, 0]
        dy = [0, 1, 0, -1]
        
        cnt = 0
        for x in range(n):
            for y in range(m):
                if grid[x][y] == "1":
                    q = deque()
                    q.append((x, y))
                    while q:
                        nx, ny = q.popleft()
                        for k in range(4):
                            nnx, nny = nx + dx[k], ny + dy[k]
                            if nnx <= -1 or nny <= -1 or nnx >= n or nny >= m:
                                continue
                            if grid[nnx][nny] == "1":
                                q.append((nnx, nny))
                                grid[nnx][nny] = "0"
                    cnt += 1
        
        return cnt
```

### DFS를 활용한 풀이

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        n, m = len(grid), len(grid[0])
        
        def dfs(x, y, grid):
            if x < 0 or y < 0 or x >= n or y >= m or grid[x][y] != '1':
                return
            
            grid[x][y] = "0"
            bfs(x+1,y,grid)
            bfs(x,y+1,grid)
            bfs(x-1,y,grid)
            bfs(x,y-1,grid)
             
        cnt = 0
        for x in range(n):
            for y in range(m):
                if grid[x][y] == "1":
                    dfs(x, y, grid)  
                    cnt += 1    
        return cnt
                

```

