---
layout: post
title: Estimator and MLE
date: 2025-08-23 23:26 +0900
categories: [Statistics, General Backgrounds]
tags: [statistics, general, backgrounds]
description: Estimator와 Maximum Likelihood Estimator 정리
math: true
---

# Estimator 란

- estimator: **measurable function (or rule)** that maps the data to quantity of interest 

    $$T : \mathcal{X}\rightarrow\mathcal{A}\quad(\text{data } X\in\mathcal{X})$$

	- data를 입력으로  추정 대상(estimand)의 추정치(estimate)를 계산
- estimand: 추정 대상. 구하고자 하는 개념. (often parameter of a model)
	- ex. 평균
- estimate: 추정치. estimated result (실제 값)

## 예시 상황

- 목표: 대한민국 국민의 키 분포를 알고 싶음.
- 모델링: 정규분포로 모델링
- 구하고자 하는 것: population mean(모평균), population variance(모분산)
- data 확보: 100 명의 키를 조사함 (sample size=100)
- data로부터, 모평균과 모분산을 어떻게 구할 것인가? $\Rightarrow$ estimator 이용

## 문제의 전환

- "data로부터, 모평균&모분산(모분포의 parameter)을 어떻게 구할 것인가"
- 모분포의 parameter가 $\theta$ 라면, 모분포로부터 데이터 x를 얻을 확률은 

    $$ p(x;\theta)$$

로 표현 (정규분포일 때, $\theta=\{\mu,\sigma\}$) 
- 샘플 data $\mathcal{D}=\{ x^{(1)}, x^{(2)}, \cdots , x^{(N)} \}$ 을 얻은 상황에서, 데이터에 iid 가정을 하면, 샘플 $\mathcal{D}$를 얻을 확률분포는 

$$p(\mathcal{D};\theta)=p(x^{(1)};\theta)\,\cdot\,p(x^{(2)};\theta)\,\cdots \,p(x^{(N)};\theta)=\overset{N}{\underset{n=1}{\prod}} p(x^{(n)};\theta)$$

- 우리는 $\mathcal{D}$를 알고 있고, $p(\mathcal{D};\theta)$를 크게 하는 $\theta$를 찾고 싶음.
	- 그 분포에서 $\mathcal{D}$가 나왔을 확률이 가장 큰 것이기 때문.
	- 또한, 만약 실제 현상이 우리와 같은 모델(여기선 정규분포)을 따른다면 진짜 파라미터 $\theta^*$에서 Likelihood가 최대가 됨.
- 그럼 $\theta$ 위주로 식을 다시 쓰면, 

    $$L(\theta)=p(\mathcal{D};\theta)$$

 처럼 쓸 수 있고, 이를 Likelihood (가능도, 우도)라고 한다
	- 왜 likelihood인가? D를 고정된 값으로 보고, 그 데이터가 $\theta$ 에서 **얼마나 그럴듯 한지**를 나타내는 함수이기 때문. (likelihood function이라고도 부른다)

- FYI) iid (Independent and Identically Distributed)
	- 확률변수나 데이터 포인트들이 동일한 확률 분포에서 독립적으로 sampling되었다는 뜻이다.
	- 예를 들어, 주사위를 3번 던지고, 동전을 두 번 던져 나온 데이터 {3,2,5,앞,앞} 은 iid가(동일 분포에서 독립적으로 추출된 것이) 아니다.
	- 위 상황에서는, $x^{(1)} \sim x^{(N)}$까지 모두 $p(\,\cdot\,;\theta)$ 의 확률로 추출되었다는 가정을 의미한다. 실제로 그럴 진 모르지만, 합리적인 것 처럼 보이고, 계산을 쉽게 해준다.
	- 한국어로 독립항등분포라고 부른다.



## Maximum Likelihood Estimator

- 우리는 likelihood를 최대화 하는 $\theta$ 를 찾고 싶다 (우리는 앞에서 likelihood를 최대화하는 $\theta$ 가 모분포의 $\theta$ 와 같다는 것을 이끌어 내었다) 이를 식으로 쓰면: 

    $$\hat{\theta}=\arg\max_{\theta} L(\theta)=\arg\max_{\theta} P(\mathcal{D};\theta)$$

	- 이때, $\hat{\theta}$ 를 Maximum Likelihood Estimator라 한다.
	- 위 식에서 숨은 변수를 넣어보면,  
  
      $$\hat{\theta}(x_{1:n})=\arg\max_{\theta\in\Theta}L(\theta;x_{1:n})$$

- 정규분포에 대입하여 우선, 확률부터 구해보면:  

    $$p(x^{(n)} \mid \mu, \sigma^2) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp\!\left(-\frac{(x^{(n)} - \mu)^2}{2\sigma^2}\right)$$

- 이 때의 Likelihood는: 

$$ L(\mu, \sigma^2) = \prod_{n=1}^N \frac{1}{\sqrt{2\pi\sigma^2}} \exp\!\left(-\frac{(x^{(n)} - \mu)^2}{2\sigma^2}\right) $$

- 계산의 편의를 위해 log likelihood로 바꾸자. (log는 함수의 증가, 감소를 바꾸지 않으므로 likelihood를 maximize하는 $\theta$ 와 log likelihood를 maximize하는 $\theta$ 는 같다.) 그러면 log likelihood는: 

    $$\begin{aligned}
    \log L(\mu, \sigma^2) 
    &= \sum_{n=1}^N \left[ -\frac{1}{2}\log(2\pi\sigma^2) - \frac{(x^{(n)} - \mu)^2}{2\sigma^2} \right] \\
    &= -\frac{N}{2}\log(2\pi\sigma^2) - \frac{1}{2\sigma^2}\sum_{n=1}^N (x^{(n)} - \mu)^2
    \end{aligned}$$

- log likelihood의 argmax를 구하기 위해 미분해보면, 

    $$\begin{aligned}
    \frac{\partial}{\partial \mu} \log L(\mu, \sigma^2) 
    &= -\frac{1}{2\sigma^2} \cdot 2 \sum_{n=1}^N (x^{(n)} - \mu)(-1) \\
    &= \frac{1}{\sigma^2} \sum_{n=1}^N (x^{(n)} - \mu)
    \end{aligned}
    $$

- 그러면, 아래의 식이 성립하므로, 

    $$\frac{\partial}{\partial \mu} \log L(\mu, \sigma^2) = 0
    \quad \Longleftrightarrow \quad 
    \sum_{n=1}^N (x^{(n)} - \mu) = 0
    $$

- Likelihood를 maximize하는 $\mu$ 를 아래와 같이 구할 수 있다. 이것은 표본평균과 같은 값이다.

    $$ \hat{\mu}_{\text{MLE}} = \frac{1}{N} \sum_{n=1}^N x^{(n)} $$



# estimator 예시

1. MLE : Maximum Likelihood Estimators
2. LSE : Least Square Estimators
3. MAP : Maximum a posteriori
4. Kalman filter
5. Particle filter
6. MCMC : Markov Chain Monte Carlo

## 각 estimator를 언제 쓰는가?

1. Classical Closed Form Estimation
	1. MLE
	2. LSE
	3. MAP
2. Sequential/dynamic Situation
	1. Kalman Filter
	2. Particle Filter
3. Stochastic estimation
	1. MCMC


### MLE

- 데이터가 특정 확률분포 family에서 나왔다고 모델링했을 때, 모델 파라미터에 대해 가장 가능성 높은 값을 찾고 싶을 때.
- 단점: 데이터가 작으면 closed form solution이 안 나올 수 있음, MAP에 비해 outlier에 민감

### LSE

- 회귀분석 등 오차의 분포를 정확히 알기 어려울 때
- 단점: outlier에 민감

### MAP

- Bayesian 추정에서 prior 지식이나 사전분포를 반영하고 싶을 때
- 장점: 데이터 부족했을 때 보정 가능, 과적합 방지
- 단점: 사전분포에 따라 성능이 달라지며, 일반화된 성능(추정량의 uncertainty) 공식이 없음


### Kalman Filter

- 선형 가우시안 시계열/state-space 모델에서 시간에 따라 변하는 상태를 추정할 때
- 장점: closed form recursive update, 실시간 처리 가능
- 단점: 선형, 정규성 가정

### Particle Filter

- 비선형 비가우시안 state-space 모델에서 상태 추정
- 장점: 일반화된 칼만필터
- 단점: 계산량이 많고, particle degeneracy 문제 등 존재

### MCMC

- 복잡한 Bayesian posterior에서 expectation, confidence bound를 구할 때
- 장점: 어떤 분포든 근사적으로 샘플링 가능
- 단점: 계산 비용 큼


## Estimator의 평가

- CRLB : Cramer-Rao bound
	- 추정량의 분산 하한(효율성)을 알고 싶을때
	- 추정량의 성능을 비교하는 이론적 기준
	- 추정량 자체보단 평가지표. 실제 추정값을 주진 않음

# References

- https://en.wikipedia.org/wiki/Estimation_theory
- https://wikidocs.net/215060
- 밑바닥부터 시작하는 딥러닝 5 (사이토 고키 지음, 한빛미디어 출판)
- https://alida.tistory.com/92
- https://process-mining.tistory.com/126
