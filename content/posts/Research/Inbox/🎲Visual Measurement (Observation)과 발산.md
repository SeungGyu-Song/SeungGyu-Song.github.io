---
title: 
date: 
tags:
  - VIO
---
### Topic : Observation 개수에 따른 발산 가능성


### Memo
> 사족보행 pump track하고 은골산 데이터를 돌려보았는데 visual measurement가 보통 1000개 넘어가면 뾰족뾰족한 움직임은 나오지 않은 반면, 700개나 500개 아래로 내려가면 굉장히 거의 백이면 백 발산하는 것을 볼 수 있었다.
> 	visual measurement (observation)이 100개 아래로 내려갈 때도 있다.

> 근데 모션이 조금 과격한 상황에서도 tracking이 잘 됐다면 발산하는 일은 자주 일어나지 않은 것 같았다.

> 하지만 tracking이 1000개 이상일 때 은골산에서 갑자기 yaw로 회전을 막 시켰을 때는 발산하는 게 있었던 것 같다.

- VINS code에서는 estimator.cpp에서 f_m_cnt로 확인할 수 있다.

일단 BASALT Observation 개수가 기본적으로 많고 근데 어떤 때는 VINS보다 적어질 때도 있지만 이럴 때마다 발산한 것 같지는 않았다.



#### bag 파일 분석
- 햇빛이 갑자기 일정 부분 환하게 들어오는 게 tracking이 많이 되던 부분인지 아니면 다른 곳인지에 따라서 observation 개수가 차이나는  거 같다.
- 그치만 은골산 데이터 돌릴 때는 
- 움직임이 격하진 않아도 observation이 현저히 떨어지는 경우가 왕왕 발생한다.

### ❓️Further More
- Observation의 quality도 quality지만 양을 결정하는 것은 정확히 어떤 문제일까?
	- image track에서 feature가 움직이는 화살표의 모양이 다르면 영향이 있나?
- Observation은 많은데 과격한 움직임으로 발산한 경우도 있을까?

- VINS에서는 observation 개수가 떨어져서 발산하는 상황에서 BASALT는 그렇지 않은 경우가 은골산 후반에 좀 있다. 이건 왜 그런 걸까?? Feature를 뽑는 데서 달라서 그런 건가? 

### Reference
- 

### Link
- 
