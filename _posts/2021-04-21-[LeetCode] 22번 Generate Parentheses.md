---
title: "[LeetCode] Generate Parentheses"
categories: 
- LeetCode
tags:
- 백트래킹
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given `n` pairs of parentheses, write a function to *generate all combinations of well-formed parentheses*.

## 예제

**Example 1:**

```
Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]
```

**Example 2:**

```
Input: n = 1
Output: ["()"]
```

## 조건

- `1 <= n <= 8`

## 답 

### 풀이 1

백트래킹 방식으로 해결하였다. )가 많은 순간 정답이 아니게 되므로 잘라주고 cnt가 2n을 넘어선 순간에도 잘라주었다.

```python
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        
        ans = []
        sub = []
        def dfs(cnt, a, b):
            
            if a < b or cnt > 2*n:
                return
            if cnt == 2*n and a == b:
                ans.append("".join(sub))
            
            sub.append('(')
            dfs(cnt+1,a+1,b)
            sub.pop()
            sub.append(')')
            dfs(cnt+1,a,b+1)
            sub.pop()
                
        
        dfs(0,0,0)
        return ans
```









