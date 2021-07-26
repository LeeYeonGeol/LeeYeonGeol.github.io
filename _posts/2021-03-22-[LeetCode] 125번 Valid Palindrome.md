---
title: "[LeetCode] Valid Palindrome"
categories: 
- LeetCode
tags:
- 문자열
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given a string `s`, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

## 예제

**Example 1:**

```
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```

**Example 2:**

```
Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
```

## 조건

> **Constraints:**
>
> - `1 <= s.length <= 2 * 105`
> - `s` consists only of printable ASCII characters.

## 답 

### 풀이 1

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        s2 = ""
        for i in s:
            if i.isdigit():
                s2 += i
            elif i.isalpha():
                s2 += i.lower()

        if s2 == s2[::-1]:
            return True
        else:
            return False
```

### 풀이 2

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        s2 = ""
        for i in s:
            if i.isdigit():
                s2 += i
            elif i.isalpha():
                s2 += i.lower()

        for i in range(len(s2)//2):
            if s2[i]  != s2[-1-i]:
                return False
        else:
            return True
```

