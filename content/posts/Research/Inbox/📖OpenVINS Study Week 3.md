OpenVINS Study 3주차에는 Initialization(Static / Dynamic)에 관해 다룰 예정입니다.

<목차> 
- Introduction / Heads up for reading the codes
- Feature Extraction / Tracking (Opticalflow / Descriptor)
- **initialization (Static / Dynamic)**
- EKF propagation
- EKF Update 
---
# Code 
[[🧩OpenVINS Code Analysis#try_to_initialize|VioManager::try_to_initialize]]

	[[🧩OpenVINS Code Analysis#InertialInitializer#initialize]]
	
		[[🧩OpenVINS Code Analysis#FeatureHelper#compute_disparity|FeatureHelper::compute_disparity]]
		
		[[🧩OpenVINS Code Analysis#StaticInitializer#initialize|StaticInitializer::initialize]]  or [[🧩OpenVINS Code Analysis#DynamicInitializer#initialize|DynamicInitializer::initialize]]
		
	
	