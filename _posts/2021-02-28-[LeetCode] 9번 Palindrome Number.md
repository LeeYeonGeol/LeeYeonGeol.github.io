---
title: "[LeetCode] 9번 Palindrome Number"
categories: 
- LeetCode
tags:
- 문자열
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given an integer `x`, return `true` if `x` is palindrome integer.

An integer is a **palindrome** when it reads the same backward as forward. For example, `121` is palindrome while `123` is not.

## 예제

**Example 1:**

```
Input: x = 121
Output: true
```

**Example 2:**

```
Input: x = -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```

**Example 3:**

```
Input: x = 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

**Example 4:**

```
Input: x = -101
Output: false
```

## 조건

> **Constraints:**
>
> - $-2^{31}$ <= x <= $2^{31}$- 1

## 답

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        ans = True
        s = str(x)
        n = len(s)
        
        for i in range((n//2)+1):
            if s[i] != s[n-i-1]:
                ans = False
                break
        return ans
```


