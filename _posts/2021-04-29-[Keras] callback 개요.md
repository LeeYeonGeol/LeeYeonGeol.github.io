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

```python
from tensorflow.keras.callbacks import ModelCheckpoint

model = create_model()
model.compile(optimizer=Adam(0.001), loss='categorical_crossentropy', metrics=['accuracy'])

mcp_cb = ModelCheckpoint(filepath='/content/gdrive/MyDrive/Colab Notebooks/weights. {epoch:02d}-{val_loss:.2f}.hdf5', monitor='val_loss',
                         save_best_only=True, save_weights_only=True, mode='min', period=1, verbose=1)
history = model.fit(x=tr_images, y= tr_oh_labels, batch_size=128, epochs=10, validation_data=(val_images, val_oh_labels),
                      callbacks=[mcp_cb])
```

- ReduceLROnPlateau()

```python
from tensorflow.keras.callbacks import ReduceLROnPlateau

model = create_model()
model.compile(optimizer=Adam(0.001), loss='categorical_crossentropy', metrics=['accuracy'])

rlr_cb = ReduceLROnPlateau(monitor='val_loss', factor=0.2, patience=3, mode='min', verbose=1)
history = model.fit(x=tr_images, y= tr_oh_labels, batch_size=128, epochs=10, validation_data=(val_images, val_oh_labels),
                      callbacks=[rlr_cb])
```

- LearningRateSchdular()
- EarlyStopping()
- TensorBoard()

보통 다음과 같이 한꺼번에 적용한다.

```python
from tensorflow.keras.callbacks import ModelCheckpoint, ReduceLROnPlateau, EarlyStopping

model = create_model()
model.compile(optimizer=Adam(0.001), loss='categorical_crossentropy', metrics=['accuracy'])

mcp_cb = ModelCheckpoint(filepath='/content/gdrive/MyDrive/Colab Notebooks/weights. {epoch:02d}-{val_loss:.2f}.hdf5', monitor='val_loss',
                         save_best_only=True, save_weights_only=True, mode='min', period=1, verbose=0)
rlr_cb = ReduceLROnPlateau(monitor='val_loss', factor=0.3, patience=5, mode='min', verbose=1)
ely_cb = EarlyStopping(monitor='val_loss',patience=7, mode='min', verbose=1)

history = model.fit(x=tr_images, y= tr_oh_labels, batch_size=128, epochs=40, validation_data=(val_images, val_oh_labels),
                      callbacks=[mcp_cb, rlr_cb, ely_cb])
```



## 참고 자료

[딥러닝 CNN 완벽가이드](https://www.inflearn.com/course/%EB%94%A5%EB%9F%AC%EB%8B%9D-cnn-%EC%99%84%EB%B2%BD-%EA%B8%B0%EC%B4%88)

