---
layout:   post
title:    "AI 서비스 기획 01 - 사용자 니즈와 성공의 정의 (User Needs + Defining Success)"
subtitle: "사용자 니즈와 성공의 정의 (User Needs + Defining Success)"
category: 서비스-기획
tags:     기획 AI
image:
  path:   /assets/img/2023-03-07/AS01.png
---
# AI 서비스 기획 01 - 사용자 니즈와 성공의 정의 (User Needs + Defining Success)

안녕하세요, Daisy 입니다 ☺️ <br>

현재 ‘서비스 기획’ 직무를 준비하고 있고, 특히 AI를 활용한 서비스 기획 직무에 가장 관심이 많습니다. 마침 구글의 AI 서비스 R&D 조직에서 제작한 “People + AI Guidebook”이라는 좋은 자료를 발견해서 스터디 후 정리해보려고 합니다. <br>

먼저 구글의 PAIR (**People + AI Research)** 조직 소개드리면, PAIR는 AI Product를 생산적이며 즐겁고 평등하게 만들기 위해 인간 중심의 연구를 진행했으며 UX 전문가들이 AI 대해 인간 중심적 접근을 할 수 있도록 [6단계의 가이드라인](https://pair.withgoogle.com/guidebook/chapters)을 제시했습니다. <br>

저는 이 6가지 가이드라인에 대해 정리해보았으며, 본 포스팅에서는 Chapter 1에 대해 다뤄보도록 하겠습니다.

> 1. [User Needs + Defining Success (사용자 니즈와 성공의 정의)](https://bbarry-lee.github.io/%EC%84%9C%EB%B9%84%EC%8A%A4-%EA%B8%B0%ED%9A%8D/Google-AI-Service-Plan-01.html)
> 2. [Data Collection + Evaluation (데이터 수집과 평가)](https://bbarry-lee.github.io/%EC%84%9C%EB%B9%84%EC%8A%A4-%EA%B8%B0%ED%9A%8D/Google-AI-Service-Plan-02.html)
> 3. [Mental Models](https://bbarry-lee.github.io/%EC%84%9C%EB%B9%84%EC%8A%A4-%EA%B8%B0%ED%9A%8D/Google-AI-Service-Plan-03.html)
> 4. [Explainability + Trust (설명 가능성과 신뢰)](https://bbarry-lee.github.io/%EC%84%9C%EB%B9%84%EC%8A%A4-%EA%B8%B0%ED%9A%8D/Google-AI-Service-Plan-04.html)
> 5. [Feedback + Control (피드백과 제어)](https://bbarry-lee.github.io/%EC%84%9C%EB%B9%84%EC%8A%A4-%EA%B8%B0%ED%9A%8D/Google-AI-Service-Plan-05.html)
> 6. Error + Graceful Failure (오류와 정상적인 실패)


---

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}


# Chapter 1. User Needs + Defining Success

## Intro

***"최고의 AI라도 사용자에게 특별한 가치를 제공하지 못하면 실패한 것이다."***
> 
1. AI로 해결할 수 있는 사용자의 문제는 무엇일까?
2. AI는 자동화하는 것과 더불어 사람의 능력을 어떻게 강화시켜줄 수 있을까?
3. 어떻게 하면 보상 기능이 AI를 적절한 방향으로 최적화시켜줄 수 있을까?
> 

Chapter 1에서는 AI가 어떤 사용자의 문제에 적합한지, 그리고 성공을 정의하는 방법을 소개합니다.<br>
다음은 인간 중심의 Product를 만들 때 가장 중요한 요소이며 주요 고려사항은 다음과 같습니다.

1. `사용자`는 누구인지?
2. 그들의 `가치`는 무엇인지?
3. 우리는 사용자를 위해 `어떤 문제`를 풀어야 할지? 
4. 우리는 그 문제를 `어떻게 해결`해야할지?
5. 경험이 완료되었는지 `어떻게 파악`할지?
<br><br>

- **주요 고려사항**
    > 1. **`사용자 니즈와 AI의 강점의 교차점 발견` :** 이후 AI가 가치를 추가하는 방식으로 실제 문제를 해결해야 함
    > 2. **`자동화 (Automation)와 증강 (Agmentation) 평가`** : 어렵고 불쾌하거나 확장성이 필요한 작업을 자동화하고,
    >    현재 어떤 일을 하고 있는 사용자가 해결책에 동의할 수 있을 때 이상적인 형태로 볼 수 있음
    > 3. **`보상기능 설계 및 평가` :** 보상기능은 AI의 성공과 실패를 정의하는 방법으로 여러 부서와 함께 이 기능을 설계하고 Product의 다운스트림 효과를 상상하여 장기적인 사용자 이점을 최적화하며, 가능하면 이 기능을 사용자와 공유하는 것이 좋음 

---

## 1. 사용자 니즈와 AI 강점의 교차점 발견

전체 단계 중 가장 중요한 단계는 ‘**`해결해야 할 문제를 정의하는 것`’**입니다. 첫 번째 단계는 사람들이 도움을 필요로 하는 실제 문제들을 확인해야 합니다. 다음으로 가상의 앱인 ‘RUN’에 대한 사용자의 니즈는 다음과 같다고 가정해봅시다.

- **사용자의 니즈**
    > 1. 사용자는 달릴 때 지루하거나 중간에 그만두지 않도록 더 다양한 방법의 달리기를 시도하고 싶음
    > 2. 사용자는 매일 앱의 실행 기록을 추적하여 6개월 안에 10k를 계획하고 싶음
    > 3. 사용자는 비슷한 수준의 다른 러너를 만나 동기부여를 얻고 싶음

우리는 항상 책임감 있는 방법으로 AI를 구축하고 사용해야 합니다. 우선, **`제품 개발 프로세스 초기에 다양한 사용자의 의견을 수용`**해야 합니다. 다양한 관점의 이야기를 수용하면 주요 시장 기회를 놓치거나 의도치 않게 특정 사용자 그룹을 배제하는 오설계를 방지할 수 있습니다.

---

## 2. 기존 워크플로우 매핑과 사용자 조사

기존 워크플로우를 매핑하는 것은 AI가 사용자의 경험을 개선할 기회를 발견하는 좋은 방법이 될 수 있습니다. 사람들이 **<U>기존 프로세스를 완료하는 방법을 살펴보면서 필요한 단계를 더 잘 이해하고 자동화하거나 강화할 수 있는 측면을 발견</U>**할 수 있습니다. 
또한 AI를 탑재한 제품이 이미 있는 경우, 사용자 조사를 실시해 전제 조건을 테스트해야 합니다. 이는 **`사용자가 Product를 사용할 때, 프로세스의 특정 측면을 자동화한 결과에 대해 어떻게 생각하는지`** 확인해야 합니다.

---

## 3. AI가 가치를 창출하는지 판단하는 방법

개선하고자 하는 측면을 파악한 다음은 AI 도입 시, **`강화가 되는 솔루션`**인지 **`성능이 저하되는 솔루션`**인지 판단해야 합니다. 오히려 AI를 도입함으로써 문제를 개선할 수 있을지 의문이 들 수 있으며, 이는 규칙 또는 휴리스틱 기반 솔루션이 AI 버전보다 낫지는 않더라도 똑같이 잘 작동하기 때문입니다. 또한 심플한 솔루션은 빌드, 설명, 디버깅 및 유지보수가 훨씬 용이하다는 이점이 있기 때문에 **`Product에 AI를 도입하면 UX가 개선될지 혹은 퇴보될지 비판적으로 고려`**해야 합니다. 다음은 AI 접근 방식이 규칙 기반 접근 방식보다 나은 경우와 그렇지 않은 경우입니다.

- **3-1. Case 1 : AI의 도입이 좋은 경우와 예시**
>- **`콘텐츠 추천` :** 넷플릭스 혹은 유튜브와 같은 개인 맞춤형 콘텐츠 추천과 같은 경우
>- **`미래 사건의 예측` :** 11월 말 덴버 행 비행기 표 가격을 예측 후 표시하려는 경우
>- **`개인화를 통한 UX 향상` :** 가정용 자동 온도 조절기를 개인화한다면, 집이 더 편안해질 뿐만 아니라 시간에 따라 온도 조절 장치의 효율성이 향상됨
>- **`자연어 이해`** : STT와 같은 받아쓰기 소프트웨어는 AI가 다양한 언어와 언어 스타일에 잘 작동되어야 함
>- **`엔터티 클래스 전체의 인식` :** 모든 얼굴 사진을 태그하는 것은 어렵기 때문에, AI를 활용한 얼굴인식을 통해 두 장의 사진을 같은 사람으로 인식시킴
>- **`낮은 발생률의 변동성 이벤트 감지` :** 신용카드 사기는 지속적으로 진화하고 있으며 개인에게 드물게 발생하지만 대규모 집단에서 자주 발생함 → AI는 진화하는 패턴을 학습하여 새로운 종류의 사기가 발생하면 탐지할 수 있음
>- **`특정 도메인의 에이전트 또는 봇`** : 호텔 예약은 다수의 사용자에 대해 유사한 패턴이 존재하기 때문에 프로세스를 신속하게 수행하기 위해 자동화할 수 있음
>- **`동적 콘텐츠의 표시` :** 동적 콘텐츠를 표시하는 것은 예측 가능한 인터페이스보다 효율적으로 볼 수 있으며, 스트리밍 서비스에서 AI가 생성한 제안은 사용자가 찾기 어려운 새로운 콘텐츠를 제시함


**`동적 콘텐츠`** : 정적 콘텐츠와 다르게 동적 콘텐츠는 누가, 언제, 어떻게 서버에 요청했는지에 따라 다른 내용이 보여지는 콘텐츠로, 예를 들면 개인 사용자가 접속하는 쇼핑몰의 장바구니, 유튜브 계정의 사용패턴에 따라 추천하는 맞춤 채널 등 사용자별 맞춤 정보 제공하는 것을 예로 들수 있음
{:.note}

---

- **3-2. Case 2 : AI의 도입이 좋지 않은 경우와 예시**
>- **`예측 가능성 유지` :** 핵심 경험의 가장 중요한 부분은 추가 사용자 입력과 관계없는 예측 가능성으로, "홈", "취소", “뒤로가기” 버튼은 같은 위치에 있을 때 탈출구로 사용하기가 더 쉬움
>- **`정적인 정보나 제한된 정보의 제공` :** 신용카드 입력 양식은 단순하고 표준적이며 사용자에 따라 정보 요건이 크게 달라지지 않음
>- **`비용이 많이 드는 오류의 최소화` :** 오프로드 경로를 제안하는 내비게이션 가이드와 같이 몇 초의 이동 시간을 절약하기 위해 오류 비용이 매우 높은 경우
>- **`완전한 투명성`** : 사용자, 고객 또는 개발자가 오픈 소스 소프트웨어 등 코드에서 발생하는 모든 것을 정확하게 이해할 필요가 있는 경우 → AI가 항상 그런 수준의 설명성을 제공할 수 없음
>- **`높은 속도와 낮은 비용을 위한 최적화` :** AI를 도입함으로써 발생하는 가치 뿐 아니라, 빠른 개발 속도와 시장의 출시는 비즈니스의 다른 무엇보다 중요함
>- **`고부가가치 작업 자동화` :** 사람들이 AI로 자동화되거나 증강되는 작업을 원하지 않는다고 명시적으로 정의한 경우 AI의 도입은 적절하지 않음


**"___에 AI를 도입할 수 있는가?"라고 묻는 대신 다음과 같은 질문을 통해 인간 중심의 AI 솔루션을 탐색** <br>
→ 1. ___를 어떻게 해결할 수 있을까? <br>
→ 2. AI가 이 문제를 독특한 방법으로 해결할 수 있을까? <br>
{:.note}

---

## 4. 자동화 (Automation)와 증강 (Augmentation)의 비교 평가

해결하고자 하는 문제를 정의하고 AI를 도입하는 것이 올바른 접근법이라고 판단하면, 다음 단계는 **`AI가 문제를 해결할 수 있는 다양한 방법을 평가하고 사용자의 목표 달성을 돕는 것`**입니다. 이 때, 고려해야할 사항은 **`AI를 사용하여 작업을 자동화할 것인지, 아니면 작업자가 직접 수행할 수 있는 능력을 강화할 것인지 여부`**입니다. 사용자 입장에서 AI가 처리해 주었으면 하는 작업도 있지만, 스스로 하고 싶은 작업 또한 존재합니다. 후자의 경우, AI는 사용자가 동일한 작업을 더 빠르고 효율적으로 또는 더 창의적으로 수행하도록 도울 수 있습니다. 더불어 자동화와 증강이 함께 이루어진다면 길고 복잡한 프로세스의 결과를 단순화하고 개선할 수 있습니다.

---

## 5. 자동화 시기

일반적으로 자동화는 바람직하지 않은 작업을 완전히 피할 수 있도록 하거나 시간, 비용 또는 노력에 대한 투자가 가치가 없을 때 선호됩니다. 이러한 작업은 일반적으로 감독이 필요하지 않거나 누구나 수행할 수 있기 때문에 AI에 쉽게 위임할 수 있습니다. 대부분의 자동화의 성공 여부는 다음과 같이 평가됩니다.

> 1. 효율성 향상
2. 안전성 향상
3. 번거로운 작업 감소
4. 자동화 없이는 불가능했던 새로운 경험 실현
> 

자동화는 **`인간의 약점을 보완하는 작업에 가장 적합`**합니다. 예를 들어 사람이 사진을 분류하거나 피사체 별로 분류하는 데는 매우 오랜 시간이 걸리지만, AI는 피드백 없이도 빠르고 쉽게 분류 할 수 있습니다. 다음과 같은 경우 자동화를 고려하면 좋습니다.

> 1. 특정의 가치를 찾기 위해서 스프레드시트의 수천 개의 행을 검색하는 것과 같은 작업
2. 문서에 대한 철자 검사
3. 가스 누출 여부를 후각으로 확인하는 것은 위험하므로 센서를 사용해 감지
> 

반면, 자동화를 선택하는 경우에도 **`사람이 감독하고 필요한 경우 개입할 수 있는 옵션`**이 있어야 합니다. 이러한 옵션은 사용자가 AI가 자동화하는 기능을 미리보기, 테스트, 편집, 실행 취소를 할 수 있도록 하는 것입니다.

## 6. 증강 시기

---

사람들은 일반적으로 **<U>AI가 업무를 완전히 자동화하기 보다는 기존의 능력을 강화하고 "초능력"을 부여하는 것을 선호</U>**하는 많은 상황들이 있으며, 증강에 성공했는지 여부는 다음과 같이 평가됩니다.

> 1. 사용자의 작업 즐거움 향상
2. 자동화에 대한 사용자 제어 수준 향상
3. 사용자의 책임과 이행 능력 향상
4. 사용자가 작업을 확장할 수 있는 능력 향상
5. 창의성 향상
> 

증강은 일반적으로 더 복잡하고 본질적으로 인간적이며 개인적으로 가치가 있습니다. 예를 들어, 최근 ChatGPT의 경우 콘텐츠 제작 시 가이드나 아이디어를 얻을 수 있고 코드 오류에 대한 해결책을 빠르게 제시하는 등 다양한 분야의 사용자들에게 창의성 및 생산성 향상과 이행 능력 향상, 작업 확장에 큰 기여를 하고 있습니다. 다음과 같은 경우 기존 능력을 강화하는 것을 고려합니다.

1. **사람들은 그 일을 즐길 때,**
> 만약 작곡을 즐긴다면, 아마 AI가 모든 곡을 써주는 것을 원하지 않을 것입니다. 반면, Magenta Studio와 같은 것을 사용하면 예술적 과정의 본질적인 인간성을 잃지 않고 창작 과정에서 도움이 될 수 있습니다.

2. **결과에 대한 개인적 책임이 요구되거나 중요시 될 때,**
> 사람들은 항상 작은 호의를 주고 받으며 누군가에게 호의를 베푸는 것의 일부는 시간과 에너지를 포기함으로써 얻는 사회적 자본입니다. 사람들은 자신이 맡은 사회적 의무를 이행하기 위해 통제권과 책임을 유지하는 것을 선호합니다.

3. **상황에 대한 이해 관계도가 높을 때,**
> 사람들은 조종사, 의사, 경찰 등 자신의 역할에 대한 위험이 높을 때 통제권을 유지하기를 원하거나 유지해야 합니다. 이는 누군가가 높은 사다리에서 안전하게 내려오는 것과 같은 물리적 이해 관계, 사랑하는 사람에게 감정을 말하는 것과 같은 감정적 이해 관계, 신용카드나 은행 정보 공유와 같은 금전적 이해 관계가 될 수 있습니다. 또한, 때로는 직무에 대한 개인적인 책임이 법적으로 요구되기도 합니다. 반면, 스트리밍 서비스에서 노래 추천을 받는 것과 같이 이해 관계가 낮은 상황에서 사람들은 낮은 오류 비용보다 새롭고 좋은 음악을 추천해주는 발견 가능성이 더 중요하기 때문에 통제권을 포기하는 경우가 많습니다.

4. **특정 선호 사항을 전달하기 어려울 때,**
> 사람들은 방을 꾸미고 파티를 계획하거나, 디자인하는 등 자신이 원하는 작업 방식에 대한 스타일이 존재하지만, 이는 말로 정의하기 어려울 때가 많습니다. 이런 종류의 상황에서 사람들은 자신의 비전을 볼 수 있도록 통제력을 유지하는 것을 선호합니다. 반면, 사람들이 비전이 없거나 비전에 투자할 시간이 없을 때 자동화를 선호할 가능성이 더 큽니다.


**사용자가 자동화와 증강에 대해 어떻게 생각하는지 파악하기 위해 질문할 수 있는 예시** <br>
1) 비슷한 역할을 맡을 새 동료를 교육하는 데 도움을 준다면 먼저 가르칠 가장 중요한 작업은 무엇인지?<br>
2) 1번 답변에 대해 얼마나 자주 수행하는지?<br>
3) 이 작업을 함께 수행할 비서가 있다고 가정한다면 부여할 수행 임무는 무엇인지?<br>
{:.note}

---

## 7. 보상기능 설계 및 평가

**`"손실 함수 (loss function)"`**는 AI 모델이 "올바른" 예측과 "잘못된" 예측을 결정하는 데 사용되는 수학 공식입니다. 이는 시스템이 최적화하려고 시도할 작업 또는 동작을 결정하고 최종 사용자 경험의 주요 동인이 됩니다. **<U>보상 기능을 설계할 때 사용자의 최종 경험에 큰 영향을 미치는 중요한 결정사항들을 정의해야하며 여러 분야의 협업 프로세스</U>**가 이루어져야 합니다. 이는 **`최소한 UX, 제품 및 엔지니어링 측면이 포함`**되어야 하고, **`프로세스 전반에 걸쳐 가능한 결과에 대해 생각하고 아이디어를 소통`**해야 합니다. 이러한 과정은 앞으로 보상 기능이 잘못된 결과로 최적화하는 것을 방지하는 것에 도움이 될 것입니다.

---

## 8. 잘못된 긍정과 부정의 비교

많은 AI 모델은 주어진 입력 값 x (실체나 물체)가 특정 범주 y에 속하는지 여부를 예측합니다. 이러한 종류의 모델을 "이진 분류기"라고 하며, 다음 네 가지 결과가 나올 수 있습니다.

> `TP (True Positives)` : 양의 결과를 올바르게 예측하는 경우 <br>
`TF (True Negatives)` : 음의 결과를 올바르게 예측하는 경우 <br>
`FP (False Positives)` : 양의 결과를 잘못 예측한 경우 <br>
`FN (False Negatives)` : 음의 결과를 잘못 예측한 경우 <br>
> 
> 
> ![https://pair.withgoogle.com/assets/UN_Vis_01.png](https://pair.withgoogle.com/assets/UN_Vis_01.png)
> 

가상의 앱 RUN에서 AI 모델을 사용하여 사용자에게 실행을 권장한다고 가정해봅시다. 그리고 모델의 결과는 다음과 같습니다.

> `TP (True Positives)` : 모델은 사용자가 좋아하는 달리기를 제안 O  <br>
`TF (True Negatives)` : 모델은 사용자가 좋아하지 않는 달리기를 제안 X   <br>
`FP (False Positives)` : 모델은 사용자가 좋아하지 않는 달리기를 제안 O <br>
`FN (False Negatives)` : 모델은 사용자가 좋아하는 달리기를 제안 X <br>
> 

보상 기능을 정의할 때 결과를 다르게 측정할 수 있습니다. FP와 FN의 비용을 측정하는 것은 사용자의 경험을 형성하는 중요한 결정입니다. 기본적으로 둘 다 동등하게 가중치를 두는 것이 좋지만, 이는 실제 사용자들에게 미치는 영향과 일치하지 않을 수 있습니다. 예를 들어, 불이 안 났는데 경보가 잘못 울리는 것 (FP)보다 불이 났을 때 경보가 울리지 않는 것 (FN)이 훨씬 더 위험에 노출됩니다. 반면에, 가끔 사용자가 좋아하지 않는 노래를 추천하는 것 (FP)은 그렇게 치명적이지 않으며 사용자가 다음으로 건너뛰면 그만입니다. 다음과 같이 특정 출력 또는 결과에 대한 신뢰 지표를 포함하면 이러한 유형의 오류로 인한 부정적인 영향을 완화할 수 있습니다.

---

## 9. 정밀도 (Precision)와 재현율 (Recall)의 Tradeoffs 검토

정밀도와 재현율은 AI가 사용자에게 제공하는 결과의 폭과 깊이, 사용자가 보는 오류 유형을 나타내는 용어입니다.

1. **`정밀도`**는 모든 `TP, FP` 중 **`올바르게 분류된 TP의 비율`**을 의미합니다. 정밀도가 높을수록 모델의 출력이 정확하다는 확신을 가질 수 있습니다. 그러나 트레이드 오프는 관련 가능성이 있는 결과를 제외하여 False Negatives의 수를 증가시킨다는 것입니다. 예를 들어 위의 모델이 정밀도에 최적화되어 있는 경우 사용자가 계속 진행하도록 선택할 수 있는 모든 단일 실행을 권장하지는 않지만 권장한 모든 실행이 사용자에 의해 수락될 것이라고 확신할 수 있습니다. **<U>사용자에게는 자신의 기본 설정과 일치하지 않는 실행이 거의 표시되지 않지만 전반적으로 더 적은 제안이 표시</U>**될 수 있습니다.
<br><br>
2. **`재현율`**은 모든 `TP, FN` 중 **`올바르게 분류된 TP의 비율`**을 의미합니다. 재현율이 높을수록 모든 관련 결과가 출력의 어딘가에 포함된다는 확신을 가질 수 있습니다. 그러나 관련이 없을 가능성이 있는 결과를 포함하여 False Positives의 수를 늘릴 수 있다는 단점이 있습니다. **<U>사용자가 계속하기를 원하는 모든 실행을 권장하고 사용자가 계속하기를 선택하지 않는 다른 실행을 포함하는 모델</U>**이라고 생각할 수 있습니다. 사용자는 해당 실행이 자신의 기본 설정과 일치하지 않더라도 항상 실행에 대한 제안을 받게 됩니다.

![https://pair.withgoogle.com/assets/UN_Vis_02.png](https://pair.withgoogle.com/assets/UN_Vis_02.png)
<br><br>

정밀도 또는 재현율을 최적화할 때의 트레이드오프를 나타내는 다이어그램입니다. 왼쪽에서 정밀도를 최적화하면 False Positives의 수를 줄일 수 있지만 False Negatives의 수는 증가할 수 있습니다. 오른쪽에서 재현율을 위해 최적화하면 더 많은 True Positives을 포착할 수 있지만 False Positives의 수도 증가합니다.

이러한 트레이드오프를 위해 특별히 설계할 필요가 있습니다. 범위 내에서 사용자의 예상과 작업 완성도를 바탕으로 Product를 설계해야하며, 정밀도와 재현율의 균형을 사용자와 함께 테스트해야 합니다.


**정밀도와 재현율 Tradeoffs에 대한 생각** <br>
만약 ‘암 세포 진단 AI 모델’이 있다고 가정한 경우 정밀도 (Precision)를 고려하여 모델을 구축한다면, False Negatives, 즉 ‘암 세포가 존재하는데 암 세포가 아니다.’ 라고 오진단할 가능성이 높아질 수 있다. 암 세포 진단은 생명과 직결되기 때문에, 이러한 경우 정밀도보다는 재현율 (Recall)을 높일 수 있도록 보수적으로 모델을 구축해야 할 것입니다. 재현율은 False Positives의 수가 증가되어 ‘암 세포가 존재하지 않는데 암 세포가 존재한다.’라고 오진단할 수도 있지만, 환자의 생명을 고려한다면 정밀도를 최적화하여 발생한 전자의 오진단 상황보다는 나을 것으로 생각합니다.
{:.note}

---

## 10. 보상 기능 결과 평가

다음 단계는 보상 기능을 평가하는 것입니다. 성공에 대한 모든 정의와 마찬가지로, 단순하고 즉각적으로 만드는 것이 매력적일 것입니다. 그러나, 단순하고 좁으며 즉각적인 보상 기능을 시간이 지남에 따라 광범위한 청중에게 적용하면 부정적인 영향이 있을 수 있습니다. 다음은 보상 기능을 평가할 때 고려해야 4가지 사항입니다.

1. **포괄성 평가**
>포괄적이라는 것은 제품을 누가 사용하고 있는지를 이해하는 데 시간을 할애하여 다양한 배경과 관점, 그리고 인종, 성별, 나이, 체형 등의 차원에 걸쳐 사용자 경험이 공평하다는 것을 확인하는 것입니다. **`AI는 처음부터 공정성을 염두에 두고 설계해야 하며, 이는 포괄적으로 구축하기 위한 필수 단계`**입니다. Facets 및 What-If Tool과 같은 오픈 소스 도구 등을 사용하여 **`데이터셋의 잠재적인 편향을 검사`**해야 합니다.

2. **시간 경과에 따른 관찰**
>시간 경과에 따른 의미도 고려해야 합니다. 단기적으로는 공유 수를 최적화하는 것이 좋은 생각처럼 보일 수 있지만, 시간이 지남에 따라 사용자에게 공유 알림이 폭주하는 것은 당황스러운 경험이 될 수 있습니다. 100일 또는 1,000일째에 제품을 사용한 개인 및 단체 사용자 경험을 상상해보고, **`장기적으로 어떤 행동과 경험을 최적화해야 할지 생각`**해야 합니다.

3. **잠재적 위험 예측**
>2차 효과는 특정 행동의 결과로 인한 결과로 볼 수 있습니다. 이들은 예측하기 어렵지만, 보상 기능을 설계할 때 고려할 가치가 있습니다. 한 가지 유용한 질문은 **`"보상 (리워드) 기능이 완벽하게 최적화되면 사용자, 그들의 친구 및 가족, 그리고 더 큰 사회에 어떤 파급효과가 나타날까?”`** 입니다. 예를 들어 검색 쿼리를 위해 최적의 웹 페이지로 이동하도록 최적화하는 것은 좋을 수 있습니다. 하지만 사람들의 관심을 하루 종일 지속적으로 유지하도록 최적화하는 것은 장기적으로 이익을 제공하지 못할 수도 있습니다.

4. **잠재적 위험 관리**
>AI가 활발히 도입됨에 따라 제품 결정의 부정적인 영향에 대한 계획과 모니터링이 더욱 중요해지고 있으며, 다양한검증 프로세스에도 불구하고 잠재적인 위험을 사전에 모두 발견하는 것은 어려울 것입니다. 대신 **`추적해야 할 잠재적인 불량 결과 및 측정항목을 식별하기 위해 정기적인 프로세스를 구축`**해야 합니다.
<br><br>

AI를 도입함으로써 발생될 수 있는 잠재적인 부정적 결과를 해결하기 위해서는 다음과 같은 표준 및 지침을 설정할 수 있습니다.
> 1. 스마트 플레이리스트와 경로에 대한 사용자의 평균 거부율이 20%를 넘으면 ML 모델을 검토한다.
2. 60% 이상의 사용자가 앱을 다운로드하고 사용하지 않는다면 마케팅 전략을 검토한다.
3. 사용자가 앱을 자주 열지만 실행이 25%만 되는 경우 UX를 체크하고 잠재적 알림 빈도를 검토한다.
> 

Product가 발전함에 따라 **`고려하지 않은 이해관계자에게 부정적인 영향이 있는지 피드백을 확인`**해야 합니다. 일부 이해관계자가 부정적인 영향을 받는 것을 발견하면, 그들의 상황을 이해하기 위해 소통해야 합니다. 이러한 **`소통을 바탕으로 지속적인 부정적인 영향을 피하기 위해 제품을 조정하는 방법을 전략화`**해야 합니다. 부정적인 영향을 감시하는 쉬운 방법은 소셜 미디어나 Google Alerts와 같은 시스템이 있습니다. 이처럼 사용자의 소리에 귀를 기울이고 의도하지 않은 잠재적인 결과를 가능한 한 빨리 파악해야 합니다.


팀의 모든 구성원은 기능의 성공과 실패가 어떻게 보이는지, 문제가 발생했을 때 팀에 알리는 방법에 대해 일치감을 느껴야 하며, 이에 대한 예제 프레임워크는 다음과 같음 <br>
→ __ {특정 기능}이(가) __ {특정 지표, 임계값} 대비 하락 혹은 상승하는 경우 __ {특정 조치} 수행
{:.note}

---

## 11. Conclusion
지금까지 사용자의 니즈를 파악하고 AI 서비스를 기획하기 위해 필요한 첫 번째 가이드라인을 정리해보았습니다. 성공적인 Product 기획을 위해 문제를 정의하고 사용자 니즈에 맞추는 것은 첫 번째 단계이며, 니즈를 찾은 후에는 정의한 문제에 대해 AI가 고유하게 해결할 수 있는지 평가해야 합니다.
다음으로는 자동화 (Automation) 혹은 증강 (Augmentation)해야 하는지 고려해야 하며, 장기적으로 모든 사용자에게 훌륭한 사용자 경험을 제공하도록 보상 기능을 설계하고 결과에 대해 평가해야 합니다. <br><br>

가이드라인의 전반적인 내용을 6가지로 요약하면 다음과 같습니다.<br><br>

1. **해결해야 할 문제를 정의하고 사용자 니즈와 AI 강점의 교차점 발견**<br>
>    → 제품 개발 프로세스 초기에 다양한 사용자의 의견 수용 <br>
>    → 기존 워크플로우 매핑하여 자동화 혹은 강화할 수 있는 측면을 발견하고 사용자의 생각 조사<br>

2. **AI가 가치를 창출하는지 판단하는 방법**<br>
>    → AI 도입 시, 강화가 되는 솔루션인지 성능이 저하되는 솔루션인지 판단<br>
>    → Product에 AI를 도입하면 UX가 개선될지 혹은 퇴보될지 비판적으로 고려<br>

3. **자동화 (Automation)와 증강 (Augmentation)의 비교 평가** <br>
>    → **자동화 성공 여부** : 효율성 및 안전성 향상, 번거로운 작업 감소, 자동화 없이 불가능했던 새로운 경험 실현<br>
>    → **증강 성공 여부** : 작업 즐거움 · 자동화에 대한 사용자 제어 수준 · 책임과 이행 능력 · 작업을 확장할 수 있는 능력 · 창의성의 향상
    
4. **보상 기능 설계 및 평가**<br>
>    → 보상 기능을 설계 시 사용자의 최종 경험에 큰 영향을 미치는 결정사항들을 정의해야 함<br>
>    → 여러 분야의 협업이 이루어져야 하며, 최소한 UX, 제품 및 엔지니어링 측면이 포함되어야 함<br>
>    → 프로세스 전반에 걸쳐 가능한 결과에 대해 생각하고 아이디어를 소통해야 함<br>

5. **정밀도 (Precision)와 재현율 (Recall)의 Tradeoffs 검토**<br>    
>    → 사용자의 예상과 작업 완성도를 바탕으로 설계해야 하며, 정밀도와 재현율의 균형을 사용자와 함께 테스트해야 함<br>
    
6. **보상 기능 결과 평가**<br>
>    **→ 포괄성 평가 :** AI는 공정성을 염두에 두고 설계하고 데이터셋의 잠재적인 편향을 검사해야 함<br>
>    **→ 시간 경과에 따른 관찰** : 장기적으로 어떤 행동과 경험을 최적화해야 할지 생각해야 함<br>
>    **→ 잠재적 위험 예측 :** 사용자, 그들의 친구 및 가족, 그리고 더 큰 사회에 어떤 파급효과가 나타날까?<br>
>    **→ 잠재적 위험 관리**<br>
>>        1) 추적해야 할 잠재적인 불량 결과 및 측정항목을 식별하기 위해 정기적인 프로세스를 구축
>>        2) 고려하지 않은 이해관계자에게 부정적인 영향이 있는지 피드백을 확인
>>        3) 소통을 바탕으로 지속적인 부정적인 영향을 피하기 위해 제품을 조정하는 방법을 전략화


<br><br>
다음은 Chapter 2 "데이터 수집과 평가 (Data Collection + Evaluation)"를 정리해보겠습니다. <br>


Next series [Data Collection + Evaluation](Google-AI-Service-Plan-02){:.heading.flip-title}
{:.read-more}
<br><br>

---

<!--more-->

<br><br>

<div align="center">
소통은 제가 공부하고 공유하는 원동력이 됩니다.<br>
해당 글이 도움이 되셨다면 소중한 격려와 응원 부탁드립니다 ☺️
</div>  