# 🐕‍🦺 +🪑


### 24. Jun
1. ~~config파일을 통해서 unitree urdf를 코드에 넘겨주기~~~ 
2. ProcessJoint 함수 안의 utility:: ~position, orientation 바꾸기.
	1. ProcessMeasurements 안에서 pinocchio 코드 대략 적고, proessJoint 함수를 하나 더 만들엇음.
	2. getJointId 함수를 통해서 기존처럼 넣어줬는데 go1 gazebo로 해보고 안 되면 바꾸기.
3. foot_integration_base에서 jacobian하고 covariance를 계산하는데 이걸 pinocchio결과로 바꿔보기. (midPointIntegration에서 되니까 push_back할 때 같이 넘겨주면 될 듯.)

### 25. Jun
Jacobian 구하는 법. [github_issue](https://github.com/stack-of-tasks/pinocchio/issues/1455)
1. computeJointJacobians
2. end-effector frame을 정의하고, end-effector frame이 joint (예 : 로봇 손목)과 일치한다면, 
		getJointJacobian 
		그렇지 않다면 getFrameJacobian


##### Frame vs Joints
Frame은 자기 parent joint 기준으로 고정되어 있음.


### 26. Jun
그리고 get함수로 값을 가져올 때  reference를 pinocchio::ReferenceFrame::LOCAL_WORLD_ALIGNED로 해서 world frame으로 받아오는데, 이 때 사실 우리 로봇은 floating base니까 world를 그냥 body로 이해하면 될 것같다.
→ 맨 처음에 model을 initialization할 때의 좌표계를 의미하는 것 같다.

1. residual에서 계속 nan이 떠서 그거 오류를 해결하고 있다.😭
		우선 Velocity가 산출이 안 돼서 q_joint처럼 v_joint를 만들어서 값을 넣어주고, forwardKinematics 함수에 인자로 넣어주니까 얻을 수 있었다!

		근데 어차피 Foot은 autoDiff여서 그냥 잘 돼야할텐데 ㅠㅠ 
### 27. Jun
- 일단 Model을 if(PINOCCHIO)에서 빠져나오기만 해도 발산한다. 실제 config로 0, 1을 어떻게 주던간에
- 근데 예제 코드에서는 joint  

### 28. Jun
- 문제는 processJoint 전에 반복문에서 getJointId함수였다. 
- 그리고 q_joint, v_joint 변수 print하는 것을 joint마다 돌게하니까 또 같은 문제가 발생했다.
- q_joint, v_joint에 값을 넣는 과정에서 좀 걸리는 거 같기도 한데.
뭔가 getJointId하는 데에서 시간이 많이 걸리는 걸까?


결론적으로 그냥 순서 맞춰서 joint 값을 정렬해주지 않아도 그냥 잘 됐다.
