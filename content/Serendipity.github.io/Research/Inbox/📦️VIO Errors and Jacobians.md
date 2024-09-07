---
aliases: 
date: 2024-05-15
title: VIO Jacobians
URL: https://alida.tistory.com/65
tags:
  - VIO
  - Jacobian
  - Optimization
  - Reprojection_Error
---
### Objective
- 실제 jacobian을 구하는 데 과정과 생김새를 공부하고 싶었는데 VINS-Derivation으로는 확 와닿지 않았음.

### Future Work
- Photometric Error, 3D Line Feature, quaternion based jacobian 아직 보지 않았음.
- [[📦️ Quaternion kinematics for ESKF]] (2.4.2 - 2.8, 4.4 읽기)

### Reprojection Error

![[Pasted image 20240515145043.png|400]]
Reprojection Error : 비교하고자 하는 frame의 image plane으로 projection 시켜서 measurement와 비교한 error이며 다음과 같다.

실제 VINS에서는 Reproejction Error가 Intrinsic parameter를 곱한 Image Plane에서 이루어지기 때문에 Jacobian의 term이 마지막 2개로만 이루어진다.

![[Pasted image 20240515145330.png]]

최적화를 하기 위해서는 [[📦️VINS-Mono Derivation, Optimization#Cost Function]]에서 볼 수 있는 것 처럼 Jacobian을 구해서 미소량만큼 움직여야한다. 이 때, Reprojection error를 통해서 state의 pose와 landmark position을 최적화할 수 있다. 따라서 pose는 $X$로, landmark는 $T$ 로 나타낼 예정이다.
#### Reprojection Error - Pose
먼저 pose에 대해서 Jacobian을 구해보면 아래와 같이 Chain Rule을 이용해서 쉽게 구할 수 있다.
![[Pasted image 20240515150227.png|300]]
한편, 내가 여기서 의문이 들었던 점은 Chain Rule에서 사이에 낑겨있는 애들을 어떻게 고르는 건가 싶었는데 **당연하게도 현재 미분하려고하는 애의 마지막 전 단계에 대해서 미분을 해주면 되는 것이다. 또한 내 추정치에 대해서 미분하는 것이지 measurement값은 건드리지 않는다.** 


- 1번 (camera plane / image plane)
- ![[Pasted image 20240515150536.png|300]]

- 2번 (image plane / 비교 기준 시점의 3차원 점)
- ![[Pasted image 20240515150606.png|300]]

- (비교 기준 시점의 3차원 점 / 그 때 필요한 R,t)
- ![[Pasted image 20240515150815.png|200]]
- ---
한편, Rotation Matrix로 바로 최적화를 하면 over-parameterization이라는 단점이 생기기 때문에 lie algebra로 변환시켜준다. 

> [!Over-parameterization 단점]
>> 파라미터를 중복해서 계산하기 때문에 비효율적이다.
>> 추가적인 자유도로 인해 수치적으로 불안정할 수 있다.
>> 해를 구할 때마다 계속해서 필요 조건을 만족하는지 점검해야한다.

이 때, 우리가 구한 증분량 $\Delta w$를 기존에 업데이트 하는 방식은 두 가지로 나눌 수 있는데 각각
- perturbation 모델을 이용하는 방법
- lie-algebra를 이용하는 방법
이 있다.
![[Pasted image 20240515151911.png]]
lie-algebra 모델은 left-Jacobian을 활용하는 더 복잡한 방식이기 때문에 위인 perturbation model이 더 선호된다고 한다. 
![[Pasted image 20240515152103.png|450]]
<mark class="hltr-red">Q : Reprojection error의 최적화의 경우 카메라 포즈와 $\Delta w$가 크지 않아서 위의 자코비안을 주로 사용한다고 하는데 정확히 무슨 자코비안, 그리고 어떤 연결고리가 있는 걸까?</mark> <a id=”question1”></a>

---
#### Reprojection Error - Inverse Depth
한편, 이제부터는 landmark에 대해서 알아보자. VINS-Mono에서는 landmark position을 state로 넣지 않고 inverse-depth로 표현하기 때문에 이에 대해서 알아보고자 한다.

Inverse depth로 표현을 하면 좋은 점
- 이미지 평면 상의 픽셀 좌표만 알고 있으면 inverse depth를 사용하여 3차원 점을 완벽하게 나타낼 수 있다.
- depth가 0일 경우가 없을테니 모든 점에 대해서 depth를 0~1로 맵핑할 수 있다.

<mark class="hltr-red">*근데 이러면 너무 intrinsic parameter에 의존하게 되는 것 아닐까?*</mark>


Chain Rule로 똑같이 구하는 것이기 때문에 $\frac{\partial\hat p} {\partial\tilde p}$ * $\frac{\partial\tilde p}{\partial X'}$ 는 그대로고 마지막만 다음과 같이 바뀌면 된다. 

![[Pasted image 20240515154039.png|300]]

### Pre-integration Error
이 부분은 [[📦️VINS-Mono Derivation, Optimization]]에서 자세히 설명을 적어놨기 때문에 이 글에서 얻어갈 부분만 적으려고 한다.

- 우선 IMU cost function에 해당하는 state들이 ( $p^w_{b_k}$,$q^w_{b_k}$ ) 그리고 속도, b_a, b_g이기 때문에 state에 속하는 td나 inverse depth는 사용되지 않는 점을 기억하자. **즉, state에 있다고 모든 residual마다 다 써먹어야하는 건 아님.** 

다음으로는 quaternion을 SO(3)로 바꿔서 활용하는 부분인데 아직도 잘 해결이 되지 않았다.[[📦️VINS-Mono Derivation, Optimization]]

$\theta$를 angular velocity vector라고 하자. 그렇다면 Jacobian은 다음과 같이 변한다.

![[Pasted image 20240515154917.png|300]]

이에 대한 근거는 다음과 같다

![[Pasted image 20240515154946.png]]

<mark class="hltr-red">근데 여기서 궁금한 점은 171번 식에서 어떻게 $\theta u$가 $\theta u/2$로 변했는지는 잘 모르겠다. 그리고 error가 매우 작아서 imaginary part만 사용이 된다는 부분도 잘 이해가 되지 않는다.</mark>
---
추가로, 최적화를 하는 IMU Residual 중 $\gamma$와 $\beta$의 순서를 바꿔서 하는 게 계산상으로 더 쉽다고 하는데 이 부분도 아직 잘 모르겠따.

### Questions

- <mark class="hltr-red">Reprojection error의 최적화의 경우 카메라 포즈와 $\Delta w$가 크지 않아서 위의 자코비안을 주로 사용한다고 하는데 정확히 무슨 자코비안, 그리고 어떤 연결고리가 있는 걸까?</mark> 
		> 분모에 들어간 식이 lie-algebra 활용한 방식은 그냥 $W$고 perturbation 방식은 $\Delta W$라서 다름.

- <mark class="hltr-red">근데 여기서 궁금한 점은 171번 식에서 어떻게 $\theta u$가 $\theta u/2$로 변했는지는 잘 모르겠다. 그리고 error가 매우 작아서 imaginary part만 사용이 된다는 부분도 잘 이해가 되지 않는다.</mark>
		> Quaternion kinematics for ESKF 2.4.2 ~ 2.8, 4.4 섹션을 읽으면 이해가 될 것이라고 함.

- 추가로, 최적화를 하는 IMU Residual 중 $\gamma$와 $\beta$의 순서를 바꿔서 하는 게 계산상으로 더 쉽다고 하는데 이 부분도 아직 잘 모르겠따.
		> VINS에서 state를 Pose와 Vel,Ba,Bg로 나눠서 Jacobian에 나눠서 담았는데 식의 순서를 위와 같이 바꾸면 J[0], J[2]로 묶어서 처리를 하는 등의 코드 상 이득이 있어서 바꾼 것이라 판단됨.




---
[[@_Errors_and_Jacobian_Derivations]]