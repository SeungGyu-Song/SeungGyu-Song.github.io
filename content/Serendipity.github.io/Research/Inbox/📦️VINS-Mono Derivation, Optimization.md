---
aliases:
  - vins_derivation_optimization
date: 2024-05-13
title: VINS-Mono Derivation, Optimization
author: 
tags:
  - Review
  - Optimization
  - VINS-Fusion
  - VIO
---

zotero : 
source : [[@VINS Derivation|raw_vins_derivation]]

---
### Critique
- [ ] Jacobian의 생김새, 원리
- [ ] Pre-integration
- [ ] Initialization

### TIGHTLY-COUPLED NONLINEAR OPTIMIZATION
#### MAP → MLE
![[Zotero/images/@Wu_Formula_2020/image-12-x135-y461.png|450]]
식을 통해서 우리는 Prior인 $P(z)$를 모르기 때문에 $P(x|z)$가 아니라 Likelyhood인 $P(z|x)$를 구해야함을 알 수 있다.  한편 측정치 $z$의 uncertainty는 Gaussian distribution을 따른다고 가정한다.
![[Zotero/images/@Wu_Formula_2020/image-12-x180-y360.png|450]]
또한 이 Likelyhood는 위와 같이 식을 정리할 수가 있게 되는데, 이에 대한 설명은 아래와 같다.
![[Zotero/images/@Wu_Formula_2020/image-12-x163-y201.png|450]]
즉, Gaussian distribution을 따르는임의의 state $x$ 에 대해 위와 같이 식을 전개하면 결국 좌변을 최대로 만들기 위해서는 우변의 첫 번째 항은 상수이고, 두 번째항을 최소로 만들면 된다는 것을 알 수 있다. 따라서 우리는 MLE를 통해 MAP를 간접으로 구할 수 있게 된다.
<mark class="hltr-yellow">제일 가능성 높은 observation을 나타내는 system의 state 찾기!</mark>
#### Cost Function

VINS의 cost function은 다음과 같다. : Prior, IMU, Camera
![[Zotero/images/@Wu_Formula_2020/image-12-x142-y99.png|450]]
이는 nonlinear least square를 이용해 최적해를 구할 수 있게 되고, 이 때 GN을 이용해 푼다고 생각해보자.

이 때, 위 식은 linear하지 않으므로, 1차 Taylor Expansion을 활용해 linearization을 한다.
(Taylor Expansion : 근사 **다항함수**로 표현)

따라서 우리는 최적의 $\delta x$만 구하면 되는 것을 알게 돼고,  위 식을 아래처럼 전개한 후 
($f(x)$는 residual 함수)

![[Zotero/images/@Wu_Formula_2020/image-13-x129-y410.png|450]]
$\delta x$<mark class="hltr-red">에 대해 미분하고 최소가 되는 값을 구하기 위해 =0에 대해 구하면 아래와 같은 식을 얻을 수 있다.</mark>

![[Zotero/images/@Wu_Formula_2020/image-13-x194-y347.png|450]]

이를 SVD, Cholesky Decompostion 등을 통해 구할 수 있게 되고, $x$ ← $x + \delta x$ 를 통해 x를 업데이트함으로써 GN의 한 cycle이 마무리가 된다.

[[📦️VIO Errors and Jacobians]]에서 <mark class="hltr-yellow">Hessian matrix가 positive-definite</mark>이라 미분해서 0이면 그 값이 극솟값이 된다고 한다. 



##### IMU Cost Function
 ![[Zotero/images/@Wu_Formula_2020/image-13-x126-y142.png|450]]

[[VINS-Mono Derivation#Pre-Integration]]에서 구했던 식들을 활용해 위 처럼 residual 식을 나타낼 수가 있게 된다. 이 때의 IMU state는 다음과 같다.
![[Zotero/images/@Wu_Formula_2020/image-13-x133-y87.png|450]]

한편, VINS-Fusion에서는 robot의 attitude를 quaternion으로 표현하는데 실제 rotation의 변수는 3개인 반면 quaternion은 4개이므로 overparameterization의 문제가 발생한다. 따라서 Lie algebra로 옮겨서 최적화 문제를 풀게 되고 이를 다시 quaternion으로 복구하는 방식으로 최적화를 진행한다.


> quaternion → SO(3) →$so(3)$ → $so(3)^+$ → SO(3) → quaternion

한편, 논문에서 [[@VINS Derivation|raw_vins_derivation ^ Quaternion Variable]]
<mark class="hltr-red">이 overparameterization을 방지하고자 J[0]과 J[2]의 마지막 행은 0으로 뒀다고 하는데 그냥 이래도 되는 건지 의문이다. quaternion은 4개의 수가 모여서 하나의 의미가 되는 게 아닌가?</mark>
→ [[📦️VIO Errors and Jacobians]] 에서 좀 더 자세한 내용 추가

##### Camera Cost Function
[[📦️VIO Errors and Jacobians#Reprojection Error]]
근데 VINS-Mono에서는 camera plane이 아니라 intrinsic Parameter를 곱한 Image Plane에서 Reprojection Error가 이루어지는 것이기 때문에 Jacobian의 term이 마지막 2개임.

###### Marginalization (Schur Complement)
$\delta x_m$에 대해서는 구하지 않는 건가? prior가 정확히 어떤 걸 의미하는 걸까?



---
##### Least Square Error  (Factor Graph 논문 읽고 따로 빼는 것도 나쁘지 않을 듯.)
Least Square Error는 $\sum$ residual $^2$ 을 최소화 함으로써 구하고자하는 parameter를 구하는 방식으로, 이는 <mark class="hltr-yellow">특히 Outlier에 취약한 특성이 있다.
</mark> 왜냐하면 *전체 residual의 제곱의 합* 을 최소화 하는 것이므로 outlier의 residual도 같이 줄이려고 한다면 값이 이상해지기 때문이다. 이 때문에 VINS에서 huber norm과 같은 function과 optimization 이후 depth가 터무니 없는 것들을 제거해주는 작업을 하는 것 같다.

###### Newton 방법
만약 우리가 푸는 식이 linear하다면, Newton 방식으로 풀 수 있다. 
즉 $f(x) = 0$이라는 식을 풀기 위해 
$x^{k+1} = x^k -\frac{f(x^k)}{f’(x^k)}$ 로 나타낼 수가 있는데, 점진적으로 다가감으로써 구할 수 있다. 
**단점** 
> 초기값 위치에 따라 수렴하는 해가 달라진다. (i.e. sine함수)
> 초기값 위치에 따라 수렴하는 속도가 달라진다.
> 만약 f’(x)=0이라면 분모가 발산해서 계산이 불가능해진다.
###### Gauss-Newton 방법 
한편 우리가 풀어야하는 식이 nonlinear하다면 Gauss-Newton 방식을 활용해 풀 수 있다.
Newton방식을 연립방정식으로 확장시킨 것으로 보면 된다.
$X^{k+1} = X^{k} - \frac{F(X^k)}{J(X^k)}$ 로 쓸 수가 있는데 사실 행렬을 분모에 쓴다는 것이 불가능하다. 그래서 다음과 같이 식을 바꿔 쓸 수 있다.
$X^{k+1} = X^k - P$
$J(X^k) P = F(X^k)$
$P = (J^TJ)^{-1}J^TF$ 
Pseudo Inverse ($J^TJ$)를 통해 해를 구할 수 있었는데, 만약 $J^TJ$가 singular 행렬과 근접하다면 역행렬이 수치적으로 불안정하므로 해가 발산할 수 있다.



### Questions

### Future Articles to Read
- [ ] [Alida Camera Factor](https://alida.tistory.com/51)

### Reference
[다크프로그래머 - Least Square Method](https://darkpgmr.tistory.com/56)
[다크프로그래머 - Non-linear Mean Square](https://darkpgmr.tistory.com/58)
[네이버 블로그 Gauss-Newton](https://blog.naver.com/tlaja/220731745142)