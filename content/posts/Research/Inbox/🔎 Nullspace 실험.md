nullspace에 대해 실제로 vins-fusion 알고리즘을 가지고 실험을 진행했다.

chatgpt와의 대화에서 unobservable variable은 Jacobian의 nullspace에 있으니까 이 4개 변수의 값이 변하더라도 cost를 낮추는 데 큰 도움이 되지 않는다고 했다.

그래서 나도 그냥 [[🧩VINS-Fusion Map.canvas|🧩VINS-Fusion Map]]에서 [[🧩 VINS-Fusion Code Analysis - Optimization, Marginalization factor#imu_factor|VINS-Fusion::imu_factor]]에서 jacobian의 0,2 인덱스에 대해 다음과 같은 코드를 통해 실험을 해보았다. ([[ㅒ]])

```C++
Eigen::JacobiSVD<Eigen::Matrix<double, 15, 7, Eigen::RowMajor>> svd0(jacobian_pose_i);

Eigen::MatrixXd singularValues0 = svd0.singularValues();

double cond0 = singularValues0(0) / singularValues0(singularValues0.rows() - 1);

printf("[init-d]: CM cond = %.3f | rank = %d of %d (%4.3e thresh)\n", cond0, (int)svd0.rank(), (int)jacobian_pose_i.cols(),

svd0.threshold());
```