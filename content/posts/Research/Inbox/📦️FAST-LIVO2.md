---
aliases: 
date: 2024-09-10
title: 
author: 
tags:
  - Review
---
Error state iterated kalman filter 기반의 direct 방식 LIVO. 

###
zotero : 
source : 

---
### Critique
- 해상도 높은 mapping을 장점으로 함.
- 이 방법의 장점 / 부족한 점
- 어떻게 써먹을 수 있을지

### Introduction
#### Error state iterated kalman filter 기반의 direct 방식 LIVO.

#### image accuracy를 향상시키기 위해 도입한 방법
1. voxel map의 plane prior를 사용
	1. dynamically reference patch를 갱신함.
2. on-demanding raycast operation : image pixel에 LiDAR point가 없을 때.
3. image exposure time을 실시간으로 구함.

#### Visual SLAM
<span style="color:blue"> 장점</span>
- color information → semantic perception
- deep learning methods → robust feature extraction and dynamic object filtering
<span style="color:red"> 단점</span>
- concurrent optimization of map points → significant computational overhead → map accuracy and density 저하
- 다른 scale에 따라 measurement noise가 다양하다 (?)
	- varying measurement noise across different scales
- illumination 변화에 민감
- texture-less 환경에서 data association이 잘 안 됨.
#### LiDAR SLAM
<span style="color:red"> 단점</span>
- detail 떨어지고, color 정보 없음
- 좁은 터널, single and extended wall에서 잘 안 됨.

#### LIVO의 3가지 challenging problems
- 데이터 양이 뒤지게 많음
- 현재 다른 알고리즘들은 visual, LiDAR feature를 따로따로 뽑았었음
- sparse한 LiDAR 데이터 + dense image를 이용해 map을 만드는 게 쉽지 않음.

### Contribution

1. LiDAR & camera dimension mismatch를 다루기 위해 sequential update를 포함한 Error state Iterated Kalman filter 활용
2. plane priors 활용. FAST-LIVO에서는 patch 안에 있는 모든 픽셀이 다 같은 depth를 가지고 있다고 가정했음.
3. image alignment 향상을 위해 reference patch update strategy를 제시. - large parallax, 충분한 texture detail을 가진 patch들.
4. online exposure time estimation
5. on-demand voxel raycasting. 
추가적으로 multi-line spining LiDARs, solid-state LiDARs과 pinhole, fisheye camera 지원.
### Methodology
[VoxelMap](https://arxiv.org/pdf/2109.07082) + [SVO](https://rpg.ifi.uzh.ch/docs/ICRA14_Forster.pdf) (sparse direct method) : sparse direct image alignment에 영감을 받았지만 LiDAR point를 re-utilizing 하는 것이 다름.
1. LiDAR update 
2. LiDAR map points를 visual map points로 활용.
	1. 이 때 선택된 visual map points는 이전에 관측된 reference image patch와 함께 사용이 되는데 현재 image로 projection 됨.
3. photometric error를 줄임으로써 pose align.

### Related Works
Fusion을 하는 이유 : 한 개의 센서가 failure나 partial degeneration을 겪을 수 있으니까.
##### Loosely Coupled (State estimation에서)
3D LiDAR Points와 2D camera image feature와 일대일 대응이 아니라서 잠재적인 오류발생 가능성이 있음. → Direct 방식을 도입.
VIO의 결과를 LIO의 initial guess로.
##### Tightly Coupled (State estimation에서)
R2Live : on-manifold iterated Kalman filter에서 Fusion. 근데 VIO는 optimization 방식.
LVI-SAM : LiDAR와 Visual을 Optimization 방식으로 tightly coupling
R3LIVE : LIO로 맵 만들고 VIO로 map texture rendering
R3LIVE++ : Online exposure estimation, photometric calibration

| 제목              | R3LIVEs                        | Ours         |
| --------------- | ------------------------------ | ------------ |
| direct방식        | O                              | O            |
| piexel level    | individual                     | patch        |
| image alignment | frame-to-frame<br>frame-to-map | frame-to-map |
DV-LOAM, SDV-LOAM, LVIO-Fusion은 LiDAR points를 새 이미지에 patch로 projection해서 tracking을 하는 것은 제시된 방법과 같음.
그러나 tightly frame-to-map image alignment를 통합, LiDAR scan registration 그리고 IMU measurements를 iterated Kalman Filter에 넣었다는 게 다름.
### Experiments
- 어떤 데이터
- 어떤 정보를 분석했는지 (ate, rpe, NEES)


### ❓️Questions

### Future Articles to Read

