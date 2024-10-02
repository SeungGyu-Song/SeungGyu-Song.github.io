OpenVINS Study 3주차에는 Initialization(Static / Dynamic)에 관해 다룰 예정입니다.

<목차> 
- Introduction / Heads up for reading the codes
- Feature Extraction / Tracking (Opticalflow / Descriptor)
- **initialization (Static / Dynamic)**
- EKF propagation
- EKF Update 

---
### Reference
- [Technical Report](https://pgeneva.com/downloads/reports/tr_init.pdf) 
	- [[📦️OpenVINS State Initialization - Technical Report]]
- [Estimator initialization in vision-aided inertial navigation with unknown camera-IMU calibration](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=6386235)
- [Closed-form Solutions for Vision-aided Inertial Navigation](https://tdongsi.github.io/download/pubs/2011_VIO_Init_TR.pdf)


## Class
- StaticInitializer
- DynamicInitializer
- CpiV1
---
# Code 
[[🧩OpenVINS Code Analysis#try_to_initialize|VioManager::try_to_initialize]]

	[[🧩OpenVINS Code Analysis#InertialInitializer#initialize|InertialInitializer::initialize]]
	
		[[🧩OpenVINS Code Analysis#FeatureHelper#compute_disparity|FeatureHelper::compute_disparity]]
		
		[[🧩OpenVINS Code Analysis#StaticInitializer#initialize|StaticInitializer::initialize]]  or [[🧩OpenVINS Code Analysis#DynamicInitializer#initialize|DynamicInitializer::initialize]]
	~~[[#propagate_and_clone|Propagator::propagate_and_clone]]~~
	[[#marginalize_old_clone|StateHelper::marginalize_old_clone]]


# Concept
platform이 움직이고 있을 때 → dynamic initialization 진행 
	Ref : [Estimator initialization in vision-aided inertial navigation with unknown camera-IMU calibration](https://ieeexplore.ieee.org/abstract/document/6386235)
	linear system을 만들어서 velocity, gravity, feature position을 구하고
	이후에 covariance recovery를 위해 full optimization 진행.
