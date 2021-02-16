---
title: "[Algorithm] 위상 정렬 알고리즘"
categories: 
- Algorithm
tags:
- Graph Algorithm
- Topology Sort Algorithm
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 위상 정렬

### 위상 정렬

<span style = "color:red">사이클이 없는 방향 그래프</span>의 모든 노드를 **방향성에 거스르지 않도록 순서대로 나열**하는 것을 의미한다.

**예시)** 선수과목을 고려한 학습 순서 설정

![image](https://user-images.githubusercontent.com/48538655/108007860-4b651400-7042-11eb-9589-3530c52b2da8.png)

### 진입차수와 진출차수

**진입차수(Indegree):** 특정한 노드로 들어오는 간선의 개수

**진출차수(Outdegree):** 특정한 노드에서 나가는 간선의 개수

![image](https://user-images.githubusercontent.com/48538655/108008015-ae56ab00-7042-11eb-9dec-db304c4e8b5b.png)

### 위상 정렬 알고리즘

**큐**를 이용하는 **위상 정렬 알고리즘의 동작 과정**은 다음과 같다.

1. 진입차수가 0인 모든 노드를 큐에 넣는다.

2. 큐가 빌 때까지 다음의 과정을 반복한다.

   1) 큐에서 원소를 꺼내 해당 노드에서 나가는 간선을 그래프에서 제거한다.

   2) 새롭게 진입차수가 0이 된 노드를 큐에 넣는다.

결과적으로 **각 노드가 큐에 들어온 순서가 위상 정렬을 수행한 결과**와 같다.

### 위상 정렬 동작 예시

위상 정렬을 수행할 그래프를 준비한다.

이때 그래프는 **사이클이 없는 방향 그래프 (DAG)**여야 한다. 

![image](https://user-images.githubusercontent.com/48538655/108014861-38f2d680-7052-11eb-8c1e-7ca8b459f80c.png)

![image](https://user-images.githubusercontent.com/48538655/108041739-4fb12180-7082-11eb-84a5-6bd0cca454ef.png)

![image](https://user-images.githubusercontent.com/48538655/108041844-6fe0e080-7082-11eb-9952-c8eef12dd124.png)

![image](https://user-images.githubusercontent.com/48538655/108041888-7c653900-7082-11eb-8047-c5964ac8ba8a.png)

![image](https://user-images.githubusercontent.com/48538655/108042071-afa7c800-7082-11eb-80ad-cee2f71d5e2b.png)

![image](https://user-images.githubusercontent.com/48538655/108042133-c3ebc500-7082-11eb-8564-76975e86a921.png)

![image](https://user-images.githubusercontent.com/48538655/108042199-d7972b80-7082-11eb-933a-d3ac72732184.png)

![image](https://user-images.githubusercontent.com/48538655/108042249-e978ce80-7082-11eb-8108-3b690c143712.png)

![image](https://user-images.githubusercontent.com/48538655/108042298-f4cbfa00-7082-11eb-888f-976098d3d44f.png)

![image](https://user-images.githubusercontent.com/48538655/108042396-1200c880-7083-11eb-8b7f-46cc7aa107d1.png)

### 위상 정렬의 특징

위상 정렬은 DAG에 대해서만 수행할 수 있다.

- **DAG (Direct Acyclic Graph)**: 순환하지 않는 방향 그래프

위상 정렬에서는 **여러 가지 답이 존재**할 수 있다.

- 한 단계에서 큐에 새롭게 들어가는 원소가 2개 이상인 경우가 있다면 여러 가지 답이 존재한다.

**모든 원소를 방문하기 전에 큐가 빈다면 사이클이 존재**한다고 판단할 수 있다.

- 사이클에 포함된 원소 중에서 어떠한 원소도 큐에 들어가지 못한다.

스택을 활용한 DFS를 이용해 위상 정렬을 수행할 수도 있다.

### 위상 정렬 알고리즘 코드

```python
from collections import deque

# 노드의 개수와 간선의 개수를 입력 받기
v, e = map(int, input().split())
# 모든 노드에 대한 진입차수는 0으로 초기화
indegree = [0] * (v + 1)
# 각 노드에 연결된 간선 정보를 담기 위한 연결 리스트 초기화
graph = [[] for i in range(v + 1)]

# 방향 그래프의 모든 간선 정보를 입력 받기
for _ in range(e):
    a, b = map(int, input().split())
    graph[a].append(b) # A에서 B로 이동 가능
    # 진입 차수를 1 증가
    indegree[b] += 1
    
# 위상 정렬 함수
def topology_sort():
    result = [] # 알고리즘 수행 결과를 담을 리스트
    q = deque() # 큐 기능을 위한 deque 라이브러리 사용
    # 처음 시작할 때는 진입차수가 0인 노드를 큐에 삽입
    for i in range(1, v + 1):
        if indegree[i] == 0:
            q.append(i)
    # 큐가 빌 때까지 반복
    while q:
        # 큐에서 원소 꺼내기
        now = q.popleft()
        result.append(now)
        # 해당 원소와 연결된 노드들의 진입차수에서 1 빼기
        for i in graph[now]:
            indegree[i] -= 1
            # 새롭게 진입차수가 0이 되는 노드를 큐에 삽입
            if indegree[i] == 0:
                q.append(i)
    # 위상 정렬을 수행한 결과 출력
    for i in result:
        print(i, end=' ')
topology_sort()
```

실행 결과는 다음과 같다.

```
Input:
7 8
1 2
1 5
2 3
2 6
3 4
4 7
5 6
6 4
Output:
1 2 5 3 6 4 7
```

### 위상 정렬 알고리즘 성능 분석

위상 정렬을 위해 차례대로 모든 노드를 확인하며 각 노드에서 나가는 간선을 차례대로 제거해야 한다.

- 위상 정렬 알고리즘의 시간 복잡도는 $O(V + E)$이다.

## 참고 자료

이것이 취업을 위한 코딩테스트다. (나동빈 저)

[관련동영상](https://www.youtube.com/watch?v=aOhhNFTIeFI)

