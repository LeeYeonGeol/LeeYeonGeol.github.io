---
title: "[LeetCode] 7번 Reverse Integer"
categories: 
- LeetCode
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given a 32-bit signed integer, reverse digits of an integer.

**Note:**
Assume we are dealing with an environment that could only store integers within the 32-bit signed integer range: [−231, 231 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

## 예제

**Example 1:**

```
Input: x = 123
Output: 321
```

**Example 2:**

```
Input: x = -123
Output: -321
```

**Example 3:**

```
Input: x = 120
Output: 21
```

**Example 4:**

```
Input: x = 0
Output: 0
```

## 조건

> **Constraints:**
>
> - `-2^31 <= x <= 2^31 - 1`

## 풀이과정

### 내 풀이

```python
class Solution:
    def reverse(self, x: int) -> int:
        # Input값을 리스트로 쪼개기
        list_str = list(str(x))
        answer = ""

        if list_str[0] == '-':
            list_str.reverse()
            answer = list_str[-1]+"".join(list_str[:-1])
        else:
            list_str.reverse()
            answer = "".join(list_str[:])
            
        # int값 제한
        if -2147483648 <= int(answer) <= 2147483647:
            return (int(answer))
        else:
            return (0)
```

string을 리스트로 변환하고 음수인 경우와 그렇지 않은 경우로 나누어서 진행하였다. reverse를 해주고 int값 제한에 맞추어 리턴하였다.

### 다른 풀이

```python
def reverse(self, x: int) -> int:
        rev = int(str(abs(x))[::-1])
        return (-rev if x < 0 else rev) if rev.bit_length() < 32 else 0
```

abs를 활용해서 절대값을 만들어주고 스트링으로 형변환을 한 뒤, [::-1]을 활용하여 reverse를 수행하고 int로 rev에 값을 넣어준다.

부호에 따라 rev를 리턴해준다. 그리고 bit_length함수를 통해 제약을 맞추어준다.