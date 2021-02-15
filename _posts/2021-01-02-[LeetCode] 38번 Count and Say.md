---
title: "[LeetCode] 38번 Count and Say"
categories: 
- LeetCode
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

The **count-and-say** sequence is a sequence of digit strings defined by the recursive formula:

- `countAndSay(1) = "1"`
- `countAndSay(n)` is the way you would "say" the digit string from `countAndSay(n-1)`, which is then converted into a different digit string.

To determine how you "say" a digit string, split it into the **minimal** number of groups so that each group is a contiguous section all of the **same character.** Then for each group, say the number of characters, then say the character. To convert the saying into a digit string, replace the counts with a number and concatenate every saying.

For example, the saying and conversion for digit string `"3322251"`:

![img](https://assets.leetcode.com/uploads/2020/10/23/countandsay.jpg)

Given a positive integer `n`, return *the* `nth` *term of the **count-and-say** sequence*.

## 예제

**Example 1:**

```
Input: n = 1
Output: "1"
Explanation: This is the base case.
```

**Example 2:**

```
Input: n = 4
Output: "1211"
Explanation:
countAndSay(1) = "1"
countAndSay(2) = say "1" = one 1 = "11"
countAndSay(3) = say "11" = two 1's = "21"
countAndSay(4) = say "21" = one 2 + one 1 = "12" + "11" = "1211"
```

## 조건

> **Constraints:**
>
> - `1 <= n <= 30`

## 풀이과정

### 내 풀이

```python
class Solution:
    
    def countAndSay(self, n: int) -> str:
        if n == 1:
            return "1"
        else:
            s = "11"
            for i in range(2,n):
                s = str(self.countt(s))
        return s

    def countt(self, s:str) -> int:
        ans = ""
        count = 1
        for i in range(len(s)-1):
            if s[i] == s[i+1]:
                count +=1
            else:
                ans += str(count)+str(s[i])
                count = 1
        if i == len(s)-2:
            ans += str(count)+str(s[i+1])
  
        return ans
```

숫자로된 string이 들어오면 그에 맞게 count and say값을 반환해주는 함수를 만들어준다. 그 후, 문제에 맞게 함수를 사용한다.

### 다른 풀이

```python
class Solution:
    
    def countAndSay(self, n):
        s = '1'
        for _ in range(n - 1):
            s = ''.join(str(len(list(group))) + digit for digit, group in itertools.groupby(s))
            print(s)
        return s
```

