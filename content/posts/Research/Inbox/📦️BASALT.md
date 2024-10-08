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
### 1. KLT Tracking
### 2. Landmark representation
### 3. Marginalization scheme
- new frame == non-keyframe
	- *drop* the landmark factors. → to maintain *sparsity* of the problem.
	- oldest non-keyframe marginalization
- new frame == keyframe
	- 새로운 frame에 대한 velocity와 bias를 marginalization
	- 그리고 landmark를 포함한 one old keyframe marginalization

[[📦️ Optimization-based VINS- Consistency, Marginalization, and FEJ Review]]
FEJ에 대한 내 설명 추가 
→ marginalization은 optimization 후에 일어나는 거기 때문에 t 시점에서 marginalization을 하면 t+1에서 optimization을 할 때 쓰임. 

→ 따라서 optimization할 때는 current time이기 때문에 linearization point가 안 맞게 됨.

→ 그래서 FEJ로 linearized marginalization factor의 nullspace를 유지하자.

### 4. Mapping
Two layered approach
- lower layer : VIO
- upper layer : BA on the visual-inertial mapping layer, 근데 keyframe pose를 

### Experiments
- 어떤 데이터
- 어떤 정보를 분석했는지 (ate, rpe, NEES)


### ❓️Questions

### Future Articles to Read

