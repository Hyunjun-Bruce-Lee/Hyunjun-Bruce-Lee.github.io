---
layout: post
title: Isolation Forest
description: Isolation Tree (iForest)
image: 
use_math: true
ml: True
---

> Esemble - Bagging
>
> un-supervised learning (비지도 학습)
>
> anomaly detection (이상치 검출) 

### Isolation Forest 작동원리

"Decision Tree로 데이터를 학습하게 되면, 이상 데이터는 빨리 분기가 되어 leaf node에 홀로 남게 될 가능성이 높아진다."라는 아이디어를 토대로 설계된 모델이 Isolation Forest 이다.

즉 정상데이터의 경우 일정 범위 내에 모여있기에, leaf node에 홀로 남으려면 tree의 depth가 깊어지게 된다. 따라서 적정한 수준의 depth 이하의 데이터를 이상치로 취급할 수 있게 된다.

아래의 그림에서 좌측의 경우 분기 (3)에 의해 데이터가 leaf node에 홀로 남게 된다(isolated). 우측 그림의 경우 분기가 한번 더 이루어 지었고 추가로 2개의 데이터가 고립되었다. 이처럼 depth에 따라 먼저 고립되는 데이터를 이상치로 분류하는 기법이다.

<center><img src="{{ "/assets/images/Isolation_Forest/I_forest_1.PNG" | absolute_url }}" width = 'auto' height = 'auto' alt="" /></center>

실제는 Random Forest를 구성하고 isolate된 leaf node마다 anomaly score를 계산한 후 평균을 계산해서 score가 1에 가까운 데이터를 이상 데이터로 판정한다.

 

### Isolation Forest 상세 과정

Isolation Forest에서 핵심적인 역할을 하는 anomaly score는 이진검색트리(Binary Search Tree)에서 사용되는 c(n)의 개념을 차용하여 아래와 같이 계산한다. (c(n) : 이진 검색 트리에서 특정데이터의 key를 찾기위해 평균적으로 들어가는 depth)

Anomaly score가 1에 가까울수록 이상데이터일 가능성이 높고, 0에 가까울수록 정상데이터일 가능성이 높다. score가 0.5일경우 정상데이터와 이상데이터의 구분이 명확하지 않다는 의미이다.

> $$
> DATA\;(X)\;=[2, 2.5, 3.8, 4.1, 10.5, 15.4]
> $$

- 위 data에서 10.5와 15.4가 이상치라고 가정.

<center><img src="{{ "/assets/images/Isolation_Forest/I_forest_2.PNG" | absolute_url }}" width = 'auto' height = 'auto' alt="" /></center>

&nbsp;

1 - Average path length of unsuccessful search in BST(Binaty Search Tree)

> $$
> \begin{align*}
> c(n)\;&=\;2H(n-1)\;-\;\big(\frac{2(n-1)}{n}\big)\;\;\;\;\;n=num\;of\;external\;node(leaf\;node)\\
> \;\\
> H(i)\;&=\;log(i)\;+\;0.5772156649(Euler's\;constant-오일러\;상수)
> \end{align*}
> $$

&nbsp;

> $$
> With\;DATA\;(X)\\
> \;\\
> AVG\;Depth\;=\;\frac{2+2+3+3+3+3}{6}\;=\;2.67\\
> \;\\
> c(n)\;=\;2\times(log(5)\;+\;0.577)\;-\;\frac{2\times5}{6}\;=\;2.70\\
> \;\\
> \;\\
> AVG\;Depth\;\cong\;c(n)
> $$

&nbsp;

2 - Anomaly Score($s(x,n)$)

> $$
> s(x,n)\;=\;2^{-\frac{E(h(x))}{c(n)}}\;\;\;\;\;\;\;^{x\;=\;data,\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;n\;=\;num(leaf\;node)}_{h(x)\;=\;data\;x's\;path\;length\;\;\;\;E(h(x))\;=\;AVG\;of\;all\;tree's\;h(x)}
> $$

&nbsp;

> $$
> With\;DATA\;(X)\\
> \;\\
> \begin{align*}
> &s(2,n=6)\;=\;2^{-\frac{3}{2.7}}\;=\;0.46\\
> \;\\
> &s(10.5,n=6)\;=\;2^{-\frac{2}{2.7}}\;=\;0.598\\
> \;\\
> &s(15.4,n=6)\;=\;2^{-\frac{2}{2.7}}\;=\;0.598\\
> \end{align*}
> $$

이 예시의 경우 정상데이터인 2, 2.5, 3.8, 4.1과 이상치인 10.5, 15.4와의 depth가 1개 밖에 차이가 나지 않기에 위처럼 score가 명확하게 차이나지 않는다. 실제 상황의 경우 depth의 차이가 많이 날 것이다.

> $$
> E(h(x))\;\to\;c(n),\;\;s\;\to\;0.5\\
> \;\\
> E(h(x))\;\to\;0,\;\;s\;\to\;1\\
> \;\\
> E(h(x))\;\to\;n-1,\;\;s\;\to\;0\\
> $$

&nbsp;

### Practice (Python)

[Anomaly Score Check]()

[Credit Data]()

