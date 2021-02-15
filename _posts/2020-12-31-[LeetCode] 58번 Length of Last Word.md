---
title: "[LeetCode] 58번 Length of Last Word"
categories: 
- LeetCode
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given a string `s` consists of some words separated by spaces, return *the length of the last word in the string. If the last word does not exist, return* `0`.

A **word** is a maximal substring consisting of non-space characters only.

## 예제

**Example 1:**

```
Input: s = "Hello World"
Output: 5
```

**Example 2:**

```
Input: s = " "
Output: 0
```

 ## 조건

> **Constraints:**
>
> - `1 <= s.length <= 104`
> - `s` consists of only English letters and spaces `' '`.

## 풀이과정

### 내 풀이

```python
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        li = s.split(" ")
        ans = ""
     
        for i in range(len(li)):
            if len(li[i]) > 0:
                ans = li[i]
        return (len(ans))
```



### 다른 풀이

```python
class Solution(object):
    def lengthOfLastWord(self, s):
        wordlist = s.split()
        if wordlist:
            return len(wordlist[-1])
        return 0
```

split()를 사용하니 조건에 더 부합했다.