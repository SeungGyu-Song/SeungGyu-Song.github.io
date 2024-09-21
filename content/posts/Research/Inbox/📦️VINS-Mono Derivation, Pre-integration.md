---
aliases:
  - vins_derivation_preintegration
date: 2024-05-15
title: VINS-Mono Derivation 1
author: 
tags:
  - Review
  - Pre-integration
  - VIO
  - VINS-Fusion
---

zotero : 
source : [[@VINS Derivation|raw_vins_derivation]]

---
### Critique
- VINS-Mono의 Pre-integration 방법 습득 , Mid-Point 방법
- [ ] on-Manifold 방식과 어떤 점이 다른지를 비교해보기.
- 


### Pre-integration 개념
본문에서는 식의 전개가 주로 이루어지기 때문에 개념적으로만 정리하고자 한다. 진짜 Pre-integration 정리하는 것은 [[📦️Preintegration]]에서 진행하고자 한다.

여기서는 사실 Rotation과 quaternion 이 쪽만 주의하면 된다.

> [!Preintegration은 body frame의 b_k에서 일어나는 것임을 명심하자! ]

##### Quaternion의 미분
우선 quaternion 을 미분하게 되면 다음과 같이 반띵나면서 cross product로 이루어진다는 것을 기억하자.

![[Zotero/images/@Wu_Formula_2020/image-3-x184-y100.png|300]]

##### Error State Equation
의미가 없는 물리량 $\alpha, \beta, \gamma$  그리고 bias들을 residual로 활용할 것이다. 근데 이 때  다음과 같은 error state equation을 활용해서 모델링을 진행한다.
$x + \delta x = \hat x$

> 만약 error에 해당하는 $\delta x$가 0이 되게끔 잘 추정하면 estimate값을 nominal 값에 수렴시킬 수 있다.
> 또한 Error state equation으로  나타냈을 때의 장점은 바로 다음과 같이 state와 noise에 대해 시스템을 **linear**하게 기술할 수 있기 때문에 매우 큰 장점을 가진다.
> 
> ![[Zotero/images/@Wu_Formula_2020/image-6-x203-y67.png|300]]
> 마지막으로 error는 매우 작을테니까 linearization과 같은 근사에서 오차가 적을 것이다.

마지막으로 continuous time에서 식을 전개하는데, 실제 컴퓨터는 discrete하니까 mid-Point 방법을 사용해서 discretise시킨다.

근데 이 때 Rotation도 왜 mid-point에 적용되는 것일까?



### Pre-integration 코드에 적용
실제 코드는 factor > integration_base.h 파일 안에 들어있다. 근데 코드로 구현함에 있어 다른 부분이 있어 적어보려고 한다.

- 코드에서 본문의 G에 해당하는 행렬 (코드에서는 V) 은 부호가 다 반대로 되어있다.
- 그리고 jacobian, covariance도 (I+F) 가 아니라 (F)로만 이루어져있다.

### ❓️Questions
Error State 마지막에 Mid-Point로 변환하는 과정에서 $R$ 도 왜 ½로 쪼개는지, 그리고 센서로부터 들어온 gyro_, acc_ noise는 절반내는데 왜 $\delta \theta^{b_k}_t$와 $\delta \theta^{b_k}_{t+1}$에 대해서는 ½을 안 해줄까?

이건 갑자기 왜, 어떤 걸 위해서 나온 거지? 흐름이 잘 이해가 안 된다.
![[Pasted image 20240515210647.png|300]]



### Future Articles to Read
[[📦️VINS-Mono Derivation, Optimization]]

### Reference
[ALIDA, VINS-Mono Derivation](https://alida.tistory.com/64)
