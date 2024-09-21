
# 9.1
- independent increment $\subset$ Markov
### Sum process
$C_S(n,k) = \min(n,k)\sigma^2$  : 더 작은 게 뽑힘.
#### Random Walk
$$D_n = 2* I_n - 1$$
이걸 기억하면 나머지 유도가 쉬워짐.
mean : 2 * np  - n, VAR[Sn] = 4 * np(1-p)

### Discrete → Continuous
- Poisson Process
- Gaussian random process (wiener process)
- **iid** 특성이 있는 거를 빼먹지 말자.
#### Poisson process
- 일정 시간 동안 손님이 찾아온 횟수 등을 알기 위해 도입한 방법.
- 그리고 일정 시간 T동안 손님이 왔으면 방문 확률은 uniformly하게 $\frac{1}{T}$가 됨.
Binomial의 continuous 버전이니까 그대로 independent, stationary increments 특징을 그대로 가지고 있음.

$\frac{{(\lambda t)}^k}{k!} e^{-\lambda t}$  라서 10초 동안 4번이면 k=4, t = 10을 넣어주어야함.


#### Gaussian Random process
samples $X_1 = X(t_1), X_2 = X(t_2), ... , X_k = X(t_k)$ 들이 jointly Gaussian random variable일 때. 

###### 예제 9.28 
1. P(x(3) < 6) 인 확률을 구할 땐 t=3일 때만 고려하는 거고
2. P(x(1)+x(2) >15) 일 때는 1,2에 대해서 고려해주어야함. 즉 Covariance를 해서 크기를 구해줘야해. 

# 9.3 Stationary processes
### Stationary process
어떤 시간에 그 process를 관측하더라도 그 process의 성질이 변하지 않음.
얘는 mean, variance, cov 같은 통계량 뿐만 아니라 cdf도 time-invariant 성질을 가져야하나봄.

first order cdf가 시간에 관계없이 일정하면
$F_X(t)(x) = F_{X(t+\tau)}(x) = F_X(x) \forall{t, \tau}$
$m_X(t) = E[X(t)] = m, \quad VAR[X(t)] = E[X(t) - m)^2] = \sigma^2, \forall t$

second-order cdf에 대해 오직 시간 차에만 random process가 의존하면
$F_{X(t_1),X(t_2)}(x_1,x_2) = F_{X(0),X(t_2-t_1)}(x_1,x_2), \forall t_1, t_2$

auto-correlation과 autocovariance도 오직 시간 차에만 관련있음.
$R_X(t_1,t_2) = R_X(t_2-t_1), \quad C_X(t_1, t_2) = C_X(t_2 - t_1), \forall t_1, t_2$

###### Sum process는 stationary process가 아니다.
$E[S_n] = n * m$
$VAR[S_n] = n * \sigma^2$
다 시간에 관한 (n에 관한)함수여서 $m, \sigma^2$가 모두 0일 때만 stationary process.

##### Wide-sense stationary process
위에서 그냥 cdf가 같은 거 빼고 나머지 mean, var, auto-correlation, auto-covariance 이 4개가 만족하면 WSS라고 하는 듯.
- [ ] <mark class="hltr-red">예제 9.34 풀어볼만 한 듯</mark>

###### 특징 2. autocorrelation function은 우함수임.
###### 특징 3. autocorrelation function은 $\tau=0$일 때 maximum을 가짐.
###### 특징 6. $X(t) = m + N(t)$ , N(t)가 zero-mean에 $R_N(\tau) \rightarrow 0 \; as\; \tau \rightarrow \infty$ 일 때 $R_X(\tau)$는 mean의 제곱으로 수렴한다. 

##### Gaussian random process가 WSS → stationary로 진급.

*random process가 WSS인지를 보일 때는 mean이 상수고 autocorrelation 함수가 시간 차이에만 변하는 것을 확인해주기*

##### Cyclostationary random processes
만약 모든 sample path가 periodic일 경우.

cyclostationary를 stationary random process로 바꾸는 거 내일 보기(6.11)

# 9-4 Random Process의 연속,미-적분
<mark class="hltr-red">*Auto Correlation 연속, 미분, 적분 존재 → Random Process의 연속, 미분, 적분 존재*</mark>

**목적** 
	Random process를 input으로 넣고 system의 output을 관찰할 때, input-output 관계가 
	미분, 적분 관계를 포함하고 있기 때문에 이러한 작업을 거쳐줘야함.

### Continuity of random processes
##### Mean Square continuity
$$E[(X(t) - X(t_0))^2] \rightarrow 0 \quad as \quad t  \rightarrow t_0$$
이를 다음과 같이 $l.i.m._{t → t_0} X(t) = X(t_0)$ 쓸 수 있따.

추가적으로
- Auto Correlation $R_X(t_1,t_2)$가 ($t_0, t_0$)에서 연속이면 $X(t)$도 점 $t_0$에서 mean square continuous이다.
- wide-sense stationary라면, $R_X(\tau)$가 $\tau=0$에서 연속이면, 모든 포인트 $t_0$에서 mean square continuous하다.
- $X(t)$가 $t_0$에서 mean square continuous라면, mean function인 $m_X(t)$역시 $t_0$에서 연속이다.



### Derivative of random processes

##### Mean square derivative
$$ X'(t) = l.i.m._{\epsilon\rightarrow0} \frac{X(t+\epsilon) - X(t)}{\epsilon}$$

- $\frac{\partial^2}{\partial t_1 \partial t_2}$ $R_X(t_1,t_2)$ 가 존재하면 $X(t)$ 미분 존재한다.
- WSS random process에 대해서 $R_X(\tau)$가 $\tau = 0$에서의 미분이 있으면 모든 t에 대해서 mean square derivative가 존재한다.
- $X(t)$가 Gaussian random process면, $X’(t)$ 는 반드시 Gaussian random process다.
- $E[X’(t)]=\frac{d}{dt}m_x(t)$
- $R_{X’}(t_1,t_2) = \frac{\partial}{\partial t_2}R_X(t_1,t_2)$ 
- $R_{X,X’}(t_1,t_2) = \frac{\partial^2}{\partial t_1 \partial t_2}R_X(t_1,t_2)$  (if WSS, $R_{X,X’}(\tau) = -\frac{d}{d\tau}R_X(\tau)$) 


### Integrals of random processes
이것도 미분하는 것과 마찬가지.


### Ergodic theorem
공식 암기해서 쓰고, upper bound로 0으로 가는지 체크하기.

$$VAR[< X(t) >_\gamma] = \lim_{T\rightarrow\infty}\frac{1}{2T}\int_{-2T}^{2T}(1-\frac{|u|}{2T})C_X(u)du = 0$$
여기서 $C_X(u)$는 auto correlation function.

discrete-time이면 분모의 T를 T+1로 바꿔주기.

time average ≠ ensemble average니까 어떻게 하면 둘을 같게 만들 수 있는지에 대한 정리임.
- 시간 축으로도 충분히 randomness가 있어야하고
- auto correlation이 시간에 따라(u축을 따라) decay하는 형태로 가야함.
- 얼마나 빨리 decay해야하는지를 이 theorem이 이야기해주는 거임.
	- correlation이 시간이 흘러감에 따라 약해져가야함.