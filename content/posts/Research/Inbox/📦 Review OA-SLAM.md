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
### Critique
- 얻어갈 것
- 이 방법의 장점 / 부족한 점
- 어떻게 써먹을 수 있을지

### Contribution
- object와 point를 동시에 사용함으로써 relocalization의 성능 향상
- 사전 정보 필요 없이 바로 쓸 수 있게 fully-automatic하게 만듦.
### Introduction
- Object를 활용한 SLAM → relocalization, reinitialization에서 일반 point-based 방식보다 robust함.
- 

### Methodology
![[Pasted image 20240708224031.png|640]]
Object도 point랑 똑같이 활용된다고 생각하면 되고, Ellipse/Ellipsoid를 활용해서 object를 표현함.


### 4.4 Initial Object Reconstruction
- 한 object에 대해 10$\degree$ 이상의 view 차이점이 있는지 → elipsoid를 만듬.
- 근데 이게 불안정해서 처음에 Sphere로 reconstruction 하고, 시간이 흐르면서 Ellipsoid가 되게 최적화.
### Experiments
- 어떤 데이터
- 어떤 정보를 분석했는지 (ate, rpe, NEES)


### ❓️Questions

### Future Articles to Read

