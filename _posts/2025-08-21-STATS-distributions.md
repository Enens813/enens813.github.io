---
layout: post
title: 여러 가지 분포들
date: 2025-08-21 22:11 +0900
categories: [Statistics, General Backgrounds]
tags: [statistics, general, backgrounds]
description: 내적 정리
math: true
---

- 분포들에 대해 알아보자
- 자세하겐 다음에 차례대로 포스팅 예정
- 아래는 GPT를 이용해 적절한 형식으로 생성했다. 틀린 부분이 있을 수 있다. 추후 개별 포스팅을 하며 공부 후 설명 수정 예정.

# discrete

| 분포                           | 특징                                  | 주요 파라미터 | 활용 예시                        |
| ------------------------------ | ------------------------------------- | ------------- | -------------------------------- |
| **베르누이 (Bernoulli)**       | 0/1 또는 성공/실패 결과               | p             | 동전 앞/뒤                       |
| **이항 (Binomial)**            | n회 독립 시행 중 성공 횟수            | n, p          | 품질검사 불량품 개수             |
| **기하 (Geometric)**           | 첫 성공 전까지 시행 수                | p             | 마케팅에서 첫 구매까지 시도 횟수 |
| **음이항 (Negative Binomial)** | k번째 성공까지 시행 수                | r, p          | 고장 전까지 시험 횟수            |
| **포아송 (Poisson)**           | 일정 시간/공간 내 희귀 사건 발생 수   | λ             | 하루 교통사고 횟수               |
| **초기하 (Hypergeometric)**    | 비복원 추출에서 성공 횟수             | N, K, n       | 카드게임 확률 계산               |
| **다항 (Multinomial)**         | 범주형 사건이 여러 범주로 나뉘는 경우 | n, p₁,...,pₖ  | 주사위 던지기 결과               |

# continuous

| 분포                             | 특징                                                     | 주요 파라미터 | 활용 예시                                  |
| -------------------------------- | -------------------------------------------------------- | ------------- | ------------------------------------------ |
| **정규 (Normal)**                | 평균 μ, 분산 σ²                                          | μ, σ          | 키, 시험점수                               |
| **Sub-Gaussian**                 | 꼬리가 정규보다 가벼운 분포(집중 불평등 분석에 중요)     | σ²-유사 척도  | 고차원 통계, 기계학습에서 일반화 성능 분석 |
| **균등 (Uniform)**               | 모든 구간 동일 확률                                      | a, b          | 난수 생성                                  |
| **지수 (Exponential)**           | 사건 간 대기 시간                                        | λ             | 고장까지 걸린 시간                         |
| **감마 (Gamma)**                 | 지수 분포 일반화                                         | α, β          | 수명분석                                   |
| **베타 (Beta)**                  | [0,1] 구간에서 확률 모델링                               | α, β          | 베이즈 사전분포                            |
| **카이제곱 (Chi-Square)**        | 표준정규 제곱합                                          | k             | 분산검정, 적합도검정                       |
| **t-분포**                       | 표본 수 작을 때 평균 추정                                | df            | 소규모 집단 평균 비교                      |
| **F-분포**                       | 두 분산 비율                                             | d₁, d₂        | ANOVA                                      |
| **Weibull**                      | 수명·고장 분석에서 자주 사용, 형태에 따라 지수/정규 유사 | k, λ          | 재료 파손 시점 예측                        |
| **Gumbel**                       | 극값 분포(최댓값, 최솟값 모델링)                         | μ, β          | 홍수 최대치, 최대 풍속 예측                |
| **Frechet**                      | 극값 이론에서 꼬리가 무거운 경우                         | α, s          | 금융 리스크, 지진 규모                     |
| **Log-Normal**                   | 로그가 정규분포                                          | μ, σ          | 소득 분포, 입자 크기                       |
| **Pareto**                       | 꼬리가 무거운 분포, 부의 분포                            | α, xₘ         | 파레토 법칙(80/20)                         |
| **Cauchy**                       | 평균·분산이 정의되지 않는 무거운 꼬리                    | x₀, γ         | 로버스트 통계 예시                         |
| **Laplace (Double Exponential)** | 중앙에서尖, 꼬리 두꺼움                                  | μ, b          | 신호처리, 희소성 모델                      |
| **Rayleigh**                     | 2D 벡터 크기 분포                                        | σ             | 무선통신 페이딩 모델                       |
| **Logistic**                     | S-curve 누적함수, 꼬리 두꺼움                            | μ, s          | 로지스틱 회귀의 에러모델                   |


# Distributions with process

| 분포                           | 생성 과정(Statistical Process)                                              | 예시/설명                    |
| ------------------------------ | --------------------------------------------------------------------------- | ---------------------------- |
| **베르누이 (Bernoulli)**       | 한 번의 독립 시행, 성공확률 p                                               | 동전 던지기 1회              |
| **이항 (Binomial)**            | n번 독립 Bernoulli 시행 성공 횟수                                           | "n회 시도 중 성공 몇 번?"    |
| **기하 (Geometric)**           | 독립 Bernoulli 시행에서 첫 성공 전 시행 수                                  | "첫 성공까지 걸린 시도 수"   |
| **음이항 (Negative Binomial)** | k번째 성공 전까지 걸린 시행 수                                              | 성공 목표를 여러 번으로 설정 |
| **포아송 (Poisson)**           | 단위 시간당 λ의 발생률을 가진 희귀 사건 과정(Poisson process)에서 발생 횟수 | 사건 발생 카운트             |
| **초기하 (Hypergeometric)**    | 유한 모집단에서 비복원 추출                                                 | 상자에서 공 뽑기             |
| **다항 (Multinomial)**         | n번 독립 시행, 각 시행이 k개 범주 중 하나                                   | 주사위 던지기                |
| **정규 (Normal)**              | 많은 독립 동일분포 확률변수의 평균(Central Limit Theorem)                   | 합/평균의 극한               |
| **카이제곱 (Chi-Square)**      | k개의 독립 표준정규제곱의 합                                                | 제곱합 분포                  |
| **t-분포**                     | (표준정규)/(독립 카이제곱/k)                                                | 표본평균 비교                |
| **F-분포**                     | (카이제곱₁/d₁) / (카이제곱₂/d₂)                                             | 분산비 검정                  |
| **지수 (Exponential)**         | Poisson process에서 사건 간 간격                                            | 대기 시간 분포               |
| **감마 (Gamma)**               | 독립 지수분포 합                                                            | 여러 사건 발생까지 걸린 시간 |
| **Weibull**                    | 비메모리형 고장률을 가진 수명모델의 변형                                    | 재료 고장 시간               |
| **Gumbel**                     | 독립 표본의 최대값(또는 최소값)의 극값 극한                                 | 기후 최대치, 공학 피크치     |
| **Fréchet**                    | 무거운 꼬리 데이터의 극값 극한                                              | 대규모 손실 분석             |
| **Log-Normal**                 | 정규분포 확률변수의 지수변환                                                | 곱셈적 성장 과정             |
| **Pareto**                     | 비율 성장/부의 축적 모델(Yule process)                                      | 소득 분포                    |
| **Rayleigh**                   | 독립 표준정규 X, Y의 벡터 크기                                              | 2D 무작위 방향 길이          |
| **Laplace**                    | 두 개의 독립 지수분포 차이                                                  | 尖한 중앙값 분포             |
| **Sub-Gaussian**               | 꼬리가 정규보다 가벼운 분포군, 주로 bounded/집중 부등식 조건에서            | Hoeffding-type 과정          |
| **Logistic**                   | 로지스틱 누적확률 역변환 과정                                               | 분류 경계 모델               |
| **Multivariate Normal**        | 다변량 선형결합 + CLT                                                       | 다변량 연속 데이터           |

# without process

- **베타 (Beta)** → [0,1] 구간에서 확률 파라미터의 사전분포로 설정, Dirichlet의 2차원 버전
    
- **Dirichlet** → 다항분포 확률벡터의 사전분포
    
- **Cauchy** → 두 독립 표준정규의 비로 생성 가능하지만, "특정 과정"이라기보다는 비율 정의
    
- **Uniform** → 무정보 상태에서 정의(최대 엔트로피)
    
- **Generalized Extreme Value (GEV)** → Gumbel, Fréchet, Weibull의 통합 형태, 극값이론에서 파라미터화된 형태
    
- **Student’s t** (위 표에도 있지만, 원래는 비율 정의라서 직접적인 물리적 process로는 잘 안 씀)
    
- **Sub-Gaussian family** (개별 분포가 아니라 tail behavior class)



# Distribution families

| 분포 패밀리                               | 핵심 아이디어                                      | 대표 멤버 / 변환                       | 특징                                                  |
| ----------------------------------------- | -------------------------------------------------- | -------------------------------------- | ----------------------------------------------------- |
| **Tukey families**                        | 정규분포 Z에 변환을 적용해 비대칭과 꼬리를 조절    | g-h, g-k, h-only 등                    | PDF가 닫힌 형태로 안 나오지만, g→skewness, h→kurtosis |
| **Location-Scale family**                 | 기본 분포를 위치(μ)와 척도(σ)로 변환               | 정규, 로지스틱, 라플라스 등            | "표준형 분포"에 shift/scale                           |
| **Exponential family**                    | PDF가 exp(theta) 형태                              | 정규, 베르누이, 포아송, 감마 등        | 대다수 유명한 분포들이 속함                           |
| **Pearson system**                        | 미분방정식으로 정의, skewness·kurtosis에 따라 분류 | Pearson I–XII, 베타·t-분포 포함        | 연속분포를 체계적으로 분류                            |
| **Generalized Extreme Value (GEV)**       | 극값 이론에서 세 가지 극값분포 통합                | Gumbel, Fréchet, Weibull               | 꼬리 형태를 shape 파라미터로 제어                     |
| **Stable distributions**                  | 독립 확률변수 합의 극한 분포                       | 정규, 코시, Lévy                       | 무거운 꼬리 포함, α-stable 파라미터                   |
| **Generalized Lambda Distribution (GLD)** | 누적분포함수의 역함수를 다항식 형태로 설정         | Tukey λ 분포 포함                      | 다양한 모양 모사 가능                                 |
| **Power transformation families**         | Box-Cox, Yeo-Johnson 등                            | 데이터 정규화에 사용                   | 분산 안정화, 대칭성 증가                              |
| **Elliptical distributions**              | 등밀도 곡선이 타원                                 | 정규, 다변량 t, Kotz                   | 다변량 분석에서 유용                                  |
| **Generalized Pareto Distribution (GPD)** | 꼬리 부분을 파라미터화                             | Pareto, 지수 포함                      | 극값 분석, 리스크 모델                                |
| **Mixture families**                      | 여러 분포를 가중합                                 | 가우시안 혼합모델(GMM), 혼합 포아송 등 | 군집·이질성 데이터 모델링                             |
| **Compound distributions**                | 한 분포의 파라미터를 다른 분포로 모델링            | Compound Poisson, Negative Binomial 등 | 사건 수 불확실성 모델                                 |

- **변환 기반**: Tukey, Box-Cox, Generalized Lambda
    
- **파라미터 계층화**: Exponential family, Location-Scale family
    
- **극값/꼬리 분석**: GEV, GPD, Stable distributions
    
- **혼합·복합 과정**: Mixture, Compound families



# Reference
ChatGPT
