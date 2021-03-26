---
title: "[LeetCode] Remove Duplicate Letters"
categories: 
- LeetCode
tags:
- 스택
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

1. Given a string `s`, remove duplicate letters so that every letter appears once and only once. You must make sure your result is **the smallest in lexicographical order** among all possible results.

   **Note:** This question is the same as 1081: https://leetcode.com/problems/smallest-subsequence-of-distinct-characters/

## 예제

**Example 1:**

```
Input: s = "bcabc"
Output: "abc"
```

**Example 2:**

```
Input: s = "cbacdcbc"
Output: "acdb"
```

## 조건

> - 1 <= s.length <= $10^4$
> - `s` consists of lowercase English letters.

## 답 

### 풀이 1

```python
class Solution:
    def removeDuplicateLetters(self, s: str) -> str:
        stack, seen, counter = [], set(), collections.Counter(s)
        
        for char in s:
            counter[char] -= 1
            
            if char in seen:
                continue
            
            while stack and stack[-1] > char and counter[stack[-1]] > 0:
                seen.remove(stack.pop())
                
            stack.append(char)
            seen.add(char)
       
        return ''.join(stack)
                    
```

### 풀이 2

```python
class Solution:
    def removeDuplicateLetters(self, s: str) -> str:
    	# 집합으로 정렬
        for char in sorted(set(s)):
            suffix = s[s.index(char):]
            # 전체 집합과 접미사 집합이 일치할 때 분리 진행
            if set(s) == set(suffix):
                return char + self.removeDuplicateLetters(suffix.replace(char, ''))
        return ''
```





