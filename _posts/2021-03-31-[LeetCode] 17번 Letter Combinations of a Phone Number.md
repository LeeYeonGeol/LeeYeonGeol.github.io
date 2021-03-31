---
title: "[LeetCode] Letter Combinations of a Phone Number"
categories: 
- LeetCode
tags:
- DFS/BFS
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

## 예제

**Example 1:**

```
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

**Example 2:**

```
Input: digits = ""
Output: []
```

**Example 3:**

```
Input: digits = "2"
Output: ["a","b","c"]
```

## 조건

- `0 <= digits.length <= 4`
- `digits[i]` is a digit in the range `['2', '9']`.

## 답 

### 풀이 1

BFS를 활용한 내 풀이

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        graph = { 
            2 : ['a', 'b', 'c'], 
            3 : ['d', 'e', 'f'],
            4 : ['g', 'h', 'i'],
            5 : ['j', 'k', 'l'],
            6 : ['m', 'n', 'o'],
            7 : ['p', 'q', 'r', 's'],
            8 : ['t', 'u', 'v'],
            9 : ['w', 'x', 'y', 'z']
        }
        
        ans = []
        
        arr = list(map(int, digits))
        
        n = len(digits)
        
        q = collections.deque()
        
        if not digits:
            return ans
        
        for i in graph[arr[0]]:
            q.append([i, 0])
        
        while q:
            letter, cnt = q.popleft()
            if cnt >= n-1:
                ans.append(letter)
                continue
            for j in graph[arr[cnt+1]]:
                q.append([letter+j, cnt+1])
                
        return ans
```

### 풀이 2

DFS를 활용한 풀이

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        graph = { 
            2 : ['a', 'b', 'c'], 
            3 : ['d', 'e', 'f'],
            4 : ['g', 'h', 'i'],
            5 : ['j', 'k', 'l'],
            6 : ['m', 'n', 'o'],
            7 : ['p', 'q', 'r', 's'],
            8 : ['t', 'u', 'v'],
            9 : ['w', 'x', 'y', 'z']
        }
        
        ans = []
        
        arr = list(map(int, digits))
        
        n = len(digits)
        
        if not digits:
            return ans
        
        
        def dfs(st, dis = ""):
            if st >= n:
                ans.append(dis)
                return
            for i in graph[arr[st]]:
                dfs(st+1, dis+i)
        
        dfs(0)
        return ans
```

### 풀이 3

책풀이

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        
        dic = {
            "2": "abc",
            "3": "def",
            "4": "ghi",
            "5": "jkl",
            "6": "mno",
            "7": "pqrs",
            "8": "tuv",
            "9": "wxyz"
              }
        result = []
        
        if not digits:
            return result    
        
        def dfs(index, path):
            # 끝까지 탐색하면 백트래킹
            if len(path) == len(digits):
                result.append(path)
                return
            
            # 입력값 자릿수 단위 반복
            for i in range(index, len(digits)):
                # 숫자에 해당하는 모든 문자열 반복
                for j in dic[digits[i]]:
                    dfs(i + 1, path + j)
        
        dfs(0,"")
        
        return result
```









