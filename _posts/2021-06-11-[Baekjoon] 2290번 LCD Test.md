---
title: "[Baekjoon] LCD Test"
categories: 
- Baekjoon
tags:
- 구현
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
comments: true
---

## 문제

지민이는 새로운 컴퓨터를 샀다. 하지만 새로운 컴퓨터에 사은품으로 온 LC-디스플레이 모니터가 잘 안나오는 것이다. 지민이의 친한 친구인 지환이는 지민이의 새로운 모니터를 위해 테스트 할 수 있는 프로그램을 만들기로 하였다.

## 입력

첫째 줄에 두 개의 정수 s와 n이 들어온다. (1 ≤ s ≤ 10, 0 ≤ n ≤ 9,999,999,999)이다. n은 LCD 모니터에 나타내야 할 수 이며, s는 크기이다.

## 출력

길이가 s인 '`-`'와 '`|`'를 이용해서 출력해야 한다. 각 숫자는 모두 s+2의 가로와 2s+3의 세로로 이루어 진다. 나머지는 공백으로 채워야 한다. 각 숫자의 사이에는 공백이 한 칸 있어야 한다.

## 예제

**Example 1:**

```
Input: 
2 1234567890
Output: 
      --   --        --   --   --   --   --   --  
   |    |    | |  | |    |       | |  | |  | |  | 
   |    |    | |  | |    |       | |  | |  | |  | 
      --   --   --   --   --        --   --       
   | |       |    |    | |  |    | |  |    | |  | 
   | |       |    |    | |  |    | |  |    | |  | 
      --   --        --   --        --   --   --  
```

## 조건

> 시간 제한 : 2초
>
> 메모리 제한 : 128 MB

## 풀이과정

### 풀이 1

```python
s, n = map(int, input().split())

n = str(n)
m = 2*s+3

ans = [[" "]*((s+2)*(len(n))+(len(n)-1)) for _ in range(m)]

st = 0
for i in n:
    if i == '1':
        st += s+1
        for j in range(1, 1+s):
            ans[j][st] = "|"
        for j in range(2+s, m-1):
            ans[j][st] = "|"
        st += 2
    elif i == '2':
        for j in range(2+s, m-1):
            ans[j][st] = "|"
        st += 1
        for _ in range(s):
            ans[0][st], ans[(m-1)//2][st], ans[m-1][st] = "-", "-", "-"
            st += 1

        for j in range(1, 1+s):
            ans[j][st] = "|"
        st += 2
    elif i == '3':
        st += 1
        for _ in range(s):
            ans[0][st], ans[(m-1)//2][st], ans[m-1][st] = "-", "-", "-"
            st += 1

        for j in range(1, 1+s):
            ans[j][st] = "|"
        for j in range(2+s, m-1):
            ans[j][st] = "|"
        st += 2
    elif i == '4':
        for j in range(1, 1+s):
            ans[j][st] = "|"
        st += 1
        for _ in range(s):
            ans[(m-1)//2][st]= "-"
            st += 1
        for j in range(1, 1+s):
            ans[j][st] = "|"
        for j in range(2+s, m-1):
            ans[j][st] = "|"
        st += 2
    elif i == '5':
        for j in range(1, 1+s):
            ans[j][st] = "|"
        st += 1
        for _ in range(s):
            ans[0][st], ans[(m-1)//2][st], ans[m-1][st] = "-", "-", "-"
            st += 1
        for j in range(2+s, m-1):
            ans[j][st] = "|"
        st += 2
    elif i == '6':
        for j in range(1, 1+s):
            ans[j][st] = "|"
        for j in range(2+s, m-1):
            ans[j][st] = "|"
        st += 1
        for _ in range(s):
            ans[0][st], ans[(m-1)//2][st], ans[m-1][st] = "-", "-", "-"
            st += 1
        for j in range(2+s, m-1):
            ans[j][st] = "|"
        st += 2
    elif i == '7':
        st += 1
        for _ in range(s):
            ans[0][st] = "-"
            st += 1
        for j in range(1, 1+s):
            ans[j][st] = "|"
        for j in range(2+s, m-1):
            ans[j][st] = "|"
        st += 2
    elif i == '8':
        for j in range(1, 1+s):
            ans[j][st] = "|"
        for j in range(2+s, m-1):
            ans[j][st] = "|"
        st += 1
        for _ in range(s):
            ans[0][st], ans[(m-1)//2][st], ans[m-1][st] = "-", "-", "-"
            st += 1
        for j in range(1, 1+s):
            ans[j][st] = "|"
        for j in range(2+s, m-1):
            ans[j][st] = "|"
        st += 2
    elif i == '9':
        for j in range(1, 1+s):
            ans[j][st] = "|"
        st += 1
        for _ in range(s):
            ans[0][st], ans[(m-1)//2][st], ans[m-1][st] = "-", "-", "-"
            st += 1
        for j in range(1, 1+s):
            ans[j][st] = "|"
        for j in range(2+s, m-1):
            ans[j][st] = "|"
        st += 2
    else:
        for j in range(1, 1+s):
            ans[j][st] = "|"
        for j in range(2+s, m-1):
            ans[j][st] = "|"
        st += 1
        for _ in range(s):
            ans[0][st], ans[m-1][st] = "-", "-"
            st += 1
        for j in range(1, 1+s):
            ans[j][st] = "|"
        for j in range(2+s, m-1):
            ans[j][st] = "|"
        st += 2
for a in ans:
    print("".join(a))
```

