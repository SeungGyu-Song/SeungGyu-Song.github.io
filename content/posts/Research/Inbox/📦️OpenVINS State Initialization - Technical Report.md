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
- 
##회저
## 3. Least-squares Problem
[[📦️VINS-Mono Derivation, Pre-integration|vins_derivation_preintegration]], [[Research/Zotero/Papers/@Forster_OnManifold_2017|On-Manifold Preintegration for Real-Time Visual--Inertial Odometry]]와 마찬가지로, gravity를 제외한 값으로 preintegration을 진행함
	근데 후자는 처음부터 gravity를 뺀 가속도로 preintegration term을 만들고
	전자는 직접 측정한 가속도 값을 이용해 진행하며, gravity는 preintegration term 밖에서 제외해줌. [[🧩OpenVINS Code Analysis]]도 이와 유사함.

#### Preintegration term
![[Pasted image 20241001215705.png]]

최종 inertial term 식 using preintegration term.
![[Pasted image 20241001215649.png]]

### Discussion on Frame Transformation

### Part 2


### ❓️Questions

