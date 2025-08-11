---
layout: post
title: Stochastic Bandits
date: 2025-08-11 17:35 +0900
categories: [Reinforcement Learning, Theory]
tags: [rl, reinforcement, learning, machine_learning, ai, ml, theory]
description: Multi armed bandit 중 stochastic 설명
math: true
---
# Assumptions of Stochastic Bandits
- 간단히 설명하면, **action 선택할 확률과 reward 보상구조가 모두 어떤 고정된 확률분포에서 sampling 되는 상황**. 자세히 설명하면..
- Stochastic Bandit is a collection of distributions $\nu = (P_a : a \in \mathcal{A})$ . 
	- $\nu$ 는 bandit instance. A bandit instance is a full specification of the environment in a bandit problem. ($\nu \in \mathcal{E}$) 
	- ex. Stochastic bandit에선 각 arm의 reward distribution $\{D_1, ..., D_k\}$ 

- 매 t round마다,
	- learner는 action $\mathcal{A}_t$를 선택.
	- $$\mathcal{A}_t$$가 environment의 input으로 들어가면, environment는 distribution $P_{\mathcal{A}_t}$ 에서 reward $X_t$를 sampling.
	- $X_t$를 learner에게 전달
- the learner(or policy)는 각 시점 t에서 확률적으로 어떤 행동을 할 지 결정. environment 또한 각 시점의 행동 $\mathcal{A}_t$에 대해 확률적으로 reward를 결정. 따라서 그 둘의 interaction의 결과인outcome sequence($A_1, X_1, ..., A_n, X_n$)는 어떠한 확률분포(probability measure)를 따른다.

- 가정:
	- $X_t$를 sampling할 확률: 
	$$P_{\mathcal{A}_t}=P(X_t |A_1, X_1, ..., A_t)$$
	- $$\mathcal{A}_t$$를 sampling할 확률분포: 
    $\pi_t(\, \cdot \, |A_1, X_1, ..., A_{t-1}, X_{t-1})$ 
		- $\pi_t$ 는 각 시점의 learner가 action을 선택할 확률 커널(probability kernel)
		- learner cannot use the future observations in current decisions
		FYI) probability kernel: 조건 변수에 따라 확률분포를 출력하는 함수



# Learning Objectives
- learner's goal :
	- maximize $S_n = \sum\limits_{i=1}^n X_t$ 
- 이게 optimization problem이 아닌 이유
	1. n을 모름. Often, the learner doesn't know ahead of time how many rounds are to be played
	2. Reward는 랜덤함. cumulative reward도 랜덤함.
	3. Learner는 Reward의 모분포 모름



# Stochastic Environment Classes
- structured와 unstructured가 있음

## Unstructured Bandits
- 정의
	1. action set $\mathcal{A}$ 가 finite 하고, 
	2. $\exists \; \mathcal{M}_a \; \text{for each } a \in \mathcal{A} \; \text{such that}$  
	$$\mathcal{E} = \underset{a\in\mathcal{A}}{\times} \mathcal{M}_a= \{\nu=(P_a : a\in\mathcal{A}): P_a \in \mathcal{M}_a \quad \forall a \in \mathcal{A} \}$$ 


- 분석
  - $P_a \in \mathcal{M}_a \quad \forall a \in \mathcal{A}$ : 각 action마다 가능한 보상 분포의 집합 $\mathcal{M}_a$ 가 있고, 실제 보상 분포 $P_a$는 $\mathcal{M}_a$ 의 원소 중 하나이다.
  - $\nu=(P_a : a\in\mathcal{A})$ : bandit instance $\nu$ 는 각 action마다 하나의 보상 분포 $P_a$를 선택한 조합. (tuple, vector)
    - ex. $\nu = (\;Bernoulli(0.5),\; Bernoulli(0.8)\;)$  
  - $\mathcal{E} = \underset{a\in\mathcal{A}}{\times} \mathcal{M}_a$ : 즉, unstructured environment class는 action마다 가능한 확률 분포 중 하나씩 선택한 조합의 집합. (product space)
    - $\mathcal{M}_1​=\{A,B\}, \mathcal{M}_2​=\{C,D\}$ 이면 $\mathcal{M}_1 \times \mathcal{M}_2 = \{(A, C), (A, D), (B, C), (B, D)\}$


- 의미: **action1을 하는 것은 다른 action에 대해서 아무런 정보도 주지 않는다.**
- typical environment classes
		![typical environment classes](assets/img/postimgs/mab-stochastic-environmentclass.png)

	- FYI)
		- parametric : finite DOF(Degrees of freedom)
		- nonparametric : infinite DOF

## Structured Bandits
- 정의: not unstructured bandits
	- **action1을 하는 것이 다른 action에 대해서도 정보를 준다. (구조적으로 연결되어있다)**

-  Example 1.
	- Let $\mathcal{A}=\{1,2\} \quad and \quad \mathcal{E}=\{\; (\; \mathcal{B}(\theta),\; \mathcal{B}(1-\theta) \;) \; : \; \theta \in [0,1] \;\}$ 
	- 이 상황에서 한 번의 선택으로, 두 arm 모두의 mean을 추정할 수 있다.
- Example 2. (Stochastic linear bandit)
	- Let $\mathcal{A} \subseteq \mathbb{R}^d \quad and\quad \theta \in \mathbb{R}^d \quad and\quad \nu_\theta= (\; \mathcal{N}(<a,\theta>,\;1) \;:\; a\in\mathcal{A}) \quad and\quad \mathcal{E}=\{ \nu_\theta \;:\; \theta \in \mathbb{R}^d \}$
	- reward는 Gaussian, reward distribution의 mean은 action과 unknown parameter의 내적. action set의 크기가 커도 $\mathbb{R}^d$를 span하는 d번의 액션으로 true environment 추정가능


# Regret
- Regret은 **learner가 얻은 보상과 optimal policy가 얻은 보상(최대 기대 보상)의 차이**
- action a의 기대 보상을 생각해보면, Let $\nu=(P_a\;:\;a\in\mathcal{A})$, $$\mu_a(\nu)=\int_{-\infty}^\infty{x\,dP_a(x)}$$
- ($\mu_a(\nu)$ exists and is finite for all a 가정하면) 최대 기대 보상은 $$\mu^*(\nu) = \max_{a\in\mathcal{A}}\mu_a(\nu)$$
- Regret of policy $\pi$ on $\nu$ is $$R_n(\pi,\nu)=n\mu^*(\nu) - \mathbb{E}\left[\, \sum_{t=1}^{n} X_t\right]$$
	- $n\mu^*$ : 최대 기대 보상을 주는 방식으로 n 번
	- $\mathbb{E}\left[\, \sum_{t=1}^{n} X_t\right]$ : 실제로 받은 보상의 기댓값
		- Expectation은 $\pi$와 $\nu$의 interaction의 결과($X_t$)의 probability measure에 대한 것.
- Lemma
	- (a) $R_n(\pi, \nu) \geq 0, \; \forall \pi$ 
	- (b) $R_n(\pi, \nu)=0\;such\;that\;\pi\;choosing\;\mathcal{A}_t \in \arg\max_a \mu_a$ 
	- (c) $if\;R_n(\pi, \nu)=0\;for\;some\;\pi,\;then\;\mathbb{P}(\mu_{\mathcal{A}_t}=mu^*)=1\;\forall t \in [n]$ 

- Weak objectives
	1. Sublinear Regret: find a policy $\pi$ with sublinear regret on all $\nu$ means, $$\forall\nu\in\mathcal{E},\quad \lim_{n\to\infty}\frac{R_n(\pi,\nu)}{n}=0$$
		- 위가 성립하면, horizon이 매우 클 때, 해당 policy는 optimal
	2. Polynomial Regret:		$$\forall \nu \in \mathcal{E}, \quad R_n(\pi, \nu) \leq C n^p \quad \text{for some } C > 0, \; p < 1$$
		- sublinear 보다 강한 조건 (평균 regret이 $n^{(p-1)} \to 0$ 로 더 빠르게 수렴 )
	3. Factorized Regret Bound: $$\forall n \in \mathbb{N}, \; \nu \in \mathcal{E}, \quad R_n(\pi, \nu) \leq C(\nu) f(n)$$
		- 가장 일반적인 형태. supervised learning에서 주로 사용됨

	- 참고) Bayesian Regret: 주어진 $\mathcal{E}$에 대한 prior 분포 Q를 기반으로 regret 평균화.$$ \mathrm{BR}_n(\pi, Q) = \int_{\mathcal{E}} R_n(\pi, \nu) \, dQ(\nu)$$
		- $\mathcal{E}$ must be equipped with a $\sigma$-algebra $\mathcal{F}$ , and regret $R_n(\pi,\,\cdot\,)$ is a measurable function w.r.t. $\mathcal{F}$. 확률분포로 평균을 구하려면, 사건에 확률을 부여해야 하므로 $\mathcal{E}$는 $\sigma$-algebra 구조를 갖춰야 함. 또한, regret이 measurable 해야 기댓값을 구할 수 있음.
		- the problem of finding a policy that minimises the Bayesian regret is just an optimisation problem


## Decomposing the Regret
- Definition (suboptimality gap)
	- the suboptimality gap = action gap = immediate regret of action a = $\Delta_a(\nu)=\mu^*(\nu)-\mu_a(\nu)$ 
- Definition (number of action chosen)
	- number of times action a was chosen by the learner after the end of round t is $$T_a(t)=\sum_{s=1}^t \mathbb{I}\{A_s=a\}$$
	- $T_a(n)$은 랜덤. t시점의 action은 이전 시점의 리워드에 의존하기 때문에 랜덤성을 inherit함.
- Lemma (Regret decomposition lemma)
	- $\text{For any } \pi\text{, stochastic bandit } \nu\text{, finite or countable }\mathcal{A}\text{, horizon }n\in\mathbb{N},$ $$ R_n(\pi,\nu) = \sum_{a\in\mathcal{A}}\Delta_a\times\mathbb{E}[\;T_a(n)\,]$$
	- $\Delta_a$ : action a의 regret
	- $\mathbb{E}[\;T_a(n)\,]$ : action a를 한 횟수
	- 이 lemma가 regret을 "각 arm을 사용한 것"과 "그 때의 loss"로 decompose 함
	- arm with larger $\Delta_a$를 더 적게 선택해야 하는 것을 목표로 해야 함을 말해줌
	- pf)![proof of regret decomposition theorem](assets/img/postimgs/mab-stochastic-regretdecomposition.png)

	- the action set $\mathcal{A}$ 가 uncountable일 때는 $T_a(n)$ 대신 measurable space $(\mathcal{A},\mathcal{G})$ 에서 measure G를 같은 방식으로 define하고, $R_n$의 decompose는 $\mathbb{E}[T_a(n)]$ 대신 integral on dG(a)로 대체한다. 


# Reference
Tor L., Csaba S., *Bandit Algorithm* 
