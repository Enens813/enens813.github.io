---
layout: post
title: Stochastic Bandit Algorithms - ETC, UCB
date: 2025-08-13 23:28 +0900
categories: [Reinforcement Learning, Theory]
tags: [rl, reinforcement, learning, machine_learning, ai, ml, theory]
description: Stochastic bandit 문제를 푸는 algorithm들 설명
math: true
---
- simplicity를 위해 assume all bandit instances are in $\mathcal{E}_{SG}^k(1)$, 즉 모든 arm에 대해 reward distribution은 1-subgaussian
	- 1-subgaussian : 꼬리(tail)가 'stdev=1인 가우시안'보다 결코 두껍지 않은 확률변수

# ETC algorithm
- explore-then-commit(ETC) 각 arm을 다 m번씩 눌러봄. 그 이후엔 best arm만 선택.
- algorithm:
	![mab-etcucb-etc-algorithm.png](assets/img/postimgs/mab-etcucb-etc-algorithm.png)
- Theorem (Regret Upper Bound of ETC Algorithm with 1-subgaussian bandit)
$$ R_n \leq m \sum_{i=1}^{k} \Delta_i + (n-mk)\sum_{i=1}^{k} \Delta_i \exp \left(-\frac{m\Delta_i^2}{4} \right)$$
- pf) 나중에...



- Exploration-Exploitation trade-off: m이 크면 suboptimal arm을 선택하는 횟수가 많아져 첫 번째 항이 너무 커지고, m이 작으면 고른 arm이 suboptimal일 확률이 높기 때문에 두 번째 항이 커진다.

- Example for 2 armed bandit case.
- Regret: $$R_n \le \min \left\{ 
n\Delta,\; 
\Delta + \frac{4}{\Delta} \left( 1 + \max \left\{ 0, \log\left( \frac{n\Delta^2}{4} \right) \right\} \right) 
\right\}.$$
- pf) 나중에..

- Definition (gap/problem/distribution/instance dependent bound)
	- suboptimality gap에 의존하는 regret bound
- Definition (worst-case / problem-free / problem-independent / gap-free bound)
	- The bound only depends on the horizon and class of bandits

- Worst-case bound of ETC Algo : $$ R_n \leq \Delta+C\sqrt{n}$$
	- without the condition $\Delta\leq1$, the worst-case bound for ETC is infinite. In fact, without bound on the reward range(range of $\Delta$), the worst-case bound of all reasonable algorithms will also be infinite since they try each action at least once.
	- pf) 나중에..

- Definition (anytime algorithm)
	- anytime algorithm $\Leftrightarrow$ horizon에 대한 정보 없어도 됨

- m depends on $\Delta$ and the horizon (not anytime algorithm)
	- Often, $\Delta$는 알 수 있지만 horizon은 알 수 없음
- 각 시점마다 immediate expected regret은 monotonically decrease. (smooth하진 않음)


## Further topics
- m을 data-dependent random variable로 보면, $\Delta$없이 near-optimal regret을 찾을 수 있음 (Exercise 6.5)
- Elimination Algorithm을 이용하여 ... (Exercise 6.8)
- $\varepsilon$-greedy : randomised relative of ETC that in round t plays the empirically best arm with probability $1-\varepsilon_t$ and otherwise explores uniformly at random.



# UCB algo
- ETC 대비 장점
	1. $\Delta$ 몰라도 됨
	2. 2 arm 이상에서도 잘 작동
- 원리
	- optimism in the face of uncertainty
	- 새로운걸 더 긍정적으로 보면, 보수적으로 원래 걸 exploitation할 때보다 optimal을 찾을 확률이 높아짐
	- **아직 불확실성이 크면 실제 평균이 더 클 수도 있다**는 가능성을 반영해 regret의 상한값(Upper Confidence Bound, UCB) 을 계산하여 UCB가 가장 높은 팔을 선택.
	- 
- UCB 알고리즘 (정확하겐 UCB($\delta$)알고리즘):

![mab-etcucb-ucbequation.png](assets/img/postimgs/mab-etcucb-ucbequation.png)
![mab-etcucb-ucb-algorithm.png](assets/img/postimgs/mab-etcucb-ucb-algorithm.png)

- Thm (gap dependent regret bound for UCB)
	- for 1-subgaussian bandit problem, if $\delta = 1 / n^2$, 
	- gap dependent regret bound: $$R_n \leq 3\sum_{i=1}^k \Delta_i + \sum_{i:\Delta_i>0}\frac{16\log(n)}{\Delta_i}$$
	- gap **in**dependent regret bound:  $$R_n \leq 8\sqrt{nk\log(n)}+3\sum_{i=1}^k\Delta_i$$
- pf) (gap dependent)
	- proof sketch)
		- 나중에..
	- proof) 나중에..
- pf) (gap independent)
	- proof sketch)
		- 나중에..
	- proof) 나중에..

- Note)
	- 나중에..

# Asymptotically Optimal UCB

- algorithm
	- 위의 UCB알고리즘은 anytime이 아님.
	- exploration할 때 $\delta$ 대신 f(t)사용.
![mab-etcucb-asymtoticucb.png](assets/img/postimgs/mab-etcucb-asymtoticucb.png)

- Thm (gap dependent regret bound for Asymptotic UCB)
	- for 1-subgaussian bandit problem,
	- gap dependent regret bound: $$R_n \le \sum_{i : \Delta_i > 0} \inf_{\varepsilon \in (0, \Delta_i)} \Delta_i \left( 1 + \frac{5}{\varepsilon^2} + \frac{2 \left[ \log f(n) + \sqrt{\pi \log f(n)} + 1 \right]}{(\Delta_i - \varepsilon)^2} \right)$$
	- asymptotic property: $$\limsup_{n \to \infty} \frac{R_n}{\log n} 
\le \sum_{i : \Delta_i > 0} \frac{2}{\Delta_i}$$ 
	- gap **in**dependent regret bound:  $$R_n \le \sum_{i : \Delta_i > 0} \left( \Delta_i + \frac{1}{\Delta_i} \left( 8 \log f(n) + 8 \sqrt{\pi \log f(n) }+ 28 \right) \right)$$

# Reference
Tor L., Csaba S., *Bandit Algorithm* 
