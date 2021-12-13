---
layout: post
title: Gradient Boosting
description: Gradient Boosting(Regression & Classification)
image:
use_math: true
ml: True
---

> - Esemble - Boosting
> - 잔차(residual) 학습



### Gradient Boosting(Regression) 작동 원리

Gradient Boosting은 여러개의 의사결정 나무를 이용하여 회귀 혹은 분류 문제를 해결하는데 사용되는 기법이며, 여러개의 동일 모델을 사용한다는 점에서 Esemble의 Boosting 계열에 속한다.

Gradient Boosting은  leaf node의 평균값을 이용하여 residual(잔차)를 줄여나가며 학습을 한다.

 학습을 완료한 후, 새로운 데이터에대한 추정의 경우 학습된 여러 개의 트리의 residual과 기존 학습데이터의 평균값을 이용하여 추정을 진행한다.



### Gradient Boosting (Regression) 상세 학습 과정 

<center><img src="{{ "/assets/images/G_Boosting_0.PNG" | absolute_url }}" width = 'auto' height = 'auto' alt="" /></center>



**아래에서 weight가 target값이며 0.1의 학습율(learning rate)을 가질 경우 다음과 같은 방법을 $residual(N)$이 충분히 작아질때까지 N회 반복하여 학습을 진행한다.**

1. $residual(0)$을 계산한 후, 계산한 $residual(0)$에 대하여 Decision Tree(1)을 생성한다.

<center><img src="{{ "/assets/images/G_Boosting_1.PNG" | absolute_url }}" width = 'auto' height = 'auto' alt="" /></center>

2. 생성한 Decision Tree(1)를 이용하여 새로운 residual(1)을 계산한다. 

<center><img src="{{ "/assets/images/G_Boosting_2.PNG" | absolute_url }}" width = 'auto' height = 'auto' alt="" /></center>

3. 계산된 $residual(1)$을 이용하여 Decision Tree(2)를 생성한다.

<center><img src="{{ "/assets/images/G_Boosting_3.PNG" | absolute_url }}" width = 'auto' height = 'auto' alt="" /></center>

3. $residual(1)$과 Tree(2)를 이용하여 새로운 $residual(2)$를 계산한다.

<center><img src="{{ "/assets/images/G_Boosting_4.PNG" | absolute_url }}" width = 'auto' height = 'auto' alt="" /></center>

**신규 데이터 추정 방법**

다음과 같은 신규 데이터가 존재할경우, 다음과 같이 residual을 줄이는 과정에서 생성된 Tree들에 신규데이터를 대입하여 신규데이터에 대한 각트리의 잔차 추정치를 얻은 후, 최종 추정치를 계산하게 된다.

<center><img src="{{ "/assets/images/G_Boosting_5.PNG" | absolute_url }}" width = 'auto' height = 'auto' alt="" /></center>

- 단 실제 모델링의 경우 예시처럼 잔차의 계산이 3회로 끝나는 것이 아니다(잔차가 충분히 작아질 떄까지 훈련을 진행해야 한다). 



**Gradient Boosting (Regression) 학습과정(수식)**

**step 1**
$$
\begin{align*}
&INPUT\;:\;Data\;\{x_i,y_i\}_i^n\;and\;differentiable(미분가능한)\;loss\;function\;L(y_i,F(x))\\
\;\\
&Step\;1:\;Initialize\;Model\;with\;a\;constant\;value\\
\end{align*}
$$

$$
F_0(x)\;=\;argmin\sum_i^nL(y_i,\gamma)\\
\gamma\;:추정치(\hat{y})\;\;\;\;F_0(x)\;:\;초기추정치
$$

**step 1 with data**
$$
\begin{align*}
y=&\{88,76,56,73,77,57\}\;\;\;\;\;\;\;L(y,\hat{y})(loss\;function)=\frac{1}{2}(y-\hat{y})^2\\
\;\\
&\frac{\partial}{\partial\gamma}\bigg(\frac{1}{2}(88-\gamma)^2+\frac{1}{2}(76-\gamma)^2\cdots+\frac{1}{2}(57-\gamma)^2\bigg)\;=\;0\\
\;\\
&-(88-\gamma)-(76-\gamma)\cdots-(57-\gamma)\;=\;0\\
\;\\
&\gamma\;=\;\frac{88+76\cdots+57}{6}\;=\;71.2\\
\;\\
&F_0(x)\;=\;71.2
\end{align*}
$$
**step 2** (A~D)
$$
for\;m=1\;to\;M\;(residual을\;줄이기위해\;아래의\;A\;to\;D를\;\;M회\;반복연산)\\
$$
**2-A** : Compute so-called pseudo-residuals (데이터들에 대한 잔차를 계산한다.)
$$
\begin{align*}
r_{im}\;=\;-\bigg[\frac{\partial L(y_i,F(x_i))}{\partial F(x_i)}\bigg]\;\;\;\;\;\;\;\;\;_{F(x)\;=\;F_{m-1}(x)}^{for\;i\;=\;1,\cdots,n}
\end{align*}\;\;\;\;\;\;\;\;(r_{im\;:\;i번째\;데이터의\;m회차\;잔차})
$$
​	**2-A** with data
$$
\begin{align*}
&when\;m=1\;(1회차\;반복)\\
\;\\
&r_{1,1}\;=\;-\frac{\partial L(y_1,F_0(x_1))}{\partial F_0(x_1)}\;=\;-\frac{1}{2}\frac{\partial}{\partial F_0(x_1)}(y_i-F_0(x_1))^2\;\\
\;\\
&\;\;\;\;\;\;=\;y_i-F_0(x_1)\;=\;88\;-\;71.2\;=\;16.8\;\to\;(i=1: 첫번째\;데이터의\;residual)\\
\;\\
&\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\vdots\\
\;\\
\;\\
&r_{i,1}\;=\;\{16.8,\;4.3,\;-13.7,\;1.4,\;5.4\}\;\leftarrow\;1회차의\;모든\;데이터에대한\;residual
\end{align*}
$$


**2-B** : Fit a regression tree to the $r_{im}$ values and create terminal regions  $R_{jm},\;for\;j=1 \cdots J_m$ (계산된 잔차들을 기준으로 회귀나무를 전개하여 최종영역을 도출한다.)

<center><img src="{{ "/assets/images/G_Boosting_6.PNG" | absolute_url }}" width = 'auto' height = 'auto' alt="" /></center>

**2-C** : for $j = 1 \cdots J_m$ compute (분기된 나무의 최종 영역에 대하여 연산을 진행한다. data A가 R1,1의 영역에 속하게된다면, $\gamma_{jm}$값으로 취급한다.)
$$
\gamma_{jm}\;=\;\underset{\gamma}{argmin}\sum_{x_i\in R_{ij}}L(y_i,F_{m-1}(x_i)+\gamma)
$$
​	**2-C** with data
$$
\begin{align*}
\gamma_{1,1}\;\to\;&\frac{1}{2}\frac{\partial}{\partial\gamma}[(57-71.2-\gamma)^2+(56-71.2-\gamma)^2]\;=\;0\\
\;\\
&\frac{1}{2}\frac{\partial}{\partial\gamma}[(-14.2-\gamma)^2+(-15.2-\gamma)^2]\;=\;0\\
\;\\
&14.2\;+\;\gamma\;+15.2\;+\;\gamma\;=\;0\;\to\;\gamma\;=-14.7\;=\gamma_{1,1}
\end{align*}
$$
**2-D** : Update the model
$$
F_m(x)\;=\;F_{m-1}(x)\;+\;\alpha\sum_{j=1}^{J_m}\gamma_{jm}I(x\in R_{jm})\;\;\;\;\;\;\;\;\alpha = training\;rate
$$



### Practice (Python)

[Boston Data](https://github.com/Hyunjun-Bruce-Lee/ML_study/blob/master/XGBoost/XGBoost(regression).py)

