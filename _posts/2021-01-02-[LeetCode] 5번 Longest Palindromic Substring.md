---
title: "[LeetCode] 5번 Longest Palindromic Substring"
categories: 
- LeetCode
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

> **Constraints:**
>
> - `1 <= s.length <= 1000`
> - `s` consist of only digits and English letters (lower-case and/or upper-case),

## 풀이과정

### 내 풀이

```python
import math

class Solution:
    def longestPalindrome(self, s: str) -> str:
        
        li = list(s)
        count = collections.Counter(li)
        ans = []
        res = []
        for i in range(len(count)):
            if list(count.values())[i] >= 2:
                ans.append(list(count.keys())[i])
           
        # 겹치는게 없을 경우
        if (len(ans) == 0):
            return s[0]

        # 겹치는게 적어도 1개이상있는 경우
        for i in range(len(ans)):
            for idx, j in enumerate(s):
                # 중복된 친구 확인
                if ans[i] == j:
                    for m in range(idx+1, len(s)):
                        if s[m] == ans[i]:
                            res.append(s[idx:m+1])
        
        res.sort(key=len)
        # palindromic한지?
        res2 = []
        print(res)
        for i in range(len(res)):
            nn = len(res[i])
            count = 0
            nnn = (len(res[i]))
            for j in range(math.floor(nn/2)):
  
                if (res[i][j] == res[i][-1-j]):
                    count += 1
                else:
                    count -= 1
            if count == math.floor(nn/2):
                res2.append(res[i])

        if len(res2) >= 1:
            return(res2[-1])
        else:
            return(s[0])
        
```

열심히 고민했는데 코드만 길어지고 좋은 풀이는 아닌것같다. 답이 맞는지도 가늠이 가지 않는다. 좀더 공부하면서 다듬을 필요가 있다.

### 다른 풀이

추후 업데이트 예정