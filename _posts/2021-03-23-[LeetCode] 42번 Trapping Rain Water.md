---
title: "[LeetCode] Trapping Rain Water"
categories: 
- LeetCode
tags:
- 배열
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

## 예제

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
```

**Example 2:**

```
Input: height = [4,2,0,3,2,5]
Output: 9
```

## 조건

> - `n == height.length`
> - `0 <= n <= 3 * 104`
> - `0 <= height[i] <= 105`

## 답 

### 풀이 1

투 포인터를 활용한 풀이.

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        n = len(height)
        
        left = 0
        right = n-1
        left_max = 0
        right_max = 0
        ans = 0
        
        if not height:
            return ans
        while(left != right):
            left_max = max(left_max, height[left])
            right_max = max(right_max, height[right])
            
            if left_max <= right_max:
                ans += left_max - height[left]
                left += 1
            else:
                ans += right_max - height[right]
                right -= 1
            
        return ans
```

### 풀이 2

스택을 활용한 풀이. (아직 이해하기 힘들다.)

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        stack = []
        ans = 0
        
        for i in range(len(height)):
            while stack and height[i] > height[stack[-1]]:
                top = stack.pop()
                
                if not stack:
                    break
                    
                distance = i - stack[-1] - 1
                waters = min(height[i], height[stack[-1]]) - height[top]
                
                ans += distance * waters
                
            stack.append(i)
        
        return ans
```

