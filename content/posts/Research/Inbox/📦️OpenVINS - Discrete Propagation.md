---
aliases: 
date: 2024-10-11
title: 
URL: https://docs.openvins.com/propagation_discrete.html
tags: 
draft: true
---

#### Reference 
- [[📦️Indirect Kalman Filter for 3D Attitude Estimation]]
- [[📖OpenVINS Study Week 5]]
- [[🧩OpenVINS Code Analysis]]
### Objective
- quaternion을 활용한 imu discrete propagation : [[🧩OpenVINS Code Analysis]]에서는 fast state propagation으로 쓰임.

### Future Work
- 내가 이해 못한 부분을 어떻게 보완할 수 있을까?

### Part 1
quaternion의 reference frame을 옮기고 싶을 때 
$\hat{\bar{q}}$ : unit quaternion, $\hat{\omega}$ : estiamted? 각속도

근데 이상한 게 reference frame이 body 좌표임
$^{I_{k+1}}_G \hat{\bar{q}} = exp(\frac{1}{2} \Omega(\hat{\omega}})\Delta t_k) ^{I_k}_G \hat{\bar{q}}$



### Part 2


### ❓️Questions

