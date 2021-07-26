---
title: "[Baekjoon] 1260번 DFS와 BFS"
categories: 
- Baekjoon
tags:
- DFS/BFS
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

그래프를 DFS로 탐색한 결과와 BFS로 탐색한 결과를 출력하는 프로그램을 작성하시오. 단, 방문할 수 있는 정점이 여러 개인 경우에는 정점 번호가 작은 것을 먼저 방문하고, 더 이상 방문할 수 있는 점이 없는 경우 종료한다. 정점 번호는 1번부터 N번까지이다.

## 입력

첫째 줄에 정점의 개수 N(1 ≤ N ≤ 1,000), 간선의 개수 M(1 ≤ M ≤ 10,000), 탐색을 시작할 정점의 번호 V가 주어진다. 다음 M개의 줄에는 간선이 연결하는 두 정점의 번호가 주어진다. 어떤 두 정점 사이에 여러 개의 간선이 있을 수 있다. 입력으로 주어지는 간선은 양방향이다.

## 출력

첫째 줄에 DFS를 수행한 결과를, 그 다음 줄에는 BFS를 수행한 결과를 출력한다. V부터 방문된 점을 순서대로 출력하면 된다.

## 예제

**Example 1:**

```
Input: 
4 5 1
1 2
1 3
1 4
2 4
3 4
Output: 
1 2 4 3
1 2 3 4
```

**Example 2:**

```
Input:
5 5 3
5 4
5 2
1 2
3 4
3 1
Output:
3 1 2 5 4
3 1 4 2 5
```

**Example 3:**

```
Input:
1000 1 1000
999 1000
Output:
1000 999
1000 999
```

## 조건

> 시간 제한 : 2초
>
> 메모리 제한 : 128 MB

## 풀이과정

### 풀이

```python
from collections import deque
# DFS 메서드 정의
def dfs(graph, v, visited):
  # 현재 노드를 방문 처리
  visited[v] = True
  print(v, end= ' ')
  # 현재 노드와 연결된 다른 노드를 재귀적으로 방문
  for i in graph[v]:
    if not visited[i]:
      dfs(graph, i, visited)
# BFS 메서드 정의
def bfs(graph, start, visited):
  # 큐(Queue) 구현을 위해 deque 라이브러리 사용
  queue = deque([start])
  # 현재 노드를 방문 처리
  visited[start] = True
  # 큐가 빌 때까지 반복
  while queue:
    # 큐에서 하나의 원소를 뽑아 출력
    v = queue.popleft()
    print(v, end= ' ')
    # 해당 원소와 연결된, 아직 방문하지 않은 원소들을 큐에 삽입
    for i in graph[v]:
      if not visited[i]:
        queue.append(i)
        visited[i] = True
# 정점의 개수 N, 간선의 개수 M, 탐색을 시작할 정점의 번호 V 입력
N, M, V = map(int,input().split())

graph =[]

# 크기가 N+1인 리스트 생성 
for i in range(N+1):
  graph.append([])

# 간선에 대한 정보를 그래프에 삽입
for i in range(M):
  a, b = map(int,input().split())
  graph[a].append(b)
  graph[b].append(a)

# 정점 번호가 작은 것을 먼저 방문하므로 sort해준다.
for i in graph:
  i.sort()

# 각 노드가 방문된 정보를 리스트 자료형으로 표현 (1차원 리스트)
visited1 = [False]*(N+1)
visited2 = [False]*(N+1)

# 정의된 DFS, BFS함수 호출
dfs(graph,V,visited1)
print('')
bfs(graph,V,visited2)
```

