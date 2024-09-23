---
aliases: 
date: ""
title: 
author: 
tags:
  - Review
draft: true
---

zotero : 
source : 

---
### Critique
- 얻어갈 것
- 이 방법의 장점 / 부족한 점
- 어떻게 써먹을 수 있을지

# Introduction
### Event Cam의 장점
1. 각각의 독립적인 픽셀들의 밝기 변화를 기록해서 event data를 asynchronous하게 내뱉는다.
	1. high temporal resolution →low latency
	2. low power consumption : low-redundancy data transmission and processing. → embedded 환경에 좋을 듯.
	3. 낮 밤에 상관없이 사용가능.

### Event Cam SLAM의 어려운 점.
1. time-continuous, sparse, asynchronous, irregular data → eventcam slam 맞춤 알고리즘을 제작해야함.
2. event는 매우 한정적인 정보만 가지고 있다. sparse하고 내제된 noise가 있어서 feature correspondence 찾기가 매우 어렵다.
3. 또한 이에 따라 camera geometry를 알아내기 쉽지 않다.

### EventCam SLAM 종류
1. Feature-based
2. Direct 
	1. image plane에서 event data를 축적시킴. (*event map*)
	2. 
3. Motion-compensation
	1. spatio-temporal relationship을 바탕으로 reference frame에 motion model을 구함.
4. Deep Learning

### Event Representation
#### Individual Event 
축적하지 않고 그냥 들어오면 바로 쓰는 거 → filter 방식이랑 같이 쓰임.
#### Event Packet
#### Event Frame
같은 pixel의 event를 축적해서 만든 2D의 표현방식.
event stream을 image로 변환 →  Conventional SLAM 방식 사용.
*pixel 위치가 고정이라는 가정이 있음*

#### Time Surface



### Experiments
- 어떤 데이터
- 어떤 정보를 분석했는지 (ate, rpe, NEES)


### ❓️Questions

### Future Articles to Read

