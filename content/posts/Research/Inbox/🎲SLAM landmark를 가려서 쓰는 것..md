---
title: 
date: 
tags: 
draft: true
---
#Marginalization #slam #landmark

[[🧩VINS-Fusion Map.canvas|🧩VINS-Fusion Map]]에서는 state의 landmark의 quality를 따지지 않고, 그냥 n번 이상 연속으로 발견된 feature들을 넣어주었던 것 같다.

하지만 [[🧩OpenVins.canvas|🧩OpenVins]]와 [[👑BASALT.canvas|👑BASALT]]는 그와는 다른 것 같다.
- [[🧩OpenVins.canvas|🧩OpenVins]]의 경우, **현재에서도 발견되면서 marginalization 될 애들** + max_clones 보다 많이 발견된 애들을 `features_SLAM`으로 넣어서 충분히 많이 발견된 feature를 솎아냈던 것 같고
	- [[🧩VINS-Fusion Map.canvas|🧩VINS-Fusion Map]]은 marginalization에 들어가는 landmarks는 그냥 넣어주었던 것 같다.
	
- [[👑BASALT.canvas|👑BASALT]]의 경우, keyframe에서만 landmark를 등록하게 되어있다. ← 이게 정확히 어떻게 좋은지는 잘 모르겠다.



