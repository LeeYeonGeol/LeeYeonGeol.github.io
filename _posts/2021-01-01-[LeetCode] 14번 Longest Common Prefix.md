---
title: "[LeetCode] 14번 Longest Common Prefix"
categories: 
- LeetCode
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

## 예제

**Example 1:**

```
Input: strs = ["flower","flow","flight"]
Output: "fl"
```

**Example 2:**

```
Input: strs = ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

## 조건

> **Constraints:**
>
> - `0 <= strs.length <= 200`
> - `0 <= strs[i].length <= 200`
> - `strs[i]` consists of only lower-case English letters.

## 풀이과정

### 내 풀이

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        n = len(strs)
        st = ""
        count = 0
        result = 0
        # 앞에서 한자리씩 비교(자릿수를 의미)
        while count >= 0:
            test = 0
            #string 개수 모두 비교(1,2)
            for i in range(1,n):
                if strs[i-1][count] != strs[i][count]:
                    test = 1
            if test == 1:
                result = count
                count = -1
            else:
                count += 1 
        st += strs[0][0:result]
        return st
```

몇번째인지 인덱스를 두고 늘려가면서 답을 구했다. 시간초과와 상대적으로 긴 코드 등의 문제점이 있었다. 

### 다른 풀이

```python
class Solution:
    def longestCommonPrefix(self, strs):
        if not strs:
            return ""
        shortest = min(strs,key=len)
        for i, ch in enumerate(shortest):
            for other in strs:
                if other[i] != ch:
                    return shortest[:i]
        return shortest 
```

strs배열에서 가장 짧은 string을 shortest라 한다. 그 후, shortest를 통해 for문을 돌리는데, strs배열과 비교하면서 Longest가 되는 index를 기억하고 그에맞게 답을 반환한다.

