---
aliases: 
date: ""
title: 
author: 
tags:
  - Review
---
![[Pasted image 20240920204819.png]]
zotero : 
source : https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=10669187

---
### Critique
- 얻어갈 것
- 이 방법의 장점 / 부족한 점
- 어떻게 써먹을 수 있을지


![[Pasted image 20240920204811.png]]
### Introduction
- moving object로 인해 correspondence matching이 잘못 되면, IMU bias term을 wrong propagation 함.
	- 그리고 부정확한 IMU bias term은 
- 기존의 연구 [[DynaVINS]]에서는 Black-Rangarajan duality (B-R duality)를 이용해 moving objects로부터의 false correspondence를 줄일 수 있었음.
	- 하지만 추가적인 optimization 단계로 인해 연산 속도가 느렸음.

### Methodology
- Adaptive truncated least squares (ATLS)
- Bias consistency check (BCC) and stable state recovery (SSR)

![[Pasted image 20240920202411.png]]
state에 보면 $\omega$가 보이는데, 이건 feature가 static인지 dynamic인지 해당하는 weight를 의미한다.
###### Weighted Parallax
동적인 물체가 있다보면 keyframe을 선정할 때 parallax로 접근할 경우, 충분히 viewpoint가 다른데도 keyframe으로 안 뽑힐 수 있고 반대로 viewpoint 차이가 작은데도 parallax가 커서 keyframe으로 될 수 있다. 따라서 *weighted average parallax*로 keyframe을 판단한다.

#### Adaptive Truncated Least Squares (ATLS)
##### DynaVINS의 문제점
1. surrogate cost로 optimization을 새롭게 바꿨지만, outlier의 gradient가 0이 안 돼서 영향이 남아있게 됨.
2. outlier correspondence들의 depth와 weights를 불필요하게 update해서 연산량이 많아짐.

##### ATLS
![[Pasted image 20240921183245.png]]
- static feature의 maximum residual을 이용해 surrogate cost를 만들었고, 이에 따라 residual 값이 일정 이상 벌어지면 gradient가 0이 되게 함.
- truncation range(버릴 영역)를 feature들의 maximum residual을 이용해 조정함.

###### 1. Weight update (Static / Dynamic)
###### 2. State Optimization

### Bias Consistency Check
abruptly dynamic object가 발생하면 ATLS가 이 feature에 weight를 1을 줌으로써 outlier를 막지 못할 때가 온다. 

pose와 다르게 bias는 objective function 식이 $k-1$과 $k$ 윈도우 간의 bias가 같다는 식에서 출발하는 거라 $l$ 번 째 window에서 abruptly dynamic object가 생겼을 때, bias는 그 전의 window까지 영향을 끼친다. 이는 preintegration term인 $\alpha, \beta, \gamma$에도 영향을 주기 때문에 

![[Pasted image 20240920230314.png]]
와 같은 식으로 갑자기 발생한 동적물체가 있는지 확인해본다.

#### Stable State Recovery
만약 pose와 bias 간의 inconsistency가 발생한다면, state를  optimization 전의 값으로 돌린 후, $r_{trunc}$를 반으로 나눔으로써 outlier를 더 tight하게 잡고, gradient=0을 만드는 애들을 더 늘림. 
이후 weight를 update하고 optimization proceess가 진행된다.
### Experiments
- VIODE Dataset(simulation), Customised Dataset(물체들이 종/횡방향으로 지나가는 거)
- SLAM을 타겟으로 한 건지 ATE를 기준으로 비교함. 
- Feature 개수에 따른 Optimization 연산시간, ATE 비교 
- 실제 동적물체들이 지나가는 위치에서 다른 비교군의 odometry와 DynaVINS++의 위치 추정 결과 비교
	- 추가적으로 실제 사진을 첨부해서 SSR이 추가되었을 때도 같이 비교해서 static / dynamic feature의 분포를 보여줌.


### ❓️Questions

### Future Articles to Read

