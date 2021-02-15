---
title: "[LeetCode] 242번 Valid Anagram"
categories: 
- LeetCode
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given two strings *s* and *t* , write a function to determine if *t* is an anagram of *s*.

## 예제

**Example 1:**

```
Input: s = "anagram", t = "nagaram"
Output: true
```

**Example 2:**

```
Input: s = "rat", t = "car"
Output: false
```

## 조건

> **Note:**
> You may assume the string contains only lowercase alphabets.
>
> **Follow up:**
> What if the inputs contain unicode characters? How would you adapt your solution to such case?

## 풀이과정

### 내 풀이

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if collections.Counter(s) == collections.Counter(t):
            return True
        else:
            return False
```

최근에 익힌 collections.Counter를 사용하여 각각 데이터 갯수를 세고 비교한 뒤, 답을 출력한다.

### 다른 풀이

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:  
        return sorted(s)==sorted(t)
```

sorted를 이용하여 해결하였다.