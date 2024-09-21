근데 ctrl-vio하고 별로 다르지 않은 거 같은데 real-time이 어떻게 된다는 거지?❓️
# OdometryManager
### SetInitialState
trajectory를 imu-only initialization에서 나온 값으로 초기값 설정.

### PrepareTwoSegMsgs
우선 data를 trajectory_start_time을 빼줘서 trajectory 기준으로 맞춰주고.

#### ToRelativeMeasureTime
- LiDAR : 각 point들을 Trajectory의 생성 시간으로 맞춰주고, point의 max_timestamp를 구함.

- Image :  trajectory_start_time 빼주기.

### UpdateTwoSeg
- 한 윈도우에 들어온 imu data의 acc, gyro의 평균과 분산을 구함.
- acc, gyro의 평균 값을 이용해 몇 개의 cp를 놓을지 결정함.(max (acc, gyro))
	- GetKnotDensity
-  ![[Zotero/images/@Lang_CocoLIC_2023/image-4-x63-y621.png|450]]

두 line segment에 대해서 각각 위의 과정 반복.

❓️~~근데 이게 두 개의 segment를 들고오면서 다루면 그 다음 것도 예측을 해야하는 건데 imu값에서 꺼내온다는 말이지. 이게 실시간이 되나? ~~~ 


### SolveLICO


# MsgManager
lidar_id는 Velodyne이냐 LiVOX냐를 의미함. 근데 그렇다면 config의 num_lidars가 의미하는 거는 라이다 개수가 아니라 라이다 **종류** 개수인가?
### GetMsgs
args : msgs, traj_last_max, traj_max, start_time




img가 있냐없냐, lidar 정보를 처리함. (아직 lidar 정보 처리는 이해하지 못했음)

#

