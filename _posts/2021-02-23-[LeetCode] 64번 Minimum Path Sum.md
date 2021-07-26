---
title: "[LeetCode] 200번 Number of Islands"
categories: 
- LeetCode
tags:
- Dynamic Programming
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given a `m x n` `grid` filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.

**Note:** You can only move either down or right at any point in time.

## 예제

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/05/minpath.jpg)

```
Input: grid = [[1,3,1],[1,5,1],[4,2,1]]
Output: 7
Explanation: Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum.
```

**Example 2:**

```
Input: grid = [[1,2,3],[4,5,6]]
Output: 12
```

## 조건

> **Constraints:**
>
> - `m == grid.length`
> - `n == grid[i].length`
> - `1 <= m, n <= 200`
> - `0 <= grid[i][j] <= 100`

## 답

오직 아래와 오른쪽으로만 이동하기 때문에 다이나믹 프로그래밍 방식으로 해결한다. 

```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        for x in range(len(grid)):
            for y in range(len(grid[0])):
                if x == 0 and y == 0:
                    continue
                elif x == 0 and y != 0:
                    grid[x][y] += grid[x][y-1]
                elif x != 0 and y == 0:
                    grid[x][y] += grid[x-1][y]
                else:
                    grid[x][y] += min(grid[x][y-1], grid[x-1][y])
        
        return grid[len(grid)-1][len(grid[0])-1]

```


