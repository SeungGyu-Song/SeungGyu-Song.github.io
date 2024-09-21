![[Pasted image 20240919141433.png]] 

## Contribution
 global positioning step에서 camera position과 3D structure를 동시에 고려해서 정확성을 높임.
 
## Introduction
 ### Incremental vs Global 
 incremental방식과 global 방식은 모두 feature extraction + matching과 two-view geometry를 바탕으로 initial view graph를 짓는 것은 동일
 
#### Incremental
 추가적인 image와 3d structure를 sequential하게 고려함
 이 때 반복되는 BA로 정확하긴 하나 연산량이 매우 많음.

#### Gloabl
1. 모든 image에 대해 한 번에 camera geometry를 구하는데, rotation과 triangulation을 따로따로 구함.
2. 이 camera geometry를 바탕으로 triangulation
3. Global BA

### Global Translation averaging step
incremental과 global 방식의 정확도 차이의 주된 요인은 ==global translation averaging step==이라고 봐도 됨.

이 Translation averaging step이 마주하고있는 세 가지 힘든 점.
1. scale ambiguity
	1. two-view geometry는 up-to-scale이라 triplets of relative directions가 필요함.
	2. 그럼에도 이 triplets가 skewed 돼있으면 계산된 scale 값은 노이즈가 많이 꼈을 가능성이 크다.
2. camera intrinsic parameter를 미리 알고있어야함.
3. co-linear한 motion은 reconstruction을 degenerate하게함.


## Review of Global Structure-from-Motion
Global SfM은 총 아래와 같은 세 단계로 이루어져있음.
1. Correspondence search
2. camera pose estimation
3. joint camera and structure refinement

### Correspondence Search
GLOMAP은 COLMAP과 같이 RootSIFT와 BoW image retrieval(brute-force)로 매칭쌍 찾음
1. feature extraction and matching 
2. 이 때 feature matching에 outlier가 있을 텐데 이거는 two-view geometry를 통해서 제거.
3. Homography Matrix $H$를 구하거나 Essential Matrix or Fundamental Matrix(intrinsics를 모를 때)를 구함.
	1. camera instrinscs를 안다고 할 때,  $R_ij$와 t로 분해 가능

### Global Camera Pose Estimation
Global camera pose estimation이 global 과 incremental 방식의 key difference임.

global 방식은 view graph를 input으로해서 모든 이미지에 대해 한 번에 global camra pose를 estimation함.

근데 main challenge는 optimization 문제를 잘 모델링하고 품으로써 view graph에서 noise와 outlier들을 어떻게 다루는  지에 달려있음.
#### Rotation Averaging

#### Translation Averaging
Rotation Averaging 이후에 이루어지는데, outliers와 noise 그리고 relative translation의 scale을 모르는 특징 때문에 이 작업이 어려움.

- view graph가 *parallel rigidity*가 있으면 camera pose가 유일하게 결정될 수 있음.
- point tracks가 translation averaging에 도움이 되면 그냥 translation averaging을 건너 뛰고 한 번에 camera랑 point position을 동시에 추정하자!

#### Structure for Camera Pose Estimation

### Global Structure and Pose Refinement
#### Global Triangulation
multiple view triangulation방식에는
- Direct Linear Transformation (DLT)
- midpoint methods
- LOST 
등이 있는데 위 방식은 다 어느 정도의 outlier들이 있으면 거의 잘 안 됨.

<span style="color:blue">근데 GLOMAP은 camera position과 함께 그냥 한 번에 BA돌려버림 </span>

#### Global Bundle Adjustment
그냥 reprojection error가 낮은 걸 cost function으로 사용

### 2.4 Hybrid Structure-from-Motion

## Technical Contributions
### Feature Track Construction
[Cheirality test](https://cmsc426.github.io/sfm/#tri) → epipole과 가깝거나 triangulation angle이 작은 point들은 제외 (Outlier로 판단)
### Global Positioning of Cameras and Points
![[Pasted image 20240919221353.png]]![[Pasted image 20240919221404.png]]
 한편, 모든 포인트와 camera variable에 대해 -1부터 1 사이의 uniform random distribution으로 initialization한다고 했는데, 무슨의미인지 모르겠다. #점검 
 또한 intrinsic을 모르는 카메라에 대해서는 factor에 가중치 2를 줌으로써 더 약하게 weight가 들어가게 했다.
#### 장점
 1. least square error 특성 상 다 더하는 거기 때문에 outlier에 민감하다.  하지만 이렇게 되면 error term이 0과 1사이로 좁혀지는데, 이는 outlier에 좀 더 강건한 error 식을 세울 수 있게 된다.
 2. Intrinsic을 모르는 상황에서 강건함 - intrinsic parameter는 relative translation을 구할 때 필요하므로 여기서는 global translation을 진행해서 intrinsic에 강건함.
	 1. 두 카메라 위치 간의 baseline이 길어질 수록 ray의 noise가 커지니까 translation을 구하기가 어려움.
	 2. intrinsic을 모르는 상황에서 relative pose와 다르게 단독으로 translation을 구하는 거다보니 overlapping cameras가 아니라 individual camera에 대해 bias가 추가되는 꼴이다.

### Global Bundle Adjustment
Global positioning에서 camera와  points의 pose를 알 수 가 있는데, intrinsic을 모르는 상황에서는 정확도가 떨어진다. 그래서 Global bundle adjustment를 하게 됨.

1. 처음에는 camera rotation 고정 후, intrinsics와 points랑 같이 optimization이 됨.
	1. 그럼 rotation 고정됐을 때는 translation만 보는 건가? #점검 

한편, 처음 BA를 하기 전에 3D point observation을 angular error 기준으로 거르고, image space에서 reprojection error로 tracking된 점들을 거름.

### Camera Clustering
인터넷에서 사진 건져오다보면 겹치지 않는 사진도 잘못 매칭되고, 서로 다른 reconstruction이 하나로 합쳐질 수가 있음. 그래서 이러한 작업을 통해 한 번 더  refinement를 해줌.

Covisibility graph를 통해 5개 보다 적게 counting 된 point 삭제.
 일정 threshold($\tau$)보다 많이 연결된 point에 대해서  두 개의 *strong components*를 merge하려고 함. (만약 0.75$\tau$ 개수보다 많은 count를 가진 두 개의 edge가 있을 때)

사실 이게 뭔 소린지 잘 모르겠다. #점검 
