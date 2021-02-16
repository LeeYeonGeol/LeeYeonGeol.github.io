---
title: "[Algorithm] 서로소 집합 알고리즘"
categories: 
- Algorithm
tags:
- Graph Algorithm
- Disjoint Set Algorithm
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 서로소 집합 알고리즘

서로소 집합(Disjoint Sets)란 <u>공통 원소가 없는 두 집합</u>을 의미한다.

![image](https://user-images.githubusercontent.com/48538655/107449991-da2be980-6b87-11eb-889b-cc01284d33b9.png)

### 서로소 집합 자료구조

<u>서로소 부분 집합들로 나누어진 원소들의 데이터를 처리하기 위한 자료구조</u>이다.

서로소 집합 자료구조는 두 종류의 연산을 지원한다.

- **합집합(Union)**: 두 개의 원소가 포함된 집합을 하나의 집합으로 합치는 연산이다.
- **찾기(Find)**: 특정한 원소가 속한 집합이 어떤 집합인지 알려주는 연산이다.

서로소 집합 자료구조는 **합치기 찾기(Union Find) 자료구조**라고 불리기도 한다.

여러 개의 합치기 연산이 주어졌을 때 서로소 집합 자료구조의 동작 과정은 다음과 같다.

1. 합집합(Union) 연산을 확인하여, 서로 연결된 두 노드 A, B를 확인한다.

   1) A와 B의 루트 노드 $A^\prime, B^\prime$를 각각 찾는다.

   2) $A^\prime$를 $ B^\prime$의 부모 노드로 설정한다.

2. 모든 합집합(Union) 연산을 처리할 때까지 1번의 과정을 반복한다.

### 서로소 집합 자료구조: 동작 과정 살펴보기

![image](https://user-images.githubusercontent.com/48538655/107451892-92a75c80-6b8b-11eb-8757-0ecb2786e035.png)

![image](https://user-images.githubusercontent.com/48538655/107451971-ba96c000-6b8b-11eb-8af3-9f1363f71a19.png)

![image](https://user-images.githubusercontent.com/48538655/107452057-e5811400-6b8b-11eb-9de7-74490845ce0c.png)

![image](https://user-images.githubusercontent.com/48538655/107452142-0cd7e100-6b8c-11eb-8fb0-0a9963e305a6.png)

![image](https://user-images.githubusercontent.com/48538655/107452342-5c1e1180-6b8c-11eb-9e38-af1986efa71d.png)

### 서로소 집합 자료구조: 연결성

서로소 집합 자료구조에서는 **연결성**을 통해 손쉽게 집합의 형태를 확인할 수 있다.

![image](https://user-images.githubusercontent.com/48538655/107452462-9e475300-6b8c-11eb-9a1d-dd340b673f18.png)

기본적인 형태의 서로소 집합 자료구조에서는 루트 노드에 즉시 접근할 수 없다.

- 루트 노드를 찾기 위해 <u>부모 테이블을 계속해서 확인</u>하며 거슬러 올라가야 한다.

다음 예시에서 노드 3의 루트를 찾기 위해서는 노드 2를 거쳐 노드 1에 접근해야 한다.

![image](https://user-images.githubusercontent.com/48538655/107452646-ef574700-6b8c-11eb-9b52-0c0196645db7.png)

### 서로소 집합 자료구조: 기본적인 구현 방법 (Python)

```python
# 특정 원소가 속한 집합을 찾기
def find_parent(parent, x):
    # 루트 노드를 찾을 때까지 재귀 호출
    if parent[x] != x
    	return find_parent(parent, parent[x])
    return x

# 두 원소가 속한 집합을 합치기
def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b

# 노드의 개수와 간선(Union 연산)의 개수 입력 받기
v, e = map(int, input().split())
parent = [0] * (v + 1) # 부모 테이블 초기화하기

# 부모 테이블상에서, 부모를 자기 자신으로 초기화
for i in range(1, v + 1):
    parent[i] = i
    
# Union 연산을 각각 수행
for i in range(e):
    a, b = map(int, input().split())
    union_parent(parent, a, b)
    
# 각 원소가 속한 집합 출력하기
print('각 원소가 속한 집합: ', end='')
for i in range(1, v + 1):
    print(find_parent(parent, i), end=' ')
    
print()

# 부모 테이블 내용 출력하기
print('부모 테이블: ', end='')
for i in range(1, v + 1):
    print(parent[i], end=' ')
```

### 서로소 집합 자료구조: 기본적인 구현 방법의 문제점

합집합(Union) 연산이 편향되게 이루어지는 경우 찾기(Find) 함수가 비효율적으로 동작한다.

최악의 경우에는 찾기(Find) 함수가 모든 노드를 다 확인하게 되어 시간 복잡도가 O(V)이다.

- 다음과 같이 {1, 2, 3, 4, 5}의 총 5개의 원소가 존재하는 상황을 확인해 보자.
- **수행된 연산들**: $Union(4,5), \, Union(3,4), \, Union(2,3), \, Union(1,2)$

![image](https://user-images.githubusercontent.com/48538655/107736724-1ad16180-6d46-11eb-945c-aad49ee8f26b.png)

### 서로소 집합 자료구조: 경로 압축

찾기(Find) 함수를 최적화하기 위한 방법으로 경로 압축(Path Compression)을 이용할 수 있다.

- 찾기(Find) 함수를 재귀적으로 호출한 뒤에 <u>부모 테이블 값을 바로 갱신</u>한다.

```python
# 특정 원소가 속한 집합을 찾기
def find_parent(parent, x):
    # 루트 노드가 아니라면, 루트 노드를 찾을 때까지 재귀적으로 호출
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]
```

경로 압축 기법을 적용하면 각 노드에 대하여 <u>찾기(Find) 함수를 호출한 이후에</u> 해당 노드의 루트 노드가 바로 부모 노드가 된다.

동일한 예시에 대해서 **모든 합집합(Union) 함수를 처리한 후 각 원소에 대하여 찾기(Find) 함수를 수행하면 다음과 같이 부모 테이블이 갱신**된다.

기본적인 방법에 비하여 시간 복잡도가 개선된다.

![image](https://user-images.githubusercontent.com/48538655/107737866-c54a8400-6d48-11eb-8607-56a8153c5169.png)

### 서로소 집합 자료구조: 경로 압축 (Python)

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
        parent[a] = b
        
# 노드의 개수와 간선(Union 연산)의 개수 입력 받기
v, e = map(int, input().split())
parent = [0] * (v + 1) # 부모 테이블 초기화하기

# 부모 테이블상에서, 부모를 자기 자신으로 초기화
for i in range(1, v + 1):
    parent[i] = i
    
# Union 연산을 각각 수행
for i in range(e):
    a, b = map(int, input().split())
    union_parent(parent, a, b)
    
# 각 원소가 속한 집합 출력하기
print('각 원소가 속한 집합: ', end='')
for i in range(1, v + 1):
    print(find_parent(parent, i), end=' ')
    
print()

# 부모 테이블 내용 출력하기
print('부모 테이블: ', end = '')
for i in range(1, v + 1):
    print(parent[i], end= ' ')
```

### 서로소 집합을 활용한 사이클 판별

서로소 집합은 **무방향 그래프 내에서의 사이클을 판별**할 때 사용할 수 있다.

- 참고로 방향 그래프에서의 사이클 여부는 DFS를 이용하여 판별할 수 있다.

**사이클 판별 알고리즘**은 다음과 같다.

1. 각 간선을 하나씩 확인하며 두 노드의 루트 노드를 확인한다.

   1) 루트 노드가 서로 다르다면 두 노드에 대하여 합집합(Union)연산을 수행한다.

   2) 루트 노드가 서로 같다면 사이클(Cycle)이 발생한 것이다.

2. 그래프에 포함되어 있는 모든 간선에 대하여 1번 과정을 반복한다.

### 서로소 집합을 활용한 사이클 판별: 동작 과정 살펴보기

![image](https://user-images.githubusercontent.com/48538655/107898167-6ec68b00-6f7e-11eb-98e8-5db125394b92.png)

![image](https://user-images.githubusercontent.com/48538655/107898228-94ec2b00-6f7e-11eb-8eb9-e8ae6396ec8a.png)

![image](https://user-images.githubusercontent.com/48538655/107898246-a2091a00-6f7e-11eb-9512-43b2df238f5d.png)

![image](https://user-images.githubusercontent.com/48538655/107898281-b6e5ad80-6f7e-11eb-82ed-64e50aa9c29e.png)

### 서로소 집합을 활용한 사이클 판별 코드

```python
# 특정 원소가 속한 집합을 찾기
def find_parent(parent, x):
    # 루트 노드를 찾을 때까지 재귀 호출
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]

# 두 원소가 속한 집합을 합치기
def union_parent(a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b
        
# 노드의 개수와 간선(Union 연산)의 개수 입력 받기
v, e = map(int, input().split())
parent = [0] * (v + 1) # 부모 테이블 초기화하기

# 부모 테이블상에서, 부모를 자기 자신으로 초기화
for i in range(1, v + 1):
    parent[i] = i
    
cycle = False # 사이클 발생 여부

for i in range(e):
    a, b = map(int, input().split())
    # 사이클이 발생한 경우 종료
    if find_parent(parent, a) == find_parent(parent, b):
        cycle = True
        break
    # 사이클이 발생하지 않았다면 합집합(Union) 연산 수행
    else:
        union_parent(parent, a, b)
        
if cycle:
    print("사이클이 발생했습니다.")
else:
    print("사이클이 발생하지 않았습니다.")
```

## 참고 자료

이것이 취업을 위한 코딩테스트다. (나동빈 저)

[관련동영상](https://www.youtube.com/watch?v=aOhhNFTIeFI)

