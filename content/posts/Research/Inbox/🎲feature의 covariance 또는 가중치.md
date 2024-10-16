---
title: <Fill me w/ a compact title>
draft: true
tags:
---
 
[[🎲Mip-NeRF를 활용할 수 있을까?]]

[[🧩VINS-Fusion Map.canvas|🧩VINS-Fusion Map]]의 개선될 수 있는 점 중 몇 가지는
1. visual covariance를 상수로 둔다는 점.
2. feature residual에서 feature별로 1/depth 로만 가중치를 준다는 점.


–>
1. initialization 때 triangulation 각도로 너무 좁은 친구들 제거하기. (아마도 [[🧩OpenVins.canvas|🧩OpenVins]])
2. 아니면 전의 motion에 따라 feature들의 가중치를 고려해주기?
	1. feature의 ray 방향과 relative pose를 cos similarity해서 고려해도 될 거 같은데. feature의 covariance를 고려한다면
	2. 근데 이 방식은 pose 결과와 feature가 좀 의존적으로 돼서 system에 문제가 생기는 건가? #점검 
3. 