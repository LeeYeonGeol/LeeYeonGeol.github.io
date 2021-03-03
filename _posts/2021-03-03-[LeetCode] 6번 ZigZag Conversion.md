---
title: "[LeetCode] ZigZag Conversion"
categories: 
- LeetCode
tags:
- 문자열
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:

```
string convert(string s, int numRows);
```

## 예제

**Example 1:**

```
Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"
```

**Example 2:**

```
Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"
Explanation:
P     I    N
A   L S  I G
Y A   H R
P     I
```

**Example 3:**

```
Input: s = "A", numRows = 1
Output: "A"
```

## 조건

> **Constraints:**
>
> - `1 <= s.length <= 1000`
> - `s` consists of English letters (lower-case and upper-case), `','` and `'.'`.
> - `1 <= numRows <= 1000`

## 답

numRows가 1인 경우는 그대로 답이므로 그대로 출력, 그렇지 않은 경우는 왔다갔다할 수 있도록 for문을 진행하였다.

```python
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        graph = [[] for _ in range(numRows)]
        index = -1
        climb = True
        if numRows == 1:
            return s
        for i in range(len(s)):

            if climb == True:
                index += 1
                if index == numRows-1:
                    climb = False
            else:
                index -= 1
                if index == 0:
                    climb = True
            print(index, i)
            graph[index].append(s[i])
            
        ans = ""
        for i in graph:
            ans += "".join(i)
        return ans
```

## 다른 사람 풀이

```python
class Solution(object):
    def convert(self, s, numRows):
        if numRows == 1 or numRows >= len(s):
            return s
        
        L = [''] * numRows
        index, step = 0, 1
        
        for x in s:
            L[index] += x
            if index == 0:
                step = 1
            elif index == numRows -1:
                step = -1
            index += step
            
        return ''.join(L)
```

