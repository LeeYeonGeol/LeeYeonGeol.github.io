---
title: "[데이터 분석] pandas, numpy, matplotlib 기초"
categories: 
- 데이터 분석
tags:
- pandas
- numpy
- matplotlib
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

# 개요

본격적인 데이터 공부에 앞서 pandas, numpy, matplotlib의 기본적인 조작방법을 정리한다.

# pandas

판다스는 파이썬에서 가장 널리 사용되는 데이터 분석 라이브러리로 **데이터 프레임**이라는 자료구조를 사용한다. 데이터 프레임은 엑셀의 스프레드시트와 유사한 형태이며 파이썬으로 데이터를 쉽게 처리할 수 있도록 한다. 

- 판다스 라이브러리 불러오기

아래 코드는 데이터 분석 라이브러리를 import하는 코드이다. 판다스 라이브러리는 보통 pd라는 이름으로 축약하여 사용한다.

```python
import pandas as pd
```

- 데이터 프레임을 생성하고 일부분 살펴보기

판다스의 데이터 프레임을 생성한다. 데이터 프레임에 들어갈 2개의 열 데이터를 입력한 뒤, list()와 zip() 함수로 데이터셋을 생성한다. 그리고 이 데이터셋으로 아래와 같은 데이터 프레임 객체를 생성할 수 있다. head() 함수로 생성된 데이터 프레임의 일부분을 살펴볼 수 있다.

```python
#판다스의 데이터 프레임을 생성한다.
names = ['Bob', 'Jessica', 'Mary', 'John', 'Mel']
births = [968, 155, 77, 578, 973]
custom = [1, 5, 25, 13, 23232]

BabyDataSet = list(zip(names,births))
df = pd.DataFrame(data = BabyDataSet, columns=['Names', 'Births'])

# 데이터 프레임의 상단 부분을 출력한다.
df.head()
```

실행 결과는 다음과 같다.

<p align="center">
    <img src="https://user-images.githubusercontent.com/48538655/109572745-1a500d80-7b31-11eb-8a35-04a48ddbaedb.png" alt="image" style="zoom: 80%;" />
</p>

- 데이터 프레임의 기본 정보 출력하기

데이터 프레임의 기본 정보를 출력해본다. dtypes, index, columns로 데이터 프레임으 행, 열 정보를 출력할 수 있다. dtypes는 열의 타입 정보, index는 행의 형태 정보를 포함하고 있다. 그리고 columns는 데이터 프레임의 열 정보를 조금 더 간략한 형태로 요약하고 있다.

```python
# 데이터 프레임의 열 타입 정보를 출력한다.
df.dtypes
```

```
Names	object
Births	int64
dtype: object
```

```python
# 데이터 프레임의 인덱스 정보이다.
df.index
```

```
RangeIndex(start=0, stop=5, step=1)
```

```python
# 데이터 프레임 열의 형태 정보이다.
df.columns
```

```
Index(['Names', 'Births'], dtype='object')
```

- 데이터 프레임의 행과 열 선택하기

데이터 프레임의 열 이름을 선택하여 데이터를 출력할 때는 아래와 같이 df['Names']를 실행한다. 그리고 행의 구간에 해당하는 데이터를 출력할 때는 df[0:3]과 같은 방법을 사용한다. 여기에서 0과 3은 데이터 프레임의 행 번호를 의미하며 모든 데이터 프레임의 행 번호는 0부터 시작이다.

```python
# 데이터 프레임에서 하나의 열을 선택한다.
df['Names']
```

```
0	    Bob
1	Jessica
2	   Mary
3	   John
4	    Mel
Name: Names, dtype: object
```

```python
# 0-3번째 인덱스를 선택한다.
df[0:3]
```

```
	Names	Births
0	  Bob	   968
1 Jessica	   155
2    Mary	    77
```

위의 두 결과는 서로 형태가 다르게 보이는데, 이는 첫 번째 결과는 시리즈라는 객체를 출력한 것이고 두 번째 결과는 데이터 프레임을 출력한 것이기 때문이다.

## 기초적인 두 가지 기능

- 조건을 추가하여 선택하기

첫 번째는 조건을 추가하여 **필터링 기능**을 사용할 수 있다. df[df['Births'] > 100]이라는 코드는 전체 데이터 프레임 내에서 Births 열에 해당하는 데이터가 100보다 큰 경우에만 데이터를 반환해달라는 코드이다.

```python
# Births 열이 100보다 큰 데이터를 선택한다.
df[df['Births'] > 100]
```

```
	Names	Births
0	  Bob	   968
1 Jessica	   155
3    John	   578
4     Mel      973
```

- 평균값 계산하기

두번째는 **평균값을 계산하는 기능**이다. 아래 코드는 현재 데이터 프레임의 열 중에서 유일하게 평균값을 구할 수 있는 Births 열의 평균을 mean() 함수로 계산한 것이다. mean() 함수는 각 열들의 데이터 타입을 체크한 뒤, 연산이 가능한 열의 평균값만을 반환한다.

```python
# 데이터 프레임에서의 평균값을 계산한다.
df.mean()
```

```
Births	 550.2
dtype: float64
```

# Numpy

넘파이(Numpy)는 Numerical Python의 줄임말로 수치 계산을 위해 만들어진 파이썬 라이브러리이다. 넘파이의 자료구조는 앞에서 살펴본 판다스 라이브러리, 그리고 다음에 살펴볼 Matplotlib 라이브러리의 기본 데이터 타입으로 사용되기도 한다.

넘파이에서는 배열(array) 개념으로 변수를 사용하며 벡터, 행렬 등의 연산을 쉽고 빠르게 수행하도록 지원한다. 파이썬이라는 언어가 기본 자료구조인 리스트(List), 딕셔너리(Dictionary) 등을 갖고 있는 것과 마찬가지로 데이터 분석이라는 언어는 기본 자료구조로 넘파이 배열을 가지고 있다.

이제 몇 가지 간단한 코드를 통해 넘파이를 알아본다. 넘파이는 통상적으로 np라는 약어로 라이브러리를 import한다.

- 넘파이 라이브러리 불러오기

```python
import numpy as np
```

- 넘파이 배열 생성하기

우선 넘파이 배열을 하나 선언해 본다. 아래 코드는 1ㅇ차원 1ㅐ열이 3개, 2차원 배열이 5개의 값을 가지는 15개의 숫자를 생성하는 코드이다. 0부터 14까지 15개의 숫자를 (3, 5)차원으로 생성한 것을 확인할 수 있다.

```python
arr1 = np.arange(15).reshape(3, 5)
arr1
```

```
array([[ 0,  1,  2,  3,  4],
       [ 5,  6,  7,  8,  9],
       [10, 11, 12, 13, 14]])
```

- 넘파이 배열 정보 확인하기

넘파이 배열 데이터의 차원을 확인하는 방법은 shape를 호출하는 것이고, 데이터 타입을 확인하는 방법은 dtype을 호출하는 것이다. 이는 판다스와 동일한 인터페이스로 구성되어 있는 것을 알 수 있다.

```python
arr1.shape
arr1.dtype
```

```
(3, 5)
dtype('int64')
```

- 다른 형태의 배열 생성하기

혹은 zeros() 함수로 데이터를 생성할 수도 있다. zeros() 함수는 0으로 채워진 넘파이 배열을 생성하는 함수이다. 1을 채워주는 역할을 하는 함수는 ones()이다.

```python
arr3 = np.zeros((3,4))
arr3
```

```
[[0, 0, 0, 0,]
 [0, 0, 0, 0,]
 [0, 0, 0, 0,]]
```

- 넘파이 배열을 이용한 사칙연산 수행하기

넘파이 배열의 존재 이유라고도 할 수 있는 **데이터 연산** 방법을 알아본다. 먼저 동일한shape를 가지는 2개의 데이터를 생성한다. 그리고 이 2개의 데이터에 다음과 같이 **+,-,*,/** 기호를 사용하여 사칙연산을 수행할 수 있다.

```python
arr4 = np.array([
    [1,2,3],
    [4,5,6]
], dtype = np.float64)

# 사칙연산을 출력한다.
print("arr4 + arr5 = ")
print(arr4 + arr5,"\n")
print("arr4 - arr5 = ")
print(arr4 - arr5,"\n")
print("arr4 * arr5 = ")
print(arr4 * arr5,"\n")
print("arr4 / arr5 = ")
print(arr4 / arr5,"\n")
```

```
arr4 + arr5 =
[[8. 10. 12.]
 [14. 16. 18.]]
 
arr4 - arr5 =
[[-6. -6. -6.]
 [-6. -6. -6.]]
  
arr4 * arr5 =
[[7. 16. 27.]
 [40. 55. 72.]]
 
arr4 / arr5 =
[[0.14285714 0.25	0.33333333]
 [0.4	0.4545454   0.5]]
```

이 외에도 넘파이 라이브러리는 dot() 함수를 이용한 행렬 연산 등 데이터 분석에 필요한 많은 기능을 제공하고 있다.

# Matplotlib

Matplitlib 라이브러리는 데이터를 시각화해주는 가장 기본적인 라이브러리이다. 주피터 노트북에서 Matplotlib로 시각화된 그래프를 출력하려면 아래와 같은 코드를 미리 실행해두어야 한다. 

%matplotlib inline 코드는 현재 실행중인 주피터 노트북에서 그래프를 출력 가능하도록 선언하는 명령어이다.

- Matplotlib 라이브러리 불러오기

```python
%matplotlib inline
import matplotlib.pyplot as plt
```

## 예제

이제, 두 가지 그래프 출력 예제를 통해 Matplotlib를 알아본다. 첫 번째 그래프는 막대 그래프(bar plot)입니다. Matplotlib 라이브러리를 사용할 때는 우선 **그래프 객체**라는 것을 생성해주어야 한다. plt.bar(x, y)를 실행하면 막대 그래프 객체가 생성되고, 이제 객체에 다른 요소를 추가해줄 수 있다. 이어지는 코드 plt.xlabel, plt.ylabel, plt.title은 그래프 객체에 각각 x축 제목, y축 제목, 그래프 전체 제목을 달아주는 코드이다. 그리고 마지막으로 plt.show()를 호출하면 그래프를 출력할 수 있다.

- 막대 그래프 출력하기

```python
y = df['Births']
x = df['Names']

# 막대 그래프를 출력한다.
plt.bar(x, y)  # 막대 그래프 객체 생성
plt.xlabel('Names')  # x축 제목
plt.ylabel('Births') # y축 제목
plt.title('Bar plot') # 그래프 제목
plt.show() # 그래프 출력
```

<p align='center'>
    <img src="https://user-images.githubusercontent.com/48538655/109887835-d5a9ab00-7cc5-11eb-9e38-37926a37eb55.png" alt="image" style="zoom:100%;" />
</p>

두 번째 그래프는 산점도 그래프(Scatter plot)이다. 아래 코드에서는 넘파이를 이용하여 데이터를 생성한 뒤, 이를 산점도 그래프로 그렸다. random.seed() 함수는 랜덤 추출 시드를 고정한 것이고 이를 토대로 random.rand() 함수가 넘파이 배열 타입의 난수를 생성한다. 그리고 arrange() 함수는 5의 간격으로 0부터 100까지의 숫자를 생성한 것이다. 지금까지의 데이터를 plt.scatter() 함수로 출력한 결과는 아래와 같다.

```python
# 랜덤 추출 시드를 고정한다.
np.random.seed(19920613)

# 산점도 데이터를 생성한다.
x = np.arange(0.0, 100.0, 5.0)
y = (x * 1.5) + np.random.rand(20) * 50

# 산점도 데이터를 출력한다.
plt.scatter(x, y, c="b", alpha=0.5, label="scatter point")
plt.xlabel("X")
plt.ylabel("Y")
plt.legend(loc='upper left')
plt.title("Scatter plot")
plt.show()
```

<p = align='center'>
    <img src="https://user-images.githubusercontent.com/48538655/109888343-af383f80-7cc6-11eb-9c42-26b05be3a7cb.png" alt="image" style="zoom:100%;" />
</p>

앞의 코드에서 scatter() 함수에 사용된 c, alpha, label 파라미터와 legend() 함수는 그래프를 꾸며주기 위한 파라미터들이다.

# 참고자료

책: 이것이 데이터 분석이다 with 파이썬 (윤기태 저)



































