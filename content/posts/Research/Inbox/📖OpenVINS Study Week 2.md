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
---

### UpdateMSCKF vs UpdateSLAM
- MSCKF는 landmark 없는 state만
- SLAM은 landmark 있는 state도 
근데 돌아갈 때는 UpdateMSCKF 후 UpdateSLAM으로 총 두 번의 update를 할 거 같음.


multi camera면 카메라 별로 thread가 돌아감. -> 한다고 해서 cpu load가 2배가 되지 않음.

ZUPT는 issue에서 잘 안 된다는 보고도 있었고
	동욱이 형 : feature 개수가 적을 때 도움이 도드라짐 : 
	 로봇이 돌다가 멈출 때, 날아가는 경우가 있는데 이 때 bias 추정을 잘 못 해서 날아가는 거 같음.

RANSAC vs PROSAC

knnMatch에 대해서 살펴보기. (러닝이 잘 해준다.)


feature 개수가 많으면 descriptor 방식이 더 좋은 거 같다.
descriptor가 상대적으로 더 엄격하게 해야 성능이 보장됨. -> 그래서 threshold 1/pixel
	knnMatching이 성능이 안 좋아


---
### To Do
1. Rviz point cloud 구분
2. Grider_Grid, Grider_FAST 방식