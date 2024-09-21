---
title: mip-nerf를 활용할 수 있을까?
date: 2024-05-14
tags:
  - VIO
  - Uncertainty
  - Undistortion
  - Triangulation
---
source : 승재님과의 대화
### Topic :
mip-nerf를 활용할 수 있을까?


### Memo
mip-nerf의 주장 중 한 가지는 하나의 픽셀이 점이 아니라 사각형인데, 이 사각형의 ray를 따라가다보면 멀리있는 물체는 이 사각형이 더 크게 보인다는 것이다. - frustum이 커버하는 영역이 커진다.
![[mip-NeRF_frustrum.png]]

생각해보면 feature extraction도 multi-scale로 뽑기 위해서 image pyramid를 만들어서 뽑는데 결국에는 level에 상관없이 다 feature를 하나로 보고있다. 
(즉 NeRF처럼 픽셀 당 극도로 좁은 단일 광선을 사용하는 것 같다.)

만약 이 아이디어를 활용해서 feature마다의 uncertainty를 고려해서 LMSE를 푼다면 더 좋은 해를 얻을 가능성도 있을 것 같다.

- [ ] 하지만 거리가 멀어짐에 따라 uncertainty가 커진다는 것이라는 큰 의미로 보았을 때 이미 VINS-Fusion에서 inverse depth로 고려를 하고 있기에 실제로 이 inverse depth가 어떻게 작동하는지 보아야겠다.
- [ ] 그리고 Mip-NeRF에서 frustrum이 어떻게 작동이 되는지도 확인해보자.
---
근데 실제 feature 좌표를 보면 픽셀 네모 안의 점이라서 위와 같이 생각하기는 조금 힘들 것 같다. - 2024.06.08

### Reference
- [mip-NeRF 리뷰 블로그](https://kimjy99.github.io/%EB%85%BC%EB%AC%B8%EB%A6%AC%EB%B7%B0/mipnerf/)


### Link
- 
