---
aliases:
  - consistent right-invariant fixed-lag smoother review
date: 2024-05-27
title: Consistent Right-Invariant Fixed-Lag Smoother Review
author: 
tags:
  - Review
---
o
zotero : 
source : [[@Huai_Consistent Right-Invariant Fixed-Lag Smoother with Application to Visual Inertial SLAM_2021]]

---
### Critique
- 기존의 쓰였던 invariant EKF를 sliding window 방식으로 구현한 방식이고, invariant ekf의 조건을 지키기위해 state에 landmark 정보를 넣지 않고 그냥 **pose, velocity만** 넣은 것이 특징이다.
- 5.27기준 이 논문의 방법론보다 전통적인 visual slam의 observability 한계에 대해서 공부하면 될 것 같다.

### Introduction
- Inconsistency는 marginalization step의 결과인 prior factor의 linearization point가 window 내의 factor들의 linearization point가 일치하지 않기 때문에 발생하는 것이다.
- 이 문제를 해결하기 위해 *measurement* Jacobian을 수정하는 방식인 [[📦️ Optimization-based VINS- Consistency, Marginalization, and FEJ Review|FEJ]]이 제시되었지만, 세 가지 단점이 있다.
	- 우선 FEJ는 linear prior factor에 있는 변수에 관련된 Jacobian을 marginalization이 일어나자마자 다시 구하는 방법이다 (❓️)
	- 1.  Jacobian 행렬들이 덜 정확한 state variable에 의해 구해져서 state estimation 정확도에 영향을 준다(❓️)
	- 2. 어떤 state variable을 lock할지 정해져있지 않다. 경험에 따라 해야하는 듯.
	- 3. 현존하는 backend tool에 이걸 구현하기가 쉽지 않다.



- 그에 반해 invariant smoother는 다음과 같은 장점이 있다.
	- error state를 Lie Group에서 정의함으로써 error state가 state variable의 lineariation point와 관계가 없게 기술이 된다.
		- 이에 따라 같은 state variable에 대해 다른 linearization point가 발생하는 문제점을 예방할 수 있다.

[[inverse depth ]]의 장점
- 원래의 feature의 Euclidian space 좌표를 최적화 하는 방식보다 훨씬 더 성능이 좋다.
- it decouples landmark parameters from the platform pose in the world frame, thus they remain invariant under Euclidean transform of the original problem and have no bearing on the observability analysis (❓️)

- local frame에서 기술된 Sensor parameters (imu biases) 와 landmark는 observabliity에 영향을 끼치지 않는다! 

### Methodology


### Experiments
- 어떤 데이터
- 어떤 정보를 분석했는지 (ate, rpe, NEES)


### ❓️Questions

### Future Articles to Read

