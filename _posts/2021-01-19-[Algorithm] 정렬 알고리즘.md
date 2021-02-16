---
title: "[Algorithm] 정렬 알고리즘"
categories: 
- Algorithm
tags:
- Sort
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true 
---

## 정렬 알고리즘

**정렬(Sorting)**이란 <u>데이터를 특정한 기준에 따라 순서대로 나열</u>하는 것을 말한다. 일반적으로 문제 상황에 따라서 적절한 정렬 알고리즘이 공식처럼 사용된다.

## 선택 정렬

처리되지 않은 데이터 중에서 **가장 작은 데이터를 선택해 맨 앞에 있는 데이터와 바꾸는 것을 반복**한다.  이 방법은 가장 원시적인 방법으로 매번 '가장 작은 것을 선택'한다는 의미에서 **선택 정렬(Selection Sort) **알고리즘이라고 한다. 

선택 정렬 소스코드는 다음과 같다.

```python
array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

for i in range(len(array)):
    min_index = i # 가장 작은 원소의 인덱스
    for j in range(i+1, len(array)):
        if array[min_index] > array[j]:
            min_index = j
    array[i], array[min_index] = array[min_index], array[i] # 스와프

print(array)
```

실행 결과는 다음과 같다.

```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### 선택 정렬의 시간 복잡도

선택 정렬은 N번 만큼 가장 작은 수를 찾아서 맨 앞으로 보내야 한다. 구현 방식에 따라 사소한 오차는 있을 수 있지만, 전체 연산 횟수는 다음과 같다.
$$
N + (N - 1) + (N - 2) + \cdots + 2
$$
이는 $(N^2+N-2)/2$로 표현할 수 있는데, 빅오 표기법에 따라서 $O(N^2)$이라고 작성한다.

## 삽입 정렬

처리되지 않은 데이터를 하나씩 골라 **적절한 위치에 삽입**한다. 선택 정렬에 비해  구현 난이도가 높은 편이지만, 일반적으로 더 효율적으로 동작한다. 

삽입 정렬 소스코드는 다음과 같다.

```python
array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

for i in range(1, len(array)):
    for j in range(i, 0, -1): # 인덱스 i부터 1까지 1씩 감소하며 반복하는 문법
        if array[j] < array[j-1]:
            array[j], array[j-1] = array[j-1], array[j]
        else: # 자기보다 작은 데이터를 만나면 그 위치에서 멈춤
            break
print(array)
```

실행 결과는 다음과 같다.

```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### 삽입 정렬의 시간 복잡도

삽입 정렬의 시간 복잡도는 $O(N^2)$이며, 선택 정렬과 마찬가지로 반복문이 두 번 중첩되어 사용된다. 삽입 정렬은 <u>현재 리스트의 데이터가 거의 정렬되어 있는 상태라면 매우 빠르게 동작</u>한다. 

>최선의 경우 $O(N)$의 시간 복잡도를 가진다.

## 퀵 정렬

<u>기준 데이터를 설정</u>하고 그 **기준보다 큰 데이터와 작은 데이터의 위치를 바꾸는 방법**이다. 일반적인 상황에서 가장 많이 사용되는 정렬 알고리즘 중 하나이다. 병합 정렬과 더불어 대부분의 프로그래밍 언어의 정렬 라이브러리의 근간이 되는 알고리즘이다. 가장 기본적인 퀵 정렬은 **첫 번째 데이터를 기준 데이터(Pivot)로 설정**한다.

### 퀵 정렬이 빠른 이유: 직관적인 이해

이상적인 경우 분할이 절반씩 일어난다면 전체 연산 횟수로 $O(NlogN)$를 기대할 수 있다.

**너비 X 높이** = $N \times logN = NlogN$

### 퀵 정렬의 시간 복잡도

퀵 정렬은 평균의 경우 $O(NlogN)$의 시간 복잡도를 가진다. 하지만 최악의 경우 $O(N^2)$의 시간 복잡도를 가진다. 

### 퀵 정렬 소스코드

퀵 정렬 소스코드는 다음과 같다.

```python
array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

def quick_sort(array, start, end):
    if start >= end: # 원소가 1개인 경우 종료
        return
    pivot = start # 피벗은 첫 번째 원소
    left = start + 1
    right = end
    while(left <= right):
        # 피벗보다 큰 데이터를 찾을 때까지 반복
        while(left <= end and array[left] <= array[pivot]):
            left += 1
        # 피벗보다 작은 데이터를 찾을 때까지 반복
        while(right > start and array[right] >= array[pivot])
    		right -= 1
        if(left > right): # 엇갈렸다면 작은 데이터와 피벗을 교체
            array[right], array[pivot] = array[pivot], array[right]
        else:  # 엇갈리지 않았다면 작은 데이터와 큰 데이터를 교체
            array[left], array[right] = array[right], array[left]
    # 분할 이후 왼쪽 부분과 오른쪽 부분에서 각각 정렬 수행
    quick_sort(array, start, right - 1)
    quick_sort(array, right + 1, end)

quick_sort(array, 0 , len(array)-1)
print(array)
```

실행 결과는 다음과 같다.

```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### 퀵 정렬 소스코드: 파이썬의 장점을 살린 방식

```python
array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

def quick_sort(array, start, end):
    # 리스트가 하나 이하의 원소만을 담고 있다면 종료
    if len(array) <= 1:
        return array
    pivot = array[0] # 피벗은 첫 번째 원소
    tail = array[1:] # 피벗을 제외한 리스트
    
    left_side = [x for x in tail if x <= pivot] # 분할된 왼쪽 부분
    right_side = [x for x in tail if x > pivot] # 분할된 오른쪽 부분
    
    # 분할 이후 왼쪽 부분과 오른쪽 부분에서 각각 정렬 수행하고, 전체 리스트 반환
    return quick_sort(left_side) + [pivot] + quick_sort(right_side)

print(quick_sort(array))
```

## 계수 정렬

특정한 조건이 부합할 때만 사용할 수 있지만 <span style="color:red">매우 빠르게 동작하는</span> 정렬 알고리즘이다. 계수 정렬은 **데이터의 크기 범위가 제한되어 정수 형태로 표현할 수 있을 때** 사용 가능하다. 데이터의 개수가 $N$, 데이터(양수) 중 최댓값이 $K$일 때 최악의 경우에도 수행 시간 $O(N+K)$를 보장한다.

계수 정렬 소스코드는 다음과 같다.

```python
# 모든 원소의 값이 0보다 크거나 같다고 가정
array = [7, 5, 9, 0, 3, 1, 6, 2, 9, 1, 4, 8, 0, 5, 2]
# 모든 범위를 포함하는 리스트 선언(모든 값은 0으로 초기화)
count = [0]*(max(array)+1)

for i in range(len(array)):
    count[array[i]] += 1 # 각 데이터에 해당하는 인덱스의 값 증가
    
for i in range(len(count)): # 리스트에 기록된 정렬 정보 확인
    for j in range(count[i]):
        print(i, end=' ') # 띄어쓰기를 구분으로 등장한 횟수만큼 인덱스 출력
```

실행 결과는 다음과 같다.

```
0 0 1 1 2 2 3 4 5 5 6 7 8 9 9
```

### 계수 정렬의 복잡도 분석

계수 정렬의 시간 복잡도와 공간 복잡도는 $O(N+K)$이다.  계수 정렬은 때에 따라서 심각한 비효율성을 초래할 수 있다. 

>데이터가 0과 999,999로 단 2개만 존재하는경우

계수 정렬은 **동일한 값을 가지는 데이터가 여러 개 등장할 때** 효과적으로 사용할 수 있다.

> 성적의 경우 100점을 맞은 학생이 여러 명일 수 있기 때문에 계수 정렬이 효과적이다.

## 정렬 알고리즘 비교하기

| 정렬 알고리즘 | 평균 시간 복잡도 | 공간 복잡도 | 특징                                                         |
| :-----------: | :--------------: | :---------: | ------------------------------------------------------------ |
|   선택 정렬   |     $O(N^2)$     |   $O(N)$    | 아이디어가 매우 간단하다.                                    |
|   삽입 정렬   |     $O(N^2)$     |   $O(N)$    | 데이터가 거의 정렬되어 있을 때는 가장 빠르다.                |
|    퀵 정렬    |    $O(NlogN)$    |   $O(N)$    | 대부분의 경우에 가장 적합하며, 충분히 빠르다.                |
|   계수 정렬   |     $O(N+K)$     |  $O(N+K)$   | 데이터의 크기가 한정되어 있는 경우에만 사용이 가능하지만 매우 빠르게 동작한다. |

대부분의 프로그래밍 언어에서 지원하는 <u>표준 정렬 라이브러리는 최악의 경우에도 $O(NlogN)$ 을 보장</u>하도록 설계되어 있다.

## 참고 자료

이것이 취업을 위한 코딩테스트다. (나동빈 저)

[관련동영상](https://www.youtube.com/watch?v=KGyK-pNvWos)