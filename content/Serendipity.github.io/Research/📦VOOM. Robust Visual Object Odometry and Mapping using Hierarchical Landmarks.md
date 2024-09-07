---
aliases: 
date: 2024-07-08
title: 
author: 
tags:
  - Review
---
#dual_quadrics #Wasserstein_distance


zotero : 
source : 

---
### Critique
- 얻어갈 것
- 이 방법의 장점 / 부족한 점
- 어떻게 써먹을 수 있을지

### Introduction
- 현재까지 Object SLAM이 feature-based SLAM보다 성능이 우수한 경우가 거의 없었음.
- 그래서 **high level object와 low level feature들을 같이 사용하는 방식**의 Visual Object Odometry and Mapping 방식을 제안.
- Object level information을 활용해서 현재 frame의 keypoint들이 map과 더 매치가 잘 됨.
#### Object SLAM에 관해

- Cuboid(직육면체)를 사용하는 것보다 dual quadrics를 이용하는 것이 projective geometry에 있어서 더 완결성이 있다.
- object residual을 도입하는 시도도 있었으나 성능 향상은 미미했다.
- OA-SLAM의 coarse-to-fine 방식 + 3D object를 landmark로 넣어서 tightly couple시킴. ( feature association.)
	- 이를 통해서 시-공간으로 모두 가까운 맵을 활용할 수 있음 🤔 → odometry의 drift를 낮춤.


### Methodology
- Observation Model of Objects
- Object-level Data Association
- Coarse-to-fine Odometry and Mapping
	- 

### Experiments
- 어떤 데이터
- 어떤 정보를 분석했는지 (ate, rpe, NEES)


### ❓️Questions

### Future Articles to Read

