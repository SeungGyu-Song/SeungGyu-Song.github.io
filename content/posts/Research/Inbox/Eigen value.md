---
title: <Fill me w/ a compact title>
draft: true
tags:
  - Linear_Algebra
---
 reference : [tistory 블로그](https://deep-learning-study.tistory.com/324)
![[Pasted image 20241018130153.png]]

reference : [다른 tistory 블로그](https://twlab.tistory.com/46)
eigenvalue가 0이면 (3D→2D projection matrix를 기준으로)
- Ax = 0이므로, A의 nullspace가 존재하고, 글로 보내버리는 거 같다
- ChatGPT에 의하면, matrix를 더 낮은 차원으로 compress하는 것이라고 한다.

## Eigen vector가 A의 main direction이라고 해석가능?
(chatgpt한테 물어봄)

Ax=b를 해석할 때 main direction이라고 해석할 수 있을 때는 제한적인데, 예를 들어 covariance matrix in PCA를 들 수 있다.
이 경우는 PCA의 eigen vector들이 제일 큰 variance를 대표하기 때문이다. 

하지만 아래와 같은 예를 보자.
$$
A = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}
$$
이 때 eigen vector는 (1,0)이 되는데 이 행렬은 사실 shear 변환을 해주는 matrix라 (1,0)이 이 행렬의 주요 특성을 대변하지는 않는다.