---
title: "[CNN] 데이터 증강(Data Augmentation)의 이해"
categories: 
- CNN
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 데이터 증강(Data Augmentation) 개요

- 오버피팅을 극복하는 가장 좋은 방법은 **다양한** 유형의 학습 이미지 데이터의 **양**을 늘리는 것이다.
- 이미지 데이터는 학습 데이터 량을 늘리기가 쉽지 않다.
- Data Augmentation은 학습 시에 원본 이미지에 다양한 변형을 가해서 학습 이미지 데이터를 늘리는 것과 유사한 효과를 발휘하고자 하는 것.
- 학습 시마다 **개별 원본 이미지를 변형해서 학습**을 수행하는 것.

## Augmentation 유형

### 공간 레벨 변형

- Flip: Vertical(up/down), Horizontal(left/right)
- Crop: Center, Random
- Affine: Rotate, Translate, Shear, Scale(Zoom)

### 픽셀 레벨 변형

- Bright, Saturation, Hue, GrayScale, ColorJitter, Contrast, Blur, Gaussian Blur, Median Blur, Noise, Cutout, Histogram, Gamma, RGBShift, Sharpen

## 참고 자료

[딥러닝 CNN 완벽가이드](https://www.inflearn.com/course/%EB%94%A5%EB%9F%AC%EB%8B%9D-cnn-%EC%99%84%EB%B2%BD-%EA%B8%B0%EC%B4%88)

