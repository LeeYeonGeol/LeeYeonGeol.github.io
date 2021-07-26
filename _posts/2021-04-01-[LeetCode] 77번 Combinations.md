---
title: "[LeetCode] Combinations"
categories: 
- LeetCode
tags:
- DFS/BFS
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given two integers `n` and `k`, return *all possible combinations of* `k` *numbers out of the range* `[1, n]`.

You may return the answer in **any order**.

## 예제

**Example 1:**

```
Input: n = 4, k = 2
Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

**Example 2:**

```
Input: n = 1, k = 1
Output: [[1]]
```

## 조건

- `1 <= n <= 20`
- `1 <= k <= n`

## 답 

### 풀이 1

itertools 모듈을 활용한 풀이

```python
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        return list(map(list,list(itertools.combinations([i for i in range(1,n+1)],k))))
```

### 풀이 2

DFS를 활용한 풀이

```python
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        results = []
        
        def dfs(elements, start: int, k: int):
            if k == 0:
                results.append(elements[:])
                return
            
            # 자신 이전의 모든 값을 고정하여 재귀 호출
            for i in range(start, n + 1):
                elements.append(i)
            	dfs(elements, i + 1, k - 1)
                elements.pop()
        dfs([], 1, k)
        return results
```









