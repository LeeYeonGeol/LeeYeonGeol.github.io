---
title: "[LeetCode] Longest Palindromic Substring"
categories: 
- LeetCode
tags:
- 문자열
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given a string `s`, return *the longest palindromic substring* in `s`.

## 예제

**Example 1:**

```
Input: s = "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

**Example 2:**

```
Input: s = "cbbd"
Output: "bb"
```

**Example 3:**

```
Input: s = "a"
Output: "a"
```

**Example 4:**

```
Input: s = "ac"
Output: "a"
```

## 조건

> - `1 <= s.length <= 1000`
> - `s` consist of only digits and English letters (lower-case and/or upper-case).

## 답 

### 풀이 1

큰 길이부터 완전탐색으로 푼 풀이이다. 시간 복잡도 측면에서 효율은 그다지 좋지 못했다.

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        for i in range(len(s), 0, -1):
            for j in range(0,len(s)-i+1):
                if s[j:i+j] == s[j:j+i][::-1]:
                    return s[j:i+j]
```

<p align='center'>
    <img src="https://user-images.githubusercontent.com/48538655/112102938-5df7dd80-8bec-11eb-84f9-c08d95a9923b.png" alt="image" style="zoom:80%;" />
</p>
### 풀이 2

2칸, 3칸으로 구성된 투 포인터가 슬라이딩 윈도우처럼 계속 앞으로 전진해나가는 방식이다.

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        # 팰린드롬 판별 및 투 포인터 확장
        def expand(left: int, right: int) -> str:
            while left >= 0 and right < len(s) and s[left] == s[right]:
                left -= 1
                right += 1
            return s[left + 1:right]
        
        # 해당 사항이 없을 때 빠르게 리턴
        if len(s) < 2 or s == s[::-1]:
            return s
        
        result = ''
        # 슬라이딩 윈도우 우측으로 이동
        for i in range(len(s) - 1):
            result = max(result, expand(i, i + 1), expand(i, i + 2), key=len)
        
        return result
```

<p align='center'>
    <img src="https://user-images.githubusercontent.com/48538655/112111294-5853c500-8bf7-11eb-84d7-9d52034ffc51.png" alt="image" style="zoom:80%;" />
</p>



