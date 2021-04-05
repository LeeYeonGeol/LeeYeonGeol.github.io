---
title: "[Baekjoon] 9663번 N-Queen"
categories: 
- Baekjoon
tags:
- 브루트포스 알고리즘
- 백트래킹
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
comments: true
---

## 문제

N-Queen 문제는 크기가 N × N인 체스판 위에 퀸 N개를 서로 공격할 수 없게 놓는 문제이다.

N이 주어졌을 때, 퀸을 놓는 방법의 수를 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에 N이 주어진다. (1 ≤ N < 15)

## 출력

첫째 줄에 퀸 N개를 서로 공격할 수 없게 놓는 경우의 수를 출력한다.

## 예제

**Example 1:**

```
Input: 
8
Output: 
92
```

## 조건

> 시간 제한 : 10초
>
> 메모리 제한 : 128 MB

## 풀이과정

### 내 풀이

재귀를 이용한 백트래킹 기법으로 해결하였다. 처음에는 함수에서 arr을 생성해서 진행하였는데 시간초과가 떠서 아예 함수밖에 선언하고 하니 시간초과문제가 해결되었다.

```python
n = int(input())

result = 0

arr = [0]*n

def recursive(x):
    global result

    for j in range(x-1):
        if arr[j] == arr[x-1]  or abs(arr[j]-arr[x-1]) == abs(x-1-j):
            return

    if x >= n:
        result += 1
        return
    else:
        for i in range(n):
            arr[x] = i
            recursive(x+1)

recursive(0)

print(result)
```

