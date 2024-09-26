---
aliases: 
date: ""
title: 
author: 
tags:
  - Seminar
draft: true
---
Mamba가 transformer architecture보다 성능이 좋다.
![[Pasted image 20240926184711.png]]

Mamba : Parallelized training + linear-time complexity

#### Contribution
a selective scan algorithm
a hardware-aware algorithm  - stroage


Mamba가 history를 압축해서 Transformer보다 메모리를 적게 먹음
![[Pasted image 20240926190143.png]]

Parallization이 가능하다. : 오직 이전 state를 가지고 있는 것만 계산하면 돼서?

SSM + Hippo = Mamba
zotero : 
source : 

---
### Critique
- 얻어갈 것
- 이 방법의 장점 / 부족한 점
- 어떻게 써먹을 수 있을지

### Introduction



- 어떤 문제를 풀 것인지

### Methodology


### Experiments
- 어떤 데이터
- 어떤 정보를 분석했는지 (ate, rpe, NEES)


### ❓️Questions

### Future Articles to Read

