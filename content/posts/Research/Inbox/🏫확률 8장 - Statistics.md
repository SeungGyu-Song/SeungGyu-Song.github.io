# 8-1
### Basic Terminology
- Parameter $\theta$ : Property of $X$  ( mean, variance, ..)
- Random Sample **$X_n$** : **iid** variables ( weights of babies born last January)
- Statistic $\hat\Theta(X_n)$ : Estimation of $\theta$ based on random samples, $X_n$
	- random vector $X_n$의 함수니까 $\hat\Theta(X_n)$얘도 Random Variable임.

### Parameter Estimation
Parameter estimation 
	Estimating a parameter $\theta$ of random variable $X$ in random sample $X_n$ 

#### Properties of a good estimator
1. a good estimator should be equal to the true parameter $\theta$, on the average.
	1. The estimator $\hat\Theta$ is an *unbiased estimator* for $\theta$  if $E[\hat\Theta] = \theta$
	2. estimator Bias : $B[\hat\Theta] = E[\hat\Theta] - \theta$ . 
		1. Bias는 constant이며 (r.v 아님) B > 0 → 평균보다 크게 추정하는 경향이 있다.
		2. B < 0 → 평균보다 작게 추정하는 경향이 있다.

2. A good estimator should give values clustered close to $\theta$ 
	1. for unbiased estimators, prefer the one with the smallest estimator variance.
	2. Minimum-variance unbiased estimator (MVUE)

3. A good estimator should tend towards the correct value of $\theta$ as n is increased.
	1. The estimator $\hat\Theta$ is a consistent estimator if $\hat\Theta$ converges to $\theta$ in probability
			$\lim\limits_{n \to \infty} P[|\hat\Theta - \theta|] = 0$   

#### Maximum likelihood estimation
- n→$\infty$ , MVUE
- Consistent estimator
- invariant estimator
	- 만약 $\theta^*$가 $\theta$에 대한 ML estimate이면, $h(\theta^*)$ 도 $h(\theta)$에 대한 ML estimate  
	- random sample의 경우 어떻게 풀어야하는지 살펴보기(iid니까 다 곱해줌)![[Screenshot from 2024-06-08 18-08-34.png]]
	- 여기서 ML estimator로 구한 분산이 biased라서 $\frac{n}{n-1}$ 곱해주면 되는데 어차피 무한대로 가면 둘이 같아짐 → MVUE  

---
## 8-2
1. Significance Test
		$H_0$이 true인지 false인지 판별, false일 때 H의 distribution을 알 수 없음.
2.  Hypothesis Test
		$H_0$이 false면 $H_1$ 채택. (distribution을 알 수 있다.)
3. Bayesian hypothesis test
		가설 자체가 확률에 기반인 거. : 동전의 앞면이 나올 확률이 ½과 ⅔일 확률은 각각 p, 1-p다.


### Significance Test
Accept or reject the null hypothesis $H_0$ based on a random sample $\mathbf{X_n}(=X_1, X_2, … , X_n)$ 

<mark class="hltr-green">Accept</mark> $H_0$ if $\mathbf{X_n} \in \tilde R^c$ , <mark class="hltr-red">Reject</mark> $H_0$ if $\mathbf{X_n} \in \tilde R$ .

Type I error : Reject $H_0$ when $H_0$ is true
Type II error : Accept $H_0$ when $H_0$ is false.

Significance level $\alpha$ := $P$(Type I error)  = $\int_{\mathbf{X}_n \in \tilde R} f_x(\mathbf{x}_n | H_0) d\mathbf{x}_n$   :  적분되는 X 구간을 잘 보자.

The reject region is chosen so that significance level is $\alpha$.


### Neyman-Pearson Hypothesis Test
![[Screenshot from 2024-06-12 15-07-43.png]]

$\Lambda (x)$  : likelihood ratio function.
Neyman-Pearson test **rejects** the null hypothesis whenever the likelihood ratio is equal or exceeds the threshold $\kappa$ .
![[Screenshot from 2024-06-12 15-11-53.png]]

*maximum likelihood test* : $\kappa = 1$ 