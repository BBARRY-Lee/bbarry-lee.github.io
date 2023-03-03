---
layout:   post
title:    "Deep Learning Basic 06 - Regularization"
subtitle: "Regularization"
category: AI-Tech
tags:     AI-Basic
image:
  path:   /assets/img/dlb_main6.jpg
---
# Deep Learning Basic 06 - Regularization

## Intro
>**Regularization의 다양한 방법**

---

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}

## 1. Regularzation (정규화)
![](https://velog.velcdn.com/images/leejy1373/post/1f99584e-038f-45cb-95e1-8f2c483599b6/image.png)


>- generation을 잘 되게 하고싶은 방법론
- 학습에 반대되도록 **`규제`**를 설정하여, 학습을 **`방해`**하는 것이 목적
- 이 방법론이 결과적으로 **`test data에서도 잘 동작`**되도록 하는 것
- 일종의 우리가 갖는 도구

---

## 2. Early Stopping
![](https://velog.velcdn.com/images/leejy1373/post/db765848-2318-4997-b1bd-40617c861797/image.png)

>- iteration이 돌아감에 따라 training error가 줄어들고 test error가 커짐
    - 이때 학습을 멈추는데, **`validation error`**를 활용
- training에 활용하지 않는 데이터 셋에 지금까지 학습된 모델 성능을 평가
- loss가 어느 시점부터 커질 가능성이 클 때, **`멈추는 것`**
    - 이를 위해 새로운 validation data가 필요

---

## 3. Parameter Norm Penalty
![](https://velog.velcdn.com/images/leejy1373/post/73aa9fcd-628e-4439-8c80-8661b14612b9/image.png)


>- NN의 파라미터가 너무 커지지 않게 하는 것
- 쉽게 말하면, 네트워크 파라미터들을 `모두 제곱한 후 더해서 숫자가 나오면 이것을 같이 줄임`
- 이왕이면 네트워크를 학습할 때, 네트워크 weight 숫자들이 작을수록 좋음 (작다는 건 크기 관점)
- 이것의 물리적인 해석은 NN이 만드는 function space에서 최대한 부드러운 함수로 보려는 것으로, 부드러운 함수일수록 generation 퍼포먼스가 높을 것이라는 가정

---

## 4. Data Augmentation (증가)
![](https://velog.velcdn.com/images/leejy1373/post/7f7b2e8b-a1e1-47ad-a553-1a2e359d04ac/image.png)

>- 가장 중요한 것은 데이터로, 데이터가 무한히 많으면 웬만하면 다 잘 됨
- 그래프를 보면 데이터가 적을 때, 딥러닝보다 Random forest 등이 더 잘 될 때가 많음, 즉 **`데이터 셋이 적으면`** 머신러닝, 딥러닝 등이 **`잘 안 될 가능성이 높음`**

---

![](https://velog.velcdn.com/images/leejy1373/post/45a8bbde-2c98-41a9-b416-e970aac5b577/image.png)

>- 하지만 데이터가 한정적이라 만들어  낼수 없으니, **`data Augmentation`**을 하는 것
- 이는 어떤 식으로든 주어진 데이터에 **`변형을 가해서 데이터셋을 늘리`**고 싶은 것
    - 예를 들어 강아지 고양이 분류를 할 때, 강아지는 각도 변형, 이미지 형태 변형 등의 변화에도 강아지는 강아지
        - 이렇게 변환을 했을 때, 나의 이미지 라벨이 박히지 않은 한도 내애서 변환하는 것을 data Augmentation라고함
- 반면 숫자 분류를 할 때는 숫자를 뒤집으면 6이 9가 되는 것과 같이, 뒤집는 변환을 하면
안 되는 것도 있으므로, **`레이블이 변환되지 않는 조건 하`** data Augmentation를 하는 것이 중요

---

## 5. Noise Robustness (견고성)
![](https://velog.velcdn.com/images/leejy1373/post/037d42dd-31be-4223-9367-e334630472f7/image.png)


>- 이 방법론이 아직 까지 왜 잘 되는지 의문
- 입력 데이터에 **`Noise`**를 넣는 것으로, Noise를 단순 입력에 넣는 것이 아닌 NN weight에도 집어넣음
- Weight를 학습시킬 때, 4번 흔들어주면 성능이 더 잘 나온다는 치명적인 결과가 나온다거나, Noise를 중간중간 집어넣으면 그 네트워크가 테스트 단계에서 잘 될 수 있다는 결과를 많이 냄

---

## 6. Label Smoothing
![](https://velog.velcdn.com/images/leejy1373/post/de8042d2-1af1-43e8-9646-4f703a354a46/image.png)

>- training 학습 데이터 단계의 데이터 2개를 꺼내서 `막 섞어 줌`
- 분류 문제를 푼다고 가정하면 2개의 클래스를 잘 구분할 수 있는 이미지 공간 속에서의 어떤 `decision bounce`를 찾아 분류를 잘 되게 하는 것이 목표
- decision bounce를 부드럽게 만드는 효과가 있음

---

![](https://velog.velcdn.com/images/leejy1373/post/0bb15fa2-69f7-42fa-94dc-0ba65aba44f0/image.png)

>- `Mixup` : 2개의 이미지를 골라 라벨을 섞고, 이미지도 섞음
- `Cutout` : 이미지에서 빼버리는 것
- `Cutmix` : 섞어줄 때 이미지를 블렌딩하듯 섞는 것 아니라 특정 영역을 분배해서 집어넣음
    - 일반적으로 이런 방법론을 사용하면 성능이 올라간다고 하며, Mixup의 같은 경우는 연구 시 많이 활용해봤고 실제로 성능이 많이 올라갔음 (최성준 교수님의 믹스업, 컷믹스 추천)

---

## 7. Dropout
![](https://velog.velcdn.com/images/leejy1373/post/7e9f4b6b-4d9b-4b7f-a909-ff3b2e3a8372/image.png)


>- NN weight를 일반적으로 `0으로 바꾸는 것`으로, 뉴럴과 인퍼런스를 할 때 뉴럴 50%를 0으로 바꿔주면, 각각의 뉴럴들이 로버스(?)한 feature를 잡을 수 있음
- 일반적으로 Dropout을 쓰면 성능이 많이 올라가는 효과가 있음

---
## 8. **Batch Normalization**

![](https://velog.velcdn.com/images/leejy1373/post/f10f9175-3546-4054-b99b-feb389c86f57/image.png)


>- (논란이 많은 논문)
- 내가 적용하고자 하는 `레이어에 statics를 정교화`시키는 것
- NN의 각각의 레이어가 각각 값들에 대한 statics가 원래 100정도의 값을 가지면,
 `0`을 가지게 함 (평균을 빼주고 분산으로 나눠 줌)
- 이를 활용하면 일반적으로 레이어가 깊게 쌓여 성능이 올라감

---
![](https://velog.velcdn.com/images/leejy1373/post/730e7558-2571-44ad-bf6f-f64cc636ad2b/image.png)

- `Batch Normalization` : variance로써 `레이어 전체`에 대해 줄임
- `Instance Normalization` : 이미지 `1장 별`로 레이어를 줄이는 static를 정교화시키는 것
- `Group Normalization` : `여러 종류의 Normalization 테크닉`이 들어가고 장 단점을 실험적으로 설명하는 좋은 논문
- Batch Normalization이 왜 잘 되는지 해석하는 것보다는 간단한 분류 문제를 풀 때 Batch Normalization을 활용하면 많은 경우 성능을 올릴 수 있다는게 알려져 있어 활용하는 것이 좋을 것  (즉, 이들은 모두 좋은 툴)
- 네트워크를 만들고 무언가 픽스 돼 있을 때 하나하나 집어넣어보면서 generation 퍼포먼스를 보면 training error는 모두 줄어들겠지만, text data, validation data에 대해서도 골라 성능이 잘 나오는 것을 보며 하나씩 추려서 선택하는 것이 좋은 방향

---

<!--more-->
<br><br>

<div align="center">
소통은 제가 공부하고 공유하는 원동력이 됩니다.<br>
해당 글이 도움이 되셨다면 소중한 격려와 응원 부탁드립니다 ☺️
</div>  