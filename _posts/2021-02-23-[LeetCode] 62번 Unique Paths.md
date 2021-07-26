---
title: "[LeetCode] 62번 Unique Paths"
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

How many possible unique paths are there?

## 예제

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

```
Input: m = 3, n = 7
Output: 28
```

**Example 2:**

```
Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Down -> Down
2. Down -> Down -> Right
3. Down -> Right -> Down
```

**Example 3:**

```
Input: m = 7, n = 3
Output: 28
```

**Example 4:**

```
Input: m = 3, n = 3
Output: 6
```

## 조건

> **Constraints:**
>
> - `1 <= m, n <= 100`
> - It's guaranteed that the answer will be less than or equal to 2 * $10^9$.

## 답

간단한 다이나믹 프로그래밍 문제이다. 시작을 1로 하고 2중 for문을 통해 dp 테이블을 갱신한다.

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[0] * n for _ in range(m)]
        dp[0][0] = 1
        for x in range(m):
            for y in range(n):
                if x != 0:
                    dp[x][y] += dp[x-1][y]
                if y != 0:
                    dp[x][y] += dp[x][y-1]
        return dp[m-1][n-1]
```

![image](https://user-images.githubusercontent.com/48538655/108843436-0894d480-761e-11eb-91df-a279849dcdb2.png)

