---
aliases: 
date: ""
title: 
author: 
tags:
  - Review
draft: true
---

zotero : 
source : 

---
### Critique
- 얻어갈 것
- 이 방법의 장점 / 부족한 점
- 어떻게 써먹을 수 있을지

## Introduction



- 어떤 문제를 풀 것인지

## Methodology
### VIO
#### 1. KLT Tracking
#### 2. Landmark representation
#### 3. Marginalization scheme
- new frame == non-keyframe
	- *drop* the landmark factors. → to maintain *sparsity* of the problem.
	- oldest non-keyframe marginalization
- new frame == keyframe
	- 새로운 frame에 대한 velocity와 bias를 marginalization
	- one old keyframe marginalization하는데,  host landmark는 marginalization하고 그 외의 landmark는 *drop*, 

[[📦️ Optimization-based VINS- Consistency, Marginalization, and FEJ Review]]
FEJ에 대한 내 설명 추가 
→ marginalization은 optimization 후에 일어나는 거기 때문에 t 시점에서 marginalization을 하면 t+1에서 optimization을 할 때 쓰임. 

→ 따라서 optimization할 때는 current time이기 때문에 linearization point가 안 맞게 됨.

→ 그래서 FEJ로 linearized marginalization factor의 nullspace를 유지하자.

[[#3. Non-Linear Factors for Distribution Approximation]] 여기서는 근데 keyframe을 marginalization할 때 keyframe pose만 제외하고 나머지 다 한다고 하는데 왜 앞 뒤가 상충하는 걸까.
### Mapping
Two layered approach
- lower layer : VIO
- upper layer : BA on the visual-inertial mapping layer, 근데 keyframe pose를 단순화해서 가지고 있는 non-linear factor를 이용함. 
	- → keyframe pose, keypoint position 최적화.

#### 1. Global Map Optimization
*To get statistically independent observations* ORB features를 사용한다. (이게 무슨 의미일까? #점검)

VIO에서 keyframe이 marginalization out되면, Markov blanket에 해당하는 linearization을 저장하고, keyframe pose를 제외한 모든 변수를 marginalize한다. 

이 marginalization prior로부터, non-linear factor를 recover한다.

#### 2. Non-Linear Factor Recovery
NFR은 원래 SLAM optimization을 bounded하기 위해 도입된 건데, 
논문에서는 VIO 정보를 globally consistent한 Visual-inertial map optimization으로 transfer하는 데 사용함.

NFR을 이용해서 원래 dense한 Markov blanket distribution을 sparse하게 만들고 싶은가봐.
(KL divergence를 이용해서)

i번째 non-linear factor를 얻기 위해서는 residual function을 정의해야한다. 
$r_i(s,z_i) = \epsilon,  \epsilon ~ N(0, H_i^{-1})$ 

그냥 NFR에서 만든 full-rank and invertible jacobian $J_r$로 만든 information matrix $H_i$로 global map optimization의 가중치로 쓰임. 
#### 3. Non-Linear Factors for Distribution Approximation
keyframe을 marginalization할 때는 current linearization point를 저장하고, keyframe pose를 제외한 나머지를 다 marginalization.
→ 이는 optimization window에 있는 keyframe pose들과 desne하게 연결된 factor가 되게끔한다.

여기서 신기한 거는 [[🧩VINS-Fusion Map.canvas|VINS-Fusion]]과 다르게 global position과 yaw가 unobservable하니까, (start pose의 initial prior로부터만 정보를 알 수 있따.) 이 정보는 필요가 없다고 판단해서 relative pose와 roll-pitch만을 가지고 map optimization을 진행함.

### Experiments
- 어떤 데이터
- 어떤 정보를 분석했는지 (ate, rpe, NEES)


### ❓️Questions

### Future Articles to Read
[Information Sparsification in Visual-Inertial Odometry](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8594007) : Sparsity에 대해 알아보기.
