---
title: "[Algorithm] 최단 경로 알고리즘"
categories: 
- Algorithm
tags:
- Shortest Path Algorithm
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 최단 경로 문제

최단 경로 알고리즘은 **가장 짧은 경로를 찾는 알고리즘**을 의미한다.

**다양한 문제 상황**

- 한 지점에서 다른 한 지점까지의 최단 경로
- 한 지점에서 다른 모든 지점까지의 최단 경로
- 모든 지점에서 다른 모든 지점까지의 최단 경로

각 지점은 그래프에서 <span style="color:red">노드</span>로 표현

지점 간 연결된 도로는 그래프에서 <span style="color:red">간선</span>으로 표현

![Shortestpath1](https://user-images.githubusercontent.com/48538655/107150371-d5f1a780-69a0-11eb-9915-2f206a2b75a9.JPG)

## 다익스트라 최단 경로 알고리즘 개요

**특정한 노드**에서 출발하여 **다른 모든 노드**로 가는 최단 경로를 계산한다. 

다익스트라 최단 경로 알고리즘은 음의 간선이 없을 때 정상적으로 동작한다. 현실 세계의 도로(간선)은 음의 간선으로 표현되지 않는다.

다익스트라 최단 경로 알고리즘은 그리디 알고리즘으로 분류된다.

**매 상황에서 가장 비용이 적은 노드를 선택**해 임의의 과정을 반복한다.

## 다익스트라 동작 과정

1. 출발 노드를 설정한다.
2. 최단 거리 테이블을 초기화한다.
3. 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택한다.
4. 해당 노드를 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블을 갱신한다.
5. 위 과정에서 3번과 4번을 반복한다.

알고리즘 동작 과정에서 최단 거리 테이블은 각 노드에 대한 현재까지의 최단 거리 정보를 가지고 있다. 처리 과정에서 더 짧은 경로를 찾으면 '이제부터는 이 경로가 제일 짧은 경로야'라고 갱신한다.

## 다익스트라 알고리즘: 동작 과정 살펴보기

![다익스트라1](https://user-images.githubusercontent.com/48538655/107196246-ba84ac00-6a35-11eb-97dd-1e4eb6b8d527.JPG)

![다익스트라2](https://user-images.githubusercontent.com/48538655/107196386-e99b1d80-6a35-11eb-8ba9-4ebf2e3393c2.JPG)

![다익스트라3](https://user-images.githubusercontent.com/48538655/107196689-472f6a00-6a36-11eb-92e3-b0dece7752e1.JPG)

![다익스트라4](https://user-images.githubusercontent.com/48538655/107196967-a7261080-6a36-11eb-9233-5d3724d79c99.JPG)

![다익스트라5](https://user-images.githubusercontent.com/48538655/107197126-d89edc00-6a36-11eb-95cc-87825490623a.JPG)

![image](https://user-images.githubusercontent.com/48538655/107197296-0f74f200-6a37-11eb-8ea9-49be4bd54061.png)

![image](https://user-images.githubusercontent.com/48538655/107197383-29163980-6a37-11eb-9a96-b39b1c3fe71e.png)

## 다익스트라 알고리즘의 특징

그리디 알고리즘: **매 상황에서 방문하지 않은 가장 비용이 적은 노드를 선택**해 임의의 과정을 반복한다. (여기서 임의의 과정이란, 해당 노드를 거쳐가는 각각의 경우를 확인해서 테이블을 갱신할지 안할지 결정하는 것을 의미)

단계를 거치며 <span style = "color:red">한 번 처리된 노드의 최단 거리는 고정</span>되어 더 이상 바뀌지 않는다.

- **한 단계당 하나의 노드에 대한 최단 거리를 확실히 찾는 것으로 이해**할 수 있다.

다익스트라 알고리즘을 수행한 뒤에 <u>테이블에 각노드까지의 최단 거리 정보가 저장</u>된다.

- 완벽한 형태의 최단 경로를 구하려면 소스코드에 추가적인 기능을 더 넣어야 한다.

## 다익스트라 알고리즘: 간단한 구현 방법

단계마다 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택하기 위해 **매 단계마다 1차원 테이블의 모든 원소를 확인(순차 탐색)**한다. 

```python
import sys
input = sys.stdin.readline
INF = int(1e9) # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수, 간선의 개수를 입력받기
n, m = map(int, input().split())
# 시작 노드 번호를 입력받기
start = int(input())
# 각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트를 만들기
graph = [[] for i in range(n + 1)]
# 방문한 적이 있는지 체크하는 목적의 리스트를 만들기
visited = [False] * (n + 1)
# 최단 거리 테이블을 모두 무한으로 초기화
distance = [INF] * (n + 1)

# 모든 간선 정보를 입력받기
for _ in range(m):
    a, b, c = map(int, input().split())
    # a번 노드에서 b번 노드로 가는 비용이 c라는 의미
    graph[a].append((b, c))
    
# 방문하지 않은 노드 중에서, 가장 최단 거리가 짧은 노드의 번호를 반환
def get_smallest_node():
    min_value = INF
    index = 0 # 가장 최단 거리가 짧은 노드(인덱스)
    for i in range(1, n + 1):
        if distance[i] < min_value and not visited[i]:
            min_value = distance[i]
            index = i
        return index
    
def dijkstra(start):
    # 시작 노드에 대해서 초기화
    distance[start] = 0
    visited[start] = True
    for j in graph[start]:
        distance[j[0]] = j[1]
    # 시작 노드를 제외한 전체 n - 1개의 노드에 대해 반복
    for i in range(n - 1):
        # 현재 최단 거리가 가장 짧은 노드를 꺼내서, 방문 처리
        now = get_smllest_node()
        visited[now] = True
        # 현재 노드와 연결된 다른 노드를 확인
        for j in graph[now]:
            cost = distnace[now] + j[1]
            # 현재 노드를 거쳐서 다른 노드로 이동하는 거리가 더 짧은 경우
            if cost < distance[j[0]]:
                distance[j[0]] = cost
                
# 다익스트라 알고리즘을 수행
dijkstra(start)

# 모든 노드로 가기 위한 최단 거리를 출력
for i in range(1, n + 1):
    # 도달할 수 없는 경우, 무한(INFINITY)이라고 출력
    if distance[i] = INF:
        print("INFINITY")
    # 도달할 수 있는 경우 거리를 출력
    else:
        print(distance[i])
```

## 다익스트라 알고리즘: 간단한 구현 방법 성능 분석

총 $O(V)$번에 걸쳐서 최단 거리가 가장 짧은 노드를 매번 선형 탐색해야 한다.

따라서 전체 시간 복잡도는 $O(V^2)$이다.

일반적으로 코딩 테스트의 최단 경로 문제에서 전체 노드의 개수가 5,000개 이하라면 이 코드로 문제를 해결할 수 있다.

- 하지만 노드의 개수가 10,000개를 넘어가는 문제라면 어떻게 해야 할까?

이를 위해 우선순위 큐 자료구조를 살펴본다.

## 우선순위 큐(Priority Queue)

<u>우선순위가 가장 높은 데이터를 가장 먼저 삭제</u>하는 자료구조이다.

예를 들어 여러 개으 ㅣ물건 데이터를 자료구조에 넣었다가 가치가 높은 물건 데이터부터 꺼내서 확인해야 하는 경우에 우선순위 큐를 이용할 수 있다.

Python, C++, Java를 포함한 대부분의 프로그래밍 언어에서 **표준 라이브러리 형태로 지원**한다.

| 자료구조                    | 추출되는 데이터             |
| --------------------------- | --------------------------- |
| 스택(Stack)                 | 가장 나중에 삽입된 데이터   |
| 큐(Queue)                   | 가장 먼저 삽입된 데이터     |
| 우선순위 큐(Priority Queue) | 가장 우선순위가 높은 데이터 |

## 힙(Heap)

<u>우선순위 큐(Priority Queue)를 구현하기 위해 사용하는 자료구조 중 하나</u>이다.

**최소 힙(Min Heap)**과 **최대 힙(Max Heap)**이 있다.

다익스트라 최단 경로 알고리즘을 포함해 다양한 알고리즘에서 사용된다.

| 우선순위 큐 구현 방식 | 삽입 시간   | 삭제 시간   |
| --------------------- | ----------- | ----------- |
| 리스트                | $O(1)$      | $O(N)$      |
| 힙(Heap)              | $O(log{N})$ | $O(log{N})$ |

## 힙 라이브러리 사용 예제: 최소 힙

```python
import heapq

# 오름차순 힙 정렬(Heap Sort)
def heapsort(iterable):
    h = []
    result = []
    # 모든 원소를 차례대로 힙에 삽입
    for value in iterable:
        heapq.heappush(h, value)
    # 힙에 삽입된 모든 원소를 차례대로 꺼내어 담기
    for i in range(len(h)):
        result.append(heapq.heappop(h))
    return result

result = heapsort([1, 3, 5, 7, 9, 2, 4, 6, 8, 0])
print(result)
```

실행 결과는 다음과 같다.

```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## 힙 라이브러리 사용 예제: 최대 힙

```python
import heapq

# 내림차순 힙 정렬(Heap Sort)
def heapsort(iterable):
    h = []
    result = []
    # 모든 원소를 차례대로 힙에 삽입
    for value in iterable:
        heapq.heappush(h, -value)
    # 힙에 삽입된 모든 원소를 차례대로 꺼내어 담기
    for i in range(len(h)):
        result.append(-heapq.heappop(h))
    return result

result = heapsort([1, 3, 5, 7, 9, 2, 4, 6, 8, 0])
print(result)
```

실행 결과는 다음과 같다.

```
[9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```

## 다익스트라 알고리즘: 개선된 구현 방법

단계마다 <u>방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택</u>하기 위해 **힙(Heap)** 자료구조를 이용한다.

다익스트라 알고리즘이 동작하는 **기본 원리는 동일**하다.

- 현재 가장 가까운 노드를 저장해 놓기 위해서 힙 자료구조를 추가적으로 이용한다는 점이 다르다.
- 현재의 최단 거리가 가장 짧은 노드를 선택해야 하므로 최소 힙을 사용한다.

## 다익스트라 알고리즘: 동작 과정 살펴보기 (우선순위 큐)

![image](https://user-images.githubusercontent.com/48538655/107230824-e2d6cf80-6a62-11eb-9985-d8763b5a0c50.png)

![image](https://user-images.githubusercontent.com/48538655/107231064-2cbfb580-6a63-11eb-9005-c05608bcae68.png)

![image](https://user-images.githubusercontent.com/48538655/107231249-6a244300-6a63-11eb-92a4-084f9806f64b.png)

![image](https://user-images.githubusercontent.com/48538655/107231404-9f309580-6a63-11eb-9102-7e3cde9453a8.png)

![image](https://user-images.githubusercontent.com/48538655/107231569-cbe4ad00-6a63-11eb-913a-b482a4512414.png)

![image](https://user-images.githubusercontent.com/48538655/107231709-f46ca700-6a63-11eb-85c1-ff912636db2b.png)

![image](https://user-images.githubusercontent.com/48538655/107231768-064e4a00-6a64-11eb-80e7-57a65d2e48c2.png)

![image](https://user-images.githubusercontent.com/48538655/107232022-4a414f00-6a64-11eb-9060-b8c9a9bb37a5.png)

![image](https://user-images.githubusercontent.com/48538655/107233080-845f2080-6a65-11eb-89a3-56422154d1b2.png)

## 다익스트라 알고리즘: 개선된 구현 방법 (Python)

```python
import heapq
import sys
input = sys.stdin.readline
INF = int(1e9) # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수, 간선의 개수를 입력받기
n, m = map(int, input().split())
# 시작 노드 번호를 입력받기
start = int(input())
# 각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트를 만들기
graph = [[] for i in range(n + 1)]
# 최단 거리 테이블을 모두 무한으로 초기화
distance = [INF] * (n + 1)

# 모든 간선 정보를 입력받기
for _ in range(m):
    a, b, c = map(int, input().split())
    # a번 노드에서 b번 노드로 가는 비용이 c라는 의미
    graph[a].append((b, c))
    
def dijkstra(start):
    q = []
    # 시작 노드로 가기 위한 최단 경로는 0으로 설정하여, 큐에 삽입
    heapq.heappush(q, (0, start))
    distance[start] = 0
    while q: # 큐가 비어있지 않다면
        # 가장 최단 거리가 짧은 노드에 대한 정보 꺼내기
        dist, now = heapq.heappop(q)
        # 현재 노드가 이미 처리된 적이 있는 노드라면 무시
        if distance[now] < dist:
            continue
        # 현재 노드와 연결된 다른 인접한 노드들을 확인
        for i in graph[now]:
            cost = dist + i[1]
            # 현재 노드를 거쳐서, 다른 노드로 이동하는 거리가 더 짧은 경우
            if cost < distance[i[0]]:
                distance[i[0]] = cost
                heapq.heappush(q, (cost, i[0]))
                
# 다익스트라 알고리즘을 수행
dijkstra(start)

# 모든 노드로 가기 위한 최단 거리를 출력
for i in range(1, n + 1):
    # 도달할 수 없는 경우, 무한(INFINITY)이라고 출력
    if distance[i] == INF:
        print("INFINITY")
    else:
        print(distance[i])
```

## 다익스트라 알고리즘: 개선된 구현 방법 성능 분석

힙 자료구조를 이용하는 다익스트라 알고리즘의 시간 복잡도는 $O(Elog{V})$이다.

노드를 하나씩 꺼내 검사하는 반복문(while문)은 노드의 개수 V 이상의 횟수로는 처리되지 않는다.

- 결과적으로 현재 우선순위 큐에서 꺼낸 노드와 연결된 다른 노드들을확인하는 총횟수는 최대 간선의 개수(E)만큼 연산이 수행될 수 있다.

직관적으로 <u>전체 과정은 E개의 원소를 우선순위 큐에 넣었다가 모두 빼내는 연산과 매우 유사</u>하다. 

- 시간 복잡도를 $O(Elog{E})$로 판단할 수 있다.
- 중복 간선을 포함하지 않는 경우에 이를 $O(Elog{V})$로 정리할 수 있다.

$$
O(ElogE) \rightarrow O(Elog{V^2}) \rightarrow O(2Elog{V}) \rightarrow O(Elog{V})
$$



## 플로이드 워셜 알고리즘 개요

<u>모든 노드에서 다른 모든 노드까지의 최단 경로를 모두 계산</u>한다.

플로이드 워셜(Floyd-Warshall) 알고리즘은 다익스트라 알고리즘과 마찬가지로 단계별로 **거쳐 가는 노드를 기준으로 알고리즘을 수행**한다.

- 다만 매 단계마다 방문하지 않은 노드 중에 최단 거리를 갖는 노드를 찾는 과정이 필요하지 않다.

플로이드 워셜은 2차원 테이블에 최단 거리 정보를 저장한다.

플로이드 워셜 알고리즘은 다이나믹 프로그래밍 유형에 속한다.

## 플로이드 워셜 알고리즘

각 단계마다 **특정한 노드 k를 거쳐 가는 경우를 확인**한다.

- $a$에서 $b$로 가는 최단 거리보다 $a$에서 $k$를 거쳐 $b$로 가는 거리가 더 짧은지 검사한다.

점화식은 다음과 같다.
$$
D_{ab} = min(D_{ab}, D_{ak}+D_{kb})
$$
![image](https://user-images.githubusercontent.com/48538655/107326851-79e96900-6aef-11eb-8b9b-808b47dcaf02.png)

![image](https://user-images.githubusercontent.com/48538655/107326969-b3ba6f80-6aef-11eb-9b95-b6b064c8f181.png)

![image](https://user-images.githubusercontent.com/48538655/107327231-2af00380-6af0-11eb-8bf1-e3046db5cbb7.png)

![image](https://user-images.githubusercontent.com/48538655/107327308-4955ff00-6af0-11eb-97c4-c6ba055fa58f.png)

![image](https://user-images.githubusercontent.com/48538655/107327362-5f63bf80-6af0-11eb-8db9-f2f893acf12d.png)

## 플로이드 워셜 알고리즘

```python
INF = int(1e9) # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수 및 간선의 개수를 입력받기
n = int(input())
m = int(input())
# 2차원 리스트(그래프 표현)를 만들고, 무한으로 초기화
graph = [[INF] * (n + 1) for _ in range(n + 1)]

# 자기 자신에서 자기 자신으로 가는 비용은 0으로 초기화
for a in range(1, n + 1):
    for b in range(1, n + 1):
        if a == b:
            graph[a][b] = 0
            
# 각 간선에 대한 정보를 입력 받아, 그 값으로 초기화
for _ in range(m):
    # A에서 B로 가는 비용은 C라고 설정
    a, b, c = map(int, input().split())
    graph[a][b] = c
    
# 점화식에 따라 플로이드 워셜 알고리즘을 수행
for k in range(1, n + 1):
    for a in range(1, n + 1):
        for b in range(1, n + 1):
            graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])
            
# 수행된 결과를 출력
for a in range(1, n + 1):
    for b in range(1, n + 1):
        # 도달할 수 없는 경우, 무한(INFINITY)이라고 출력
        if grap[a][b] = INF:
            print("INFINITY", end=" ")
        # 도달할 수 있는 경우 거리를 출력
        else:
            print(graph[a][b], end = " ")
    print()
```

## 플로이드 워셜 알고리즘 성능 분석

노드의 개수가 $N$개일 때 알고리즘상으로 $N$번의 단계를 수행한다.

- 각 단계마다 $O(N^2)$의 연산을 통해 현재 노들르 거쳐 가는 모든 경로를 고려한다.

따라서 플로이드 워셜 알고리즘의 총 시간 복잡도는 $O(N^3)$이다.

## 참고 자료

이것이 취업을 위한 코딩테스트다. (나동빈 저)

[관련동영상](https://www.youtube.com/watch?v=acqm9mM1P6o)