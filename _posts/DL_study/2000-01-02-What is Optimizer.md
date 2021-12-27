---
layout: post
title: What is Optimizer?
description: What is Optimizer?
image:
dl: True
---



### 용어 설명

**Epoch**

- 전체 데이터셋을 한번 훈련시키는것을 의미한다.
- 즉 100개의 데이터가 있다면 100개의 데이터를 전부 한번씩 모델에 반영한 것을 의미한다.

&nbsp;

**Batch**

- 배치(Batch)는 한번의 Iteration(반복 : 순전파 $\to$ 역전파)에 사용되는 데이터의 집합이다.

- 즉 100개의 데이터를 5개씩 20개로 나누게 되면  Batch size는 20이 되며 1Epoch당 5번의 Iteration을 수행하게된다.

- 신경망에서의 계산은 행렬을 기반으로 수행되기에 배치크기는 다음과 같이 설명될 수 있다.(12개의 feature를보유하는 100개의 데이터를 토대로 결과가 참인지 거짓인지 계산하는 경우 1epoch당 iteration의 수)

- > $$
  > No\;Batch : (1,12)\to(1,6)\to(1,3)\to(1,1)\;:1\;epoch=\;100\;iteration(1\times100=100)\\
  > \;\\
  > With\;Batch(size=20)\;:\;(20,12)\to(20,6)\to(20,1)\;:\;1\;epoch=5\;iteration(5\times 20=100)
  > $$

- 

<center><img src="{{ "/assets/images/DL_INTRO/DL_INTRO_4.PNG" | absolute_url }}" width = 'auto' height = 'auto' alt="" /></center>

&nbsp;

**Loss Function(손실함수)**

- 모델이 최종적으로 도출한 값과 실제 값간의 차이를 정량적으로 측정하는 함수
- 모델의 예측값이 얼마나 정확한지를 판단하는 척도

&nbsp;

**Gradient Descent**

<center><img src="{{ "/assets/images/DL_INTRO/DL_INTRO_5.PNG" | absolute_url }}" width = 'auto' height = 'auto' alt="" /></center>

- weight(가중치)에대한 편미분을 통하여 에러를 줄일수 있는 방향(기울기)를 도출하고, 계산된 방향에 학습률을 곱하여 가중치를 수정해나감으로서 모델의 오차를 최소화 시키는 방법.
- 즉 미분을 총하여 목적지에 도달하기위한 방향을 구하고, 그 방향으로 학습률 만큼 전진하는것을 목적지에 도달할 때 까지 반복하는것.

- Gradient Descent는 목표(Loss의 최소화)에 도달할 수 있다는 것은 확실하다. 그러나, 오차를 최소화 하는 방향으로 한번 전진을 하기 위해서 모든 데이터를 반영해야한다는 단점이 있다. (1epoch당 시간이 오래걸림) 

&nbsp;

**Stochastic Gradient Descent**





**Mini-batch Stochastic Gradient Descent**





