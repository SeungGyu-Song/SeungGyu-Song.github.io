---
aliases: 
date: 2024-06-01
title: 
author: 
tags:
  - Review
URL: https://www.youtube.com/watch?v=FAAt0jejWOA&t=28s
---
### Objective
- 이 지식을 왜 공부해야 했는지

### Future Work
- 내가 이해 못한 부분을 어떻게 보완할 수 있을까?

### Part 1
AutoML :  머신러닝에 필요한 일부 작업을 자동화 하는 것. 
ML을 발전시키기 위한 단계 : 모델 설계, Optimizer 설계, 데이터 전처리

NAS-FPN : Object Detection으로 AutoML 분야 확장 (정확히는 FPN 모듈에 AutoML 적용)

#### FPN (Feature Pyramid Network)
기존의 방식들은 최종 feature map에서 한 번의 prediction을 했다면 제시된 방법은 여러 feature map들을 **섞어서** prediction을 여러 번. → 정확도를 높임. 근데 (a)각 층마다 prediction을 하는 것보다 속도도 빠르게할 수 있었다는데 어떻게 한 걸까?❓️

##### RetinaNet
NAS-FPN 논문에 따르면 
![[Zotero/images/@Ghiasi_NASFPN_2019/image-3-x50-y555.png|500]]
얘가 기반을 하고 있는 RetinaNet이 파란색 FPN이 어떻게 디자인 되느냐에 따라 성능이 좌우가 된다고 한다. → FPN을 ML로 디자인해보자. (왼쪽 층은 RetinaNet)

![RetinaNet](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDsRg4%2FbtqWWsTsmDN%2FnckkQnI21549nkiLMruNr1%2Fimg.png)

Retinanet의 구조는 위와 같다. NAS_FPN은 여기서 우측의 feature pyramid net에서 어떤 층을 어떻게 더해서 만들지를 ML방식으로 찾았다고 보면 됨.

#### Merging Cell

![[Zotero/images/@Ghiasi_NASFPN_2019/image-3-x298-y279.png|]]

![[Zotero/images/@Ghiasi_NASFPN_2019/image-4-x56-y410.png|300]]

merging cell은 다음과 같이 두 개의 feature layer들을 아래의 binary operation으로 적절히 연산하여 하나의 layer로 다시 만드는 것을 함. Sum을 하고 나서 Relu-3x3 Conv - BN을 통과 .


### Part 2
#### 전체 구조는 NAS 논문 기반
- PPO(Proximal Policy Optimization) 알고리즘을 사용해서 학습 (강화학습 agent를 학습하는 방식)
- 그리고 강화학습이다보니 Reward를 어떻게 주냐가 포인트인데 여기서는 각 세대에서 찾아낸 구조들의 Validation Set 정확도를 이용
- ResNet-10과 같은 작은 모델을 가지고 학습

### ❓️Questions


zotero : 
source : 

---
### Critique
- 얻어갈 것
- 이 방법의 장점 / 부족한 점
- 어떻게 써먹을 수 있을지

### Introduction



- 어떤 문제를 풀 것인지

### Methodology


### Experiments
- 어떤 데이터
- 어떤 정보를 분석했는지 (ate, rpe, NEES)


### ❓️Questions

### Future Articles to Read

