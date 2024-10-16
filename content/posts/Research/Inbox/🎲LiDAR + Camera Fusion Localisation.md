---
title: 
date: 
tags:
---

### Topic : LiDAR 맵에 VIO localization 하기.
- LiDAR 10hz / Camera 30 hz → camera가 더 많이 들어오고 dense 하니까 LiDAR를 range image로 활용한다고함.
- 그럼 LiDAR 한 번에 camera 3장이니까 msckf 느낌으로 낭낭하게 fusion하면 되지 않을까?
- 그리고 LiDAR pointcloud도 있으니까 굳이 VIO에 feature를 state로 넣지 않고, 만약 매칭이 안 된 애들만 넣으면 kalman filter  돌리는 때에도 별로 무리가 없을 거 같은데.



### Memo
> [ ] FAST-LIVO, R3Live 아이디어를 알아보기.

### Reference
- 

### Link
- 
