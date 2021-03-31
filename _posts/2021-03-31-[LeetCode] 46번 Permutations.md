---
title: "[LeetCode] Permutations"
categories: 
- LeetCode
tags:
- DFS/BFS
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given an array `nums` of distinct integers, return *all the possible permutations*. You can return the answer in **any order**.

## 예제

**Example 1:**

```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

**Example 2:**

```
Input: nums = [0,1]
Output: [[0,1],[1,0]]
```

**Example 3:**

```
Input: nums = [1]
Output: [[1]]
```

## 조건

- `1 <= nums.length <= 6`
- `-10 <= nums[i] <= 10`
- All the integers of `nums` are **unique**.

## 답 

### 풀이 1

BFS를 활용한 내 풀이

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        ans = []      
        q = collections.deque()
        
        for i in (nums):
            q.append([i])
        
        while q:
            li = q.popleft()
            if len(li) == len(nums):
                ans.append(li)
                continue
            
            for i in nums:
                if i not in li:
                    q.append(li+[i])
        
        return ans
```

### 풀이 2

DFS를 활용한 풀이

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        results = []
        prev_elements = []
        
        def dfs(elements):
            # 리프 노드일 때 결과 추가
            if len(elements) == 0:
                results.append(prev_elements[:])
            
            # 순열 생성 재귀 호출
            for e in elements:
                next_elements = elements[:]
                next_elements.remove(e)
                
                prev_elements.append(e)
                dfs(next_elements)
                prev_elements.pop()
                
        dfs(nums)
        
        return results
```

### 풀이 3

itertools 모듈을 사용한 풀이

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        return list(itertools.permutations(nums))
```









