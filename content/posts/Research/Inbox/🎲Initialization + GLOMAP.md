---
title: <Fill me w/ a compact title>
draft: true
tags:
---
 
[[🧩VINS-Fusion Map.canvas|🧩VINS-Fusion Map]]에서 Initialization은 곰곰히 생각해보면, global SfM과 같다.

최근에 [[📦GLOMAP Review]], [[🎲GLOMAP 결과]] 이 나왔듯이, 이를 적용해보는 건 어떨까한다.

즉, position만 먼저 optimization이든 뭐든 구하고 그 다음 rotation을 구하는 방식인 거다.

## 생각하게된 이유
OpenVINS는 initialization이 강건하거나 그러진 않는 거 같다. [[🔎OpenVINS Experiments]]
imu noise만 조금 적게줘도 바로 날아가니까. 

그래서 [[🧩VINS-Fusion Code Analysis]]이 잘 되는 이유는 Initialization을 잘 해서 그런 건 아닐까 싶다. 

## 점검해볼 것.
1. 우리는 IMU가 있으니까 굳이 이렇게 나눌 필요가 없는지?
	1. 그래도 B-Spline 그리는 거 보면 position / rotation 따로 구하는 게 더 성능면으로 좋다고 했었으니까.
2. 