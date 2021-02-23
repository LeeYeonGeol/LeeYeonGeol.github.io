---
title: "[LeetCode] 63번 Unique Paths 2"
categories: 
- LeetCode
tags:
- Dynamic Programming
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

A robot is located at the top-left corner of a `m x n` grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and space is marked as `1` and `0` respectively in the grid.

## 예제

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/04/robot1.jpg)

```
Input: obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]
Output: 2
Explanation: There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/11/04/robot2.jpg)

```
Input: obstacleGrid = [[0,1],[0,0]]
Output: 1
```

## 조건

> **Constraints:**
>
> - `m == obstacleGrid.length`
> - `n == obstacleGrid[i].length`
> - `1 <= m, n <= 100`
> - `obstacleGrid[i][j]` is `0` or `1`.

## 답

[Unique Paths](https://leeyeongeol.github.io/leetcode/LeetCode-62%EB%B2%88-Unique-Paths/)의 후속 문제이다. 처음부터 1인 부분을 -1로 바꾸어서 할 수도 있지만.. 더 빠르게 처리하기 위해서 그냥 그대로 for문을 돌리다가 1을 만나면 -1로 바꿔주는식으로 하였다. 이렇게 하니 시작 혹은 마지막이 장애물인 경우가 예외가 생겼고 이를 앞에서 처리해주었다.

```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        m = len(obstacleGrid)
        n = len(obstacleGrid[0])
        if obstacleGrid[m-1][n-1] == 1 or obstacleGrid[0][0] == 1:
            return 0
        obstacleGrid[0][0] = 1
        for x in range(m):
            for y in range(n):
                if x == 0 and y == 0:
                    continue
                if obstacleGrid[x][y] == 1:
                    obstacleGrid[x][y] = -1
                elif obstacleGrid[x][y] == 0:
                    if x != 0 and obstacleGrid[x-1][y] != -1:
                        obstacleGrid[x][y] += obstacleGrid[x-1][y]
                    if y != 0 and obstacleGrid[x][y-1] != -1:
                        obstacleGrid[x][y] += obstacleGrid[x][y-1]

        return obstacleGrid[m-1][n-1]
                        
```

![image](https://user-images.githubusercontent.com/48538655/108844793-e603bb00-761f-11eb-908c-b9dce8e9a6d0.png)

