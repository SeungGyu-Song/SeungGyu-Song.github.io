OpenVINS를 돌릴 때, imu noise 값들을 작게 주면 쉽게 발산하는 것을 관찰하였따. 
(EuRoC dataset에 맞추어진 값으로 넣었을 때)

bag file : 1115_north go1 

| 항목   | 기존 imu noises | EuRoC imu noises |
| ---- | ------------- | ---------------- |
| n_a  | 0.2           | 0.002<br>        |
| n_ba | 0.02          | 0.003<br>        |
| n_g  | 0.002         | 1.6968e-4        |
| n_bg | 0.0002        | 1.9393e-5        |
|      |               |                  |

| initialization | Window time | init max feature | dyn_num_pose | imu_thresh | 결과                            |     |
| -------------- | ----------- | ---------------- | ------------ | ---------- | ----------------------------- | --- |
| Static         |             |                  |              |            |                               |     |
| Dynamic        | 5.0         | 50               | 10           | 1.5        | 발산                            |     |
| Dynamic        | 10.0        | 50               | 10           | 1.5        | 발산 / eigenvalue not full rank |     |
| Dynamic        | 5.0         | 150              | 10           | 1.5        | 발산<br>                        |     |
| Dynamic        | 2.0         | 150              | 10           | 1.5        | 발산<br>                        |     |
| Dynamic        | 5.0         | 150              | 10           | 0          | **수렴 but 오차가 큼**              |     |
| Dynamic        | 2.0         | 150              | 10           | 0          | 발산  / 오차 큰 수렴                 |     |
| Dynamic(기존)\   | 2.0         | 150              | 10           | 0          | 수렴, 오차도 좀 있음. / 제일따봉          |     |
| Dynamic(기존)    | 2.0         | 50               | 10           | 0          | 우주 발산                         |     |
| Dynamic(기존)    | 5.0         | 150              | 10           | 0          | 수렴, 제일 괜찮음.                   |     |
|                |             |                  |              |            |                               |     |
## 은골산 데이터셋 비교
뭔가 1115 north dataset보다 그래도 잘 되는 이유는 landmark feature 수가 좀 잘 나와서 그런 것도 있는 것 같다.
그리고 IMU가 막 커질때, 즉 움직임이 과격해질 때는 확실히 조금 튀는 경향이 있다.

| RPE_RMSE     | OpenVINS | VINS-Fusion | BASALT       |     |
| ------------ | -------- | ----------- | ------------ | --- |
| GT : FASTLIO | 0.056751 | 0.059772    | **0.017033** |     |

### 결과 사진

![[VINS_trio_topview.png]]

![[VINS_trio_xyz_view.png]]

## KAIST-VIO 데이터셋
### Circle
| RPE_RMSE   | OpenVINS |     | BASALT       |     |
| ---------- | -------- | --- | ------------ | --- |
| GT : Mocap | 0.012796 |     | **0.006040** |     |
#### 결과 사진
![[basalt_openvins_topview.png]]![[basalt_openvins_xyz_view.png]]