---
title: 
date: 
tags: 
draft: true
---

## 문제점
X-ICP처럼 LiDAR Degeneracy한 환경에서 LIO가 흐르지 않게 하는 것을 목표로 한다.

예시 : 긴 복도, 좁은 계단.

LiDAR Data들이 대칭적으로 나오면 robot이 움직였을 때, local map의 변화가 거의 없다고 생각해서 unobservability가 생긴다. 
아마 긴 통로면 패턴이 반복되는 방향의 평행한 방향으로 unobservability가 생길 것 같은데 → 이건 계단의 경우 패턴이 반복되는 것과 내가 움직이는 게 평행하지 않아서 아닌 것 같다.

## 해결방안
그럼 LiDAR measurement에 Gaussian noise를 전체적으로 줘서 대칭성을 깬 다음에, 이거를 원래 분포와 KL-Divergence로 맞춰줄 수는 없을까?

마치 Auto Encoder 하는 방식처럼. 
- Gaussian noise를 주고,  원래의 이미지와  inferenced 이미지를 비교해서 노이즈를 제거하는 방식

그래서 [[📦️BASALT]]에서도 언급이 됐듯이, 만약 Jacobian이 full-rank면 KL-Divergence가 closed form으로 풀린다고한다.

그러면 결과적으로 대칭성을 깨서 덜 흐르게 만들고, 다시 update 후에 local 맵을 복구할 때에는 

여기서의 문제는 그럼 원래 LiDAR의 분포를 어떻게 알 것인가가 중요함. 

## Reference
- [[📦️BASALT]]
- KL divergence
- Auto Encoder
- Diffusion

## Link
- 
