---
sidebar_position: 1
---

# LabeledImage

이 페이지는 `image.py`의 `LabeledImage` 클래스에 대해서 소개합니다. `LabeledImage`는 서문에서 설명해드린 것처럼, 한 프레임의 `wrapper` 클래스입니다. 즉, `LabeledImage` 객체는 `OpenCV`로 영상을 읽어오는 `while`문을 돌 때마다 생성됩니다. 이 문서에서는 R, G, B로 구성된 행렬, 즉, `OpenCV`에서 제공한 프레임을 `raw_image`로 명시하겠습니다.

## 목적
머신러닝 모델에게 이미지 데이터를 제공하고 이를 기반으로 동작을 분류하라고 하면 정확도가 매우 낮게 나올 것입니다. 하지만 높은 정확도가 증명되고 보장된 `Movenet` 모델을 활용하고, 여기에서 반환된 관절 좌표 값들을 머신러닝 모델에게 제공하면 더욱 더 좋은 성능을 기대할 수 있을 것이라고 믿었습니다.

## record_activity 메소드
`record_activity`는 데이터 수집을 위한 메소드입니다. 지금 이 `LabeledImage` 객체가 갖고 `raw_image`를 전처리한 후, **Movenet** 모델에게 넘깁니다. 그러면 **Movenet**은 17개 관절 각각에 대한 (y, x, confidence) 값을 반환합니다. 이 `record_activity` 메소드가 하는 일은 진행상황에 대한 일을 UI에 표시하고(`OpenCV`에서 제공받은 프레임 위에다 컴포넌트 렌더링), 이 반환받은 17개의 (y, x, confidence)를 JSON 파일로 저장하는 것 입니다.

## get_activity 메소드
`get_activity` 메소드는 데이터 해석을 위한 메소드로, 현재 이미지와 이전의 이미지들을 함께 **Actlbl** 모델에 제공합니다. 그 후, 모델의 판단 결과, 즉 동작을 반환합니다.

## get_subactivity 메소드
`get_subactivity` 메소드는 데이터 해석을 위한 메소드로, `YOLO`를 이용하여 상호작용중인 사물을 이용하여 세부적인 동작을 파악합니다.

