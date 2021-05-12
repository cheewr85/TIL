## Improving Predict Models

## Roadmap
- [Cross Validation](#Cross-Validation)
- [Hyperparameter optimization](#Hyperparameter-optimization)

## Cross Validation
- update model, 모델을 개선하는 작업, loss를 낮추고 accuracy를 높이고 complexity를 낮추고, 일반화 시키기 위해서
- 나오는 결과에 따라서 다름, 상황에 따라서 써야하는 방법론이 다름, Ensemble, Hyperparameter는 거의 무조건 씀

![one](/img/MachineLearning/Improving/one.png)

- 모델을 evaluation 하는 도구, 이를 바탕으로 이 피드백을 가지고 Hyperparameterr optimization을 실행함
- 기존 작업에서는 Training과 Validation을 비율을 나눠서 계산을 함, 하지만 이 나눈 비율이 일반화해서 보기 힘듬, 편향적일 수 있음

![one](/img/MachineLearning/Improving/two.png)

- 이러한 편향을 막고 일반화된 형태로 data set을 나누기 위해서 kfold 방식을 사용함, 아래와 같이 데이터를 나눈뒤 돌아가면서 validation set을 사용하고 training set을 그 나머지로 사용해서 씀

![one](/img/MachineLearning/Improving/three.png)

- 그리고 각각 계산한 loss를 합쳐서 평균값으로 k-fold loss로 나옴

![one](/img/MachineLearning/Improving/four.png)

- 기존에 쓰던 Holdout과 비교하여 아래와 같이 k-fold를 통해서 각각의 데이터를 하나씩 사용함
- k가 크면 클수록 일반화해서 계산할 수 있는 loss율이 나오는 것은 맞음
- k-fold는 holdout과 비교했을 때 holdout은 fitting된 모델을 기준으로 predict가 가능하지만 k-fold는 predict method가 없음, 즉 예측을 할 수가 없음, 그래서 Hyperparameter Optimization을 같이 사용함

![one](/img/MachineLearning/Improving/five.png)

- 이전의 실습한 내용의 결과를 table로 확인하고 그 다음 kFoldLoss에 대해서 zeros를 추가함, 여기서 pruned tree는 cross validation이 되지 않으므로 제거함

![one](/img/MachineLearning/Improving/six.png)

- 그리고 validation 데이터에 대해서 partition을 나누고 그 부분을 KFold로 나눠서 계산함

![one](/img/MachineLearning/Improving/seven.png)

- 우선 Holdout 방식을 통해서 training과 validation이 있는 data와 20%의 test data를 나눌 것임

![one](/img/MachineLearning/Improving/eight.png)

- 그 다음 training + validation data에 대해서 Holdout 방식으로 나눈 뒤 모델을 진행함
- 파란색이 클수록, 빨간색은 작을수록 좋음
- 아래와 같은 방식으로 HoldOut을 통해서 튜닝을 통해서 모델을 수정함

![one](/img/MachineLearning/Improving/nine.png)

- predict를 통해서 Holdout으로 나눈 80%에서 새로운 데이터 20%를 가지고 모델을 가지고 예측을 할 수 있음

![one](/img/MachineLearning/Improving/ten.png)

- holdout 방식에서는 아래와 같이 knn에 대해서 training data를 가지고 기본값으로 loss를 평가하고 NumNeighbors 방식으로 그 loss를 건드릴 수 있음
- 근데 kfold의 경우 training data가 아닌 전체 데이터를 집어넣음, training, validation data set을 서로 교차되어 있으므로 전체 데이터에서 cvpartition으로 나눈 것을 가지고 그것을 집어넣어 결과를 봐주면 됨
- partition을 나누는 것은 똑같으나 training, validation을 교차적으로 사용하기 때문에 전체 데이터를 넣어서 cvpartition을 통해서 나누어서 넣어서 kFold를 사용했다는 것을 보여주면 됨

![one](/img/MachineLearning/Improving/eleven.png)

- 에러를 확인하기 위해서는 다른 방식을 써야함 기존의 resubLoss, loss는 의미가 없는 것임, training과 validation이 혼재되어 있기 때문에 사용을 못함, 나누지 않았으므로
- kfoldLoss를 활용해야함, kfold는 kfold로만 가지고 loss를 계산하면 됨

![one](/img/MachineLearning/Improving/twelve.png)

- 하지만 아래와 같이 kfold 방식은 예측을 할 수가 없어서 에러가 뜸
- kfold는 전체 데이터에 대한 일반화된 데이터를 보여줄 수 있는 강점이 있을 뿐 예측은 안됨
- 그래서 kfold를 다른것과 같이 사용함

![one](/img/MachineLearning/Improving/thirteen.png)

## Hyperparameter optimization
- parameter값을 automation 알고리즘으로 자동으로 optimization을 해 줌
- 모델 내부 설정을 하는 것임, Hyperparameter는 parameter 중의 하나로써 학습이 시작되면 변하지 않는 값임
- Holdout 방식을 먼저 사용해서 써볼 것임, 일반화되지 않게 나누어지지 않는 경우 Hyperparameter를 써도 정확도는 떨어짐, 그래서 kfold 방식을 쓰면 성능이 극대화됨 그래서 같이 씀

![one](/img/MachineLearning/Improving/fourteen.png)

- 위를 기준으로 Hyperparameter 적용시 그리고 kfold를 써서 적용시를 비교해볼 것임
- 학습하는데 가장 오래 걸리는 것이 Hyperparameter임, 컴퓨터가 계산을 다 해주기 때문에
- 아래와 같이 Hyperparameter를 사용하고 auto로 설정함, auto로 설정시 knn에서 NumNeighbors와 Distance에 대해서 Optimize를 함
- 아래와 같은 방식으로 학습을 하고 최적의 값을 확인함

![one](/img/MachineLearning/Improving/fifteen.png)
![one](/img/MachineLearning/Improving/sixteen.png)
![one](/img/MachineLearning/Improving/seventeen.png)

- 여기서 위에서 연산한 최선의 값을 다 뽑을 수 있음

![one](/img/MachineLearning/Improving/eighteen.png)

- 단순히 계산한 knn과 비교해서 loss 값을 비교할 수 있음, 정확도가 더 높아졌음을 알 수 있음

![one](/img/MachineLearning/Improving/nineteen.png)

- 여기서 kfold를 사용할 때 Optimization Options을 활용해서 쓸 수 있음, 이 옵션을 활용하기 위해서 struct array를 만들어서 활용함
- 여기서 기존에 사용한 kfold와는 다르게 training data만을 이용하는데 그 이유는 먼저 holdout 방식으로 training과 validation을 나눈뒤 해당 방식을 다시 trdata에 대해서 kfold를 하고 Hyperparameter optimization을 하게 된다면 test data에 대해서 predict를 할 수 있기 때문에 이와 같이 활용을 함
- 여기서 옵션을 건드릴 때 struct array로 변환해서 만드는데 이 부분에서 option에 대한 것은 자동완성이 안되므로 다 확인하고 넣어주어야함

![one](/img/MachineLearning/Improving/twenty.png)

- 여기서 all을 하면 knn의 모든 요소들에 대해서 최적화함, 3차원이 아니라 다 하므로 그래프로 보여줄 수 없음
- 여기서 하나의 값으로 수렴하게 하기 위해서는 Evaluation을 많이 해야함, 많이 돌려야함

![one](/img/MachineLearning/Improving/twentyone.png)
![one](/img/MachineLearning/Improving/twentytwo.png)

- kfold와는 다르게 hyperparameter에서는 평가하는 도구로써 loss를 사용할 수 있음 그래서 kfold와 같이 쓰는 것
- loss에 대해서 알 수 있음

![one](/img/MachineLearning/Improving/twentythree.png)