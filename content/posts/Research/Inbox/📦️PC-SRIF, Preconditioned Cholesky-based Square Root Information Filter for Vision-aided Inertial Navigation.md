---
aliases: 
date: 2024-10-05
title: 
author: 
tags:
  - Review
draft: true
---
#Icra25 #review #confidential

zotero : 
source : 

---
### Critique
- 

### Introduction
현재 VINS 알고리즘들은 information matrix를 포함한 방정식을 풀 때 numerical stability를 위해 QR decomposition (float32)를 이용해 풀곤했다. 
하지만 연구에서 이 stability에 관련된 ill-conditioned는 VINS system에 있는 게 아니라 state parameter에서 있는 거라고 밝혀냈고, 이에 따라 precondition을 해서 QR보다 약 2배 빠른 ($O(mn^2) , O(2mn^2)$) Cholesky decomposition을 활용하는 새로운 기법 제시.

### Methodology


### Experiments
- 어떤 데이터
- 어떤 정보를 분석했는지 (ate, rpe, NEES)


### ❓️Questions

### Future Articles to Read

### Ax=b와 condition number
condition number는 matrix A의  max singular value / min singular value인데 
b의 민감성에 대한 solution 변화를 생각하면 된다.

condition numbe가 
- 작다 → well-conditioned : b에 perturbation이 있어도 값이 잘 안 변함
- 유한 ; A가 invertible → well-posed
- 매우 크다 → ill-conditioned 
- 무한 → ill-posed; 변수보다 식이 적어서 해가 무한 or 없을 때.