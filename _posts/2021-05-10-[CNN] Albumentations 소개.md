---
title: "[CNN] Albumentations 소개"
categories: 
- CNN
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## Albumentations 개요

keras의 ImageDataGenerator는 **임의로 적용되기 때문에 각 기능별로 변환 확률을 정할 수 없는 단점**이 있음. 따라서 Albumentations를 사용하게 되는데, Keras Pipeline Integration을 위한 별도의 작업이 필요하다.

또한 매우 다양한 augmentation 기능을 제공한다.

## Albumentations 수행 로직

1. augmentor = A.HorizontalFlip(p=1)
2. aug_image_dict = augmentor(image=원본_이미지)
3. 변환_이미지 = aug_image_dict['image']

## 대표적인 augmentation

- HorizontalFlip
- VerticalFlip
- ShiftScaleRotate
- Crop
  - Crop
  - CenterCrop
  - RandomCrop
  - RandomResizedCrop
- RandomBrightnessContrast
- HueSaturationValue
- ColorJitter (밝기, 대비, 채도, 색상 한번에)
- Noise관련 기법
  - GaussNoise
  - Cutout
  - CoarseDropout
  - CLAHE (원본보다 명암대비가 선명한 이미지 재생)
  - Blur
  - GaussianBlur
  - 날씨관련 Noise
    - RandomRain
    - RandomShadow
    - RandomSnow

## Compose, OneOf

### Compose

보통 다음과 같이 Compose를 사용하여 여러 Augmentation을 체인 형태로 연속 적용한다.

```python
augmentor = A.Compose([
    A.CnterCrop(height=300, width=800),
    A.HorizontalFlip(p=0.5),
    A.RandomBrightnessContrast(p=0.5),
    A.Resize(579, 1024, p=1)
], p = 0.5)
```

### OneOf

OneOf를 이용하여 여러개의 변환 중 하나의 변환을 선택적으로 적용가능하다. 

```python
augmentor = A.OneOf([
    A.VerticalFlip(p=1),
    A.HorizontalFlip(p=1),
    A.Rotate(limit=(45, 90), p=1, border_mode=cv2.BORDER_CONSTANT)
], p=1)
```

따라서 다음과 같이 Compose안에 OneOf를 넣는 구성이 가능하다.

```python
augmentor = A.Compose([
    A.HorizontalFlip(p=0.5),
    A.ShiftScaleRotate(p=0.5),
    A.OneOf([
        A.CLAHE(p=0.3),
        A.Blur(blur_limit=(10, 15), p=0.3)
    ], p=0.5)
])
```

## 유의사항

- 과도한 Augmentation은 오히려 모델 성능을 저하시킬 수도 있다.
- 원본 이미지의 특성을 잘 파악하여 적절한 Augmentation을 적용하는 것이 중요하다.

## 참고 자료

[딥러닝 CNN 완벽가이드](https://www.inflearn.com/course/%EB%94%A5%EB%9F%AC%EB%8B%9D-cnn-%EC%99%84%EB%B2%BD-%EA%B8%B0%EC%B4%88)

