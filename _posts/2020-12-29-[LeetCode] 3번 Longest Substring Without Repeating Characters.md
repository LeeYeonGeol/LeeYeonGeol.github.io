---
title: "[LeetCode] 3번 Longest Substring Without Repeating Characters"
categories: 
- LeetCode
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given a string `s`, find the length of the **longest substring** without repeating characters.

## 예제

**Example 1:**

```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

**Example 2:**

```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

**Example 3:**

```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

**Example 4:**

```
Input: s = ""
Output: 0
```

## 조건

> **Constraints:**
>
> - `0 <= s.length <= 5 * 104`
> - `s` consists of English letters, digits, symbols and spaces.

## 풀이과정

### 내가 실패한 방식

1. 알파벳이 나오는지 여부를 세기 위해서 [0]*26 리스트 생성
2. 인풋 스트링 for문돌려서 1.에서 생성된 리스트에 체크
3. 0이 아닌 부분만 뽑아서 부분집합만들고 기존 인풋에 들어가는지 확인

> __문제점?__
>
> 알파벳을 위해서는 아스키 코드로 체크해야했는데, 다른 digit, symbol, space를 고려하지 않음.
>
> __해결방법__
>
> 따라서 어떤 문자가 오든지 조건을 만족할 수 있는 알고리즘을 만들어야 한다.

## Approach 1. Brute Force

Solution의 자바 코드를 참고하여 파이썬으로 작성하였다.

```python
def allUnique(s: str, start:int, end:int):
  s1 = set([])
  for i in range(start, end):
    if s[i] in s1:
      return False
    s1.add(s[i])
  return True

class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        n = len(s)
        ans = 0
        for i in range(0,n):
            for j in range(i+1,n+1):
            # n이 6이라면
            # 0 1, 0 2, ..., 0 6
    		# 1 2, ..., 1 6
    		# 2 3, ..., 2 6
    		# ...
    		# 5 6 
                if (allUnique(s,i,j)):
                    ans = max(ans, j-i)
        return(ans)
    
```

기본적인 틀은 다음과 같다.

1. 우선 for문을 2중으로 중첩하여 substring이 나오는 모든 경우의 수를 가정한다.
2. 그 후 if문에서 allUnique를 수행한다. 
3. allUnique가 true라면 ans를 업데이트해준다.

allUnique 함수에 대해서 보자.

1. s1이라는 집합을 선언. (순서에 상관없이 중복을 잡아내기 위해서)

2. 중복이 있다면 False를 return하고 그렇지 않으면 True를 return한다.

allUnique 함수로 인해 모든 substring에 대해 중복을 검사할 수 있고 이를 인해 문제가 해결된다.

### 문제점

> 자바를 파이썬으로 바꾸다보니 로직은 맞는거 같은데 시간부족문제가 생김.

### 요약

> 모든 substring에 대해 중복 여부를 검사하고 답을 업데이트하는 방식이다.

## Approach 2: Sliding Window

Approach 1은 매우 무식한 방식이다. 따라서 이를 최적화하여야 한다. 

기본적인 생각은 이렇다. 모든 substring을 다 check한다면 중복이 생길 수 있다. 이를 해결하기 위함이다.

만약 substring이 기존 string의 i번째에서 j번째라고 하자. i에서 j-1까지는 이미 중복에 대해 체크되어있다면 j에 대해서만 체크하면 된다.

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        n = len(s)
        s1 = set([])
        ans = 0
        i = 0
        j = 0
        while (i < n and j < n):
            if  s[j] in s1:
                s1.remove(s[i])
                i += 1
            else:
                s1.add(s[j])
                j += 1
                ans = max(ans, j-i)
        return(ans)
    
```

1. Approach 1과 마찬가지로, 집합 s1을 선언한다.
2. i-0, j=0로 선언.
3. s1에 s[j]가 있다면 s[i]를 제거하고 i를 1만큼 증가
4. s1에 s[j]가 없다면 s[j]를 s1에 추가하고 j를 1만큼 증가
5. 3,4를 i혹은 j가 n이 될때까지 반복

### 요약

> 불필요한 연산을 줄여서 시간부족문제는 해결되었다.

## Approach 3: Sliding Window Optimized

추후 업데이트 예정.