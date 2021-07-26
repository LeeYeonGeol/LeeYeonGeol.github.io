---
title: "[LeetCode] Valid Parentheses"
categories: 
- LeetCode
tags:
- 스택
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

## 예제

**Example 1:**

```
Input: s = "()"
Output: true
```

**Example 2:**

```
Input: s = "()[]{}"
Output: true
```

**Example 3:**

```
Input: s = "(]"
Output: false
```

**Example 4:**

```
Input: s = "([)]"
Output: false
```

**Example 5:**

```
Input: s = "{[]}"
Output: true
```

## 조건

> - 1 <= s.length <= $10^4$
> - `s` consists of parentheses only `'()[]{}'`.

## 답 

### 풀이 1

```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        for i in s:
            if stack:
                if i == ']' and stack[-1] == '[':
                    stack.pop()
                elif i == ')' and stack[-1] == '(':
                    stack.pop()
                elif i == '}' and stack[-1] == '{':
                    stack.pop()
                else:
                    stack.append(i)
            else:
                stack.append(i)
        
        return len(stack) == 0
```





