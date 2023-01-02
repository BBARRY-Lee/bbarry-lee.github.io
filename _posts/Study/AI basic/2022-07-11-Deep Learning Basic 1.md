---
layout:   post
title:    "Deep Learning Basic 1"
subtitle: "Deep Learning에 대한 소개 및 keyword"
category: Study
tags:     AI-Basic
image:
  path:   /assets/img/boostcourse.png
---
# Deep Learning Basic 1

## Intro
>1. 딥러닝에 대한 소개 및 keyword
2. `CNN`(Convolutional Neural Networks), `RNN`(Recurrent Neural Networks)와 같은 딥러닝 모델 학습 전, <br>
 중요한 요소인 `Data`, `Model`, `Loss`, `Optimization algorithms`에 대해 학습

---

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}

## 1. AI < ML < DL
- **사람의 지능 모방 → 데이터 기반 머신러닝 → 딥러닝 → 데이터를 통한 학습**

![](https://velog.velcdn.com/images/leejy1373/post/fef480db-7b1e-4899-a62b-4e2d88b3d125/image.png)

---

## 2. 논문을 볼 때 주의깊게 보면 좋은 점

>- **Key Components of Deep Learning (딥러닝 분야의 기본요소)**
- The data that the model can learn. (`데이터` : 이미지, 말뭉치, 비디오 등)
- The model how to transform the data. (`학습`하고자 하는 `모델`)
- The loss function that quantifies the badness of the model. (모델의 불량을 정량화하는 `손실함수`)
- The algorithm to adjust the parameters to minimize the loss. (손실을 최소화하는 매개변수 조정 `알고리즘`)

---

## 3. **Data depend on the type of the problem to solve.**

![](https://velog.velcdn.com/images/leejy1373/post/2ffd9ee4-95a6-48ac-b6e3-a3cac8581967/image.png)

>→ 1~2. 이미지를 픽셀 별 구분 <br>
→ 3. Detection : 물체에 대한 바운딩 박스 <br>
→ 4. Pose Estimation : 3차원 스켈레톤 정보 <br>
→ 5. Visual QnA : 이미지가 주어졌을 때, 눈 색깔을 설명할 수 있는 것

---

## 4. Model

![](https://velog.velcdn.com/images/leejy1373/post/116f91f7-768e-418e-9433-3b0e5d37fdce/image.png)
- 이미지, 텍스트 등 데이터가 주어졌을 때, 직접적으로 알고 싶은 것들을 바꿔주는 것
- Alexnet, GoogLeNet, ResNet, DenseNet, LSTM, DeepAutoEncoders, GAN ...

---

## 5. Loss function

![](https://velog.velcdn.com/images/leejy1373/post/0ec5bec5-983a-44b6-80b4-17bff25197e0/image.png)

>### 손실 함수(loss function)
> - 머신러닝 혹은 딥러닝 **`모델의 출력값`**과 **`사용자가 원하는 출력값의 오차`**를 의미
>- 손실함수는 **정답 (y)**와 **예측 ($$\hat y$$)**를 입력으로 받아 실수값 점수를 만드는데,<br>
    이 오차점수가 높을수록 모델 성능이 좋지 않다고 볼 수 있음
>- 추후, 손실함수값이 `최소화`되도록 하는 **`가중치(weight)`**와 **`편향(bias)`**를 찾는 것이 목표
>→ `Regression Task` : 회귀문제<br>
>→ `Classification Task` : 분류문제<br>
>→ `Probabilistic Task` : 확률모델을 활용해서 평균, 분산으로 모델링 했을 때<br>

**💡 모델과 데이터가 정해졌을 때, 모델을 어떻게 학습을 할지?**
- 단, 일반적으로 분류 및 회귀문제를 풀 때 단순히 loss function이 줄어드는게 목적으로 볼 수 있지만, <br>
    이 값이 줄어든다고 해서 원하는 값을 항상 이룬다는 보장은 없음
- 추후 이런 관계를 잘 이해하는 것이 새로운 연구하는 것에 도움이 됨

---

## 6. Optimization Algorithm (최적화 방법)

![](https://velog.velcdn.com/images/leejy1373/post/0c8ef765-437c-48bd-9202-9f6c0fbee811/image.png)
<br>
**💡 핵심 아이디어**
>- Neural network의 parameter를 loss function에 대해 1차 미분한 정보 활용
- loss function을 단순히 최소화 하는 것이 아닌,<br>
    이 모델이 학습하지 않은 데이터에 대해서도 잘 작동되도록 하는 것이 목표

---

<!--more-->

<br><br>

<div align="center">
소통은 제가 공부하고 공유하는 원동력이 됩니다.<br>
해당 글이 도움이 되셨다면 소중한 격려와 응원 부탁드립니다 ☺️
</div>  