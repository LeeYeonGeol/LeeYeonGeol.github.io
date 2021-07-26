---
title: "[LeetCode] Jewels and Stones"
categories: 
- LeetCode
tags:
- 해시
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

You're given strings `jewels` representing the types of stones that are jewels, and `stones` representing the stones you have. Each character in `stones` is a type of stone you have. You want to know how many of the stones you have are also jewels.

Letters are case sensitive, so `"a"` is considered a different type of stone from `"A"`.

## 예제

**Example 1:**

```
Input: jewels = "aA", stones = "aAAbbbb"
Output: 3
```

**Example 2:**

```
Input: jewels = "z", stones = "ZZ"
Output: 0
```

## 조건

- `1 <= jewels.length, stones.length <= 50`
- `jewels` and `stones` consist of only English letters.
- All the characters of `jewels` are **unique**.

## 답 

### 풀이 1

Counter를 활용한 내 풀이

```python
class Solution:
    def numJewelsInStones(self, jewels: str, stones: str) -> int:
        ans = 0
        cnt = collections.Counter(stones)
        for i in jewels:
            ans += cnt[i]
        return ans
```

### 풀이 2

해시 테이블을 이용한 풀이

```python
class Solution:
    def numJewelsInStones(self, jewels: str, stones: str) -> int:
        freqs = {}
        count = 0
        
        for char in stones:
            if char not in freqs:
                freqs[char] = 1
            else:
                freqs[char] += 1
        
        # 보석의 빈도 수 합산
        for char in jewels:
            if char in freqs:
                count += freqs[char]
        
        return count
```

### 풀이 3

defaultdict를 이용한 풀이

```python
class Solution:
    def numJewelsInStones(self, jewels: str, stones: str) -> int:
        freqs = collections.defaultdict(int)
        count = 0
        
        # 비교 없이 돌(S) 빈도 수 계산
        for char in stones:
            freqs[char] += 1
        
        # 비교 없이 보석(J) 빈도 수 합산
        for char in jewels:
            count += freqs[char]
            
        return count
```

### 풀이 4

파이썬다운 방식

```python
class Solution:
    def numJewelsInStones(self, jewels: str, stones: str) -> int:
        return sum(s in jewels for s in stones)
```









