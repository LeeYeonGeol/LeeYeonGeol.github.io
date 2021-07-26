---
title: "[Baekjoon] 17939번 Gazzzua"
categories: 
- Baekjoon
tags:
- Greedy Algorithm
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

때는 2119년, 정명이는 드디어 타임머신을 개발했다. 흙수저였던 지훈이는 타임머신을 이용해 100년 전으로 돌아가서 가상화페인 주홍코인을 통해 비루한 인생을 바꿔보기로 굳게 마음을 먹는다. 그에게는 할아버지 때부터 대대로 전해 내려오는 주홍코인의 가격 변동 차트가 있기 때문에 금수저 인생은 따 놓은 당상이다.
다만, 타임머신이 아직 완벽하지 않기에 제한 시간이 지나면 다시 현재 시점으로 돌아오게 된다. 또한 주홍코인은 거래소의 규제로 인해 거래를 하는데 다음과 같은 제약이 있다.

- 주홍코인의 구매는 매 분마다 1개만 가능하다.
- 주홍코인의 판매는 몇 개든 할 수 있다.
- 모든 거래에 대한 수수료는 발생하지 않는다.

물론 구매도 판매도 하지 않고 그냥 시간을 보낼 수도 있다. 정명이는 가격 변동 차트를 갖고 있기 때문에 앞으로 가격이 어떻게 변할지 모두 알고 있는 셈이다. 정명이가 과거로 돌아가서 주홍코인 거래를 통해 얻을 수 있는 최대의 수익이 얼마일지 구해보자.

## 입력

첫 번째 줄에 타임머신의 제한 시간 N분이 정수로 주어진다. (1 ≤ N ≤ 105)

두 번째 줄에 매 분마다의 주홍코인 가격이 공백으로 구분되어 N개 주어진다. 주홍코인의 가격은 1,000 이하의 자연수이다.

## 출력

첫 번째 줄에 정명이가 주홍코인 거래를 통해 얻을 수 있는 최대의 수익을 출력한다.

## 예제

**Example 1:**

```
Input: 
4
1 2 3 4
Output: 
6
```

**Example 2:**

```
Input:
6
1 5 10 2 4 3
Output:
16
```

## 조건

> 시간 제한 : 1초
>
> 메모리 제한 : 256 MB

## 풀이과정

### 풀이

```python
import heapq
n = int(input())
li = list(map(int,input().split()))
index = 0
buy_list = []
heapq.heapify(buy_list)

ans = 0
max_li = max(li)
index = 0

# 이전 최대 인덱스
prev = 0
new_li = li[index:]
# 1. 남은거 중에 최대를 찾는다.
# 2. 최대를 향해 달려간다.
# 3. 최대를 발견하면 정산하고 prev, index, max_li 교체
# 4. 종료 조건 = 최대가 남은거 중에 첫번째 or index 끝날때
#print(new_li)

while (index < len(li)):
  if li[index] != max_li:
    buy_list.append(li[index])
    index += 1

  # 큰경우
  else:
    for i in range(len(buy_list)):
      ans += max_li-heapq.heappop(buy_list)
    index += 1
    if index != len(li):
      max_li = max(li[index:])
print(ans)키 포인트는 차트의ㅇ
```

차트에서 최대값 전에 코인을 사면 모두 이득이므로 최대값을 찾아서 계산을 한다. 그리고 그 뒤 남은 부분에 대해서도 똑같이 진행을 한다.