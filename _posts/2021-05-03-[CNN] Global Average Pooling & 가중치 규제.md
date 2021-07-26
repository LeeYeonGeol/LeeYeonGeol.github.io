---
title: "[CNN] Global Average Pooling & 가중치 규제"
categories: 
- CNN
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## Global Average Pooling

- 피처맵의 가로x세로의 특정 영역을 subsampling하지 않고 채널별로 평균 값을 추출
- 3차원 피처맵을 1차원 Dense Classification layer에 연결 시 맣은 연결 노드와 파라미터가 피요하나 GAP를 이용하면 효과적으로 노드와 파라미터를 줄일 수 있다.
- 충분히 피처맵의 채널수가 많을 경우 이를 적용하고 채널 수 가 적다면 Flattem이 유리하다.

## 가중치 규제

모델이 Loss를 줄이는 것에만 집착하면서 가중치 값이 학습데이터에만 지나치게 정교화 되는 현상이 발생하기 쉽다.(오버피팅) 원래 Loss함수의 출력값에 전체 가중치 행렬값의 제곱값을 일정계수만큼 곱한 값을 더해서 Loss 출력 결과를 어느 정도 무뎌지게 만든다.

> 손실 함수 목표 = $Min(Loss(W) \ +alpha*||W||^2_2)$

l2: 가중치의 제곱, keras.regularizers.l2(0.001)

l1: 가중치의 절대값, keras.regularizers.l1(0.001)

l1_l2: l1과 l2를 결합, keras.regularizers.l1_l2(l1=0.001, l2=0.001)



## 참고 자료

[딥러닝 CNN 완벽가이드](https://www.inflearn.com/course/%EB%94%A5%EB%9F%AC%EB%8B%9D-cnn-%EC%99%84%EB%B2%BD-%EA%B8%B0%EC%B4%88)

