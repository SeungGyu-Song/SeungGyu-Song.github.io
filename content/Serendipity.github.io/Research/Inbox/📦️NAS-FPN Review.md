---
aliases: 
date: ""
title: 
author: 
tags:
  - Review
---
참고 블로그 : [참고블로그](https://magmatart.dev/deep%20learning/2019/06/03/NAS-FPN.html)
zotero : [[@Ghiasi_NASFPN_2019]]
source : 

---
### Critique
	- 목적 : RetinaNet의 성능을 가장 높이는 최적의 FPN 구조를 찾기.

### Introduction
##### NAS 
- 강화학습 기법을 이용해서 최고의 성능을 내는 딥러닝 아키텍쳐를 찾는 방식 
- Model의 구조를 변경하면서 탐색할 수 있는 Search Space를 제공해 주면 RNN 구조의 Controller가 그 안을 탐색하면서 하나의 Model 구조를 만들어냄 (Child Model)
##### FPN 
- 다양한 크기의 feature를 찾기위해 하는 방식인 Feature Pyramid Network

#### 풀고자하는 문제점
1. The challenge of designing feature pyramid architecture is in its *huge design space*
2. using Deep ConvNets to generate pyramidal representations by featurizing image pyramid imposes large computation burden.

#### Contribution
- 모든 가능한 cross-scale connection을 커버하는 novel한 search space 제시 (multiscale feature representation을 위해)
- 다양한 backbone과 잘 작동할 수 있는 great flexibility
- pyramidal architecture에서 처음으로 NAS를 성공시킨 레포트

### Methodology
#### Neural Architecture Search
기존의 NAS 방식과는 크게 두 가지 다른 점이 있다. (framework를 참고한 기존의 방식)
1. 기존의 방식은 output이 single인 반면, 제안된 방식은 multiscale feature를 결과로 내보낼 수 있다.
2. 기존의 방식은 같은 feature resolution에서 connection을 찾는데 제시된 방식은 c*ross-scale connection*을 찾는다.
#### 3.1 Architecture Search Space
a feature pyramid는 여러 개의 “*merging cells*”로 이루어져있고, 이거는 많은 input layer를 RetinaNet의 표현바식으로 결합해준다?

네트워크의 Feature Layer입력과 출력은 모두 5개지만 중간의 Merging Cell은 몇 번이고 쌓아서 사용가능 → Merging Cell의 개수를 조절해서  Speed와 Accuracy의 Tradeoff를 맞춘다.
![[Zotero/images/@Ghiasi_NASFPN_2019/image-3-x50-y555.png|450]]
##### Merging Cell
이전의 object detection에서의 중요한 관점은 다른 scale의 feature들을 “*merge*”하는 것이었따. 
cross-scale connections는 모델이 high-level feature (strong semantics)와 low-level features(high resolution)을 결합하도록 한다. 
![[Zotero/images/@Ghiasi_NASFPN_2019/image-3-x298-y279.png|]]
그림에서 보이다시피 Pyramid에서 두 개의 feature layer를 선택해서 Merging Cell에 입력하여 하나의 원하는 스케일의 output feature layer로 만든 후, 이를 기존 Pyramid의 맨 아래에 합쳐진 Layer를 추가한다. 그러면 또다시 이 Layer는 merging cell의 재료가 될 수 있다.

그리고 이 merging cell을 어떻게 만들지는 controller RNN에 의해 결정된다.

### Experiments
- 어떤 데이터
- 어떤 정보를 분석했는지 (ate, rpe, NEES)


### ❓️Questions

### Future Articles to Read




##### 일반 [[@Lin_Feature_2017|Feature Pyramid Network]]
![[image-1-x294-y402.png|]]
여기서 보면 
	(a)는 sift와 같은 일반 hand crafted feature detection에서 쓰이는 방식. 우리가 미리 이미지 스케일을 지정해놓고 각 스케일마다 feature를 뽑는 건데 CNN에서는 연산량이 많아서 적절치않다.
	(b) YOLO에서 쓰이는 방법
	(c) 각각 feature map들에 대해서 prediction. - SSD - 성능이 높지만 feature 간의 representation 차이가 있어서 semantic gap이 발생. (모델 초반 -  low feature, 깊어질 수록 high level feature)
	(d) semantic gap을 극복할 수 있는 방법! 
	


##### Feature pyramid 만드는 방법
![feature_pyramid](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F0ela2%2FbtqUsdFXuAe%2FzSFO8k1p1JIbMoz5vWi75k%2Fimg.png)

top-down pathway : 각 pyramid level에 있는 feature map을 두 배로 upsampling해주면서 채널 수는 같게 해주는 방법 

각 층은 두 배로 upsampling이 되고, 채널 수는 (제일 낮은) 256으로 맞춘다. 