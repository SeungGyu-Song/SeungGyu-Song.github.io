---
title: VINS-Fusion Code Analysis - Optimization, Marginalization
date: 2024-05-16
tags:
  - VINS-Fusion
  - Optimization
  - Marginalization
  - VIO
---

### Marginalization
optimization과 다르게
각 factor들을 만들고 
→ ResidualBlockInfo 클래스의 instance 구성요소로 넣어줌(drop_set 체크하기).
→ MarginalizationInfo 클래스 객체에 [[🧩 VINS-Fusion Code Analysis - Optimization, Marginalization factor#addResidualBlockInfo|addResidualBlockInfo]]로 넣어줌.

한편 여기서 MarginalizationFactor





### Class ResidualBlockInfo


### Class MarginalizationInfo

##### 변수 정리
unordered_map : 
> parameter_block_**idx** : dropset → marginalize함수 이후 parameter block size에 있는 값도 가지고 있음.
> parameter_block_**size** : parameter block (해당 state)
> parameter_block_**data** : parameter block 값을 동적 복사해서 가지고 있는 거
> m : marginalization에 해당하는 size 개수
> n : remaining size개수 (n = pos - m)
> linearized_jacobian : remain Hessian 행렬을 분해하고 처리한 jacobian
> linearized_residual : remain Hessian 행렬을 분해하고 처리한 residual

##### addResidualBlockInfo
factors에 해당 residual block info를 추가하고 
parameter_block_size에 parameter block 요소들의 주소와 size를 추가해줌.

parameter_block_idx에 drop set 요소들의 주소와 0값을 추가해줌.

그래서 parameter block size 안의 요소와 parameter block idx의 요소는 같을 수 있음.

##### preMarginalize

**각 factor마다**
>  **Evaluate()**
>>	각 factor마다 residual과 parameter 개수에 맞춰서 다시 jacobian을 맞추고 factor의Evaluate함수를 호출 : 직접 residual과 jacobian을 구하겠다는 의미.
> 
> 이어서
> parameter_block_data에 factor의 parameter block **값**을 동적으로 복사해서 넣음.




##### marginalize
parameter block idx에 넣을 건데 모든 parameter의 주소와 second로는 사이즈마다 칸막이를 놓듯이 localSize 값이 들어감.

> 먼저 dropset의 애들이 들어가고 → m
> dropset에 포함 안 된 parameter 값들이 들어감 → n


thread를 나눠서 multi-threading으로 [[#ThreadsConstructA]] 함수를 통해 Hessian Matrix와 b를 구함. ($H \Delta x = b$에서 $H = J^T\Omega J, b = J^T\Omega e$ , $e$는 residual )
다만 행렬 안의 순서는 marginalization 후보 , remaining 후보로 되어있음.

remaining 후보 
- MarginOld일 때
- > Pose[1], SpeedBias[1], Pose[imu_j], para_Ex_Pose, Td, 그리고 last marginalization parameter blocks에서 Pose[0] 제외한 나머지

- Margin Second New일 때
- > last marginalization parameter blocks에서 Pose[WINDOW_SIZE -1 ] 뺴고 나머지

다음으로 remain 부분행렬에 대한 Schur Complement 후 Eigen vector decomposition을 이용해서 linearized_jacobian과 linearized_residual을 구함. → marginalization factor Evalute에서 쓰임.


###### Eigen vector Decomposition 코드
``` 
Eigen::MatrixXd Amm = 0.5 * (A.block(0, 0, m, m) + A.block(0, 0, m, m).transpose()); // 왜 대각행렬 말고 나머지를 다 대칭으로 만들어주지? 이미 대칭 아닌가?

Eigen::SelfAdjointEigenSolver<Eigen::MatrixXd> saes(Amm); // Eigen Value Decomposition

Eigen::MatrixXd Amm_inv = saes.eigenvectors() * Eigen::VectorXd((saes.eigenvalues().array() > eps).select(saes.eigenvalues().array().inverse(), 0)).asDiagonal() * saes.eigenvectors().transpose(); // pseudo-inverse of Amm

Eigen::VectorXd bmm = b.segment(0, m);

Eigen::MatrixXd Amr = A.block(0, m, m, n);

Eigen::MatrixXd Arm = A.block(m, 0, n, m);

Eigen::MatrixXd Arr = A.block(m, m, n, n);

Eigen::VectorXd brr = b.segment(m, n);

A = Arr - Arm * Amm_inv * Amr;

b = brr - Arm * Amm_inv * bmm;

  

Eigen::SelfAdjointEigenSolver<Eigen::MatrixXd> saes2(A); // 이걸로 eigen value를 구함

Eigen::VectorXd S = Eigen::VectorXd((saes2.eigenvalues().array() > eps).select(saes2.eigenvalues().array(), 0));

Eigen::VectorXd S_inv = Eigen::VectorXd((saes2.eigenvalues().array() > eps).select(saes2.eigenvalues().array().inverse(), 0));

  

Eigen::VectorXd S_sqrt = S.cwiseSqrt(); // element-wise sqrt

Eigen::VectorXd S_inv_sqrt = S_inv.cwiseSqrt();

  

linearized_jacobians = S_sqrt.asDiagonal() * saes2.eigenvectors().transpose();

linearized_residuals = S_inv_sqrt.asDiagonal() * saes2.eigenvectors().transpose() * b;
```







##### getParameterBlocks
marginalization info 오브젝트에 marginalization 이후 남아있는 parameter_block size, idx, data, addr를 keep_block size, idx, data, addr 에 업데이트 해주고

keep_block_addr를 return

→ 이래서 remain 애들 중에 다른 일반 residual이랑 공통으로 들어가있는 애가 있는데 그 둘의 미분값이 달라져서 consistency에 문제가 생기는 건가? 음.. 아닐텐데 그렇게 따지면 IMU, Visual 둘 다 Pose가 겹치는 게 있을텐데? 근데 결국 남아있는 애들이 **Prior**로 작동하는 건 맞음.

#### Evaluate


### Struct ThreadsStruct
#### ThreadsConstructA
(이건 어디에도 속해있지 않은 함수지만 그냥 여기에 넣음.)

여기서는 Hessian matrix와 b를 여러 Thread로 나눠서 구하게됨. 

<mark class="hltr-pink">근데 구하는 과정과 머리로 그려지는 게 아직 잘 안 됨.
</mark>
