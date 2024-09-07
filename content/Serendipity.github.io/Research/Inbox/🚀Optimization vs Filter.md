---
title: 
date: 2024-08-28
tags:
---

### Topic :
#Optimization vs #Filter
성능 비교를 해보고 싶어서 1016 펌프트랙 데이터셋으로 비교를 해보았다.

### Memo
전반적으로 Optimization 기반([[🧩VINS-Fusion Code Analysis|VINS-Fusion]])은 스무스 한 반면, 한 번 발산을 크게 하면 다시 돌아오기까지 오래 걸리는 거 같다.
Filter 방식([[🧩OpenVINS Code Analysis|OpenVINS]])은 자잘자잘하게 계속 발산하는 거 같아서 성능이 구데기다. 

- [ ] filter도 그렇고 optimization 방식도 그렇고 언제, 무엇 때문에 발산하는 걸까? covariance가 전부 다 높으면 그렇게 되는 건가?
- [ ] imu noise를 조금만 낮게 해줘도 open vins 바로 터져버려서 bias를 찍어봐야 할 듯.
	- [ ] initialization에서 터지는 걸로 봐서 걸을 때마다 생기는 imu spike가 문제인 듯.

##### 펌프트랙 결과
###### VINS-Fusion

![[Pasted image 20240828133735.png|400]] 
###### OpenVINS
얘는 백 중간에 그냥 우주로 발산해버림
![[Pasted image 20240828134737.png|400]]

###### BASALT
바살황 ㄷㄷ ㄹㅇ 레전드네
![[Pasted image 20240828140636.png|00]]


---

### Reference
- 

### Link
- 
