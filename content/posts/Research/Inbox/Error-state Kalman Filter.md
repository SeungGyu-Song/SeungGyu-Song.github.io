---
aliases:
  - eskf
date: 2024-10-14
title: Error-state Kalman Filter
URL: https://gsk1m.github.io/slam/2022/09/23/kf-tutorial10.html
tags: 
draft: true
---
## Objective
- OpenVINS, FAST-LIO 등 최근 filter 기반 논문에서 eskf를 베이스로 하고있다.
- Error state Kalman filter를 왜 사용해야하는지, 장점에 대해 알아보자
- **결론적으로 일반 EKF보다 Manifold 특성을 고려한 연산이 된다는 장점이 있다.**
## Introduction
#### Kalman Filter 
- prior와 measurement 사이의 weighted sum을 해주는 장치
- 그냥 고정된 상수로 융합해주는 게 아니라, a posteriori의 covariance를 최소화하는 것을 cost로 해서 최적 gain을 결정하는 방법.
- Kalman filter는 Bayesian Filter를 기반으로 하고있고, Bayesian filter의 철학은 현재의 최적값이 다음 턴의 사전정보가 된다는 것이다. 따라서 다음 턴의 prior는 현재의 최적 정보가 되겠다.

### EKF와 ESKF
1. state가 nonlinear하거나, 
2. measurement model이 non-linear 
하다면 시스템에 non-linearity가 발생하고, 이를 Taylor expansion을 통해 근사를 할 수 있따.

한편, KF도 covariance라는 *squared loss*를 cost로하는 estimator인 것이다. 
이 점에서 least-square를 최적화하는 방식인 Gauss-Newton과 비슷하다고 할 수 있다.


### GN에 대해서
![[Pasted image 20241014153928.png]]
결국에는 $J^{\top} J \Delta x = -J^{\top} b$ 를 푸는 것. 
블로그 포스트에 있는 [Grisetti 교수님의 ICRA tutorial 자료](https://www.diag.uniroma1.it//~labrococo/tutorial_icra_2016/icra16_slam_tutorial_grisetti.pdf#page=3.00)에서 최종적으로 하고자 하는 말은 :
**state에 nonlinear한 element가 있다면, 그것의 tangent space에서 update해주어야한다.** 
예로, rotation의 경우, 3차원 공간에서 rotation은 보통 SO(3)로 표현이 되고, 이는 3x3 matrix이다. 이를 최적화 하기 위해 9-dimension  vector로 만들고 이 9개의 값들을 조금씩 조절해가면서 cost를 줄여나간다는 것은 안된다는 것이다.
이런 non-linear entity들은 vector space가 아니므로, 기존의 기계적인 GN pipeline에 바로 적용될 수 없다.


## Future Work
- 내가 이해 못한 부분을 어떻게 보완할 수 있을까?

## Part 1

## Part 2


### ❓️Questions

