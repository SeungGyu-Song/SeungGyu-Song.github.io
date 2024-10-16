## 2024-04-29 21:39

## Topic : Invariant EKF 


---

### Memo

### 장점

> 1. Kalman gain을 구할 때 추정값에 영향을 받지 않아 EKF보다 더 강건하다. (trajectory 모양에 상관 없음)
> 2. 그래서 수렴을 보장한다. (EKF는 Linearization 과정에서 true값과 너무 차이가 커지면 보장하지 못함)
> 3. Error propagation is <mark class="hltr-purple">autonomous</mark> (?)
> 4. 

### IEKF 특징
1. state들을 Lie Group위에서 작성해야한다.  
	1. linearised error -> logarithm of invariant error : vector space에서 Gaussian 분포를 따른다.
	2. uncertainty 분포도 *concentrated Gaussian distribution* 이 되며, conventional한 방법보다 더 성능이 좋다고 한다.
2. Group Affine 특징을 통해 error propagation 단계에서  non-linear equation -> linear equation -> 최적해 찾을 수 있다.
3. SE_2(3)든 SE_n(3)든, Rotation 옆에는 body frame이 아닌 world frame에서의 값이 와야함.

## Reference
- [Federated Invariant EKF for Mutli-sensor Navigation System](https://dcollection.snu.ac.kr/public_resource/pdf/000000169106_20240429223145.pdf)
  

## Link




#IEKF
