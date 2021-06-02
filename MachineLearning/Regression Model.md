## Regression Model

## Roadmap
- [Regression Model](#Regression-Model)
- [Linear Regression Model](#Linear-Regression-Model)
- [Stepwise Fitting](#Stepwise-Fitting)
- [SVMs](#SVMs)
- [Decision Tree Model](#Decision-Tree-Model)
- [Gaussian Process Regression](#Gaussian-Process-Regression)

## Regression Model
- response variable에서 output 데이터가 숫자로 나타남
- 크게 parametric model과 nonparametric model로 나뉘어짐
- parametric model의 대표적인 것으로 Regressionn model이 있음, 수치함수 활용함
- linear Regression Model가 대표적, 수치함수를 이용해서 수치화할 수 있음, output값이 특정 공식에 의해 정해진다고 가정을 함, 다양한 predictor variable간의 상관관계를 알거나 어느정도 알고 있을 때 사용하기 좋음
- nonparametric은 알고리즘 활용, response variable을 구함, 수치함수 없어도 됨, SVM, tree, Gaussian Process Regression model이 있음, output만 정확하게 예측을 하려고 할 때만 씀

## Linear Regression Model
- predictor와 Response간의 수치함수를 아래와 같이 만드는 것, 선형화 된 함수를 만드는 것, 직선을 의미하는 것은 아님

![one](/img/MachineLearning/Regression/one.png)
![one](/img/MachineLearning/Regression/two.png)
![one](/img/MachineLearning/Regression/three.png)
![one](/img/MachineLearning/Regression/four.png)

- nonparametric model은 수치함수는 모르고 알고리즘을 통해서 알아서 진행이 됨

![one](/img/MachineLearning/Regression/five.png)

- Linear은 아래와 같이 나와야함, coefficient와 function간의 곱으로 그 총합으로 나타낸 것을 linear라고 할 수 있음

![one](/img/MachineLearning/Regression/six.png)

- exponential은 nonlinear함

![one](/img/MachineLearning/Regression/seven.png)

- 수치함수는 linear equation을 생각하고 만듬, linear equation을 생성하고 하나의 함수로 만들고 이용하면 됨
- classification과는 다르게 반드시 입력값을 테이블 형태로 넣어줘야함, 테이블 형태로 넣어주지 않으면 wilkins-Roger notation이 적용이 되지 않음, array 형태로 있어도 강제로 테이블 형태로 만드는 것이 좋음
- 우선 어떤 것이 linear한 것인지 확인할 것임
- 우선 linear 하다는 것은 아래와 같이 시그마로 정리가 가능하다 C0의 경우도 x1의 0제곱이라서 1이므로 시그마로 정리해서 표현이 가능함, 곱 값이 표현되어도 마찬가지임

![one](/img/MachineLearning/Regression/eight.png)

- 5,6번은 linear하지 못함 6번은 exponentioal 형태로 들어갔기 때문에 안됨, 그리고 5번은 b와 c가 각각 따로 들어가고 각각 product값이 엮여 있기 때문에 아님, b와 c간의 새로운 relation이 성립되기 때문에

![one](/img/MachineLearning/Regression/nine.png)

- single predictor linear model을 아래와 같이 간단하게 확인할 것임, 무조건 테이블 형태로만 만들것임, 선형 모델로 잘 나옴

![one](/img/MachineLearning/Regression/ten.png)

- 그리고 예측을 한 뒤 아래와 같이 비교를 해 볼 것임, 하나의 predictor에서는 매우 부정확하게 나옴, 전체적인 추세선 정도로만 나옴, linear를 확인했기 때문에

![one](/img/MachineLearning/Regression/eleven.png)

- 실제값은 2번째 결과와 같음

![one](/img/MachineLearning/Regression/twelve.png)

- 에러값을 표시하기 위해서는 원래는 kfoldloss와 resubloss, loss로 하였지만 이것은 조금 다름
- 각각이 얼마만큼 차이가 나는지 알려주기 때문에, 틀린 예측과 response의 차이를 반영을 해줘야함, 수치화된 loss로 나타내야함
- 아래와 같이 err을 계산을 하고 한눈에 시각화를 해야함

![one](/img/MachineLearning/Regression/thirteen.png)

- 이를 수치화하면 Mean Square Error 즉 나온 err에 대해서 마이너스 플러스는 중요하지 않으므로 제곱으로 나타낸 것의 평균값을 구함, 0 값에서 얼마나 차이가 나는지 알 수 있음

![one](/img/MachineLearning/Regression/fourteen.png)

- percentage error는 아래와 같이 알 수 있음, 정답값에서 에러 값이 얼마나 차지하는지 알 수 있음

![one](/img/MachineLearning/Regression/fifteen.png)

- 두 개의 predictor에 대해서 확인할 수 있음, 여기서 array가 아닌 table 형태로 사용해야함
- wilkinson notation을 쓰는 것이 훨씬 더 간편하기 때문에
- 2개의 데이터를 아래와 같이 파악하고 사용함, 테이블 형태로 넣어줘야함

![one](/img/MachineLearning/Regression/sixteen.png)

- 하지만 2개의 regression type이 같은 방식으로 입력되지 않아서 에러가 뜸

![one](/img/MachineLearning/Regression/seventeen.png)

- 그래서 테이블 타입으로 입력하라는 것이 의미하는 것은 마지막 칼럼은 항상 Response data이므로 아래와 같이 처리해야함
- 테이블 타입으로 통으로 넣는것을 원칙으로함, array 타입은 일일이 파악해서 처리해줘야함

![one](/img/MachineLearning/Regression/eighteen.png)

- 하나 이상일 경우 무조건 테이블 타입으로 넣어주는 것이 좋음, 단일 predictor에도 마찬가지로 하는 것이 좋음, 통일성을 위해서

![one](/img/MachineLearning/Regression/nineteen.png)

- 예측값 역시 테이블로 묶어서 나타냄

![one](/img/MachineLearning/Regression/twenty.png)

- plot을 보기 위해서 2x2로 볼 것임
- 설명대로 observation을 확인하고 실제 값과 predict 값을 그리고 45-degree 정답값을 그려주고 비교를 분포와 함께 보고 에러의 분포와 percentage 에러를 그려줄 수 있음
- 여기서 num2str을 통해서 제목을 달 수 있음

![one](/img/MachineLearning/Regression/twentyone.png)

- 이를 한 눈에 볼 수 있게끔 function 형태로 만들 수 있음
- predictor를 다 포함해서 linear regression model을 만들 수 있음, 이를 function 형태로 스크립트에 저장함
- evaluatefit이라는 함수를 통해서 위에서 한 작업을 다 할 수 있음, 여러개의 predictor를 사용하여 linear regression model을 확인하는 것을

![one](/img/MachineLearning/Regression/twentytwo.png)

- 모든 predictor를 사용해서 모델을 만들 수 있음 아래와 같이

![one](/img/MachineLearning/Regression/twentythree.png)

- 옵션을 RobustOpts 노이즈 생성시 outliers 바깥으로 빠진 값을 자연스럽게 배제하는 옵션임
- on을 사용해도 되고 cauchy를 사용해도 됨, 각각의 알고리즘과 수식이 정해져 있음

![one](/img/MachineLearning/Regression/twentyfour.png)

## Stepwise Fitting
- Sequential Feature Selection과 유사함, 더 간단한 모델이기도 함

![one](/img/MachineLearning/Regression/twentyfive.png)

- evaluation function 대신에 기준을 가지고 선택을 함, 속도가 더 빠름
- 아래와 같이 쓴다면 그에 맞춰서 학습을 하여서 결과를 도출함, 학습을 하는데 시간이 좀 걸림

![one](/img/MachineLearning/Regression/twentysix.png)

- 여기서 정밀도 문제가 나타나는데 기준을 바꿔서 모델을 학습할 수 있음
- Upper limit을 정하는 것, 어디까지 갈 건지 interaction을 넣어줄 수 있고 다른 옵션도 가능함
- 크기 자체는 비슷하게 나옴, 기본 default보다는 낮아짐을 알 수 있음
- 몇 가지 기준을 정하고 구동시킬 수 있음, aic, bic등, Sequential Feature selection과 비교해봐도 좋음

![one](/img/MachineLearning/Regression/twentyseven.png)


## SVMs
- Nonparametric Models
	- 수치함수를 생성하지 않고 결과만을 예측을 함
- SVMs은 classification model과 방법이 동일함, 아래와 같이 사용하면 됨
- table 형식으로 넣는것을 추천함

![one](/img/MachineLearning/Regression/twentyeight.png)

- 아래와 같이 loss를 확인할 수 있음 이전에 사용한 evaluatefit 함수 사용함

![one](/img/MachineLearning/Regression/twentynine.png)

- 여기서 그대로 loss 함수를 써도 상관없으나 mean 값만 보면 의미가 없음, 그 분포를 봐야함, 값만 뽑아서는 의미가 없음
- 정규화를 하지 않았다면 아래와 같이 정규화 옵션을 사용하면 됨
- 그리고 아래와 같이 Gaussian을 kernelfunction에서 활용해도 됨

![one](/img/MachineLearning/Regression/thirty.png)

- Gaussian을 사용하면 전체적으로 값이 높아짐을 알 수 있음

## Decision Tree Model
- 아래와 같이 Decision Tree 역시 동일하게 사용할 수 있음
- 값이 매우 크게 나옴을 알 수 있음, 이를 해결하기 위해서 prune을 활용

![one](/img/MachineLearning/Regression/thirtyone.png)

- 아래와 같이 prune과 leaf size를 줄여줄 수도 있음, 하지만 크게 차이는 없음

![one](/img/MachineLearning/Regression/thirtytwo.png)

- parametric은 predictor의 관계들을 명확하게 알고 있을 때 좋고 직접 시간을 쏟아서 체크를 할 때 수치를 직접 낮추는데 상관관계를 알기 좋음
- 결과만 알고 싶다면 nonparametric이 훨씬 더 좋음

## Gaussian Process Regression
- 확률분포(정규분포)를 점에 대해서 늘리는 것이 아닌 function으로 늘려서 아래와 같이 확대해서 Regression model에 적용하는 것임

![one](/img/MachineLearning/Regression/thirtythree.png)

- 3차원의 predictor가 있다고 할 때, 점이 나타내어 지는 것을 아래와 같이 함수로 확대를 하는 것임, 매우 정확함
- 새로운 observation이 들어왔을 때 어느 정도의 확률로 어떤 분포내의 값이 어느정도 사이값으로 들어오는지도 보여줌, prediction interval 거의 95%를 사용함, 어디 사이의 95%확률로 여기 안에 떨어진다고 하는 그 범위값(interval)을 주어지고 그게 predict에 예측이 됨
- 각각의 predictor 값을 response로 찍고 아래와 같이 function이 생김

![one](/img/MachineLearning/Regression/thirtyfour.png)

- predictor가 많으면 많을수록 더 촘촘한 간격이 아래와 같이 생기고 function이 점점 더 정교해짐
- predictor가 많을수록 정확한 결과를 알려줌
- kernelfunction에 의해서 smooth함을 정할 수 있음

![one](/img/MachineLearning/Regression/thirtyfive.png)

- 이것도 역시 mean function covariance function이 아래와 같이 존재함

![one](/img/MachineLearning/Regression/thirtysix.png)

- 하지만 여기서 covariance function의 경우 정해지는 kernelfunction에 의해서 아래와 같이 정할 수 있음, 각 predictor의 간격을 서로 조절함으로써 전체적인 basis function들의 모양을 결정할 수 있음
- kernelfunction에 매우 영향을 크게 받음

![one](/img/MachineLearning/Regression/thirtyseven.png)

- 그리고 다양한 observation을 기준으로 아래와 같이 생기는데 여기서 하나를 기준으로 prediction interval이 형성이 됨
- 하나의 새로운 값이 들어왔을 때 다양한 예측이 있는데 아래와 같이 interval이 형성이 됨

![one](/img/MachineLearning/Regression/thirtyeight.png)

- 아래와 같이 사용할 수 있음, 3개의 Output값이 나옴
- econStd는 받지 않아도 됨

![one](/img/MachineLearning/Regression/thirtynine.png)

- 여기서 econInt가 95% 확률로 어떻게 되는지 subplot의 첫번째 칸에 같이 표현할 수 있음
- upper limit과 lower limit을 아래와 같이 정해줄 수 있음

![one](/img/MachineLearning/Regression/fourty.png)

- 다른 kernel을 활용할 수 있음, 아래와 같이 matern kernel을 활용할 수 있음

![one](/img/MachineLearning/Regression/fourtyone.png)

- ard라는 다른 kernel도 활용할 것임, 아래와 같이
- ARD(Automatic Relevance Determination), Predictor의 간격을 일정하게 하는 것이 아니고 각각 predictor 알고리즘에 의해서 상대적으로 정해줌 어떤건 넓게 적게 표현을 해 줌, length scale이 다 다름
- tic - toc을 활용해서 시간이 얼마나 걸리는지 알 수 있음

![one](/img/MachineLearning/Regression/fourtytwo.png)
