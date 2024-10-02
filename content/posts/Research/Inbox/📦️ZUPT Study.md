---
aliases: 
date: 
title: 
URL: 
tags: 
draft: true
---
### Objective
- [[🧩OpenVINS Code Analysis|OpenVINS]]에서 소개된 Zero Velocity Update (ZUPT)를 이해해보자!

### Future Work
- 내가 이해 못한 부분을 어떻게 보완할 수 있을까?

### Part 1
Monocular system에서 temporal SLAM feature가 없을 때 중요하게 작동할 수 있다.
로봇이 가만히 있으면 triangulation도 안 되고, 이에 따라 Update를 할 수가 없게 됨. 
→ Stereo cam 사용 or temporal SLAM feature를 확보하기

추가적으로 Stereo나 temporal SLAM이 있더라도 dynamic한 object들에 대해서는 대처방안이 없다. 하지만, ZUPT를 통해서 feature tracking을 안 하면 이에 대해 대응할 수가 있게 된다.

### Zero Velocity Detection
#### Inertial-based Detection
- imu measurement model를 기반으로 한 threshold를 통해 판단( $\chi^2$ )
	- 이를 통해서 등속도 운동할 때를 검출하고싶어함.
- ![[Pasted image 20241002173155.png]]

#### Disparity-based Detection

tracking된 feature의 parallax의 차가 일정 범위보다 작으면 멈춰있다고 생각함. 근데 상황 자체가 dynamic object가 많은 환경이면 이게 적용되지는 않음.

![[Pasted image 20241002173257.png]]

### ❓️Questions

