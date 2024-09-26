Mamba가 transformer architecture보다 성능이 좋다.
![[Pasted image 20240926184711.png]]

Mamba : Parallelized training + linear-time complexity

#### Contribution
a selective scan algorithm
a hardware-aware algorithm  - stroage


Mamba가 history를 압축해서 Transformer보다 메모리를 적게 먹음
![[Pasted image 20240926190143.png]]

Parallization이 가능하다. : 오직 이전 state를 가지고 있는 것만 계산하면 돼서?