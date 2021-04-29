---
title: "[Keras] callback 개요"
categories: 
- Keras
tags:
- callback
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## Callback 개요

- 사용자는 특정 Callback API를 작성하여 model.fit( callbacks-[...])로 등록 시키면 fit() iteration 시 특정 이벤트 발생 시마다 등록된 callback이 호출되어 수행.
- 주로 최적의 Learning rate를 Control하는데 사용

## 대표적인 Callback

- ModelCheckpoint()
- ReduceLROnPlateau()
- LearningRateSchdular()
- EarlyStopping()
- TensorBoard()

## 참고 자료

[딥러닝 CNN 완벽가이드](https://www.inflearn.com/course/%EB%94%A5%EB%9F%AC%EB%8B%9D-cnn-%EC%99%84%EB%B2%BD-%EA%B8%B0%EC%B4%88)

