---
title: "[LeetCode] Combinations Sum 2"
categories: 
- LeetCode
tags:
- 백트래킹
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given a collection of candidate numbers (`candidates`) and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sum to `target`.

Each number in `candidates` may only be used **once** in the combination.

**Note:** The solution set must not contain duplicate combinations.

## 예제

**Example 1:**

```
Input: candidates = [10,1,2,7,6,1,5], target = 8
Output: 
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]
```

**Example 2:**

```
Input: candidates = [2,5,2,1,2], target = 5
Output: 
[
[1,2,2],
[5]
]
```

## 조건

- `1 <= candidates.length <= 100`
- `1 <= candidates[i] <= 50`
- `1 <= target <= 30`

## 답 

### 풀이 1

백트래킹 방식으로 해결하였다.  합이 타겟보다 큰 순간 가지치기를 한다.

```python
class Solution:
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:

        if sum(candidates) < target:
            return []
        ans = []
        sub = []
        def dfs(index, csum):
            if csum == target:
                if not sorted(sub) in ans:
                    ans.append(sorted(sub))
                return
            
            for i in range(index, len(candidates)):
                if csum + candidates[i] > target:
                    continue
                sub.append(candidates[i])
                dfs(i+1, csum+candidates[i])
                sub.pop()
        
        dfs(0, 0)
        return ans
```









