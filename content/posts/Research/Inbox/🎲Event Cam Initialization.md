---
title: <Fill me w/ a compact title>
draft: true
tags:
---
 
Event Cam은 로봇과 주변 환경이 정적일 때 event가 들어오지 않아 문제가 생긴다. 

보통 Initializtion은 로봇도 가만히 있거나 조금 움직이기 때문에 충분한 양의 event가 들어오지 않을 수도 있다. [[🎲EventCam 분석]] [[🧩VINS-Fusion Map.canvas|🧩VINS-Fusion Map]]

[[🧩VINS-Fusion Map.canvas|🧩VINS-Fusion Map]]은 드론을 날릴 때 좀 천천히 날리면서 initialization 잡고 시작하나?


- [ ] [[📦️PL-EVIO; Robust Monocular Event-Based VisualInertial Odometry With Point and Line Features|PL-EVIO]]는 initialization 어떻게 했는지 찾아보기.


그래서 [[🧩OpenVins.canvas|🧩OpenVins]]의 [[🧩OpenVINS Code Analysis#StaticInitializer|StaticInitializer]]를 넣어야할 거같다. 

추가적으로 [[🎲Initialization + GLOMAP]] 이 거랑 같이 생각해서 해보자. 
