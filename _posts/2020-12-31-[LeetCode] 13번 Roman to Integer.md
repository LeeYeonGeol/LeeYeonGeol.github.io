---
title: "[LeetCode] 13번 Roman to Integer"
categories: 
- LeetCode
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

For example, `2` is written as `II` in Roman numeral, just two one's added together. `12` is written as `XII`, which is simply `X + II`. The number `27` is written as `XXVII`, which is `XX + V + II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

- `I` can be placed before `V` (5) and `X` (10) to make 4 and 9. 
- `X` can be placed before `L` (50) and `C` (100) to make 40 and 90. 
- `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

Given a roman numeral, convert it to an integer.

## 예제

**Example 1:**

```
Input: s = "III"
Output: 3
```

**Example 2:**

```
Input: s = "IV"
Output: 4
```

**Example 3:**

```
Input: s = "IX"
Output: 9
```

**Example 4:**

```
Input: s = "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
```

**Example 5:**

```
Input: s = "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

 ## 조건

> **Constraints:**
>
> - `1 <= s.length <= 15`
> - `s` contains only the characters `('I', 'V', 'X', 'L', 'C', 'D', 'M')`.
> - It is **guaranteed** that `s` is a valid roman numeral in the range `[1, 3999]`.

## 풀이과정

### 내 풀이

```python
def calculate(s1:str, s2:str):
        ans = 0
        if s1 == "I":
            if s2 == "V" or s2 == "X":
                ans = -1
            else:
                ans = 1
        elif s1 == "V":
            ans = 5
        elif s1 == "X":
            if s2 == "L" or s2 == "C":
                ans = -10
            else:
                ans = 10
        elif s1 == "L":
            ans = 50
        elif s1 == "C":
            if s2 == "D" or s2 == "M":
                ans = -100
            else:
                ans = 100
        elif s1 == "D":
            ans = 500
        elif s1 == "M":
            ans = 1000
        return ans

class Solution:
    def romanToInt(self, s: str) -> int:
        n = len(s)
        ans = 0
        for i in range(n-1):
            ans += calculate(s[i], s[i+1])
        ans += calculate(s[-1], "P")   
        
        return ans
    
```

예외인 경우를 고려하여 계산하는 함수를 만든 뒤, For를 돌려서 진행하였다. 연속하는 2문자를 계산해야하므로 마지막값은 indexerror를 피하기 위해 따로 상관없는 스트링과 계산을 진행하였다.

### 다른 풀이

```python
class Solution:
# @param {string} s
# @return {integer}
def romanToInt(self, s):
    roman = {'M': 1000,'D': 500 ,'C': 100,'L': 50,'X': 10,'V': 5,'I': 1}
    z = 0
    for i in range(0, len(s) - 1):
        if roman[s[i]] < roman[s[i+1]]:
            z -= roman[s[i]]
        else:
            z += roman[s[i]]
    return z + roman[s[-1]]
```

dict을 활용하여 로마문자에 숫자를 대입하였다.  그리고 for문을 활용하면서 연속하는 두 문자를 비교하고 값을 계산한다. 마지막 문자는 비교대상이 없으므로 리턴시 추가하여 리턴한다.