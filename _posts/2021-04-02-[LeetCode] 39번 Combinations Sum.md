---
title: "[LeetCode] Combinations Sum"
categories: 
- LeetCode
tags:
- DFS/BFS
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given an array of **distinct** integers `candidates` and a target integer `target`, return *a list of all **unique combinations** of* `candidates` *where the chosen numbers sum to* `target`*.* You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

It is **guaranteed** that the number of unique combinations that sum up to `target` is less than `150` combinations for the given input.

## 예제

**Example 1:**

```
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.
```

**Example 2:**

```
Input: candidates = [2,3,5], target = 8
Output: [[2,2,2,2],[2,3,3],[3,5]]
```

**Example 3:**

```
Input: candidates = [2], target = 1
Output: []
```

**Example 4:**

```
Input: candidates = [1], target = 1
Output: [[1]]
```

**Example 5:**

```
Input: candidates = [1], target = 2
Output: [[1,1]]
```

## 조건

- `1 <= candidates.length <= 30`
- `1 <= candidates[i] <= 200`
- All elements of `candidates` are **distinct**.
- `1 <= target <= 500`

## 답 

### 풀이 1

BFS를 활용한 풀이

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        q = collections.deque()
        ans = []
        for c in candidates:
            q.append([c,[c]])
        
        while q:
            num, li = q.popleft()
            
            if num > target:
                continue
            elif num == target:
                li.sort()
                if not li in ans:
                    ans.append(li)
                continue
            
            for i in candidates:
                q.append([num+i,li+[i]])
        
        return ans
```

### 풀이 2

DFS를 활용한 풀이

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        result = []
        def dfs(csum, index, path):
            if csum < 0:
                return
            if csum == 0:
                result.append(path)
                return
            
            for i in range(index, len(candidates)):
                dfs(csum-candidates[i], i, path+[candidates[i]])
                
        dfs(target, 0, [])
        return result
```









