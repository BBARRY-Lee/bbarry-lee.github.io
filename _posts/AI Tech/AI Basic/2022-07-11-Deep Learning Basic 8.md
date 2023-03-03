---
layout:   post
title:    "Deep Learning Basic 08 - Sequential Models (RNN)"
subtitle: "Sequential Models - RNN"
category: AI-Tech
tags:     AI-Basic
image:
  path:   /assets/img/dlb_main8.jpg
---
# Deep Learning Basic 08 - Sequential Models (RNN)

## Intro
>- 주식, 언어와 같은 `Sequential data`와 이를 이용한 **`Sequential model`의 `정의`와 `종류`**
- 딥러닝에서 sequential data를 다루는**`Recurrent Neural Networks` 에 대한 `정의`와 `종류`**

---

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}

## 1. Sequntial Model (순차 모형)
![](https://velog.velcdn.com/images/leejy1373/post/48bc4120-f8d9-455f-bbea-477c9b30e212/image.png)


>- RNN은 주어지는 입력 자체가 Seqential 입력
- **`Seqential Data`** : 일상생활에서 접하는 대부분의 데이터 (음성, 비디오, 손동작 등)

---

**💡 Seqential 모델과 데이터를 다루는데 어려움은?**
- 얻고싶은 것은 어떤 하나의 `라벨`일 때가 많음 (혹은 정보)
    - 가장 간단한 분류라고 볼 때 원하는 것은 내가 하는 말이 `무엇`이다인데,
Seqential Data는 `길이가 언제 끝날지 모름`
        - 그래서, 기본적으로 받아드려야하는 `입력의 차원을 알 수가 없음`
            - 그렇기 때문에 앞에서 배운 것들을 사용할 수 없음
- 즉, 몇 개의 `입력`이 들어오든 `상관없이` 이 모델은 `동작`할 수 있어야 함

---

- **`Seqential 모델`** : 입력이 여러 개 들어왔을 때 다음 입력에 대한 `예측`하는 것
  - 랭귀지 모델이 있다면, 이전 말이 나올 때 다음 단어가 뭐가 나올지 예측하는 것으로, 예를 들면 10개의 입력이 있는데 첫 번째 입력은 아무 것에도 컨비젼 돼 있지 않고 두 번째는 처음만 고려하고 세 번째는 1~2번째를와 같이,
    `고려해야하는 컨비션 이펙터의 숫자가 늘어가게 됨`
- **`The number of inputs varies`** : 과거에 고려해야하는 정보량이 점점 늘어난다는 것으로, 이것이 어려운 문제

---

## 2. Autoregressive Model

![](https://velog.velcdn.com/images/leejy1373/post/cfd2614b-b7e9-4253-b522-86e168395bcc/image.png)


>- 제일 쉽게 할 수 있는 것은 `과거의 몇 개만` 보는 것
- 과거의 5개만 본다면 항상 5개를 보기 때문에 훨씬 계산이 쉬워짐

---

## 3. Markov Model
![](https://velog.velcdn.com/images/leejy1373/post/247b87b1-910c-472c-8c3b-b358f2a0a146/image.png)


>- 제일 쉬운 것 중 하나로 가장 큰 특징은 내가 가정하기에 나의 현재는 과거에만 dependent한다는 것 (**`과거는 바로 전 과거`**)
  - 하지만, 이 모델이 현실에서 말이 안 됨.
예를 들어, 내일 수능점수는 과거 몇 년간 공부했던 것이 누적 돼서 점수가 나와야 하는데, 이는 전날 공부한다는 것에 dependent한다는 것으로 설명됨
- 그래서 markov model 많은 정보를 버릴 수 밖에 없음
- 반면 markov model의 가장 큰 장점은 **`joint distribution`**을 표현하기 쉬워짐

---

## 4. Latent autoregressive model
![](https://velog.velcdn.com/images/leejy1373/post/7065959c-726e-43f4-beec-c2e4c0a1fefb/image.png)


>- markov의 단점은 과거에 많은 정보를 고려해야하는데, 고려 할 수 없는 것
- 그래서 이 모델은 중간에 **`Hidden state`**가 하나 있는데, 이 Hidden state가 과거의 정보를 **`요약`**하고 있고, 다음 time step은 Hidden state 하나에만 dependent
- 여기서 하나의 과거가 나의 과거 이전의 state가 아니라 이전의 정보를 요약한 어떤 Hidden state라고 봄
- 물론 어떻게 만드느냐에 따라 차이가 있겠지만, 중간의 Hidden state이 추가함으로써 과거 정보를 요약 (summary)

---

## 5. Recurrent Neural Network
![](https://velog.velcdn.com/images/leejy1373/post/81e0b413-67d0-4198-a96a-d4f1d22c2c2f/image.png)


>- 이 컨셉들을 가장 쉽게 설명하고 구현하는 방법
- 자기자신을 돌아오는 구조가 하나 있는데, $h_t$는 $x_t$에만 dependent 하는 것이 아니라, 이전의 cell state에 dependent하는 것

---

![](https://velog.velcdn.com/images/leejy1373/post/7100583a-d4b7-4f79-9959-ccc01d3f4254/image.png)

>- RNN은 `시간 순`으로 푼다고 이야기를 함
- x가 A로 들어가고 그 정보가 x1과 합쳐저 h1이 나오고 (…) 반복
- 중요한 사실은 RNN으로 불리는 구조를 시간 순으로 풀면, RNN 학습과 동일
- recurancy가 있어 그 자체로 복잡하고, 만약 timestep을 픽스 후 시간 순으로 풀게되면, 결국 각각 네트워크 파라미터를 쉐어하는 굉장히 인풋의 위치가 큰 네트워크가 됨

---

## 6. Short-term dependencies
![](https://velog.velcdn.com/images/leejy1373/post/7a1204aa-07f4-4f48-b82a-5cfd203dcf83/image.png)

>- 과거에 얻어진 정보들을 취합해서 미래에서 고려해야 하는데,RNN 자체는 하나의 픽스로 이 정보를 계속 취합하기 때문에 `과거에 있던 정보가 미래까지 살아남기가 힘듦`
  - 그래서 몇 스텝 전 정보는 고려가 잘 되지만, 멀리있는 정보는 고려하기 힘듦
    - 예를 들어, 음성인식 서비스가 있다고 보면 문장이 길어져도 이전에 중요하다고 생각한 정보를 다 가지고 있다가, 요약을 계속하고 표현할 때 써야 하는데 5초 전에 들은 말을 하나도 기억 못하는 것

---

## 7. Long-term dependencies
![](https://velog.velcdn.com/images/leejy1373/post/6c821680-27e7-40fb-9b26-29fdfa0d8e44/image.png)


>- 이것이 일반적으로 알려진 RNN의 가장 큰 단점
    - 이를 해결하는 것이 어려움

---
![](https://velog.velcdn.com/images/leejy1373/post/06699b0e-dc51-4c77-bc42-cd8c3292126d/image.png)


> **💡 RNN은 어떤 식으로 학습되며 왜 어려울까?**
- 네트워크을 풀어보면 굉장히 큰 네트워크, 위치가 커진 것이 됨
- $h_1$이라고 불리우는것은 $h_0$에서 나오는 값과 $x_1$과 합쳐짐
- $h_2$ = $h_1$ + 동일 (….)

---

- 이처럼 중첩되는 구조가 들어가기 때문에 $h_0$가 4까지 가기 위해, 똑같은 weight를 곱하고 통과시킴
- 어떤 정보가 네트워크 weight를 곱하고 반복하면, 그 값이 의미가 없어져 줄어듦
- `ReLU`를 쓴다고 가정해보면, w는 양수이고 이 w를 n번 곱하면, $h_0$의 값이 4로 갈 때 엄청 크게 반영될 것
- activation function이 `sigmoid`일 경우 `vanishing` 돼서 학습 안 됨
- activation function이 `ReLU`일 경우 학습할 때 네트워크가 `폭발`해 학습 안 됨
  - 따라서 RNN에서는 ReLU를 많이 쓰지 않으며, 학습이 어려운 것도 있음
- 그래서 **`LSTM`**이라는 모델이 나오게 됨!

---

![](https://velog.velcdn.com/images/leejy1373/post/7c2269f3-909d-41b7-bd08-8b1d333395ab/image.png)

>- RNN 의 기본구조 (위의 과정들)

---

## 8. LSTM Model

>LSTM이 각각 컴포넌트가 어떻게 동작을 하고 어떻게 긴 dependencies를 잡는지 아는 것이 목표

![](https://velog.velcdn.com/images/leejy1373/post/cbc1ee45-2206-43c2-8f0d-9f4254555476/image.png)
![](https://velog.velcdn.com/images/leejy1373/post/4a1018e5-e82d-45cf-93dd-9f3f19ae0534/image.png)


>- $x_t$ : Input (랭귀지 모델이면 단어)
- $h_t$ : Output → 최종적으로 t번째 step의 아웃풋이 출력
- **`Previous cell state`** : 밖으로 나가지 않고 내부에서만 흐르며,
지금까지 `time step t까지` 들어왔던 것을 `모두 취합`한 정보
- **`Previous hidden state`** : 아웃풋이 위로도 가지만 아래도 흐름
  - 입력으로 들어가는 건 `이전의 출력 값` 혹은 Previous hidden state와 밖으로 나가지 않는 `Previous cell state` 그리고 현재의  `time step t번째의 t`가 됨
- 네트워크만 보면 입력 3개와 출력 3개이지만, 실제로 나가는 것은 아웃풋
- 안에서 각각 구조를 잘 보면 로우라고 돼 있는 것이 3개 있음
💡 LSTM은 `gate`를 위주로 이해하면 좋음 (**Forget gate, Input gate, Output gate**)

---

![](https://velog.velcdn.com/images/leejy1373/post/89bf60db-f786-4ee4-8297-32f1b3702310/image.png)


>- 가장 큰 아이디어는 중간에 흐르는 `cell state`
- time step t까지 들어오는 정보를 요약하는 것으로 `컨베이너 벨트`로 빗대어 보면,
  - 어떤 물건이 올라올 때 조작공들이 어떤 정보가 유용하고 유용하지 않은지를 조작한 후 다음으로 넘김
  - 이 역할을 컨베이너 벨트 위에서 어떻게 **`올리고 빼고 조작`**할지에 대한 정보가 `gate`에 해당 (원 안의 기호들이 모두 `gate`)

---

![](https://velog.velcdn.com/images/leejy1373/post/8ecb0c47-6c42-4186-bc6a-bac5049146d6/image.png)


>- **`Forget gate`** : 어떤 정보를 버릴지 정함, 입력으로 들어가는 건 현재 입력과 이전 입력이 들어가서 $f_t$라는 숫자를 얻음 (`sigmoid`를 통과하기 때문에 항상 0~1값을 가짐)
  - 뒤에서는 $f_t$를 이전 cell state에서 나온 정보 중 어떤 걸 버리고 살릴지를 정함
- **`Input gate`** :  입력이 들어오면, 이를 무조건 cell state에 올리는 것이 아니라,
 이 정보 중 `어떤 것을 올릴지 말지`를 정함
  - hidden state와 현재 입력을 가지고 $i_t$라는 정보를 만들고, $i_t$는 어떤 정보를 올리고 말지를 정함
- **`C 틸다`** : 현재 정보와 이전 출력값을 가지고 만든 cell state 예비군,
이전에 나온 cell state와 현재의 정보와 아웃풋을 잘 섞어 업데이트

---

![](https://velog.velcdn.com/images/leejy1373/post/7b2f9eaf-e262-4598-a473-17eb744876b6/image.png)


>- **`Update cell`** : $f_t$에 이전 C 탈다를 곱해서 버릴 건 버린 후, C 틸다에 $i_t$만큼 곱해서 어느 값을 올릴지를 정한 후, 이 두 값을 합해서 새 cell state로 업데이트 
(인풋과 아웃풋의 취합)
- **`Output gate`** : 어떤 값을 내보낼지 해당하는 output gate를 만들고,
이를 곱해서 $h_t$가 현재 아웃풋이 된 뒤, 다음으로 넘어감

---

![](https://velog.velcdn.com/images/leejy1373/post/528fa6ab-1bd2-478f-aca5-a1f7dcbef593/image.png)


>- NN 네트워크 안에서 어떤 정보와 이전 cell state를 얼마만큼 지울지 정함
- 어떤 값을 올릴지 C 틸다를 정하고, 업데이트된 cell state와 현재 올릴 데이터를 조합해 새로운 cell state를 정하고 얼마만큼 뺄지를 정해서, 최종적인 출력 값이 나옴

---

## 9. GRU

![](https://velog.velcdn.com/images/leejy1373/post/c60c7ed7-7fbf-4c7f-b218-a3664dafaabe/image.png)


>- `GRU` : 게이트가 2개 밖에 없음 (`reset gate`, `update gate`)
- `hidden state`가 곧 output
- cell state가 없고 hidden state가 바로 있음으로써 output gate가 필요 없음
  - 대신, reset gate와 update gate가 있음
- 2개의 게이트만 가지고도  LSTM과 비슷한 성능
- 똑같은 task에 대해서 GRU가 성능이 더 높기도 함 (네트워크 파라미터가 적기 때문)
    - 그런 관점에서 GRU를 많이 활용하기도 함
- 사실 `Transformer`가 나오면서 이 둘도 많이 활용 안 됨

---

<!--more-->
<br><br>

<div align="center">
소통은 제가 공부하고 공유하는 원동력이 됩니다.<br>
해당 글이 도움이 되셨다면 소중한 격려와 응원 부탁드립니다 ☺️
</div>  