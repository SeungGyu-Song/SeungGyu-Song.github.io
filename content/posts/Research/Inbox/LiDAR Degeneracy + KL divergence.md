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
그럼 LiDAR measurement에 Gaussian noise ($\mu = 0, \sigma$)를 전체적으로 줘서 대칭성을 깬 다음에, 이거를 원래 분포와 KL-Divergence로 맞춰줄 수는 없을까?

마치 Auto Encoder 하는 방식처럼. 
- Gaussian noise를 주고,  원래의 이미지와  inferenced 이미지를 비교해서 노이즈를 제거하는 방식

그래서 [[📦️BASALT]]에서도 언급이 됐듯이, 만약 Jacobian이 full-rank면 KL-Divergence가 closed form으로 풀린다고한다.

그러면 결과적으로 대칭성을 깨서 덜 흐르게 만들고, 다시 update 후에 local 맵을 복구할 때에는 복구하면 될 수도.

근데 이렇게 되면 local map to scan에서 local map은 깨끗한데 noise가 추가된 scan에서는 내가 이동한 방향으로의 결과가 안 나올 수도 있을 것 같은데. 


## 추후 해결해야할 문제
1. LiDAR의 분포를 어떻게 수학적으로 표현할 것인가.
2. 그럼 LiDAR measurement에 대한 Jacobian이 full-rank면 되는 건지? 정확히 어떤 게 full-rank여야하는 건지 알아야함.
3. 내 생각에는 Gaussian-noise가 mean이 0이니까 뭔가 다 합치면 update할 때 noise가 상쇄될 것으로 예상했는데, 이에 대해 확실하지 않음. 
	1. 근데 filter  방식이면 imu가 크게 관여하는 게 아니니까 lidar의 information matrix처럼 계수로 들어가는 matrix가 6 DoF에 대해서 차이가 크지 않다면 괜찮을 거 같은데. 
4.  ICP가 일어나는 원리를 알면 좋을텐데. 

~~아니면 Localizability와 같은 행위를 해서 어디로 degeneracy가 일어날 것 같다는 것을 사전에 체크 하고, 이 방향으로의 point cloud에 gaussian noise를 줘도 될 거 ㅅ같다.~~ 


## Reference
- [[📦️BASALT]]
- KL divergence
- Auto Encoder
- Diffusion

## Link
- 
