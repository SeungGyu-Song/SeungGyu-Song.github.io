---
aliases: 
date: 2024-10-01
title: 
URL: 
tags: 
draft: true
---
### Objective
- OpenVINS Dynamic initialization 파트 이해를 위함. 
- 
### Future Work

# Concept 
우선 linear system을 만들어서 velocity, feature position, gravity를 구한 후 → full optimization을 이용해서 covariance recovery 진행.
## Extra Takeaways
- Orientation은 비선형이다. 
	- geometrical : rotation은 한 축에 대해 회전하는 것이고, 이는 Euclidian 좌표계와는 다르다. 즉, 조금 움직임을 기술하기 위해서는 euclidian이 아닌 구면 위를 표현하는 좌표계로 표현해야한다.
	- mathematical : 3차원 회전의 특성상, 회전은 선형적으로 더하거나 곱해서 표현할 수 없습니다. 두 회전이 겹쳐지는 경우, 그 결과는 단순히 각 회전의 벡터 합으로 나타나지 않으며, 이는 **비선형적**입니다.
- Lagrange multiplierㅁ
	- 제약 조건이 있는 최적화 문제를 푸는 방법
	- 
## 3. Least-squares Problem
[[📦️VINS-Mono Derivation, Pre-integration|vins_derivation_preintegration]], [[Research/Zotero/Papers/@Forster_OnManifold_2017|On-Manifold Preintegration for Real-Time Visual--Inertial Odometry]]와 마찬가지로, gravity를 제외한 값으로 preintegration을 진행함
	근데 후자는 처음부터 gravity를 뺀 가속도로 preintegration term을 만들고
	전자는 직접 측정한 가속도 값을 이용해 진행하며, gravity는 preintegration term 밖에서 제외해줌. [[🧩OpenVINS Code Analysis]]도 이와 유사함.

### 3.1 Preintegration term
![[Pasted image 20241001215705.png]]

최종 inertial term 식 using preintegration term.
![[Pasted image 20241001215649.png]]

### Discussion on Frame Transformation
gravity와 상관 없이 초기의 좌표계 $I_0$를 설정하면, non-linear한 $^{I_0}_G R$을 구해줘야하는데, 아예 gravity를 $I_0$로 아예 표현해버리면 $^{I_0}g$에 대한 linear problem을 가지게 된다?? #점검 

### 3.4 Linear Ax = b Problem
Reprojection error를 이용해서 다음과 같이 linear model을 설계
![[Pasted image 20241001221124.png]]
![[Pasted image 20241001221139.png]]

이 때, feature는 image plane에서 x,y 좌표 두 개가 있으니까, 2N ≥9 , 즉 N=5일 때 위 식의 해를 구할 수 있음. 하지만 gravity의 크기를 알고있으니까 2N≥8이 되어서 N=4 여도 구할 수 있음.
### <span style="color:red">Quadratic Constrained Least-squares </span>
<span style="color:red"> 여기 잘 이해해야함. </span>

Lagrange multiplier 방법으로 velocity, feature positions, gravity 벡터를 구함. 
- gravity norm = 9.81이라는 constraint

### Recovering Inertial States
[[Gram-Schmidt]] 방식을 통해서 나머지 x,y 축에 대해서도 구함.

## 4.Maximum Likelihood Estimation
### 4.1 inertial measurement model
[[📦️VINS-Mono Derivation, Pre-integration|vins_derivation_preintegration]]과 마찬가지로 식을 구성함. 
$\alpha, \beta$는 bias에 dependent해서 bias가 변할 때 $\alpha, \beta$가 변하는 식을 세움. 
이 때, quaternion은 vins랑 그냥 역행렬의 관계로 기술되어있다. 왜인지는 모르겠음. (실제 vins-fusion 코드에서는 derivation과 역행렬 관계로 쓰여져있던 것 같음.)

### 4.2 camera measurement model
reprojection error 사용

### 4.3 Prior Cost
VINS는 global yaw와 global position에 대해 unobservable함. 
추가적으로, window가 매우 작을 시, rotation이 매우 작고, 이에 따라 gyroscope와 특히 accelerometer bias는 거의 unobservable하게 된다.

- linearization point와 현재 state의 estimate간의 차이를 loss function으로 세움
- 근데 이 때 이 prior term의  information matrix를 통해 (inverse해서) covariance를 구하게 된대. 
	- 코드로 확인해보기 #점검 
### ❓️Questions

