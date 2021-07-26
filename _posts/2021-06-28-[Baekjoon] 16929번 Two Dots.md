---
title: "[Baekjoon] Two Dots"
categories: 
- Baekjoon
tags:
- 그래프 이론
- 그래프 탐색
- 깊이 우선 탐색
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
comments: true
---

## 문제

[Two Dots](https://www.dots.co/twodots/)는 Playdots, Inc.에서 만든 게임이다. 게임의 기초 단계는 크기가 N×M인 게임판 위에서 진행된다.

![img](https://upload.acmicpc.net/6a0e30d5-c325-40e4-b8b2-e5878b8dbc49/-/preview/)

각각의 칸은 색이 칠해진 공이 하나씩 있다. 이 게임의 핵심은 같은 색으로 이루어진 사이클을 찾는 것이다.

다음은 위의 게임판에서 만들 수 있는 사이클의 예시이다.

| ![img](https://upload.acmicpc.net/33712230-43d5-45f7-8b2d-dcb21b9c602c/-/preview/) | ![img](https://upload.acmicpc.net/93730ab5-3ecf-4553-a411-50c22aa1e413/-/preview/) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              |                                                              |

점 k개 d1, d2, ..., dk로 이루어진 사이클의 정의는 아래와 같다.

- 모든 k개의 점은 서로 다르다. 
- k는 4보다 크거나 같다.
- 모든 점의 색은 같다.
- 모든 1 ≤ i ≤ k-1에 대해서, di와 di+1은 인접하다. 또, dk와 d1도 인접해야 한다. 두 점이 인접하다는 것은 각각의 점이 들어있는 칸이 변을 공유한다는 의미이다.

게임판의 상태가 주어졌을 때, 사이클이 존재하는지 아닌지 구해보자.

## 입력

첫째 줄에 게임판의 크기 N, M이 주어진다. 둘째 줄부터 N개의 줄에 게임판의 상태가 주어진다. 게임판은 모두 점으로 가득차 있고, 게임판의 상태는 점의 색을 의미한다. 점의 색은 알파벳 대문자 한 글자이다.

## 출력

사이클이 존재하는 경우에는 "Yes", 없는 경우에는 "No"를 출력한다.

## 제한

- 2 ≤ N, M ≤ 50

## 예제

**Example 1:**

```
Input: 
3 4
AAAA
ABCA
AAAA
Output: 
Yes
```

**Example 2:**

```
Input:
3 4
AAAA
ABCA
AADA
Output:
No
```

**Example 3:**

```
Input:
4 4
YYYR
BYBY
BBBY
BBBY
Output:
Yes
```

**Example 4:**

```
Input:
7 6
AAAAAB
ABBBAB
ABAAAB
ABABBB
ABAAAB
ABBBAB
AAAAAB
Output:
Yes
```

**Example 5:**

```
Input:
2 13
ABCDEFGHIJKLM
NOPQRSTUVWXYZ
Output:
No
```

## 조건

> 시간 제한 : 2초
>
> 메모리 제한 : 512 MB

## 풀이과정

### 풀이 1

```python
import sys

n, m = map(int, input().split())

graph = []

for _ in range(n):
    graph.append(list(input()))

dx = [0,1,0,-1]
dy = [1,0,-1,0]

def dfs(x,y,level,visited):
    for k in range(4):
        nx = x + dx[k]
        ny = y + dy[k]
        if 0 <= nx < n and 0 <= ny < m and graph[x][y] == graph[nx][ny]:
            if level < 3:
                if not (nx,ny) in visited:
                    dfs(nx,ny,level+1,visited+[(nx,ny)])
            else:
                if not (nx, ny) in visited:
                    dfs(nx,ny,level+1,visited+[(nx,ny)])
                else:
                    if visited[0] == (nx, ny):
                        print("Yes")
                        sys.exit()

for a in range(n):
    for b in range(m):
        dfs(a,b,1,[(a,b)])

print("No")
```



