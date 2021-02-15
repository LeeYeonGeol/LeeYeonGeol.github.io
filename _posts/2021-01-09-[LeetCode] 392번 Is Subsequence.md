---
title: "[LeetCode] 392번 Is Subsequence"
categories: 
- LeetCode
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given a string **s** and a string **t**, check if **s** is subsequence of **t**.

A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, `"ace"` is a subsequence of `"abcde"` while `"aec"` is not).

**Follow up:**
If there are lots of incoming S, say S1, S2, ... , Sk where k >= 1B, and you want to check one by one to see if T has its subsequence. In this scenario, how would you change your code?

**Credits:**
Special thanks to [@pbrother](https://leetcode.com/pbrother/) for adding this problem and creating all test cases.

## 예제

**Example 1:**

```
Input: s = "abc", t = "ahbgdc"
Output: true
```

**Example 2:**

```
Input: s = "axc", t = "ahbgdc"
Output: false
```

## 조건

> **Constraints:**
> 
>- `0 <= s.length <= 100`
> - `0 <= t.length <= 10^4`
> - Both strings consists only of lowercase characters.

## 풀이과정

### 내 풀이

```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        count = 0
        if len(s) == 0:
            return True
        
        for i in range(len(t)):
            if (s[count] == t[i]):
                count += 1
                
            if count == len(s):
                return True
        return False
```

s가 ""인 경우도 subsequence이므로 따로 조건을 걸어둔다. t를 하나씩 늘려가면서 s의 원소가 존재하는지 비교해준다.

### 다른 풀이

```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        ## RC ##
        ## APPROACH : 2 POINTERS ##
        
		## TIME COMPLEXITY : O(N) ##
		## SPACE COMPLEXITY : O(1) ##
        p1 = p2 = 0
        while p1 < len(s) and p2 < len(t):
            # move both pointers or just the right pointer
            if s[p1] == t[p2]:
                p1 += 1
            p2 += 1
        return p1 == len(s)
```



