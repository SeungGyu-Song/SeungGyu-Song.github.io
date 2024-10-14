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



## Future Work
- 내가 이해 못한 부분을 어떻게 보완할 수 있을까?

## Part 1

## Part 2


### ❓️Questions

