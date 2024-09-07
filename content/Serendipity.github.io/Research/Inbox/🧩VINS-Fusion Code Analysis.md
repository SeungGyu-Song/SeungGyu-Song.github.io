---
title: VINS-Fusion Code Analysis - IMU
date: 2024-05-13
tags:
  - VINS-Fusion
  - IMU
  - Pre-integration
---
ro
- [ ] class별로 함수 찢어놓고 여기에는 링크로 걸어서 관리하기
### Code DeCode: 
###### inputIMU : 
fastPredictIMU
- 여기서 주의할 건 acceleration값을 곱할 때 방향(quaternion)을 고려해준다는 것.
- `Eigen::Vector3d un_acc_0 = latest_Q * (latest_acc_0 - latest_Ba) - g`
- `latest_Q = latest_Q * Utility::deltaQ(un_gyr * dt)`



#### ProcessMeasurements
###### getIMUInterval
featureTime 기준(prevTime, curTime) 사이의 IMU 값을 잘라오기
accVector, gyrVector


##### initFirstIMUPose(accVector)
IMU로는 yaw 값을 얻을 수 없으니까 현재 IMU로만 계산한 값에서 yaw에 해당하는 값을 없애주는 작업.
###### Eigen::Matrix3d Utility::g2R (g)
 g와 {0,0,1}사이의 quaternion을 구하고 여기서 계산된 yaw는 observable하지 않으니까 빼서 없애줌.






##### ProcesIMU(linear_acceleration,angular_velocity )
이제부터 pre-integration 시작
###### midPointIntegration
> midPoint니까 각 윈도우의 처음과 끝을 평균내서 그 시간동안 등속운동했다는 가정하에 P,V,attitude를 계산함.
>  그리고 이를 바탕으로 **<mark class="hltr-yellow">jacobian과 covariance</mark>** 를 계산

그리고 Bias를 제거한 acc,gyr 값을 이용해 Rs, Ps, Vs값을 업데이트. 즉, optimization의 initial guess를 여기서 처리함.
그리고 acc_0, gyr_0은 현재 들어온 input인 linear_acceleration, angular_velocity로 refresh해줌.

## processImage
### INITIALIZATION
### NON_LINEAR

### Optimization

#### outlierRejection
모든 Observation과 제일 오래된 observation의 
average error * <mark class="hltr-red">Focal_Length >3</mark> → 해당 feature를 outlier로 보고 삭제
이 threshold는 어디서 튀어나온 건지 아직 모르겠음.

###### reprojectionError
camera frame에서 Normalized 평면에 대해 reprojection error를 구하는 함수.
#### SlideWindow
**최적화 후 window 관리를 하는 함수**

>window에 해당하는 변수들
>>Ps, Rs
>>Vs, Bas, Bgs, pre_integrations, dt_buf, linear_acceleration_buf, angular_velocity_buf

*MARGIN_OLD* : $2^{nd}$ latest가 keyframe
 > 뒤의 것을 앞에 것과 swap 후 
 > >
 > [[🧩VINS-Fusion Code Analysis#SlideWindowOld|SlideWindowOld]] 를 호출
 
 *MARGIN_SECOND_NEW* : $2^{nd}$ latest가 <mark class="hltr-orange">non</mark>-keyframe
 > latest를 $2^{nd}$ latest 자리에 넣어주고, 바뀐 마지막은 없애주기.
 > [[🧩VINS-Fusion Code Analysis#slideWindowNew|slideWindowNew]] 를 호출
 > 
 > 
##### SlideWindowOld
 만약 NON_LINEAR라면
 > 없어져야할 R0, P0과 새로운 제일 고참 R1,P1으로 f_manager.removeBackShiftDepth
 > f_manager.removeBackShiftDepth
 아니면 (INITIAL)
 > f_manager.removeBack
 
 
###### removeBackShiftDepth
- 만약 start_frame이 0이 아니라면  → start_frame --
- start_frame이 0이면
	- 제일 오래된 애(start_frame)을 삭제하고 observation 개수가 0개, 1개면 feature 아예 삭제
	- 그런데도 살아남았다?
		- 그러면 지우기 전의 feature를 새로운 고참 윈도우로 reprojection해서 Depth를 update.


###### removeBack
- 만약 start_frame이 0이 아니라면 → start_frame --
- start_frame이 0이면 그냥 삭제해주고, 만약 observation이 0개면 feature를 아예 삭제

 > 
 
###### slideWindowNew
- [[🧩VINS-Fusion Code Analysis#removeFront|removeFront]] 호출

###### removeFront
- 변수 feature 중 방금 새로 뽑힌 feature는 start frame -1
- 기존의 feature들 중에서도 최근에 발견된 정보는 삭제해주기

### Memo
> need to write ...

### Reference
- 

### Link
- [[🧩VINS-Fusion Map.canvas|VINS-Fusion Map]]
- [[📦️VINS-Mono Derivation, Optimization]]
- [[📦️VINS-Mono Derivation, Pre-integration]]
- 

##### marginalization (Optimization함수 안)
drop_set : drop할 애들?
아직 visual feature에 대해 covariance 어떻게 두는지 안 나와있음.
marginalization에서 schur complement구하는 쪽 아직 못 봄
schur complement를 해서 결국에 어떻게 쓰겠다는 게 안 나와있는데

###### double2vector
- **최적화 후 State 값을 업데이트하기**
- 만약 IMU를 쓴다면
	- Window 제일 고참과 업데이트 된 값 (Quaterniond)를 비교해서 yaw만 추출한 다음에 Rs, Ps, Vs에 yaw를 곱해줘서 업데이트해주기 → 즉 yaw는 optimization에서만 구할 수 있게 됨.
	- 이 때 Ps는 Ps[0]을 기준으로의 변위에다 yaw를 곱해주는데 이거에 대한 타당성 검토하기
- feature depth를 f_manager에 업데이트

##### optimization_process
여기서는 state에 대해 ceres의 addParameterBlock을 활용해 선언해주고, addResidualblock을 통해 각 factor의 residual과 state 중 이에 해당하는 값들을 할당해줌.

그리고 observation이 3개 이하인 feature들은 아예 최적화 대상이 아님.
###### AddParameterBlock
pose의 경우 quaternion을 SO(3)로 맵핑 시키기 위해 ceres::LocalParameterization 을 활용.
state 중 고정을 하고 싶으면 SetParameterBlockConstant

###### AddResidualblock
각 factor에 맞게 loss function과 미분이 될 state를 짝을 맞추어 problem에 넣어주는 작업.

###### ❓️Questions
<mark class="hltr-red">한편, 여기서 나온 td가 imu와 camera 간 차이인 걸까? 그럼 왜 속도가 작으면 constant로 두는 걸까? 정체가 뭐임</mark>

왜 feature의 depth 값은 addParameterBlock을 안 해주지?