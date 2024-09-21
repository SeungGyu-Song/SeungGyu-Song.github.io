---
aliases:
  - STEP
date: 2024-05-20
title: STEP Review
author: 
tags:
  - Review
  - VIO
  - Legged
---

zotero : 
source : [[@Kim_STEP_2022]]

---
### Critique
- 전반적으로 논문의 흐름은 foot velocity factor에 관해 계산이 어떻게 이루어졌는지를 주로 이루고 있어서 개념적으로만 얻어가면 될 것 같다.
-

- <mark class="hltr-red">발의 Rotation 값이 필요한가? 발에 대해서 rpy가 있는 게 아닌데 Position만 있어야 하는 게 아닌가싶다. (End effector를 활용해서)</mark>
- <mark class="hltr-red">Foot Factor를 최적화 할 때 Body Pose가 state에 안 들어가는데 foot pose만 최적화해서 odometry 성능이 올라가는 이유를 찾아보자.</mark> [[#Factor Graph]]
- [[@Kim_STEP_2022#^344201|STEP 불안정한 가정 1]] : foot angular velocity를 등속도로 두고 풀었는데 실제로는 등속도로 움직이지 않을 가능성이 큼
- [[@Kim_STEP_2022#^3f6575|STEP 불안정한 가정2]] : optical flow로부터 body velocity를 얻고, image frame 간 body vel도 등속도라는 가정하에 풀었기 때문에 가정이 틀릴 수 있음.
- 
 
### Introduction
- 많은 멍멍이 Odometry 알고리즘들은 contact 조건에서의 non-slip이라는 강력한 constraint를 이용해 발전해오곤 했다. 하지만 이는 미끄러운 곳에서 가정이 깨지기 때문에 보완책이 필요하다.
	- slip effect를 Gaussian noise로 놓을 경우 심하게 slip이 일어난 경우 valid하지 않게 된다.
	- > 아무래도 큰 noise는 분포의 꼬리여서 확률값이 낮아져서 그런가?
### Methodology

#### State
![[Zotero/images/@Kim_STEP_2022/image-3-x87-y72.png|300]]
state에 foot rotation($\Psi$)와 position($s$)이 있는 것을 확인할 수 있다.
#### Factor Graph
여기 Factor Graph에서도 foot velocity factor는 pose 사이에 연결이 돼있으니까 Pose를 활용해야하는 것 같다.
![[Zotero/images/@Kim_STEP_2022/image-4-x51-y619.png|300]]

#### Foot Velocity Factor Residual
Residual은 Position에 대한 Residual만을 계산한다.

 ![[Zotero/images/@Kim_STEP_2022/image-6-x51-y496.png|450]]


 ![[Zotero/images/@Kim_STEP_2022/image-6-x55-y335.png|450]]
이렇게 World Frame의 Foot Rotation인 $\Psi$를 이용해 풀게 되는데, 이는 
 ![[Zotero/images/@Kim_STEP_2022/image-5-x92-y441.png|300]]
 식에서 양 변에 $\Psi^T$를 해주기 때문이다. 
 - ❓️ 근데 왜 $\dot s$를 해주어야 했을까?


---
### 0724 보충
foot factor noise propagation이 preintegration에서 쓰인 방식하고 좀 차이가 있다. (손으로 직접 구해봄)
![[Pasted image 20240724194926.png]]
현재는 이렇게 되어있는데 여기서 A의 (0,0)에 있는 Identity Matrix를 $\tilde \Psi^T_{j,j+1}$ 로 바꿔주는 게 맞는 것 같다. 
- [ ] STEP에 구현해놓기. #점검

### Experiments
- Gazebo와 실제 데이터를 이용해 Pronto와 [[📦️VINS-Fusion Review]], WALK-VIO을 활용했다.


### ❓️Questions

### Future Articles to Read
Cerberus : 같은 VINS-Fusion 기반의 코드인데 발을 어떻게 활용했는지 살펴보기.


