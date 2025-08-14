---
layout: post
title: Stochastic Linear Bandit
date: 2025-08-14 23:40 +0900
categories: [Reinforcement Learning, Theory]
tags: [rl, reinforcement, learning, machine_learning, ai, ml, theory]
description: Stochastic Linear Bandit 설명
math: true
---
# Contextual Bandits
- 많은 bandit 상황에서, the learner can access to additional information.
	- 예를 들면, 영화 추천에서 각 영화의 장르나, 감독, 혹은 추천대상의 demographic feature 등.
- 과거 관측 보상뿐아니라, additional information까지 반영하는 모델이 contextual bandit.

# Stochastic Contextual Bandits
- linear bandit은 Contextual bandit의 한 종류
- reward: $$X_t = r(C_t, A_t) + \eta_t$$
	- $r:\mathcal{C}\times[k]\rightarrow\mathbb{R}$ is called **reward function**, and $\eta_t$ is noise(assume 1-subgaussian)
- precisely, Let $\mathcal{F}_t = \sigma(C_1,A_1,X_1,...,C_t, A_t)$ be the $\sigma$-field summarizing the information available before $X_t$ is observed
- Assume $\eta_t$ 1-subgaussian (subgaussian이면 되긴 하지만 편의상 1-subG로 가정):  $$\mathbb{E}[\; \exp(\lambda\eta_t)\,|\,\mathcal{F}_t\;] \leq\exp\left( \frac{\lambda^2}{2} \right) \quad\text{almost surely}$$
	- cf) if $X \sim\text{subG}(\sigma^2)$ , $$\mathbb{E}[\exp(sX)]\leq\exp\left(\frac{\sigma^2s^2}{2} \right)$$
	- almost surely : 확률변수의 수렴에 사용하는 표현.
	- Then, $\mathbb{E}[X_t|\mathcal{F}_t]=r(C_t,A_t)$

- 무튼, 무슨 상황이냐..
	- 최적의 action $A_t^* \in \arg\max_{a\in[k]}r(C_t,a)$ 는 $C_t$에 비례한는 random variable. 따라서 (expected) regret은 각 시점의 최대 reward에서 실제로 받은 reward를 빼면: $$R_n = \mathbb{E}\left[ \sum_{t=1}^n \max_{a\in[k]}r(C_t,a) - \sum_{t=1}^n X_t\right]$$
	- 근데 이 정의는 항상 쓸 수 있진 않음. 왜 why? t시점에서 낮은보상을 선택하는 것이 컨텍스트를 변경시켜 t+1시점에서 더 큰 보상을 줄 가능성 있음. 따라서 이 정의는 learner의 행동이 후속 컨텍스트에 영향을 주지 않을 때만 의미 있음.
	- 그러면? 각 모든 Context와 action에 대해 r을 추정할 수 있지만 그 때의 worst-case regret은 at least $\Omega(\sqrt{nMk})$. (M: 컨텍스트 수). 보통 context 수 $M$은 매우 크므로, 나쁨.
	- 근데 이 상황은 context가 다를 때 정보공유가 안되는 상황($r(c,\cdot)$ provides no useful information about  $r(c',\cdot)$). 실제로는 context간에 structure가 있음.($r(\cdot,\,\cdot)$ changes smoothly)
	- 이 때 상황을 단순화하기 위한 선형모델 도입!
		- assume
			- feature map $\psi:\mathcal{C}\times[k]\rightarrow\mathbb{R}^d$ exists
			- and for unknown parameter vector $\theta_*\in\mathbb{R}^d$, $$r(c,a)=<\theta_*,\psi(c,a)>$$
		- 이렇게 하면 (c,a)별로 보상을 추정하는 대신 d차원의 벡터 $\theta_*$만 학습하면 됨. 새로운 (c,a) pair에 대해서도 예측이 쉬워짐.
		- $\theta_*$는 각 feature가 보상에 얼마나 기여하는 지에 대한 weight
		- 이 가정의 우려, 단점
			- context와 action간의 보상이 비선형인 경우는 feature map을 비선형으로 해야 함
			- feature map이 잘못 설계되었거나 불완전할 경우, $\theta_*$를 아무리 학습해도 bias남음
			- $\theta_*$ 고정되어있다고 가정하므로 non stationary한 상황에선 잘 작동 x
			- feature와 action이 독립적이지 않은 경우 잘 작동하지 않을 수 있음
		- The subspace $\Psi$ spanned by the feature vectors ${\psi(c,a)}_{c,a} \in\mathbb{R}^d$  is called feature space
		- Holder's inequality에 의해 $$|r(c,a)-r(c',a')|
		- \leq||\theta_*||\,||\psi(c,a)-\psi(c'a')||$$
			- 이로부터, $||\theta_*||$가 작다고 가정하면 보상 함수 r의 변화가 크지 않음 -> 매끄러운 함수라고 볼 수 있음.
			- $||\theta_*||$에 대한 제한은 dimensionality d가 finite하다는 가정과 같은 효과.
				- 왜? $r(c,a)$의 복잡도는 두 요소: parameter 차원 d와 parameter 크기 $||\theta_*||$ 에 비례. ($\because$ d가 크면 자유도가 높아지고, 크기가 크면 같은 feature 차이에도 보상 변화폭이 커짐. 통계학적으로 function class의 Rademacher complexity나 covering number를 줄이는 역할 )
		- 참고) Dual norm $$||y||_*=\sup_{||x||\leq1}<y,x>$$
			- 의미: 원래 노름에서 unit ball($||\,\cdot\,||\leq1$) 안에 있는 모든 벡터와 y를 내적했을 때 가능한 최댓값
			- 그러면, $||x||\leq1$에 대해 $$||<x,y>||\leq||y||_*$$
			- 어떤 $x$에 대해  확장한 다음 부등식을 Holder's Inequality라 부른다. $$||<x,y>||\leq||x||\cdot||y||_*$$
# Stochastic Linear Bandits
- 자 이제 우리는 reward를 다음과 같이 정의한다. $$X_t=<\theta_*, A_t>+\eta_t \quad(A_t\in\mathcal{A}_t)$$
	- 이때, t시점의 decision set $\mathcal{A}_t\in\mathbb{R}^d$에 따라 설정을 다르게 줄 수 있다.
		1. Finite-armed bandit: ($e_i$는 표준기저벡터) $$\mathcal{A}_t = \{e_1, ...,e_d\}$$
		2. Contextual linear bandit: $$\mathcal{A}_t=\{\psi(C_t,i):i\in[k]\}$$
		3. Combinatorial action set: $$\mathcal{A}_t\subset \{0,1\}^d$$
- 그럼 random (pseudo-)regret과 regret은 각각 $$\hat{R_n}=\sum_{t=1}^n\max_{a\in\mathcal{A}_t}<\theta_*,\;a-A_t>$$ $$R_n=\mathbb{E}\left[ \hat{R_n}\right]=\mathbb{E}\left[ \sum_{t=1}^n\max_{a\in\mathcal{A}_t}<\theta_*,\;a> -\sum_{t=1}^nX_t\right]$$

- Stochastic linear bandit algorithm : UCB
	- variants of UCB are nearly minimax optimal, instance optimal, and exactly optimal asymptotically.
		- minimax optimal: worst environment regret이 정보이론적 하한과 같은 order로 맞는 경우. 식: $$\inf_\pi \sup_{\nu\in\mathcal{E}}R_n(\pi,\nu)$$ 
		- instance optimal: 



# Reference
Tor L., Csaba S., *Bandit Algorithm* 
https://convex-optimization-for-all.github.io/contents/chapter13/2021/04/05/13_03_Dual_norms/
