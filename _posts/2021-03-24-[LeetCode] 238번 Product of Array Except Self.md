---
title: "[LeetCode] Product of Array Except Self"
categories: 
- LeetCode
tags:
- 배열
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given an integer array `nums`, return *an array* `answer` *such that* `answer[i]` *is equal to the product of all the elements of* `nums` *except* `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

## 예제

**Example 1:**

```
Input: nums = [1,2,3,4]
Output: [24,12,8,6]
```

**Example 2:**

```
Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]
```

## 조건

> - 2 <= nums.length <= $10^5$
> - -30 <= nums[i] <= 30
> - The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

## 답 

### 풀이 1

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        answer1 = [1 for _ in range(len(nums))]
        answer2 = [1 for _ in range(len(nums))]
        
        for n in range(len(nums)-1):
            answer1[n+1] = answer1[n]*nums[n]
        for n in range(len(nums)-1,0,-1):
            answer2[n-1] = answer2[n]*nums[n]
            
        answer = [1 for _ in range(len(nums))]
        
        for n in range(len(nums)):
            answer[n] = answer1[n]*answer2[n]
        
        return answer
 
```





