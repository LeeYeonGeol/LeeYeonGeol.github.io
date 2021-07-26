---
title: "[Baekjoon] 12018번 Yonsei TOTO"
categories: 
- Baekjoon
tags:
- Priority Queue
- Greedy Algorithm
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

연세대학교 수강신청이 얼마 전부터 바뀌어, 마일리지 제도로 바뀌었다. 이 제도는 각각의 학생들에게 마일리지를 주어 듣고 싶은 과목에 마일리지를 과목당 1~36을 분배한다. 그리고 모두 분배가 끝이 나면 과목에 대해서 마일리지를 많이 투자한 순으로 그 과목의 수강인원만큼 신청되는 방식이다.

성준이는 연세대학교 재학 중인 학생이다. 성준이는 저번 수강신청에서 실패하여 휴학을 했기 때문에 이번 수강신청만은 필사적으로 성공하려고 한다. 그래서 성준이는 학교 홈페이지를 뚫어버렸다.

그 덕분에 다른 사람들이 신청한 마일리지를 볼 수 있게 되었다. 성준이는 주어진 마일리지로 최대한 많은 과목을 신청하고 싶어 한다. (내가 마일리지를 넣고 이후에 과목을 신청하는 사람은 없다) 마일리지는 한 과목에 1에서 36까지 넣을 수 있다.

## 입력

첫째 줄에는 과목 수 n (1 ≤ n ≤ 100)과 주어진 마일리지 m (1 ≤ m ≤ 100)이 주어진다. 각 과목마다 2줄의 입력이 주어지는데 첫째 줄에는 각 과목에 신청한 사람 수 Pi과 과목의 수강인원 Li이 주어지고 그 다음 줄에는 각 사람이 마일리지를 얼마나 넣었는지 주어진다. (1 ≤ Pi ≤100, 1 ≤ Li ≤ 100)

(단 마일리지가 같다면 성준이에게 우선순위가 주어진다고 하자.)

## 출력

첫째 줄에 주어진 마일리지로 최대로 들을 수 있는 과목 개수를 출력한다.

## 예제

**Example 1:**

```
Input: 
5 76
5 4 
36 25 1 36 36
4 4
30 24 25 20
6 4
36 36 36 36 36 36
2 4
3 7
5 4
27 15 26 8 14
Output: 
4
```

## 조건

> 시간 제한 : 1초
>
> 메모리 제한 : 128 MB

## 풀이과정

### 풀이

```python
import heapq
import sys

ans = []
subject, m = map(int,(sys.stdin.readline().split()))

for i in range(subject):
  P,L = map(int,(sys.stdin.readline().split()))
  Q = list(map(int,sys.stdin.readline().split()))
  heapq.heapify(Q)
  if P < L:
    last = 1
  else:
    for j in range(P-L+1):
      last = heapq.heappop(Q)
  ans.append(last)
ans.sort()
count = 0
summ = 0
for i in range(len(ans)):
  summ += ans[i]
  if summ <= m:
    count += 1
  else:
    break

print(count)
```

우선순위 큐를 활용하였다. 제시된 과목 수만큼 for문을 돌린다. 이때 각 과목마다  신청한 사람 수 P와 수강인원 L을 받는다. 그리고 각 신청한 마일리지는 우선순위 큐 Q에 저장한다. 만일 수강인원보다 신청한 사람이 적다면 사용할 마일리지를 1로 한다. 수강인원보다 신청한 사람이 많다면 P-L+1만큼 for문을 돌려서 최소값을 heappop을 한다. 이를 통해 수강 가능한 최소 마일리지를 얻는다.

각 과목마다 for문이 끝날때마다 ans 리스트에 최소 마일리지를 append해준 뒤, sort()를 진행한다.그리고 for문을 통해 최대로 들을 수 있는 과목 개수를 count한다.