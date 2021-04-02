---
title: "[LeetCode] Subsets"
categories: 
- LeetCode
tags:
- DFS/BFS
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given an integer array `nums` of **unique** elements, return *all possible subsets (the power set)*.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

## 예제

**Example 1:**

```
Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```

**Example 2:**

```
Input: nums = [0]
Output: [[],[0]]
```

## 조건

- `1 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`
- All the numbers of `nums` are **unique**.

## 답 

### 풀이 1

BFS를 활용한 풀이

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        ans = []
        sub = []
        
        q = collections.deque()
        q.append([sub, -1])
        
        while q:
            li, index = q.popleft()
            ans.append(li)
            
            if index == len(nums) - 1:
                continue
            for i in range(index+1, len(nums)):
                q.append([li+[nums[i]], i])
        
        return ans
```

### 풀이 2

DFS를 활용한 풀이

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        result = []
        
        def dfs(index, path):
            # 매번 결과 추가
            result.append(path)
            
            # 경로를 만들면서 DFS
            for i in range(index, len(nums)):
                dfs(i + 1, path + [nums[i]])
        
        dfs(0, [])
        return result
```









