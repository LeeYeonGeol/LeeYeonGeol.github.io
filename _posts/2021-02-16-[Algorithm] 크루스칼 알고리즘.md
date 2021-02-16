---
title: "[Algorithm] 크루스칼 알고리즘"
categories: 
- Algorithm
tags:
- Graph Algorithm
- kruskal Algorithm
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 크루스칼 알고리즘

### 신장 트리

<u>그래프에서 모든 노드를 포함하면서 사이클이 존재하지 않는 부분 그래프</u>를 의미한다.

- 모든 노드가 포함되어 서로 연결되면서 사이클이 존재하지 않는다는 조건은 **트리**의 조건이기도 하다.

![image](https://user-images.githubusercontent.com/48538655/107912012-0937c600-6fa1-11eb-8677-b18923bad7f5.png)

### 최소 신장 트리

<u>최소한의 비용으로 구성되는 신장 트리를 찾아야 할 때</u> 어떻게 해야 할까?

예를 들어 N개의 도시가 존재하는 상황에서 두 도시 사이에 도로를 놓아 **전체 도시가 서로 연결**될 수 있게 도로를 설치하는 경우를 생각해 보자.

- 두 도시 A, B를 선택했을 때 A에서 B로 이동하는 경로가 반드시 존재하도록 도로를 설치한다.

![image](https://user-images.githubusercontent.com/48538655/107918469-0f33a400-6fad-11eb-8454-a253130736b9.png)

### 크루스칼 알고리즘

대표적인 **최소 신장 트리 알고리즘**이다. 그리디 알고리즘으로 분류된다.

구체적인 동작 과정은 다음과 같다.

1. 간선 데이터를 비용에 따라 **오름차순으로 정렬**한다.

2. 간선을 하나씩 확인하며 <u>현재의 간선이 사이클을 발생시키는지 확인</u>합니다.

   1) 사이클이 발생하지 않는 경우 최소 신장 트리에 포함시킨다.

   2) 사이클이 발생하는 경우 최소 신장 트리에 포함시키지 않는다.

3. 모든 간선에 대하여 2번의 과정을 반복한다.

 ### 크루스칼 알고리즘: 동작 과정 살펴보기

![image](https://user-images.githubusercontent.com/48538655/108006598-4357a500-703f-11eb-9bf4-12d301d440a1.png)

![image](https://user-images.githubusercontent.com/48538655/108006663-700bbc80-703f-11eb-96ca-220d8bfbb158.png)

![image](https://user-images.githubusercontent.com/48538655/108006702-8ade3100-703f-11eb-932e-d731b789c233.png)

![image](https://user-images.githubusercontent.com/48538655/108006744-a0ebf180-703f-11eb-8cf7-ab76dfd8ce03.png)

![image](https://user-images.githubusercontent.com/48538655/108006765-aba68680-703f-11eb-8178-9afaa69afdce.png)

![image](https://user-images.githubusercontent.com/48538655/108006784-b7924880-703f-11eb-8a70-1216339cddf2.png)

![image](https://user-images.githubusercontent.com/48538655/108006806-c37e0a80-703f-11eb-8be9-7ab4946def66.png)

![image](https://user-images.githubusercontent.com/48538655/108006840-d5f84400-703f-11eb-89bc-0d3f633c59e7.png)

![image](https://user-images.githubusercontent.com/48538655/108006856-e14b6f80-703f-11eb-8de0-4b9f954bc476.png)

![image](https://user-images.githubusercontent.com/48538655/108006882-edcfc800-703f-11eb-9c76-1c702416e60f.png)

![image](https://user-images.githubusercontent.com/48538655/108006910-faecb700-703f-11eb-9aff-5dc0ee64bab9.png)

### 크루스칼 알고리즘 코드

```python
# 특정 원소가 속한 집합을 찾기
def find_parent(parent, x):
    # 루트 노드를 찾을 때까지 재귀 호출
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]

# 두 원소가 속한 집합을 합치기
def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        pranet[a] = b
        
# 노드의 개수와 간선(Union 연산)의 개수 입력 받기
v, e = map(int, input().split())
parent = [0] * (v + 1) # 부모 테이블 초기화하기

# 모든 간선을 담을 리스트와, 최종 비용을 담을 변수
edges = []
result = 0

# 부모 테이블상에서, 부모를 자기 자신으로 초기화
for i in range(1, v + 1):
    parent[i] = i
    
# 모든 간선에 대한 정보를 입력 받기
for _ in range(e):
    a, b, cost = map(int, input().split())
    # 비용순으로 정렬하기 위해서 튜플의 첫 번째 원소를 비용으로 설정
    edges.append((cost, a, b))
    
# 간선을 비용순으로 정렬
edges.sort()

# 간선을 하나씩 확인하며
for edge in edges:
    cost, a, b = edge
    # 사이클이 발생하지 않는 경우에만 집합에 포함
    if find_parent(parent, a) != find_parent(parent, b):
        union_parent(parent, a, b)
        result += cost
print(result)
```

### 크루스칼 알고리즘 성능 분석

크루스칼 알고리즘은 간선의 개수가 $E$개일 때, $O(ElogE)$의 시간 복잡도를 가진다.

크루스칼 알고리즘에서 가장 많은 시간을 요구하는 곳은 간선을 정렬을 수행하는 부분이다.

- 표준 라이브러리를 이용해 $E$개의 데이터를 정렬하기 위한 시간 복잡도는 $O(ElogE)$이다.

## 참고 자료

이것이 취업을 위한 코딩테스트다. (나동빈 저)

[관련동영상](https://www.youtube.com/watch?v=aOhhNFTIeFI)

