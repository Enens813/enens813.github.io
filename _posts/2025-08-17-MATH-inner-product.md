---
layout: post
title: 내적
date: 2025-08-17 20:43 +0900
categories: [Mathematics, Linear Algebra]
tags: [math, mathematics, linear, algebra]
description: 내적 정리
math: true
---


# Definition (Inner Product)

- $F$-벡터공간 $V$에서 정의된 inner product는 $<x,y>$로 표기하며, 임의의 벡터 $x$와 $y$의 순서쌍을 $F$에 관한 스칼라에 대응시키는 사상 

  $$ <\cdot\;,\;\cdot>:V\times V \rightarrow F$$
      
  를 가리키며, 다음 네 조건을 만족한다. 임의의 $x,y,z\in V, \;c\in F$에 대해

  1. $<x+z,y>=<x,y>+<z,y>$
  2. $<cx,y>=c<x,y>$
  3. $\overline{<y,x>}=<x,y>$
  4. $\forall x\in V,\; <x,x>\geq 0\;\,\text{and}<x,x>=0\Leftrightarrow x=0$


## Definition (Inner Product Space)
- 적어도 하나의 내적을 갖는 벡터공간 $V$를 내적공간이라 한다. 
- $F=\mathbb{R}$ 이면 $V$를 real inner product space, $F=\mathbb{C}$이면 $V$를 complex inner product space라 한다.


## 여러 가지 내적들

### Standard Inner Product (벡터의 표준 내적)

- $F^n$의 두 벡터 $x=(a_1,a_2, ... ,a_n),\quad y=(b_1,b_2, ... ,b_n)$ 에 대해 

$$<x,y>=\sum_{i=1}^n a_i\bar{b_i}$$

### Frobenius inner product (실수 행렬의 표준 내적)

- $M_n(\mathbb{R})$의 두 행렬 $A,\; B$에 대해

$$<A,B>=tr(AB^\top)$$

### (함수의 표준 내적)
- 닫힌구간 $[a,b]$ 에서의 연속함수 집합 $C[a,b]$의 두 함수 $f,g$ 에 대해

$$<f,g>=\int_a^b f(x)\overline{g(x)}\,dx$$

- 위의 '벡터의 표준내적'과 사실 같은 말이다.


## 내적의 성질
1. 첫 번째 변수에 대해 linearity (조건 2) & 두 번째 변수에 대해선 conjugate linearity: $$<x,cy>=\bar{c}<x,y>$$
	- 왜? 
		- 조건 2,3에 의해 
      
      $$<cx,y>=\overline{<y,cx>}=c<x,y>=c\,\overline{<y,x>}$$
      
		- 두 번째와 네 번째 항을 뽑아서 conjugate 하면,

      $$<y,cx>=\bar{c}<y,x>$$

	- 첫번째가 conjugate, 두번째가 그냥 linearity여도 됨 (ex. 브라-켓 notation)

# References
https://gosamy.tistory.com/255
