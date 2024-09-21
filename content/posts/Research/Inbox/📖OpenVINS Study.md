# Week 1 
~~[doxygen으로 document 만들기](https://docs.openvins.com/dev-docs.html)~~
state설명
전체 구조 
(IMU intrinsic)
## Miscs for general understanding of code 
### namespace
- ov_init : initialization을 위한 namespace
- ov_msckf :  실제 VIO 돌릴 때 high level에서 필요한 함수, class의 namespace
-  ov_core : 나머지 함수 / class 들 (feature tracking…)
### Class
- Type.h
- State.h`
### functions
[[🧩OpenVINS Code Analysis#debugPrint|Printer::debugPrint]] 
## code
- run_subscribe_msckf.cpp
	- main()
	- viz→setup_subscribers(parser)
- ROS1Visualizer.cpp
	- parser→parse_external : config 파일 값 받아오기.
	- [[🧩OpenVINS Code Analysis#callback_stereo|callback_stereo]] : camera data 저장 및 time 기준 sort
	- [[🧩OpenVINS Code Analysis#callback_inertial|callback_inertial]] : imu callback
		- [[🧩OpenVINS Code Analysis#feed_measurement_Imu|feed_measurement_imu]] : imu data 저장
		- ([[🧩OpenVINS Code Analysis#visualize_odometry|visualize_odometry]] : imu fast propagation)
		- thread 생성
			- stereo image가 정상적으로 들어오면
			- ([[🧩OpenVINS Code Analysis#feed_measurement_camera|feed_measurement_camera]]) : feature tracking & initialization & filter propagation - update
			- visualize() : state, image publish. 

[[📖OpenVINS Study Week 2]]
