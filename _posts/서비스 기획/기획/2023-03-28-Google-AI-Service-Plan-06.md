---
layout:   post
title:    "AI 서비스 기획 06 - 오류와 정상적인 실패 (Errors + Graceful Failure)"
subtitle: "Mental Models"
category: 서비스-기획
tags:     기획 AI
image:
  path:   /assets/img/2023-03-07/AS06.png
---
# AI 서비스 기획 06 - 오류와 정상적인 실패 (Errors + Graceful Failure)

안녕하세요, Daisy 입니다 ☺️ <br>

구글의 AI 서비스 R&D 조직 PAIR에서 제작한 “People + AI Guidebook”의 [6단계의 가이드라인](https://pair.withgoogle.com/guidebook/chapters) 중 마지막 Chapter 6에 대해 다뤄보도록 하겠습니다.

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


# Chapter 6. Errors + Graceful Failure (오류와 정상적인 실패)

## Intro

***AI가 에러를 범하거나 실패하면 상황이 복잡해질 수 있습니다. 마지막 장에서는 다음을 다룹니다.***
>
**Q. 사용자는 언제 신뢰도가 낮은 예측을 "에러"로 간주할까?** <br>
**Q. 복잡한 AI에서 에러의 원인을 어떻게 신뢰있게 식별할 것인가?** <br>
**Q. AI 실패 후 AI는 사용자가 앞으로 나아갈 수 있도록 허용하는지?** <br>
> 

<br>

사용자는 Product와 상호 작용할 때 개발 과정에서 예측할 수 없는 방식으로 Product를 테스트합니다. 오해, 잘못된 시작, 부적절한 행동이 발생할 수 있으므로 이러한 경우를 위한 설계는 모든 사용자 중심 Product의 핵심 구성 요소입니다. **`에러는 기회이기도 합니다. 테스트를 통해 더 빠른 학습을 지원하고 올바른 Mental model을 설정하는 데 도움을 주며 사용자가 피드백을 제공하도록 장려`**할 수 있습니다. AI 기반 시스템에서 에러를 해결하기 위한 주요 고려 사항은 다음과 같습니다.

> 1. **`"Error (오류)"와 "Failure (실패)" 정의` :** 사용자가 에러라고 생각하는 것은 AI 시스템에 대한 사용자의 기대와 깊은 관련이 있음. 예를 들어 60%의 시간 동안 유용한 추천 시스템은 사용자와 시스템의 목적에 따라 실패 또는 성공으로 보일 수 있음. 이러한 상호 작용을 처리하는 방법은 Mental model을 설정 및 수정하고 사용자 신뢰를 조정해야 함
> <br><br>
> 2. **`에러 원인의 식별` :** AI 시스템을 사용하면 에러가 여러 곳에서 발생할 수 있고 식별하는 것이 더 어려우며 사용자와 시스템 작성자에게 직관적이지 않은 방식으로 나타날 수 있음
> <br><br>
> 3. **`실패로부터의 경로 제공` :** AI 기능은 시간이 지남에 따라 변경될 수 있음. 사용자가 발생하는 에러에 대응하여 조치를 취할 수 있는 경로를 생성하면 시스템에 대한 인내심이 높아지고 사용자-AI 관계가 계속 유지되며 전반적으로 더 나은 경험을 지원함

---

## 1. "Error (오류)"와 "Failure (실패)" 정의

**`AI를 Product에 통합한다는 것`**은 **<U>사용자가 AI 시스템과 상호 작용할 때 변경되는 관계를 설정하는 것을 의미</U>**합니다. 사용자는 자신의 취향과 행동에 맞게 상호 작용이 조정되고 사용자마다 경험이 다를 것이라고 기대하게 될 것입니다. 따라서 **<U>에러를 정의하는 것은 전문 지식, 목표, Mental model 및 Product를 사용한 과거 경험에 따른 사용자마다 다를 수 있습니다.</U>**

예를 들어 누군가가 AI 기반 음악 추천 시스템이 "즐겨찾기"로 표시된 노래만 사용하여 추천을 제공한다고 가정하는 경우 시스템이 자신의 즐겨찾기 목록에 없는 장르를 추천하면 에러로 간주할 수 있습니다. 하지만 추천 시스템이 다양한 요인을 기반으로 한다고 가정하는 다른 사람은 이를 에러로 간주하지 않을 수 있죠.

<br>

- **1-1. 사용자 에러, 시스템 에러, 컨텍스트 에러의 식별**

비 AI 시스템에서 **`"사용자 에러"`**는 일반적으로 **<U>시스템 설계자의 관점에서 정의되며 사용자는 에러를 초래하는 "오용"에 대해 비난</U>**을 받습니다. 반면에 **`"시스템 에러"`**는 **<U>일반적으로 사용자의 관점에서 정의되며, 사용자는 자신의 니즈를 충족할 만큼 유연하지 않은 Product에 대해 시스템 설계자를 비난</U>**합니다.

세 번째 유형의 오류 **`“컨텍스트 에러”`**는 AI 시스템에서 **<U>사용자가 특정 시간이나 장소에서 원하는 작업에 대해 잘못된 가정을 함으로써 AI 시스템의 유용성이 떨어지는 경우</U>**입니다. 결과적으로 사용자는 혼란스러워하거나 작업에 실패하거나 Product를 완전히 포기할 수 있습니다.

개인의 라이프 스타일이나 선호도와 관련될 수 있고 패턴은 더 넓은 문화적 가치와 연결될 수 있습니다. 예를 들어 레시피 제안 앱을 사용하는 사람이 저녁에 추천 사항을 자주 거부하는 경우 이 패턴은 지속적인 이유가 있을 수 있음을 Product 팀에 알려야 합니다. 사용자가 야간 근무를 하는 경우 출근하기 전에 아침 식사 추천 사항을 선호할 수 있습니다. 반면 특정 그룹의 모든 사용자가 연중 특정 시기에 지속적으로 육류 기반 식사 제안을 거부했다면 이는 팀이 고려하지 않은 문화적 가치나 선호도와 관련이 있을 수 있습니다.

컨텍스트 오류를 방지하거나 수정하려면 AI가 사용자의 컨텍스트에 대해 가정하는 데 사용하는 신호를 살펴보고 해당 신호가 잘못되었거나 간과되었거나, 과소평가 혹은 과대평가되었는지 평가해야 합니다.

<br>

- AI가 사용자의 상황에 대해 높은 신뢰도를 가질 때 능동적 추천 사항 제공
    
    ![https://pair.withgoogle.com/assets/EF1_aim-for.png](https://pair.withgoogle.com/assets/EF1_aim-for.png)
    

- 추측에 따라 설계하면 컨텍스트 에러가 발생할 수 있음
    
    ![https://pair.withgoogle.com/assets/EF1_avoid.png](https://pair.withgoogle.com/assets/EF1_avoid.png)
    
<br>
컨텍스트 에러 및 기타 에러는 **<U>사용자 기대와 시스템 가정 간의 상호 작용</U>**으로 생각할 수 있습니다. 다음은 사용자 기대 수준과 시스템 기대 수준이 상호 작용하여 에러를 일으키는 방식에 대한 분석입니다.

<br>

- **1-2. 사용자가 인지한 에러 분류**

**`컨텍스트 에러`**는 시스템이 **`"의도한 대로 작동"`**하지만 **<U>시스템의 동작이 잘 설명되지 않았거나 사용자의 Mental model을 깨뜨리거나 잘못된 가정을 기반으로 했기 때문에 사용자는 에러를 인식</U>**합니다. 예를 들어, 친구의 항공편 확인 이메일이 나의 캘린더에 이벤트를 생성했지만 이는 원하지 않거나 필요하지 않은 경우일 것입니다.

이러한 에러를 해결하는 방법은 빈도와 심각한 정도에 따라 다릅니다. 사용자의 니즈와 기대에 더 잘 부합하도록 시스템이 **`작동하는 방식을 변경`**할 수 있습니다. 또는 **`Product의 온보딩을 조정하여 더 나은 Mental model을 설정`**하고 이러한 상황에 대한 **`사용자의 인식을 에러에서 예상 동작으로 전환`**합니다.

**`장애 상태 (Failstates)`**는 **`시스템의 내재된 한계`**로 인해 올바른 답을 제공할 수 없거나 전혀 답을 제공할 수 없는 것이며, 이는 **`True negatives`**일 수 있습니다. AI는 주어진 입력에 대해 사용 가능한 출력이 없다는 것을 식별하는 데 정확하지만 사용자는 출력 결과를 원할 것입니다.

예를 들어 이미지 인식 앱이 다양한 종류의 동물을 식별할 수 있지만 사용자가 Training dataset에 없는 동물 사진을 앱에 입력하여 식별되지 않는 경우 이 또한 True negatives인 것이죠. 따라서 **<U>사용자가 인지한 에러에 대한 메시지는 시스템의 제한 사항에 대해 가능한 구체적으로 사용자에게 알려야</U>** 합니다.

<br>
- 에러 상태를 사용하여 AI에 필요한 입력 또는 AI 작동 방식을 사용자에게 알림
    
    ![https://pair.withgoogle.com/assets/EF2_aim-for.png](https://pair.withgoogle.com/assets/EF2_aim-for.png)
    

- 다음의 상황에서 AI 시스템을 설명할 기회를 놓치지 말 것
    
    ![https://pair.withgoogle.com/assets/EF2_avoid.png](https://pair.withgoogle.com/assets/EF2_avoid.png)
    

<br>

- **1-3. 사용자의 인식이 불가능한 에러의 진단**

이러한 에러는 사용자에게 보이지 않으므로 사용자 인터페이스에서 설명하는 방법에 대해 걱정할 필요가 없지만 이러한 에러를 인식하면 AI 개선에 도움이 될 수 있습니다.

> **`Happy accidents` :** 시스템은 무언가를 잘못된 예측, 제한 또는 에러로 표시할 수 있지만, 드문 경우 긍정적 결과로 이어질 수 있음. 예를 들어, 사용자는 스마트 스피커에게 쓰레기를 버릴 수 없다는 것을 알면서 농담으로 쓰레기를 버리라고 요청했고 사용자의 가족은 이런 스피커의 응답에 즐거움을 느낌
> 

> **`Background errors`** : **<U>시스템이 올바르게 작동하지 않지만 사용자와 시스템 모두 에러의 인식이 불가능한 상황</U>**입니다. 예를 들어 검색 엔진이 잘못된 결과를 반환하고 사용자가 이를 인식할 수 없는 경우, 이러한 유형의 에러는 장기간 감지되지 않으면 심각한 결과를 초래할 수 있습니다. 또한 시스템이 고장 및 에러율을 측정하는 방법에 중요한 영향을 미치는데, 사용자 피드백에서 이러한 에러를 감지할 가능성이 낮기 때문에 시스템을 **`Stress test`**하고 "알려지지 않은 미지수"를 식별하기 위한 **`전용 품질 보증 프로세스`**가 필요함
> 

`Stress test` : 높은 수준의 스트레스나 부하에서 시스템의 성능과 안정성을 평가하는 일종의 소프트웨어 테스트로, 목적은 갑작스러운 트래픽 증가 또는 많은 수의 동시 사용자와 같은 과도한 사용량을 처리할 수 있는 시스템의 능력을 결정하기 위함이며, 스트레스 테스트 중에 시스템은 많은 양의 요청, 트랜잭션 또는 데이터로 의도적으로 과부하를 시킴. 이는 UX와 비즈니스 운영에 부정적인 영향을 미칠 수 있는 성능 문제, 다운타임 및 데이터 손실을 방지하는 데 도움이 될 수 있음
{:.note}

<br>

- **1-4. 사용자 여정에서의 타이밍 고려**

사용자는 Product **`사용 초기 발생 에러`**와 Product가 할 수 있는 것과 불가능한 것에 대해 더 큰 기대를 갖는 **`후기 발생 에러`**에 대해 다르게 반응할 수 있습니다. 사용자가 Product를 얼마나 오래 사용했는지에 따라 AI가 에러를 전달하고 사용자가 정상으로 돌아오도록 돕는 방법에 영향을 미칠 수 있습니다.

예를 들어 사용자가 처음으로 음악 추천 시스템과 상호 작용할 때 초기 추천이 자신과 관련이 없으면 에러로 간주하지 않을 수 있습니다. 그러나 1년 동안 듣고 좋아하고 즐겨찾기를 재생 목록에 추가한 후 사용자는 시스템 추천 사항의 관련성에 대한 기대수준이 높아져 관련 없는 음악 추천 사항을 에러로 간주할 수 있습니다.

<br>

- **1-5. 상황별 이해관계 및 에러 위험 평가**

AI의 에러와 실패는 심각한 결과를 초래할 수 있습니다. 예를 들어, AI가 제안한 이메일 응답의 에러는 자율주행 차량 취급과 관련된 에러와 매우 다른 이해 관계가 있습니다. 이것은 비 AI 시스템에도 해당되지만 AI 시스템의 복잡성과 컨텍스트 오류의 가능성으로 인해 AI가 결정을 내리는 각 상황의 이해 관계에 대해 추가로 생각해야 합니다.

주어진 시나리오에는 내재된 이해 관계가 있지만 에러의 위험은 다른 상황적 요인에 따라 달라질 수 있습니다. 예를 들어, 사용자가 AI 기반 Product를 사용하는 동안 멀티태스킹을 하거나 시간 압박을 받고 있는 경우 시스템 출력을 다시 확인하는 데 사용할 수 있는 정신적 자원이 줄어듭니다.

<br>

- **1-6. 잠재적인 에러에 대한 위험 측정**
    
    > `낮은 경우` 
    > - 사용자는 작업에 대한 전문 지식을 가지고 있음
    > - 매우 높은 시스템 신뢰수준
    > - 많은 성공적인 결과
    
    > `높은 경우`
    > - 사용자 작업 = 초보자
    > - 주의력 또는 응답 시간 감소 (멀티태스킹)
    > - 낮은 시스템 신뢰수준
    > - 성공적인 결과에 대한 한정적인 정의

<br>

- **1-7. 상황의 위험 평가**
    
    > `낮은 경우`
    > - 테스트
    > - 놀이 또는 창의성
    > - 가벼운 엔터테인먼트
    > - 필수적이지 않은 추천사항
    
    > **`높은 경우`**
    > - 건강, 안전 또는 재정적 결정
    > - 민감한 사회적 맥락

1) 시스템이 에러에 어떻게 대응할지 설계를 시작하기 전에 사용자가 이미 인식할 수 있거나 발생할 것으로 예측할 수 있는 에러를 식별한 후, 다음 범주로 분류하세요. <br>
→ **시스템 제한** : 우리의 시스템은 시스템에 내재된 한계로 인해 올바른 답을 제공할 수 없거나 전혀 답을 제공할 수 없음<br>
→ **컨텍스트 :** 시스템은 "의도한 대로 작동"하지만 사용자는 시스템의 동작이 잘 설명되지 않았거나 사용자의 Mental model을 깨뜨리거나 잘못된 가정을 기반으로 했기 때문에 에러를 인식<br>
<br>
2) 백그라운드 에러, 즉 시스템이 제대로 작동하지 않지만 사용자나 시스템 모두 에러를 등록하지 않는 상황을 주의하세요. 또한, 위의 각 상황에 대해 질문해보세요.<br>
→ 이 에러는 사용자에게 어떤 영향을 줍니까?<br>
→ 이 상황에서 사용자의 이해 관계가 높거나 낮습니까?<br>
{:.note}

---

## 2. 에러 원인 식별

사용자 요구 + 성공 정의 장에서는 AI가 출력을 최적화하는 데 사용하는 보상 기능을 설계하고 평가하는 방법을 보여줍니다. 시스템에서 발생할 수 있는 에러의 범위와 유형은 이 보상 기능에 따라 다르지만 일반적으로 AI 고유의 여러 에러 원인이 있습니다.

<br>

- **2-1. 예측 및 학습 데이터 에러 발견**
    
    > 이러한 에러는 **<U>학습 데이터의 문제와 모델 Tuning 방식에서 비롯</U>**됩니다. 예를 들어 내비게이션 앱에 특정 지리적 지역의 도로에 대한 학습 데이터가 없을 수 있어 기능이 제한될 수 있습니다.
    > 

<br>

- **2-2. Label이 잘못 지정되었거나 잘못 분류된 결과**
    
    > **<U>학습 데이터가 좋지 않아 시스템의 출력에 Label이 잘못 지정되거나 분류된 경우</U>**입니다. 예를 들어, 식물 분류 앱의 학습 데이터에서 일관되지 않게 Label이 지정된 베리는 딸기를 라즈베리로 잘못 분류하게 합니다.
    > 
    > **`Response`** : 사용자가 가이드라인을 제공하거나 데이터 또는 Label을 수정할 수 있도록 허용하여 Dataset를 개선하거나 팀에 추가 학습 데이터의 필요성을 알리기 위해 모델로 피드백

<br>

- **2-3. 잘못된 추론 또는 모델**
    
    > 충분한 학습 데이터가 있음에도 불구하고 **<U>ML 모델이 충분히 정확하지 않은 경우</U>**입니다. 예를 들어, 식물 분류 앱에는 딸기가 포함된 Label이 잘 지정된 Dataset이 있지만 모델 Tuning이 불량하면 딸기를 식별할 때 많은 수의 False positives가 반환됩니다.
    > 
    
    > **`Response`** : 사용자가 가이드라인을 제공하거나 데이터 또는 Label을 수정하도록 허용하여 AI 모델로 다시 피드백하고 Tuning하는 데 도움을 줌
    > 

<br>

- **2-4. 누락되거나 불완전한 데이터**
    
    > **<U>사용자가 학습 데이터를 기반으로 모델이 수행할 수 있는 한계에 도달한 경우</U>**입니다. 예를 들어 사용자가 강아지에게 식물 분류 앱을 사용하려고 하는 경우입니다.
    
    > **`Response`** : 시스템이 수행해야 하는 작업과 작동 방식을 전달하고 누락된 부분이나 제한 사항을 설명, 이로써 사용자가 시스템이 충족하지 못하는 니즈에 대한 피드백을 제공할 수 있음
    > 

<br>

- **2-5. 입력 오류 예측 또는 계획**
    
    > 이러한 에러는 **<U>AI가 실제로 할 수 있는지 여부에 관계없이 시스템이 실제로 내가 의미하는 바를 "이해"할 것이라는 사용자의 기대에서 비롯</U>**됩니다.

<br>

- **2-6. 예상치 못한 입력**
    
    > 사용자가 AI 시스템에 대한 **<U>입력의 자동 수정을 예상하는 경우</U>**입니다. 예를 들어, 사용자가 오타를 만들고 시스템이 의도한 철자를 인식하기를 기대합니다.
    > 
    
    > **`Response`** : 사용자의 입력과 "예상" 답변의 범위를 확인하여 해당 입력 중 하나를 의도했는지 확인함 (예를 들어 "XYZ를 검색하려고 했습니까?")
    > 

<br>

- **2-7. 습관화 깨기**
    
    > 사용자가 **<U>시스템 UI와 습관적인 상호 작용을 구축했지만 변경으로 인해 작업이 다른 원치 않는 결과로 이어지는 경우</U>**입니다. 예를 들어 파일 저장 시스템에서 사용자는 항상 인터페이스의 오른쪽 상단 영역을 클릭하여 폴더에 액세스했지만 새로 구현된 AI 기반 동적 설계로 인해 폴더 위치가 자주 변경됩니다. 이는 **`Muscle memory`**로 인해 해당 영역을 클릭하면 이제 잘못된 폴더가 열리겠죠.
    > 
    
    > **`Response`** : 예측하기 어려운 AI 출력 결과에 대해 인터페이스의 특정 영역을 지정하는 등 습관화를 깨지 않는 방식으로 AI를 구현, 또는 사용자가 특정 상호 작용 패턴으로 되돌리거나 선택하거나 재교육
    > 

**`Muscle memory` :** 규칙적으로 훈련하고 연습한 후 시간이 지남에 따라 특정 움직임이나 활동을 더 쉽고 효율적으로 반복하는 근육의 능력을 설명하는 데 사용되는 용어로, 이는 개인이 반복적인 연습과 경험을 통해 복잡하거나 반복적인 작업을 보다 쉽고 빠르게 수행할 수 있는 능력을 의미하며 코딩, 데이터 입력, 특정 소프트웨어 또는 도구 사용과 같은 작업에 적용될 수 있음
{:.note}

<br>

- **2-8. 잘못 보정된 입력**
    
    > 시스템이 **<U>행동이나 선택에 부적절하게 가중치를 부여하는 경우</U>**입니다. 예를 들어 음악 앱에서 아티스트를 검색하면 해당 아티스트의 음악에 대한 끝없는 추천이 이어집니다.
    > 
    
    > **`Response`** : 시스템이 입력과 출력을 일치시키는 방법을 설명하고 사용자가 피드백을 통해 시스템을 수정할 수 있도록 함
    > 

<br>

- **2-9. 관련성 에러에 대한 출력 품질 확인**
    
    > AI 기반 시스템이 항상 적시에 적절한 정보를 제공할 수 있는 것은 아니며, **`비관련성은 종종 컨텍스트 오류`** (의도한 대로 작동하는 시스템과 사용자의 실제 니즈 사이의 충돌)의 원인입니다. 사용자 입력 에러 또는 데이터 에러와 달리 이는 정보의 진실성 또는 시스템이 결정을 내리는 방식과 관련된 문제가 아닙니다. 이러한 에러는 **`결과가 전달되는 방법과 시기의 문제`**입니다.
    > 

<br>

- **2-10. 낮은 신뢰수준**
    
    > **<U>불확실성 제약으로 모델이 주어진 작업을 수행할 수 없는 경우</U>** 사용 가능한 데이터 부족, 예측 정확도 요구 사항 또는 불안정한 정보 때문입니다. 예를 들어 항공권 가격 예측 알고리즘이 상황 변화로 인해 내년 가격을 정확하게 예측할 수 없는 경우입니다.
    > 
    
    > **`Response`** : 특정 결과가 제공될 수 없는 이유를 설명하고 앞으로의 대체 경로를 제공 <br>
    > → 예시 : “내년 파리행 항공권 가격을 예측하기에는 데이터가 충분하지 않습니다. 한 달 후에 다시 확인하십시오.”

<br>

- **2-11. 무관계**
    
    > **<U>시스템 출력이 신뢰수준이 높지만 사용자의 니즈와 관련이 없는 방식으로 사용자에게 제공되는 경우</U>**입니다. 예를 들어 사용자가 가족 장례식을 위해 휴스턴 여행을 예약하고 여행 앱에서 "재미있는 휴가 활동"을 추천합니다.
    > 
    
    > **`Response`** : 사용자가 시스템 기능을 개선하기 위해 피드백을 제공할 수 있음
    > 

<br>

- **2-12. 명확한 시스템 계층 구조 에러**
    
    > 이러한 에러는 **<U>서로 통신하지 않을 수 있는 여러 AI 시스템을 사용하여 발생</U>**합니다. 이러한 중첩은 상황 제어 또는 사용자의 주의에 대한 충돌을 초래할 수 있습니다. AI 시스템이 다른 시스템과 상호 작용할 수 있는 방법을 미리 계획하고 출력을 관리하고 충돌을 방지하기 위한 여러 수준의 제어를 사용자에게 제공합니다.

<br>

- **2-13. 다중 시스템**
    
    > 사용자가 우리의 **<U>Product를 다른 시스템에 연결하고 주어진 시간에 어느 시스템이 담당하고 있는지 명확하지 않은 경우</U>**입니다. 예를 들어, 사용자는 "스마트 온도 조절기"를 "스마트 에너지 계량기"에 연결하지만 두 시스템은 에너지 효율을 최적화하는 방법이 다릅니다. 시스템은 서로 충돌하는 신호를 보내고 제대로 작동하지 않습니다.
    > 
    
    > **`Response`** : 연결된 여러 시스템을 설명하고 사용자가 우선 순위를 결정할 수 있도록 함. 여러 AI 시스템을 서로 다른 위치에 매핑하여 Product 인터페이스에서 여러 AI 시스템 간의 관계를 시각적으로 표현하는 방법을 고려해야 함
    > 

<br>

- **2-14. 신호 충돌**
    
    > **<U>여러 시스템이 단일 (또는 유사한) 출력을 모니터링하고 이벤트로 인해 동시 경고가 발생하는 경우</U>**입니다. 신호 충돌은 사용자가 무슨 일이 일어났는지, 어떤 조치를 취해야 하는지 파악하기 위해 여러 정보 소스를 분석해야 하기 때문에 사용자의 정신적 부하를 증가시킵니다. 예를 들어 사용자의 음성 입력이 서로 다른 방식으로 동시에 응답하는 여러 음성 활성화 시스템에서 인식된다고 하면, 사용자는 다음에 무엇을 해야할지 모를 것입니다.
    > 
    
    > **`Response`** : 사용자가 다른 신호와 겹치지 않는 AI에 대한 독립적인 컨트롤을 설정할 수 있도록 해야 함. 예를 들어 스마트 스피커가 듣기 시작하는 시계 단어는 고유할 수 있는데, 팀에서 새 컨텍스트 에러 생성을 방지할 수 있는 경우 시스템은 사용자가 우선권을 갖도록 의도한 시스템이 어떤 시스템인지 추론하려고 시도할 수 있음
    > 

각 에러에 대해 결과 `UX를 기반`으로 원인을 확인해야 합니다. 아래 예를 기반으로 어떤 종류의 에러인지 질문을 수행해보세요.<br>
→ `예측 및 학습 데이터 오류` : 시스템의 기능이 학습 데이터에 의해 제한될 때 발생 <br>
→ `입력 오류` : 사용자가 AI 시스템에 대한 입력의 자동 수정을 예상하거나 습관화가 중단될 때 발생 <br>
→ `관련성 오류` : 시스템 출력이 사용자의 요구와 관련이 없는 시간, 장소 또는 형식으로 나타날때 발생 <br>
→ `시스템 계층 오류` : 사용자가 Product를 다른 시스템에 연결하고 어떤 시스템이 담당하고 있는지 명확하지 않을 때 발생 <br>
{:.note}

---

## 3. 실패 발생 경로 제공

기술의 한계에 대한 합리적인 기대수준을 설정하면 에러에 대한 좋은 경험을 설정하는 데 도움이 되지만 사용자가 앞으로 나아가는 방법 또한 중요합니다. **<U>시스템이 실패한 후 사용자가 할 수 있는 일에 초점을 맞추면 Product의 유용성을 유지하면서 권한을 부여</U>**할 수 있습니다.

우리가 식당의 웨이터이고 고객이 메뉴의 무언가를 주문했지만 다 떨어졌다면 그들의 **`묵시적인 선호도를 고려하여 대체 옵션을 생각`**해냈을 것입니다. 예를 들어, "코카콜라가 없지만 펩시는 있습니다, 펩시로 드릴까요?" 라고 할 수 있습니다.

상황적 이해관계가 더 높은 경우 **`대안이 실제로 안전한 옵션인지 확인하기 위한 추가 확인`**이 있어야 합니다. 예를 들어, 사용자가 식당에 없는 요리를 원해 제시한 대안에 알레르겐 성분이 포함된 경우 웨이터는 추천하기 전에 두 번 생각해야 할 것입니다. 이러한 **<U>실패 상태의 기본 목표는 사용자에게 과도한 피해를 방지하고 사용자가 작업을 진행하도록 돕는 것</U>**입니다.

<br>

- **3-1. 피드백 기회 만들기**
    
    > 위 섹션에서 강조한 것처럼 사용자가 경험하는 많은 **<U>에러는 시스템을 개선하기 위해 피드백이 필요</U>**합니다. 특히 Label이 잘못된 데이터와 같이 시스템 자체에서 쉽게 인식되지 않는 에러 유형은 수정을 위해 **`외부 피드백에 의존`**합니다. **<U>"올바른" 시스템 출력과 함께 에러 메시지가 표시될 때 사용자가 피드백을 제공할 수 있는 기회</U>**를 제공해야 합니다. 예를 들어 사용자에게 시스템 장애 후 예상되는 상황을 묻고 부적절한 제안을 보고할 수 있는 옵션을 제공합니다.

<br>

- AI 출력을 반복적으로 거부하는 경우 사용자에게 피드백을 요청해야 함
![](/assets/img/2023-03-07/4.gif)

<br>

- **3-2. 사용자에게 제어권 반환**
    
    > AI 시스템이 실패할 때 가장 쉬운 경로는 **`사용자가 대신하도록 하는 것`**입니다. 사용자에게 완전한 "재지정" 권한을 부여할 수 있는지 여부와 그 형태는 시스템마다 다릅니다. 하지만 경우에 따라 **`수동 제어로 되돌리는 것이 위험`**할 수 있습니다. <br>
    <br>
    예를 들어, 내비게이션 시스템이 러시 아워 트래픽 동안 낯선 환경에서 길을 탐색하는 사용자에게 안내를 완전히 중단하는 경우, 이 AI에서 수동 제어로의 전환이 발생하면 사용자가 시스템이 중단된 지점을 쉽고 직관적으로 빠르게 선택할 수 있도록 해야 하며, 사용자는 **`고삐를 잡기 위해 필요한 모든 정보`** (상황 인식, 다음에 해야 할 작업 및 수행 방법)를 가지고 있어야 합니다.

<br>

- **3-3. 파괴적인 사용 (Subversive use)의 가정**
    
    > 유익하고 실행 가능한 에러 메시지를 작성하는 것이 중요하지만 Product 팀은 **`일부 사람들이 의도적으로 이를 남용할 것이라는 점을 기억하여 Product를 설계`**해야 합니다. 사용자 요구 + 성공 정의 장 에서와 같이 Product의 잠재적인 부정적인 영향을 매핑하는 것 외에도 실패를 안전하며 Product의 자연스러운 부분으로 만들려고 노력해야 하며, **<U>위험한 에러를 흥미롭게 만들거나 시스템 취약점을 과도하게 설명하지 말아야 합니다.</U>**<br>
    <br>
    > 예를 들어 사용자가 받은 편지함에서 이메일을 스팸으로 표시할 때마다 이메일 앱은 시스템이 해당 메시지를 스팸으로 분류하지 않은 이유를 설명하여, **`오히려 스패머에게 필터에 걸리지 않는 방법에 대한 유용한 팁을 제공`**할 수 있습니다.
    <br>
    Product의 잠재적으로 발생할 수 있는 모든 막다른 골목에 대해 명확한 아이디어를 얻으려면 베타 테스트 및 파일럿 프로그램에 투자해야 합니다. 많은 Product는 미로와 같은 옵션과 가능성이 존재하기 때문에, 사용자는 이러한 미로에 갇힐 수 있습니다.
    > 

**`Subversive use`** : 특정 기술, 도구 또는 시스템이 기존 시스템, 조직 또는 사회를 약화시키거나 방해하려는 개인 또는 그룹에 의해 불법적이거나 악의적인 목적으로 사용될 것이라고 예상하거나 기대하는 것을 의미함. 본질적으로 새로운 기술, 시스템, 제품을 개발하거나 구현할 때 유해하거나 비윤리적인 목적으로 사용될 수 있는 방법을 고려하고 이러한 위험을 방지하거나 완화하기 위한 조치를 취해야 함. 이 접근 방식은 종종 사이버 보안 전략 및 정책 개발과 잠재적인 보안 영향을 가진 새로운 기술 설계에 사용됨
{:.note}

초기에 품질 보증 연습 및 파일럿을 사용하여 에러를 찾을 수 있지만 출시하는 새 기능을 계속 모니터링해야 합니다.<br>
팀별로 사용자의 새로운 에러 발견을 위해 모니터링할 채널을 결정하고, 각 에러를 발견하면 해당 에러에서 올바른 경로를 설계하기 위해 팀으로 작업해야 합니다.
아래 에러 보고서 예시 중 우리의 팀에 적합한 것은 무엇일지 생각해보세요. <br>
→ 고객 서비스로 전송된 보고서<br>
→ 소셜 미디어 채널을 통해 전송된 의견 및 보고서<br>
→ Product 내 측정 항목<br>
→ Product 내 설문 조사<br>
→ 사용자 조사 : Product 외 설문 조사, 심층 인터뷰, 다이어리 스터디<br>
{:.note}


---

## 4. Conclution

지금까지 마지막 가이드라인, Errors + Graceful Failure을 정리해보았습니다. '실패는 성공의 어머니'라는 속담처럼 기계와 사람을 비롯하여 모든 것의 학습은 실수 없이는 일어날 수 없습니다. 에러는 필수적이라는 생각을 바탕으로 시스템을 설계하고 구축하면 사용자와 대화할 수 있는 기회를 만드는 데 도움이 됩니다. 그러면 에러 해결을 위한 보다 효율적인 경로를 생성하여 사용자가 목표를 완료할 수 있도록 할 수 있습니다.

에러 경험을 설계할 때 기계가 아닌 사람이 되어야 하며, 에러 메시지는 시스템이 실수했음을 공개해야 할 수 있습니다. 겸손함을 기반으로 실수를 해결하고 시스템의 한계를 설명하면서 사람들이 계속 앞으로 나아갈 수 있도록 유도해야 할 것입니다. Chapter 6을 정리하면 다음과 같습니다.

> 1. **`"Error (오류)"와 "Failure (실패)" 정의` :** 확률적 동적 시스템을 다룰 때 사용자는 시스템이 의도한 대로 작동하는 상황에서 에러를 인식할 수 있으며, Product가 진행 중인 작업임을 인정하면 디자이너와 엔지니어가 AI를 계속 개선하는 데 필요한 채택 및 피드백을 장려하는 데 도움이 될 수 있음
><br><br>
2. **`에러 원인의 식별` :** AI 기반 시스템의 고유한 복잡성으로 인해 에러의 원인을 식별하기 어려울 수 있으며, 에러를 발견하고 소스를 식별하는 방법을 팀으로 논의하는 것이 중요함
><br><br>
3. **`실패로부터의 경로 제공` :** 요점은 실패를 피하는 것이 아니라 그 실패를 찾아 나머지 Product와 마찬가지로 사용자 중심으로 만드는 것. 제대로 작동하는 시스템을 보장하기 위해 아무리 노력해도 AI는 **본질적으로 확률적**이며 모든 시스템과 마찬가지로 어느 시점에서 실패할 수 있음. 이런 일이 발생하면 Product는 사용자가 작업을 계속하고 AI를 개선할 수 있는 방법을 제공해야 함
>

<br><br>
지금까지 구글의 AI 서비스 R&D 조직에서 제작한 “People + AI Guidebook” [6단계의 가이드라인](https://pair.withgoogle.com/guidebook/chapters)을 스터디 후, 정리해보았습니다.
비록 2020년에 나온 본 가이드라인은 최신의 정보는 아니지만, 사용자와 Product를 개발하는 실무자 관점에서 실제 AI를 활용한 Product를 개발하고 운영할 때 고려해야 할 사항들을 생각해 볼 수 있어 좋은 시간이었습니다. 

이 가이드라인은 AI 서비스를 기획하기 위한 프레임워크를 제시하기에 AI 서비스가 윤리적, 법적, 사회적 의미를 고려하면서 사용자들의 니즈를 충족하며 설계할 수 있도록 방향을 제시하며, AI 서비스 개발과 관련하여 발생할 수 있는 위험과 함정을 방지할 수 있도록 돕습니다. 이는 AI 기반 Product가 아니여도, Product 개발 및 운영 과정에 적용해 봄으로써 조직 내 책임감 있는 개발 문화를 구축하는 데 도움을 줄 수도 있을 것으로 생각합니다. 

AI 시대가 도래한 2023년 현재, Chat GPT를 환호하는 동시에 우려의 목소리도 많은 것이 현실입니다. 앞으로 AI가 우리 삶에서 점점 더 중요한 역할을 하고 있기 때문에, 책임감 있고 윤리적인 방식으로 개발되고 사용되도록 하는 것이 무엇보다도 중요하다고 생각합니다.


더불어 최근 6개월 동안 AI 기술을 활용하여 두 차례의 개발 프로젝트를 진행하면서 고려하지 못한 아쉬웠던 부분과 개선점을 생각할 수 있었기에, 이 부분은 따로 추가로 정리해 콘텐츠를 만들어 보면서 추후 또 다른 AI 서비스를 기획하고 개발할 때 유사한 실수를 피하고 더 나은 결정을 내릴 수 있도록 저만의 방향을 찾아보려고 합니다. 언젠가 윤리적, 법적, 사회적 의미를 고려하며 사용자의 니즈를 충족하는 사람을 위한 AI 서비스를 기획하고 운영하고 싶습니다 ☺️


끝으로 제가 정리한 가이드라인이 대한민국의 책임있는 AI 개발 문화를 구축하고 이 기술이 사회 전체에 이익이 되는 방식으로 사용되는데 작게나마 도움이 되었으면 좋겠다는 소망을 담아 본 포스팅을 마무리하겠습니다!
<br><br>



---


<!--more-->

<br><br>

<div align="center">
소통은 제가 공부하고 공유하는 원동력이 됩니다.<br>
해당 글이 도움이 되셨다면 소중한 격려와 응원 부탁드립니다 ☺️
</div>  