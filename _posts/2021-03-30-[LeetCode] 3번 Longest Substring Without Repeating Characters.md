---
title: "[LeetCode] 3번 Longest Substring Without Repeating Characters"
categories: 
- LeetCode
tags:
- 해시
- 투 포인터
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given a string `s`, find the length of the **longest substring** without repeating characters.

## 예제

**Example 1:**

```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

**Example 2:**

```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

**Example 3:**

```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

**Example 4:**

```
Input: s = ""
Output: 0
```

## 조건

> **Constraints:**
>
> - `0 <= s.length <= 5 * 104`
> - `s` consists of English letters, digits, symbols and spaces.

## 풀이과정

### 내 풀이

투 포인터를 활용하여 풀이하였다.

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        ans = 0
        
        p1 = 0
        p2 = 0
        
        if not s:
            return 0
        
        while(1):
            if s[p2] in s[p1:p2]:
                p1 += 1
            else:
                p2 += 1
            ans = max(ans, p2-p1)
            if len(s) <= p2:
                break
                
        return ans
```

### 해시를 활용한 풀이

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        used = {}
        max_length = start = 0
        for index, char in enumerate(s):
            # 이미 등장했던 문자라면 'start' 위치 갱신
            if char in used and start <= used[char]:
                start = used[char] + 1
            else:	# 최대 부분 문자열 길이 갱신
                max_length = max(max_length, index - start + 1)
                
            # 현재 문자의 위치 삽입
            used[char] = index
           
      	return max_length
```

