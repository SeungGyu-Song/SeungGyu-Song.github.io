nullspace에 대해 실제로 vins-fusion 알고리즘을 가지고 실험을 진행했다.

chatgpt와의 대화에서 unobservable variable은 Jacobian의 nullspace에 있으니까 이 4개 변수의 값이 변하더라도 cost를 낮추는 데 큰 도움이 되지 않는다고 했다.

그래서 나도 그냥 [[🧩VINS-Fusion Map.canvas|🧩VINS-Fusion Map]]에서 [[🧩 VINS-Fusion Code Analysis - Optimization, Marginalization factor#imu_factor|VINS-Fusion::imu_factor]]에서 jacobian의 0,2 인덱스에 대해 다음과 같은 코드를 통해 실험을 해보았다. ([[🧩OpenVINS Code Analysis#DynamicInitializer|OpenVINS]] 참고.)

```C++
Eigen::JacobiSVD<Eigen::Matrix<double, 15, 7, Eigen::RowMajor>> svd0(jacobian_pose_i);

Eigen::MatrixXd singularValues0 = svd0.singularValues();

double cond0 = singularValues0(0) / singularValues0(singularValues0.rows() - 1);

printf("[init-d]: CM cond = %.3f | rank = %d of %d (%4.3e thresh)\n", cond0, (int)svd0.rank(), (int)jacobian_pose_i.cols(),

svd0.threshold());
```

---
## 결과

뭔가 optimization이 돌아갈 때 window에 있는 10개의 imu factor에 대해서는 다  over-confident한 상태인데
marginalisation 할 때는 rank가 2로 줄어들어서 괜찮은 상태로 돌아오는 거 같다.

→ 이런 상태가 계속 발생했는데 그럼 발산하는 건 언제지? 
→ 그리고 그냥 점선으로만 나올 때도 추적해서 각각이 언제인지 정확히 알아야함.

## Todo
- [ ] 어떻게 visualization을 할 수 있을까?
- [ ] 그리고 그냥 점선으로만 나올 때도 추적해서 각각이 언제인지 정확히 알아야함.
- [ ] 발산하는 것과 nullspace와의 관계를 생각해보기. 
- [ ] 
