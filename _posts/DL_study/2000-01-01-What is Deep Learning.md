---
layout: post
title: Deep Learning intro
description: What is Deep Learning?
image:
dl: True
---

### What is Deep Learning?

딥러닝은 머신러닝에 포함되는 개념으로 인간의 신경망이 모방되어 적용된 머신러닝을 의미한다.

딥러닝은 1900년대에 최초로 소개된 단층 퍼셉트론에서 출발한다. 단층 퍼셉트론은 XOR연산의 한계를 극복하기 위하여 다층퍼셉트론으로 발전하게되었으며, 다층퍼셉트론에 Weight(가중치)와 Bias(편향)설정의 한계를 해결하는 Back Propagation(오차 역전파)기법이 더해고, Activation Function(활성함수)의 개념이 더해지면서 현재의 딥러닝의 구조를 확립하였다.

1990년대에 들어서며 실생활 문제의 데이터의 구조가 복잡해지면서 기울기소실, 실제 최적값이 아닌 일시적 최적값에서 학습을 중단하는 등의 알고리즘적인 문제와 컴퓨터 자원의 한계로인하여 학습시간이 너무나도 길게 소요된다는 점등의 이유로 점차 사장되어가기 시작했다.

그러나 2000년대에 점어들며 다양한 비선형함수를 이용한 기울기 소실문제의 해결법이 연구되고, 컴퓨터 하드웨어 기술의 발전 등의 긍정적 요인으로 인해  현재의 딥러닝이 갖는 위상을 갖게 되었다.



### Deep Learning HOW?

앞서 언급되었듯이 딥러닝은 인간의 신경망을 모방한 머신러닝으로 인간의 신경망과 유사한 구조를 갖는다. 인간의 신경세포는 수상돌기로 받아들이 외부의 전달물질을 세포체에 저장하고, 자신의 용량을 넘어서면 축색돌기를 통해 외부로 전달물질을 내보낸다고 알려져 있으며 구조는 다음과 같다.

<center><img src="{{ "/assets/images/DL_INTRO/DL_INTRO_1.PNG" | absolute_url }}" width = 'auto' height = 'auto' alt="" /></center>

딥러닝에서는 이러한 신경세포의 구조를 모방하여 모델을 설계하며, 신경세포의 집합이 모델을 이룬다는 점에서 이러한 모델을 인공신경망 모델 이라고 부른다.  (인공신경망이 깊어지는 경우 이를 심층 신경망(Deep Neural Network)이라고 부른다.)

<center><img src="{{ "/assets/images/DL_INTRO/DL_INTRO_2.PNG" | absolute_url }}" width = 'auto' height = 'auto' alt="" /></center>

- 단층 퍼셉트론
  - 단일신경 1개(Activation Function 제외)로만 이루어짐
- 다층 퍼셉트론 
  - 복수개의 단일신경(Activation Function 제외)이 연결되어 구성됨
- 인공신경망
  - Activation Function을 포함한 단일신경이 연결되어 구성됨



위 그림의 구조를 이용하는 딥러닝은 학습을 진행하며 weight(가중치)를 개선해 나가간다. 가중치는 데이터가 각뉴런간 간선을 통과할때 곱해지는 변인으로 다음과같은 형태로 계산된다.

<center><img src="{{ "/assets/images/DL_INTRO/DL_INTRO_3.PNG" | absolute_url }}" width = 'auto' height = 'auto' alt="" /></center>

> $$
> \begin{align*}
> Point\;A\;:\;X_1\times w_1&\;+\;X_2\times w_2\;+\;X_3\times w_3\;+\;b\\
> \;\\
> &\sum_{i=1}^nX_iw_i\;+\;b
> \end{align*}
> $$



이후 다양한 활성함수 중 한가지를 통화하여 다음 뉴런에게 계산된 정보를 전달해주거나 최종 출력값으로 계산된 정보를 반환 한다. (아래의 예시 활성함수 = Sigmoid)

> $$
> Point\;B:\;\frac{1}{1+e^{(-Point\;A)}}
> $$

&nbsp;

가중치의 개선은 데이터를 모델에 정방향으로 통과시키는 Foeward Propagation(순전파)와 Back propagation(역전파)를 통하여 이루어진다. 

순전파의 경우 주어진 입력값을 토대로 위의 계산을 모델이 끝날때까지 전개해나가는 것을 의미하며, 역전파의 경우 순전파를 통해 최종적으로 도출된값에 지정된 오차 함수(Loss Function)를 통해 오차를계산하여 해당 오차를 역방향으로 전달하며  줄이도록 가중치를 갱신하는것을 의미한다. 실제 가중치의 개선은 역전파 과정에서 이루어진다.

순전파와 역전파를 충분히 반복하게되면, 모델은 주어진 문제에 대한 답을 도출하는데 최적의 상태가 되고, 이때 훈련을 종료한다. (단, 과적합의 가능성이 있기에 이를 주의해야한다.  무조건 정확도가 높다고 좋은것은 아니다. $\to$ Cross Validation을 통하여 개선가능)

&nbsp;

### Back Propagation(역전파)

<center><img src="{{ "/assets/images/DL_INTRO/DL_INTRO_4.PNG" | absolute_url }}" width = 'auto' height = 'auto' alt="" /></center>

역전파는 엄밀히 말하면 Error Back Propagation이다. 순전파를 통해 도출된 최종 예측값과 실제 값간의 차이(Error)를 지나온 과정에 전달하며 가중치에 이를 반영하는 것을 통해 Error를 최소화하는 과정이다.  이 과정은 Optimizer(최적화 알고리즘)를 기반으로 이루어지며, Optimizer에 따라 전달된 에러가 특정 단계에 미치는 영향(가중치의 변화)이 달라진다. ([What is Optimizer?]()) 이때 전달된 에러를 기준으로 기존의 가중치를 얼마나 변화시킬지는 학습률(Learning Rate)에 의하여 결정된다. 

 &nbsp;

#### 수식으로 보는 Back Propagation

하나의 신경망 모델의 다음과 같은 수식처럼 여러 함수들이 합쳐진 합성함수로 볼 수 있다.(함수가 적용된 출력이 다음 함수의 인자로 전달됨)

<center><img src="{{ "/assets/images/DL_INTRO/DL_INTRO_5.PNG" | absolute_url }}" width = 'auto' height = 'auto' alt="" /></center>

> $$
> \hat{y}\;=\;sigmoid(W_3\cdot sigmoid(W_2\cdot sigmoid(W_1\cdot x+b_1)+b_2)+b_3)
> $$

이는 해당 신경망에 연쇄 법칙(Chain Rule)을 적용할 수 있다는 의미이다. 

- Chain Rule : 합성함수의 미분은 해당 함수를 구성하는 개별 함수(미분 가능 해야함) 미분의 곱으로 나타낼 수 있음

- > $$
  > t\;=\;3x\;\;\;\;\;\;\;z\;=\;t^2\\
  > \;\\
  > \frac{\partial z}{\partial x}\;=\;\frac{\partial z}{\partial t}\cdot\frac{\partial t}{\partial x}
  > $$

- 이는 $x$가 변화했을때 $t$가 얼마나 변화하는지, $t$가 변화된 것이 $z$를 얼마나 변화시키는지를 알 수 있다는 의미이다.(미분 = 기울기 도출 = 변화량 도출)

- 즉 위식에서 좌변의 값(x에대한  z의 변화량)은 t에대한 z의 변화량과 x에대한 t의 변화량으로 표현된다는 것이다. 

Chain Rule의 이러한 특성을 이용하여 최종출력값에 각 노드들이 얼마만큼의 영향을 미쳤는지를 구할 수 있다.

&nbsp;

다음과 같은 신경망이 있을때 Chain Rule에 기반한 역전파는 다음과 같이 이루어 진다. 

<center><img src="{{ "/assets/images/DL_INTRO/DL_INTRO_6.PNG" | absolute_url }}" width = 'auto' height = 'auto' alt="" /></center>

- 초기의 bias와 weight를 임의로 설정한후 순전파를 진행한다.

> $$
> w_1\;,\;w_2\;,\;w_3\;,\;w_4\;,\;w_5\;=\; 0.3\;,\;0.2\;,\;0.1\;,\;0.5\;,\;0.6\\
> w_6\;,\;w_7\;,\;w_8\;,\;w_9\;,\;w_{10}\;=\;0.2\;,\;0.4\;,\;0.3\;,\;0.2\;,\;0.5\\
> $$

> $$
> \begin{align*}
> st_{11}\;&=\;x_1\times w_1 +x_2\times w_3\;=\;0.997762\\
> st_{12}\;&=\;x_1\times w_2 +x_2\times w_4\;=\;0.989013\\
> \;\\
> st_{21}\;&=\;st_{11}\times w_5 +st_{12}\times w_7\;=\;0.729929\\
> st_{22}\;&=\;st_{11}\times w_6 +st_{12}\times w_8\;=\;0.621579\\
> \;\\
> \hat{y}\;=\;st_{3}\;&=\;st_{21}\times w_9+st_{22}\times w_{10}\;=\;0.612248\\
> \end{align*}
> $$

&nbsp;

- loss function(손실함수)를 이용하여 error를 구한다.

> $$
> loss\;function\;=\;MSE\;=\;\frac{1}{n}(y-\hat{y})^2
> $$

> $$
> error = (0.9 - 0.612248)^2\;=\;0.0828006
> $$

&nbsp;

- Chain Rule을 이용하여 에러를 역전파 한다.
  - $w_9$에 대한 역전파($w_9$가 오차에 얼마나 기여하였는지 계산)

> $$
> \frac{\partial Error}{\partial w_9}\;&=\;\frac{\partial Error}{\partial st3_{out}} \times \frac{\partial st3_{out}}{\partial st3_{in}} \times \frac{\partial st3_{in}}{\partial w_9}\\
> $$

> $$
> \begin{align*}
> \frac{\partial Error}{\partial st3_{out}}\;&=\;-2\times \frac{1}{1}(y\;-\;\hat{y})^{2-1}\\
> \;\\
> &=\;-2\times(0.9\;-\;0.612248)\;=\;-0.575504\\
> \;\\
> \frac{\partial st3_{out}}{\partial st3_{in}}\;&=\; st3_{out}\times(1-st3_{out})\\
> &=\;0.612248\times(1-0.612248)\;=\;0.237400\\
> \;\\
> \frac{\partial st3_{in}}{\partial w_9}\;&=\;st_{21}\;=\;0.729929
> \end{align*}
> $$

- 계산된 $w_9$의 기여도와 학습률을 이용하여 새로운 $w_9$을 구한다. (learning rate = $\alpha$ = 0.3)

> $$
> w_9^{new}\;=\;w_9-\alpha \frac{\partial Error}{\partial w_9}\;=\;0.2-0.3\times(-0.575504\times 0.237400\times 0.729929)\;=\;0.237479
> $$

- 순전파를 진행한 후, 위의 과정을 모든 가중치에 대하여 수행한 것을 1 iteration을 수행하였다고 한다.

&nbsp;

- 갱신된 $w_9$을 반영하여 출력값을 다기 계산해보면, 오차가 이전보다 감소함을 확인 할 수 있다.
  - 실제로는 $w_9$만 갱신하는것이 아닌 모든 $w$에대하여 갱신을 진행해야한다.

> $$
> \begin{align*}
> st_{11}\;&=\;x_1\times w_1 +x_2\times w_3\;=\;0.997762\\
> st_{12}\;&=\;x_1\times w_2 +x_2\times w_4\;=\;0.989013\\
> \;\\
> st_{21}\;&=\;st_{11}\times w_5 +st_{12}\times w_7\;=\;0.729929\\
> st_{22}\;&=\;st_{11}\times w_6 +st_{12}\times w_8\;=\;0.621579\\
> \;\\
> \hat{y}\;=\;st_{3}\;&=\;st_{21}\times w_9^{new}+st_{22}\times w_{10}\;=\;0.618723\\
> \end{align*}
> $$

> $$
> previous\;error = (0.9 - 0.612248)^2\;=\;0.0828006\\
> \;\\
> current\;error = (0.9 - 0.618723)^2\;=\;0.079116
> $$







