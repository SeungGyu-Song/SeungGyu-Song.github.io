OpenVINS를 돌릴 때, imu noise 값들을 작게 주면 쉽게 발산하는 것을 관찰하였따. 
(EuRoC dataset에 맞추어진 값으로 넣었을 때)

| 항목   | 기존 imu noises | EuRoC imu noises |
| ---- | ------------- | ---------------- |
| n_a  | 0.2           | 0.002<br>        |
| n_ba | 0.02          | 0.003<br>        |
| n_g  | 0.002         | 1.6968e-4        |
| n_bg | 0.0002        | 1.9393e-5        |
|      |               |                  |

| initialization | Window time | init max feature | dyn_num_pose | imu_thresh | 결과                            |
| -------------- | ----------- | ---------------- | ------------ | ---------- | ----------------------------- |
| Static         |             |                  |              |            |                               |
| Dynamic        | 5.0         | 50               | 10           | 1.5        | 발산                            |
| Dynamic        | 10.0        | 50               | 10           | 1.5        | 발산 / eigenvalue not full rank |
| Dynamic        | 5.0         | 150              | 10           | 1.5        | 발산<br>                        |
| Dynamic        | 2.0         | 150              | 10           | 1.5        | 발산<br>                        |
| Dynamic        | 5.0         | 150              | 10           | 0          | **수렴 but 오차가 큼**              |
| Dynamic        | 2.0         | 150              | 10           | 0          | 발산                            |
