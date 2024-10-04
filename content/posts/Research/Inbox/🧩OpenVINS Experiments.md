OpenVINS를 돌릴 때, imu noise 값들을 작게 주면 쉽게 발산하는 것을 관찰하였따. 
(EuRoC dataset에 맞추어진 값으로 넣었을 때)

| initialization | Window time | init max feature | dyn_num_pose |
| -------------- | ----------- | ---------------- | ------------ |
| static         |             |                  |              |
| Dynamic        | 5.0         | 50               | 10           |
