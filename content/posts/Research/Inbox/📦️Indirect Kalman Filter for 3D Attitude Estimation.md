---
aliases: 
date: ""
title: 
author: 
tags:
  - Review
---

zotero : 
source : [Indirect Kalman Filter](https://mediawiki.isr.tecnico.ulisboa.pt/images/d/db/Indirect_Kalman_Filter_for_3D_Attitude_Estimation.pdf])

---
### Critique
- #quaternion
- 

### Introduction
- quaternion 특성과 연산에 대해 학습하자!

### 내용

## 1. Elements of Quaternion Algebra
### 1. Quaternion Definitions
unit quaternion $\bar{q} = \begin{bmatrix} \mathbf{q} \\ q_4 \end{bmatrix}$ 여기서  **q**는 허수로, 각 허수 i,j,k는 x,y,z 축을 의미합니다.
$q_4$는 scalar로 rotation direction을 의미하는데, 양수면 shortest rotation 을 의미합니다.
$\mathbf{q} = \begin{bmatrix} k_x \sin(\theta/2) \\ k_y \sin(\theta/2) \\ k_z \sin(\theta/2) \end{bmatrix}$ , $q_4 = \cos(\theta/2)$

$\bar{q} \otimes \bar{p} = \mathcal{L}(\bar{q})\bar{p} = \mathcal{R}(\bar{p})\bar{q}$ ,     $\bar{q}_I = [0 \quad 0 \quad0 \quad1]^{\top}$  , $\bar{q} \otimes \bar{q}_I = \bar{q}_I \otimes \bar{q}  = \bar{q}$ 
$\mathcal{L}(\bar{q}) = \begin{bmatrix} \Psi(\bar{q}) \quad \bar{q} \end{bmatrix}$                                            $\mathcal{R}(\bar{p}) = \begin{bmatrix} \Xi(\bar{p}) \quad \bar{p} \end{bmatrix}$ 
$\Psi(\bar{q}) = \begin{bmatrix} q_4 \mathbf{I}_{3\mathsf{x}3} - \lfloor q \; \mathsf{x} \rfloor \\ -\mathbf{q}^{T} \end{bmatrix}$                                 $\Xi(\bar{p}) = \begin{bmatrix} p_4\mathbf{I}_{3\mathsf{x}3} + \lfloor p \; \mathsf{x} \rfloor \\ -\mathbf{p}^{T} \end{bmatrix}$               

$\Psi^{T}\Psi = \Xi^{T}\Xi = \mathbf{I}_{3x3}$

$\Phi$ → $\mathcal{L}$ , $\Xi$ → $\mathcal{R}$ 로 대응시켜서 생각하면 편한 것 같다.
$\bar{q}^{-1} = \begin{bmatrix} -\mathbf{q} \\ q_4 \end{bmatrix} = \begin{bmatrix} -\hat{k} \sin(\theta/2) \\ \cos(\theta/2) \end{bmatrix} = \begin{bmatrix}\hat{k} \sin(-\theta/2) \\ \cos(-\theta / 2) \end{bmatrix}$

$(\bar{q} \otimes \bar{p})^{-1} = \bar{p}^{-1} \otimes \bar{q}^{-1}$

이것도 중요한 성질 같아. quaternion이 역이면 연산자에 transpose 취하는 거.
$\mathcal{L}(\bar{q}^{-1}) = \mathcal{L}^T(\bar{q})$
$\mathcal{R}(\bar{p}^{-1}) = \mathcal{R}^T(\bar{p})$
![[Pasted image 20240903134337.png]]

### 1.3.2 Properties of the cross product skew-symmetric matrix
$\lfloor \omega \; \mathsf{x}\rfloor = -\lfloor \omega \; \mathsf{x}\rfloor ^{T}$
$\mathbf{a}^T\lfloor \mathbf{b} \; \mathsf{x} \rfloor = -\mathbf{b}^{T} \lfloor \mathbf{a} \; \mathsf{x} \rfloor$
$\lfloor \mathbf{a} \; \mathsf{x} \rfloor + \lfloor \mathbf{b} \; \mathsf{x} \rfloor = \lfloor \mathbf{a} + \mathbf{b} \; \mathsf{x} \rfloor$

##### Lagrange’s Formula
![[Pasted image 20240903125153.png]]
##### Jacobi Identity & Rotations
C가 회전이라고 했을 때.  ( 행렬이라고 봐도 되겠지?)
![[Pasted image 20240903125227.png]]

##### skew-symmetric 제곱
에 관한 것도 있으니 이건 직접 찾아보는 게 나은 듯.

#### 1.3.3 Properties of the matrix $\Omega$ 
얘는 input이 $\omega$로 3x1 임.
$\Omega(\omega) = \begin{bmatrix} 0 & \omega_z & -\omega_y & \omega_x \\-\omega_z & 0 & \omega_x & \omega_y \\ \omega_y & -\omega_x & 0 & \omega_z \\ -\omega_x & -\omega_y & -\omega_z & 0 \end{bmatrix} = \begin{bmatrix} -\lfloor \omega \; \mathsf{x} \rfloor & \omega \\ -\omega^T & 0 \end{bmatrix}$  

그리고 $\Omega$의 제곱도 나와있으니까 참고하기. 마치 imaginary number와 특성이 비슷함.

#### 1.3.4 Properties of the matrix $\Xi$ 
얘는 위에서 봤듯이 input은 quaternion 임. 근데 $\Omega(\mathbf{a})$와 $\Xi(\bar{q})$의 관계는 multiplication matrices인 $\mathcal{L}(\bar{q})$와 $\mathcal{R}(\bar{p})$ 와 유사함.

$\Phi$ → $\mathcal{L}$ , $\Xi$ → $\mathcal{R}$ 로 대응시켜서 생각하면 편한 것 같아요.


- $\Xi(\bar{q})\Xi^T(\bar{q}) = \mathbf{I}_{4\mathsf{x}4} - \bar{q}\bar{q}^T$
- $\Xi^T(\bar{q})\bar{q} = \mathbf{0}_{3\mathsf{x}1}$
- $\Omega(\mathbf{a})\bar{q} = \Xi(\bar{q})\mathbf{a}$

### 1.4 Relationship b/w Quaternion and Rotational Matrix
coordinate frame을 바꾸기
$^{L}\mathbf{p} = ^L_G\mathbf{C}(\bar{q}) ^G\mathbf{p}$
여기서 행렬 $\mathbf{C}$는 3x3 회전행렬. 
다음과 같이 연산이 될 수 있다.

![[Pasted image 20240903133748.png]]

![[Pasted image 20240903133756.png]]
![[Pasted image 20240903133802.png]]


$\bar{q} \otimes \bar{p} \otimes \bar{q}^{-1}$
= $\mathcal{L}(\bar{q})\mathcal{R}^T(\bar{q})\bar{p}$
= $\mathcal{R}^T(\bar{q})\mathcal{L}(\bar{q})\bar{p}$
= $\begin{bmatrix} \mathbf{C}(\bar{q}) \; 0 \\ 0 \quad 1 \end{bmatrix} \; \begin{bmatrix} \mathbf{p} \\ p_4 \end{bmatrix}$\
 = $\begin{bmatrix} \mathbf{C}(\bar{q})\mathbf{p} \\ p_4 \end{bmatrix}$

#### quaternion perturbation
$\delta \bar{q} = \begin{bmatrix} \delta\mathbf{q} \\ \delta q_4 \end{bmatrix} \\ = \begin{bmatrix} \hat{\mathbf{k}} \sin{\delta\theta / 2} \\ \cos{\delta\theta / 2} \end{bmatrix} \\ \approx \begin{bmatrix} \frac{1}{2}\delta \theta  \\ 1 \end{bmatrix}$



 다음으로는 아래에 대해 다루겠습니다.
![[Pasted image 20240903143956.png]]

![[Pasted image 20240903144207.png]]
이게 왜 이렇게 되는지 식 95번에 대해 잘 아직 파악을 못했습니다. #점검 

Fig 1.![[Pasted image 20240903144244.png]]
z축 기준으로 돌렸으니까 z축에 $\sin(\Phi / 2)$ 가 오는 거 같긴한데..
### 1.5 Quaternion Time Derivative
이게 가지는 의미가 뭘까.
![[Pasted image 20240903144549.png]]




### ❓️Questions

### Future Articles to Read
[[🧩OpenVINS Code Analysis]]
