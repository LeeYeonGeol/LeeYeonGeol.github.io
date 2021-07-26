---
title: "[LeetCode] Daily Temparatures"
categories: 
- LeetCode
tags:
- 스택
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given a list of daily temperatures `T`, return a list such that, for each day in the input, tells you how many days you would have to wait until a warmer temperature. If there is no future day for which this is possible, put `0` instead.

For example, given the list of temperatures `T = [73, 74, 75, 71, 69, 72, 76, 73]`, your output should be `[1, 1, 4, 2, 1, 1, 0, 0]`.

**Note:** The length of `temperatures` will be in the range `[1, 30000]`. Each temperature will be an integer in the range `[30, 100]`.

## 답 

### 풀이 1

```python
class Solution:
    def dailyTemperatures(self, T: List[int]) -> List[int]:
        answer = [0]*n
        stack = []
        for idx, i in enumerate(T):
            while stack and T[stack[-1]] < i:
                last = stack.pop()
                answer[last] = idx - last
            stack.append(idx)
        return answer
```







