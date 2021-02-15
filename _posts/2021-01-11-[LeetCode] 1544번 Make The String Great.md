---
title: "[LeetCode] 1544번 Make The String Great"
categories: 
- LeetCode
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given a string `s` of lower and upper case English letters.

A good string is a string which doesn't have **two adjacent characters** `s[i]` and `s[i + 1]` where:

- `0 <= i <= s.length - 2`
- `s[i]` is a lower-case letter and `s[i + 1]` is the same letter but in upper-case or **vice-versa**.

To make the string good, you can choose **two adjacent** characters that make the string bad and remove them. You can keep doing this until the string becomes good.

Return *the string* after making it good. The answer is guaranteed to be unique under the given constraints.

**Notice** that an empty string is also good.

## 예제

**Example 1:**

```
Input: s = "leEeetcode"
Output: "leetcode"
Explanation: In the first step, either you choose i = 1 or i = 2, both will result "leEeetcode" to be reduced to "leetcode".
```

**Example 2:**

```
Input: s = "abBAcC"
Output: ""
Explanation: We have many possible scenarios, and all lead to the same answer. For example:
"abBAcC" --> "aAcC" --> "cC" --> ""
"abBAcC" --> "abBA" --> "aA" --> ""
```

**Example 3:**

```
Input: s = "s"
Output: "s"
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
    def makeGood(self, s: str) -> str:
        li = list(s)
        count = 0
        while(count == 0):
            count2 = 0
            n = len(li)
            for i in range(len(li)-1):
                count2 += 1
                if (ord(li[i]) - 32 == ord(li[i+1])) or (ord(li[i]) + 32 == ord(li[i+1])):
                    del li[i:i+2]
                    break
            if count2 == n-1:
                return "".join(li)
            
```

s를 li리스트로 넣어준 뒤, 아스키 코드를 사용해서 소문자와 대문자가 인접한 경우 삭제해준다. 

### 다른 풀이

```python
class Solution:
    def makeGood(self, s: str) -> str:
        result = []
        for c in s:
            if not result:
                result.append(c)
            elif result[-1].isupper() and result[-1].lower() == c:
                result.pop()
            elif result[-1].islower() and result[-1].upper() == c:
                result.pop()
            else:
                result.append(c)
        return ''.join(result)
```

배워야할 점

1. 아스키코드보다 upper()나 lower()사용하면 편했을 것.
2. 굳이 리스트에 넣지 않고도 for c in s로 전개.

가볍게 풀어보려고 했는데 생각보다 오래걸림. 열심히 해야겠다. 생각보다 문자열에서 배울게 많았던 문제.