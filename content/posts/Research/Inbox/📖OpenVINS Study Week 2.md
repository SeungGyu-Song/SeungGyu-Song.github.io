OpenVINS Study 2주차에는 Feature Extraction / Tracking에 관해 다룰 예정입니다.

<목차> 
- Introduction / Heads up for reading the codes
- **Feature Extraction / Tracking (Opticalflow / Descriptor)**
- initialization (Static / Dynamic)
- EKF propagation
- EKF Update 

---
코드에서는 Monocular, Stereo, 여러 개의 mono로 이루어진 시스템에 대해 다루기 때문에 이에 대한 차이점을 짚어주시면 감사하겠습니다.
## Class
- [[🧩OpenVINS Code Analysis#FeatureDatabase|ov_core::FeatureDatabase]]
- [[🧩OpenVINS Code Analysis#Feature|ov_core::Feature]]
# Code

[[🧩OpenVINS Code Analysis#feed_measurement_camera|VioManager::feed_measurement_camera]]
[[🧩OpenVINS Code Analysis#track_image_update|VioManager::track_image_update]]
 
## KLT Tracking
[[🧩OpenVINS Code Analysis#TrackKLT ← TrackBase#feed_new_camera|ov_core::trackKLT::feed_new_camera]] : pixel histogram 처리, ImagePyramid 만들기
	[[🧩OpenVINS Code Analysis#TrackKLT ← TrackBase#feed_stereo | trackKTL::feed_stereo]]
		[[🧩OpenVINS Code Analysis#perform_detection_stereo|trackKLT::perform_detection_stereo]] : FAST corner detection
			[[🧩OpenVINS Code Analysis#perform_griding|Grider_GRID::perform_griding]] 
		 [[🧩OpenVINS Code Analysis#perform_matching|trackKLT::perform_matching]] : Optical Flow
		 
## Descriptor
[[🧩OpenVINS Code Analysis#TrackDescriptor ← TrackBase#feed_new_camera|ov_core::trackDescriptor::feed_new_camera]]
	[[🧩OpenVINS Code Analysis#TrackDescriptor ← TrackBase#feed_stereo|TrackDescriptor::feed_stereo]] : pixel histogram처리
		[[🧩OpenVINS Code Analysis#TrackDescriptor ← TrackBase#perform_detection_stereo|TrackDescriptor::perform_detection_stereo]] : 새로운 descriptor 뽑기
			[[🧩OpenVINS Code Analysis#Grider_FAST#perform_griding|Grider_FAST::perform_griding]]
			
		[[🧩OpenVINS Code Analysis#TrackDescriptor ← TrackBase#robust_match|TrackDescriptor::robust_match]] 
