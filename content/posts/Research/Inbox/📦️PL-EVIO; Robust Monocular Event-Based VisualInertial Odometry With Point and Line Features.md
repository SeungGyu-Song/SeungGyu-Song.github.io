---
aliases:
  - PL-EVIO
date: 2024-10-14
title: 
author: 
tags:
  - Review
draft: true
---

zotero : 
source : https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=10287884

---
## Critique
- EVIO에 그냥 point feature, line feature를 붙인 논문인 듯.
	- event(point, line)+image(point)+IMU tightly coupled
- loop closure도 들어있긴 한데 색다른 방식을 준 건 아닌 거 같아.
- Event data representation에 따른 성능을 보고 가기.
## Introduction
### Event Reperenstation
#### Direct
#### Combining with an image sensor
learning based method.
#### Motion-compensated
[[📦️Ultimate SLAM]] 이 이 방식으로 했다.

이걸 통해서 image처럼 만든 후, 기존 VIO에서 했던 Feature extraction / tracking을 그대로 사용함 (FAST, Shi-Tomasi, Lucas Kanade optical flow)
#### Time Surface or Surface of Active Event (SAE)
- 각 픽셀에 최근 event 시점을 알려주는 시간값 t가 들어있음.
- 어떤 문제를 풀 것인지

### Event-based Motion Estimation
여기서 Event SLAM 방법들의 역사를 짚어주는데 읽기 괜찮음.

- Static한 환경에서 event가 안 들어올 때도 pose를 어떻게 줄 수 있을까?

[[📦️IDOL]] 알고리즘역시 line을 활용했는데 houghline을 이용해서 했다. 
-  line의 속도가 constant 하다는 가정 때문에 aggressive motion에 약하고, 기타 event camera의 특성을 잘 살리지 못한다. 
## Methodology
event feature는 asynchrnonous한 

## Experiments
- 어떤 데이터
- 어떤 정보를 분석했는지 (ate, rpe, NEES)



### Appendix
#### A. Ablation study on Different Event Representations for Event-Based Feature Tracking

## ❓️Questions

## Future Articles to Read

