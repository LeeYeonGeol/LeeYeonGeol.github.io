---
title: "[LeetCode] 347번 Top K Frequent Elements"
categories: 
- LeetCode
tags:
- 해시
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given an integer array `nums` and an integer `k`, return *the* `k` *most frequent elements*. You may return the answer in **any order**.

## 예제

**Example 1:**

```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

**Example 2:**

```
Input: nums = [1], k = 1
Output: [1]
```

## 조건

> **Constraints:**
>
> - 1 <= nums.legth <= $10^5$
> - `k` is in the range `[1, the number of unique elements in the array]`.
> - It is **guaranteed** that the answer is **unique**.

## 풀이과정

### 내 풀이

카운터를 활용하여 풀이하였다.

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        ans = []
        cnt = collections.Counter(nums).most_common()
        
        for i in range(k):
            ans.append(cnt[i][0])
        return ans
```

### 파이썬다운 풀이

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        return list(zip(*collections.Counter(nums).most_common(k)))[0]
```

