---
aliases: 
date: 2024-07-08
title: 
author: 
tags:
  - Review
---

zotero : 
source : 

---
![[Pasted image 20240708212508.png]]
### Critique
- 발이 닿아있으면 고정돼있다는 가정이 있음. [[📦️STEP Review]]과는 다름.
-  #Kalman_filter 
-   [ ] contact preintegration residual 식 이해 #점검  
-   [ ] Appendix foot velocity jacobian #점검 
- 왜 noise modeling을 이렇게 했을까?

### Introduction
- 사족보행 위치추정을 잘 하는 것이 목표
- 

### Methodology
- VINS-Fusion 뼈대
- Contact → uncertatinty👇 (forward kinematics, velocity measurement)
- prior contact schedule에 따라 IMU data와 Leg Odometry를 활용하는 Kalman Filter 사용
	- KF로 contact 여부를 확인하고, Forward Kinematics로 계산한 foot vel과 일치하면 contact, 다르면 contact 결과를 반대로 뒤집음.
- Kinematics parameter를 calibration하는 함수도 포함돼있음.
	- 실제 로봇이 돌아다니다보면 link deformation과 rolling contact으로 인해 link 길이가 변할 수도 있다??
	- 따라서 LO velocity measurement에 bias처럼 작용하게 된다. ← #점검 
#### [[📦️STEP Review|STEP]]과 다른 점
joint encoder 값에 대한 modeling 식이 다름.
- STEP : foot의 gyro, linear velocity에 대한 noise를 사용 
	- [ ] #점검 하기.
- Cerberus : joint angle, joint vel, kinematic parameter random walk noise, contact preintegration motion constraint에 대한 noise 사용.

### Experiments
- 어떤 데이터
- 어떤 정보를 분석했는지 (ate, rpe, NEES)


### ❓️Questions

### Future Articles to Read

