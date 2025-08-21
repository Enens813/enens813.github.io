---
layout: post
title: 스칼라, 벡터, 행렬의 미분
date: 2025-08-17 20:00 +0900
categories: [Mathematics, General]
tags: [math, mathematics, calculus]
description: 스칼라, 벡터, 행렬의 미분 법칙 정리
math: true
---

## 요약
- 스칼라 미분: 

$$
df=f'(x)dx
$$

- 벡터 미분: 

  $$df=\nabla f(\mathbf{x})^\top dx$$

  - $$f(\mathbf{x})=\mathbf{a}^\top \mathbf{x}\rightarrow df/d\mathbf{x}=\mathbf{a}$$.
- 행렬 미분:

  $$df=\operatorname{tr}\left( \left( \frac{\partial\,f}{\partial\,X} \right)^\top   dX\right)$$

  - $\mathbf{y} = A\mathbf{x} + \mathbf{b} \rightarrow d\mathbf{y}/d\mathbf{x}=A$.
  - $f = g(WX),\;\text{g is elementwise function}\rightarrow \frac{\partial f}{\partial X} = g'(WX) \circ \frac{\partial (WX)}{\partial X} = g'(WX) \circ W$.


## 기본

- Let, $x,y\in\mathbb{R},\;\mathbf{x}\in\mathbb{R}^n,\;\mathbf{y}\in\mathbb{R}^m,\;A\in\mathbb{R}^{m\times n}$ 
- 참고) 행/열벡터는 바뀌어도 됨 (한 document안에서만 notation지키면 됨됨)

- 스칼라를 벡터로 미분 (Gradient)

$$
\frac{\mathrm{d}y}{\mathrm{d}\mathbf{x}}
= \nabla_{\mathbf{x}}\,y(\mathbf{x})=
\begin{bmatrix}
\frac{\partial y}{\partial x_{1}} &
\frac{\partial y}{\partial x_{2}} &
\cdots &
\frac{\partial y}{\partial x_{n}}
\end{bmatrix}
\in \mathbb{R}^{1 \times n}
$$

- 벡터를 스칼라로 미분

 $$
\frac{\mathrm{d}\mathbf{y}}{\mathrm{d}x}
=
\begin{bmatrix}
\frac{\partial y_{1}}{\partial x} \\
\frac{\partial y_{2}}{\partial x} \\
\vdots \\
\frac{\partial y_{m}}{\partial x}
\end{bmatrix}
\in \mathbb{R}^{m \times 1}
$$

- 스칼라를 행렬로 미분

$$
\frac{\mathrm{d}y}{\mathrm{d}A}
=
\begin{bmatrix}
\frac{\partial y}{\partial a_{11}} & \frac{\partial y}{\partial a_{12}} & \cdots & \frac{\partial y}{\partial a_{1n}} \\
\frac{\partial y}{\partial a_{21}} & \frac{\partial y}{\partial a_{22}} & \cdots & \frac{\partial y}{\partial a_{2n}} \\
\vdots & \vdots & \ddots & \vdots \\
\frac{\partial y}{\partial a_{m1}} & \frac{\partial y}{\partial a_{m2}} & \cdots & \frac{\partial y}{\partial a_{mn}}
\end{bmatrix}
\in \mathbb{R}^{m \times n}$$

- 행렬을 스칼라로 미분

 $$
\frac{\mathrm{d}A}{\mathrm{d}x}
=
\begin{bmatrix}
\frac{\partial a_{11}}{\partial x} & \frac{\partial a_{12}}{\partial x} & \cdots & \frac{\partial a_{1n}}{\partial x} \\
\frac{\partial a_{21}}{\partial x} & \frac{\partial a_{22}}{\partial x} & \cdots & \frac{\partial a_{2n}}{\partial x} \\
\vdots & \vdots & \ddots & \vdots \\
\frac{\partial a_{m1}}{\partial x} & \frac{\partial a_{m2}}{\partial x} & \cdots & \frac{\partial a_{mn}}{\partial x}
\end{bmatrix}
\in \mathbb{R}^{m \times n}
$$

- 벡터를 벡터로 미분(Jacobian)

$$
\frac{\mathrm{d}\mathbf{y}}{\mathrm{d}\mathbf{x}}
= J_{\mathbf{y}}(\mathbf{x})=
\begin{bmatrix}
\frac{\partial y_{1}}{\partial x_{1}} & \frac{\partial y_{1}}{\partial x_{2}} & \cdots & \frac{\partial y_{1}}{\partial x_{n}} \\
\frac{\partial y_{2}}{\partial x_{1}} & \frac{\partial y_{2}}{\partial x_{2}} & \cdots & \frac{\partial y_{2}}{\partial x_{n}} \\
\vdots & \vdots & \ddots & \vdots \\
\frac{\partial y_{m}}{\partial x_{1}} & \frac{\partial y_{m}}{\partial x_{2}} & \cdots & \frac{\partial y_{m}}{\partial x_{n}}
\end{bmatrix}
\in \mathbb{R}^{m \times n}
$$

- 벡터를 행렬로 미분 (for $\mathbf{y} \in \mathbb{R}^{m}, \quad A \in \mathbb{R}^{p \times q}$ )

$$
\frac{\partial \mathbf{y}}{\partial A}
=
\begin{bmatrix}
\frac{\partial y_{1}}{\partial a_{11}} & \frac{\partial y_{1}}{\partial a_{12}} & \cdots & \frac{\partial y_{1}}{\partial a_{1q}} & \cdots & \frac{\partial y_{1}}{\partial a_{p1}} & \cdots & \frac{\partial y_{1}}{\partial a_{pq}} \\
\frac{\partial y_{2}}{\partial a_{11}} & \frac{\partial y_{2}}{\partial a_{12}} & \cdots & \frac{\partial y_{2}}{\partial a_{1q}} & \cdots & \frac{\partial y_{2}}{\partial a_{p1}} & \cdots & \frac{\partial y_{2}}{\partial a_{pq}} \\
\vdots & \vdots & \ddots & \vdots & \ddots & \vdots & \ddots & \vdots \\
\frac{\partial y_{m}}{\partial a_{11}} & \frac{\partial y_{m}}{\partial a_{12}} & \cdots & \frac{\partial y_{m}}{\partial a_{1q}} & \cdots & \frac{\partial y_{m}}{\partial a_{p1}} & \cdots & \frac{\partial y_{m}}{\partial a_{pq}}
\end{bmatrix}
\in \mathbb{R}^{m \times (pq)}$$

- 행렬을 벡터로 미분

 $$
\frac{\partial A}{\partial \mathbf{x}}
=
\begin{bmatrix}
\frac{\partial a_{11}}{\partial x_{1}} & \frac{\partial a_{11}}{\partial x_{2}} & \cdots & \frac{\partial a_{11}}{\partial x_{n}} \\
\frac{\partial a_{12}}{\partial x_{1}} & \frac{\partial a_{12}}{\partial x_{2}} & \cdots & \frac{\partial a_{12}}{\partial x_{n}} \\
\vdots & \vdots & \ddots & \vdots \\
\frac{\partial a_{1q}}{\partial x_{1}} & \frac{\partial a_{1q}}{\partial x_{2}} & \cdots & \frac{\partial a_{1q}}{\partial x_{n}} \\
\vdots & \vdots & \ddots & \vdots \\
\frac{\partial a_{p1}}{\partial x_{1}} & \frac{\partial a_{p1}}{\partial x_{2}} & \cdots & \frac{\partial a_{p1}}{\partial x_{n}} \\
\vdots & \vdots & \ddots & \vdots \\
\frac{\partial a_{pq}}{\partial x_{1}} & \frac{\partial a_{pq}}{\partial x_{2}} & \cdots & \frac{\partial a_{pq}}{\partial x_{n}}
\end{bmatrix}
\in \mathbb{R}^{(pq) \times n}$$

---
## 심화

### 1. 선형형식

$$f(\mathbf{x}) = \mathbf{a}^\top \mathbf{x}$$

$$\nabla_{\mathbf{x}} f= \begin{bmatrix}
\frac{\partial f}{\partial x_1} \\
\frac{\partial f}{\partial x_2} \\
\vdots \\
\frac{\partial f}{\partial x_m}
\end{bmatrix}
= \mathbf{a}$$

---
### 2. 이차형식

$$f(\mathbf{x}) = \mathbf{x}^\top A \mathbf{x}$$
s
$$\nabla_{\mathbf{x}} f = (A + A^\top)\mathbf{x}$$

- 증명:

$$\text{Let, }A=S+K,\;\text{where }S=\frac{1}{2}(A+A^\top)\text{ and }K=\frac{1}{2}(A-A^\top)$$

$$\text{then, }\mathbf{x}^\top K\mathbf{x}=\mathbf{x}^\top K^\top \mathbf{x}=-\mathbf{x}^\top K\mathbf{x}=0$$

$$\text{therefore, }\mathbf{x}^\top A\mathbf{x}=\mathbf{x}^\top S\mathbf{x}$$

$$\frac{\partial}{\partial x_k}(\mathbf{x}^\top S\mathbf{x})=\sum_j s_{kj}x_j\,+\sum_i s_{ik}x_i=(S\mathbf{x})_k+(S^\top\mathbf{x})_k=2(S\mathbf{x})_k$$

$$\text{therefore, }\nabla_{\mathbf{x}} f = 2S\mathbf{x}=(A + A^\top)\mathbf{x}$$

---
## 확장

### 아이디어
- 위처럼, 미분을 해봤을 때 스칼라의 미분과 결과가 매우 유사하게 나옴.
- 변수가 몇 개든, 미분은 "선형 근사"로 정의됨.
	- 1변수 함수: 
    
    $$ f(x+h) - f(x) \approx f'(x)\,h	$$

	- 다변수 함수:
    
    $$ f(\mathbf{x}+\mathbf{h}) - f(\mathbf{x}) \approx (\nabla f(\mathbf{x}))^\top \mathbf{h} $$

- $\rightarrow$ 스칼라 미분에서 사용하던 방식을 다변수에도 적용 가능!
- 결론
	- 스칼라 미분:
    
    $$df=f'(x)dx$$

	- 벡터 미분:
  
    $$df=\nabla f(\mathbf{x})^\top dx$$

	- 행렬 미분:
  
      $$df=\operatorname{tr}\left( \left( \frac{\partial\,f}{\partial\,X} \right)^\top   dX\right)$$

		- 증명:
			- let $X\in\mathbb{R}^{m\times n}, f(X)\in\mathbb{R}$ 
			- $X$를 펼쳐서 벡터화 할 수 있음: $\operatorname{vec}(X)\in\mathbb{R}^{mn}$ 
			- 이제 $f:\mathbb{R}^{mn}\rightarrow\mathbb{R}$
			- 그럼, 벡터 미분에 의해,
      
          $$df=\left(\frac{\partial\,f}{\partial\operatorname{vec}(X)}\right)^\top d(\operatorname{vec}(X))$$

			- 다음 식은 직접 결과를 계산해보면 같음:
      
          $$\operatorname{tr}(A^\top B)=\operatorname{vec}(A)^\top \operatorname{vec}(B)$$

  		- 위 성질을 이용하면,
      
          $$df=\operatorname{tr}\left(\left(\frac{\partial\,f}{\partial X}\right)^\top d(X)\right)$$

			- 여기서 $\frac{df}{dX}$는 $m\times n$ 행렬로,
      
          $$\left(\frac{\partial\,f}{\partial X}\right)_{ij}=\frac{\partial\,f}{\partial X_{ij}}$$

- FYI ) 더 깊은 내용이 궁금하면 total difference 공부하기

- 합 규칙 

    $$ d(\mathbf{a}^\top \mathbf{x} + \mathbf{b}^\top \mathbf{x}) = d(\mathbf{a}^\top \mathbf{x}) + d(\mathbf{b}^\top \mathbf{x})$$

- 곱 규칙 

    $$ d(\mathbf{x}^\top A \mathbf{x}) = (d\mathbf{x}^\top)A\mathbf{x} + \mathbf{x}^\top A(d\mathbf{x})$$

- Chain Rule 

    $$ df(\mathbf{x}) = (\nabla f(\mathbf{u}))^\top d\mathbf{u}, \quad d\mathbf{u} = J_g(\mathbf{x})\,d\mathbf{x}$$ 
    
    $$ \Rightarrow\quad df(\mathbf{x}) = (\nabla f(\mathbf{u}))^\top J_g(\mathbf{x})\,d\mathbf{x}$$

### 2.1 이차형식 증명 2

$$\begin{align*}
d(\mathbf{x}^\top A\mathbf{x}) &= d\mathbf{x}^\top(A\mathbf{x})+\mathbf{x}^\top A(d\mathbf{x}) \\
&= (A\mathbf{x})^\top(d\mathbf{x})+ (\mathbf{x}^\top A)(d\mathbf{x}) \\
&=\mathbf{x}^\top(A+A^\top)(d\mathbf{x})
\end{align*}$$

$$\text{since }df=(\nabla f)^\top dx,$$

$$\nabla_\mathbf{x} (\mathbf{x}^\top A \mathbf{x})=(A+A^\top)\mathbf{x}$$

---
### 3. L2-Norm

$$f(\mathbf{x})=||\mathbf{x}||_2=\sqrt{\mathbf{x}^\top \mathbf{x}}$$

$$\nabla f(\mathbf{x})=\nabla \sqrt{g(\mathbf{x})}=\frac{1}{2\sqrt{g(\mathbf{x})}}\nabla g(\mathbf{x})=\frac{2\mathbf{x}}{2||\mathbf{x}||_2}=\frac{\mathbf{x}}{||\mathbf{x}||_2}\quad(\mathbf{x}\neq \mathbf{0})$$

- 결과는 방향벡터

---

### 4. 선형 trace 함수

$$f(X) = \operatorname{tr}(A^\top X)$$

$$\dfrac{\partial f}{\partial X} = A$$


- 증명:  직접 미분해보면 나옴


---
### 5. 선형사상

$$\mathbf{y}(\mathbf{x}) = A\mathbf{x} + \mathbf{b}$$

$$\frac{\partial \mathbf{y}}{\partial \mathbf{x}} = A$$

---
### 6. 합성 및 성분별 비선형
 - $g$는 성분별 작용할 때,

$$\mathbf{y} = g(B\mathbf{x})=g(\mathbf{z})$$

$$\dfrac{\partial \mathbf{y}}{\partial \mathbf{x}} = \dfrac{\partial \mathbf{y}}{\partial \mathbf{z}} \dfrac{\partial \mathbf{z}}{\partial \mathbf{x}}= \operatorname{Diag}(g'(B\mathbf{x}))\, B=g'(B\mathbf{x})\,\circ\,B$$

- 성분별로 작용하는 함수의 경우, $\dfrac{\partial \mathbf{y}}{\partial \mathbf{z}}$할 때, $y_i,\,z_j$의 i=j일 때만 미분했을 때 0이 아니고 나머지는 0 $\rightarrow$ Diag 형태와 같음.
- $\circ$ : Hadamard product. 행렬의 원소별 곱
	- ex. 

    $$A = \begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}, 
\quad
B = \begin{bmatrix}
5 & 6 \\
7 & 8
\end{bmatrix}$$

$$A \circ B =
\begin{bmatrix}
1 \cdot 5 & 2 \cdot 6 \\
3 \cdot 7 & 4 \cdot 8
\end{bmatrix}
=
\begin{bmatrix}
5 & 12 \\
21 & 32
\end{bmatrix}$$

$$ \text{then, }
\mathrm{Diag}(u) =
\begin{bmatrix}
u_1 & 0   & \cdots & 0 \\
0   & u_2 & \cdots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0   & 0   & \cdots & u_n
\end{bmatrix},
\quad
v =
\begin{bmatrix}
v_1 \\ v_2 \\ \vdots \\ v_n
\end{bmatrix}$$

$$\mathrm{Diag}(u)\, v =
\begin{bmatrix}
u_1 v_1 \\
u_2 v_2 \\
\vdots \\
u_n v_n
\end{bmatrix}$$

$$u \circ v =
\begin{bmatrix}
u_1 v_1 \\
u_2 v_2 \\
\vdots \\
u_n v_n
\end{bmatrix}$$

### 6.1 성분별 softmax

$$s(\mathbf{z})_i = \frac{e^{z_i}}{\sum_k e^{z_k}}$$

$$J_{ij} =
\begin{cases}
s_i(1 - s_i), & i = j, \\[6pt] - s_i s_j, & i \neq j.
\end{cases}
=\operatorname{Diag}(\mathbf{s}) - \mathbf{s}\mathbf{s}^\top$$

---
### 7. 이차 trace 형태

$$f(X) = \operatorname{tr}(X^\top A X B)$$

$$\dfrac{\partial f}{\partial X} = A X B^\top + A^\top X B$$

- 증명(트레이스 순환법칙 사용):  

$$\begin{aligned}
\mathrm{d}f
&= \operatorname{tr}(\mathrm{d}X^\top A X B) + \operatorname{tr}(X^\top A \mathrm{d}X B) \\
&= \operatorname{tr}(B^\top X^\top A^\top \mathrm{d}X) + \operatorname{tr}(B X^\top A\, \mathrm{d}X) \\
&= \operatorname{tr}\!\Big(\big( A X B^\top + A^\top X B \big)^\top \mathrm{d}X\Big) \\
&\Rightarrow \frac{\partial f}{\partial X} = A X B^\top + A^\top X B.
\end{aligned}$$

---
### 8. 행렬 내부 선형변환

$$Y = A X B + C,\;f = g(Y)$$  

$$\frac{\partial f}{\partial X} = A^\top \frac{\partial f}{\partial Y} B^\top$$

- 증명:  

$$\mathrm{d}Y = A\, \mathrm{d}X\, B$$

$$\mathrm{d}f = \operatorname{tr}\big( (\tfrac{\partial g}{\partial Y})^\top \mathrm{d}Y \big)
= \operatorname{tr}\big( B^\top (\tfrac{\partial g}{\partial Y})^\top A^\top \mathrm{d}X \big)$$

---
### 9. 역행렬 

$$d(X^{-1})=-X^{-1}(dX)X^{-1}$$

- 증명 

$$XX^{-1}=I$$

$$d(XX^{-1})=(dX)X^{-1} + X(dX^{-1})=dI=0$$

$$X(dX^{-1})=-(dX)X^{-1}$$

$$\therefore d(X^{-1})=-X^{-1}(dX)X^{-1}$$


- $d(1/x)=-(1/x^2)dx$ 와 형태 동일
- if $f(X)=X^{-1}$,

    $$\frac{\partial X^{-1}}{\partial x_{ij}}=-X^{-1}E_{ij}X^{-1}$$

	- $E_{ij}$는 $(i,j)$ 원소만 1이고 나머지는 0인 행렬

---
### FYI) Trace 관련 법칙

- 정의에 의해,

$$\operatorname{tr}(A^\top) = \operatorname{tr}(A)$$

- 순환법칙: 

$$\operatorname{tr}(AB) = \operatorname{tr}(BA)$$

$$\operatorname{tr}(ABC) = \operatorname{tr}(BCA) = \operatorname{tr}(CAB)$$

- 스칼라화: 스칼라 $s$에 대해,

$$s = \operatorname{tr}(s)$$

---
### FYI) 이차형식 trace trick으로 증명

$$\mathbf{x}^\top A\mathbf{x}=\text{tr}(\mathbf{x}^\top A\mathbf{x})=\text{tr}(A\mathbf{x}\mathbf{x}^\top)$$

- Using $d\,\text{tr}(M)=\text{tr}(dM)$, $\text{tr}(UV)=\text{tr}(VU)$, 

$$
\begin{align*}
df
&=d\,\text{tr}(A\mathbf{x}\mathbf{x}^\top) \\
&=\text{tr}(A\;d(\mathbf{x}\mathbf{x}^\top)) \\
&=\text{tr}(A\;\{(d\mathbf{x})\mathbf{x}^\top + \mathbf{x}(d\mathbf{x}^\top) \}) \\
&=\text{tr}(\mathbf{x}^\top A(d\mathbf{x}) ) + \text{tr}((d\mathbf{x}^\top)A\mathbf{x} ) \\
&=\mathbf{x}^\top A(d\mathbf{x}) + (A\mathbf{x})^\top(d\mathbf{x}) \\
&=((A+A^\top)\mathbf{x})^\top (d\mathbf{x})
\end{align*}
$$

$$\therefore \nabla_\mathbf{x}(\mathbf{x}^\top A\mathbf{x}) = (A+A^\top)\mathbf{x}$$

# References
https://atmos.washington.edu/~dennis/MatrixCalculus.pdf
https://en.wikipedia.org/wiki/Matrix_calculus
https://darkpgmr.tistory.com/141
