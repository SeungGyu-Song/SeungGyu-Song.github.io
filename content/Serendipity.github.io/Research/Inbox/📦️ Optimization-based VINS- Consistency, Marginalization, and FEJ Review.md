---
aliases: 
date: 2024-05-23
title: Optimization-based VINS- Consistency, Marginalization, and FEJ
author: ChuChu Chen
tags:
  - Review
---

zotero : 
source : [[@Chen_OptimizationBased_2023]]
Technical Report와 같이 보기.

---
### Critique
- Observability와 Consistency가 정확히 어떻게 깨지는 건지 알아가기
- 
- 이 방법의 장점 / 부족한 점
- 어떻게 써먹을 수 있을지

### Introduction
#### Observability
VINS의 Cost function은 Non-linear하다. 이렇기 때문에 measurement function과 system dynamics에 대해서 linearization 과정을 하게 되는데, 이 때 연속적인 linearization point가 다르기 때문에 unobservable한 방향으로 정보가 들어왔다고 판단해서 system이 over confident해지고 정확도가 낮아지며, estimation이 inconsistent 해진다.

> 한편 estimation이 consistent 하다는 얘기는 zero mean, estimation에서 산출한 covariance의 Gaussian distribution이 실제와 같다는 것을 의미한다.




#### FEJ를 활용한 다른 알고리즘들
- OKVIS와 Basalt 모두 FEJ 방식을 사용했으나, marginal prior factor와 연결된 imu, visual factor의 linearization point를 수정하지 않는다(❓️)
	- 근데 observability에 영향을 끼치는 건 Global Position과 Global yaw라서  bias나 다른 변수에 대해서 FEJ를 할 필요가 없다 → BASALT의 방식은 조금 틀린 방식.
- DM-VIO는 delayed marginalization을 통해서 이미 marginalized 상태의 state를 다시 relinarization 해준다.
- 



### Marginalization and Consistency
#### State marginalization
[[ccchen_technical_report]]
Prior term에서 
#### System Observability
full batch vs fixed lag smoother



### Experiments
- 어떤 데이터
- 어떤 정보를 분석했는지 (ate, rpe, NEES)


### ❓️Questions
근데 Loop Closure나 Map Localization의 경우는 강력한 constraint로 인해 global xyz 정보를 얻는데 이러면 똑같이 시스템이 불안정해지나?

### Future Articles to Read

