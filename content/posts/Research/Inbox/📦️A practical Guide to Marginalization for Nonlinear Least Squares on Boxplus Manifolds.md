---
aliases: 
date: 2024-10-15
title: 
URL: https://evanlev.github.io/marginalization.pdf
tags: 
draft: true
---
### Critics
- 이 지식을 왜 공부해야 했는지

### Future Work
- 내가 이해 못한 부분을 어떻게 보완할 수 있을까?

## Intorudction
### 논문의 중심내용
1. manifold를 고려한 marginlization
2. implementation을 위한 square-root and Schur-complement-based marginlization을 다루고, novel한 Cholesky factorization에 대해서도 다룸.

#manifold manifold란 내가 관심이 있는 변수들을 표현하기 위한 공간이라고 생각하면 되고, smooth geometry를 가진 mathematical sets라고 받아들이자.

## 3 Generic Marginalization
### 1. Schur-complement
### 2. Cholesky Factorization based
### 3. QR Factorization based
[[📦️Square Root Marginalization for Sliding-Window Bundle Adjustment]]


## 결론

이 technical report에서는 아래의 방법을 통해서 실험했다. (GPS-IMU의 optimization)
#### Schur-complement
- ##### Eigen Decomposition
- #### Cholesky 
- ##### Modified Cholesky
#### Specialised QR Decomposition

결론적으로 두 방식 모두  marginalization에서 rank-deficient Jacobian을 사용했고, well-conditioned 문제에서는 거의 동일하게 작동했다.


### ❓️Questions




