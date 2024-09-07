#### class
- Model : robot의 constant parameter를 가지고 있음 (masses, segment length, body names, etc) - algorithm에 의해 변하지 않는 값들
- Data : 근데 algorithm을 돌리다보면 data 값들을 받아서 계산해야하니까 이를 여기에 담는 거임. 
```
pinocchio::urdf::buildModel(URDF_path, model);

data = pinocchio::Data(model);
```


pinocchio::forwardKinematics(model,data,q_joint);

pinocchio::updateFramePlacements(model,data);

pinocchio::computeJointJacobians(model, data, q_joint);


❗️STEP은 근데 로봇이 넘어질라고 할 때 버퍼링이 심하게 걸렸음.