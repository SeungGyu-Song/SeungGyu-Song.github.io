컨셉 자체가 0.1초만에 trajectory update를 하는 거고 그 사이에 얼마나 많이 cp를 넣을지를 계산하는 거.
# Trajectory
## Se3Spline
 public :
 > template <int _N, typename _Scalar = double>
	std::vector<int64_t> knts;
	**std::vector<Eigen::Matrix4d> blending_mats;**
	**std::vector<Eigen::Matrix4d> cumu_blending_mats;**

---

*private* 
	RdSpline<3, _N, _Scalar> pos_spline; ///< Position spline
	So3Spline<_N, _Scalar> so3_spline; ///< Orientation spline
	int64_t dt_ns_; ///< Knot interval in nanoseconds
	int64_t max_time_ns;

initBlendMat함수 → blending matrix 초기화.





# TrajectoryManager
##### AddIMUData
trajectory_→setDataStartTime으로 받아온 data의 시간으로 맞춰주고
imu_data_에 해당 imudata를 추가, 그리고 이 imu_data_에 방금 들어간 데이터의 시간을 trajectory의 태어난 시간에서 빼줌. 
imu_state_estimator_ → FeedIMUData


### PredictTrajectory


#### UpdateIMUInlio
위에서 target 시간을 이전 trajectory 시간과 현재 시간인 traj_max_time_cur로 설정해줘서 
이 시간 사이에 있는 imu_data_의 맨 처음, 끝 data의 index (iterator)를 tparam에 넣기.

#### InitTrajWithPropagation
b_a, b_g, g는 lock 걸고, lock_tran = false. 