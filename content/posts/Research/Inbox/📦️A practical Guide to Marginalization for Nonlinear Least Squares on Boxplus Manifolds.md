---
aliases: 
date: 2024-10-15
title: A practical Guide to Marginalization for Nonlinear Least Squares on Boxplus Manifolds
URL: https://evanlev.github.io/marginalization.pdf
tags:
  - Marginalization
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

- 일반 Cost function ($x_m$ : to be marginalized, $x_b$ : markov blanket, $x_r$ : remaining)
 ![[Pasted image 20241017194141.png]] 
![[Pasted image 20241017194214.png]]
위 식을 다음과 같이 marginaglization 부분을 변경![[Pasted image 20241017194428.png]]

![[Pasted image 20241017194506.png]]
($x_m = \hat x_m \boxplus \delta_m$ ) : \hat_x 가 linearization point.
![[Pasted image 20241017194657.png]]
![[Pasted image 20241017194736.png]]


#### Schur-complement
![[Pasted image 20241017194840.png]]
$$
g_m = J_m^Tf \qquad  g_b = J_b^Tf
$$
$$
\Lambda_{mb} = J_m^TJ_b \qquad \Lambda_{bb} = J_b^TJ_b \qquad \Lambda_{mm} = J_m^TJ_m
$$

가 [[📦️VINS-Mono Derivation, Optimization]]하고 똑같은 구조로 되어있음.
![[Pasted image 20241017194957.png]]
로 $\delta_m^*$를 Pseudo-inverse로 한 번에 구함.
이제 구했으니, $x_b$에 대해 구해야하기 때문에 schur-complement를 도입.
$$
\begin{bmatrix} I & 0 \\ -\Lambda_{bm}\Lambda_{mm}^{-1} & I]\end{bmatrix} \begin{bmatrix} \Lambda_{mm} & \Lambda_{mb} \\ \Lambda_{bm} & \Lambda_{bb} \end{bmatrix}  = \begin{bmatrix} \Lambda_{mm} & \Lambda_{mb} \\ 0 & -\Lambda_{bm}\Lambda_{mm}^{-1}\Lambda_{mb} + \Lambda_{bb} \end{bmatrix}
$$

이래서 

- ##### Eigen Decomposition
- #### Cholesky 
- ##### Modified Cholesky
#### Specialised QR Decomposition

결론적으로 두 방식 모두  marginalization에서 rank-deficient Jacobian을 사용했고, well-conditioned 문제에서는 거의 동일하게 작동했다.

### Numerical stability
- $LDL^{\top}$과 modified $LDL^{\top}$ factorization이 제일 연산량이 적었따.
- #### Graph\
- ##### Rotation RMSE, Condition number, $\Lambda_t$의 perturbation 
- ![[Pasted image 20241017193057.png|800]]
- 10초 후부터 Rotation error가 줄어들고, Jacobian $J_b, J_m$으로부터의 condition number도 줄어들었다. (eigen decomposition을 했을 때)
##### Ill-conditioned problem
- $LDL^{\top}$ 는 $\Lambda_t$에 perturbation을 줄 거다. 여러 identity를 추가하면서. → spurious measurement of zero error
- $LDL^{\top}$이 제일 큰 perturbation을 준다.
- modified cholesky가 lowest overall computational cost, worst case에서 smaller perturbation을 요구함. 


### ❓️Questions




