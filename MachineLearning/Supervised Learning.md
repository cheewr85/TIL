## Supervised Learning 

## Roadmap
- [Supervised Learning](#Supervised-Learning)
- [Nearest Neighbor Classification](#Nearest-Neighbor-Classification)
- [Decision Tree Classification](#Decision-Tree-Classification)
- [Navie Bayes Classification](#Navie-Bayes-Classification)
- [Discriminant Analysis](#Discriminant-Analysis)
- [Support Vector Machines](#Support-Vector-Machines)
- [Multiclass Support Vector Machines](#Multiclass-Support-Vecotr-Machines)

## Supervised Learning
- 지도학습은 Output이 존재함
- Input variable이 존재하고 Output variable이 존재함, 이 Input 데이터를 바탕으로 response(output) variable을 바탕으로 학습을 시킴
- 결과를 알고 있음, 즉 output variable이 있기 때문에 이를 input 데이터와 매칭을 시켜서 새로운 데이터가 들어왔을 때 해당 output이 어떻게 나오는지 예측을 하는 것임 
- Classification -> response variable이 categorical로 확실하게 discrete하게 나타남
- Regression -> Continuous한 상수로 예상을 하는 것이 Regression임
- 아래와 같은 작업으로 진행됨
- 여기서 Algorithm 즉, 앞에서 배운 kmeans와 같은 분류기들이 존재함
- 그래서 학습을 하고 parameter를 튜닝을 하던가 아니면 Model을 업데이트하여서 주어진 데이터내에서 계속 업데이트를 하여 트레이닝 시키고 최적의 상태를 파악함

![one](/img/MachineLearning/Supervised/one.png)

- 심장질환에 대한 데이터 활용해서 사용할 것임
- 각각 심장질환의 output variable을 포함한 전체 데이터, numeric한 데이터만 있는 것 그리고 array 형태의 데이터와 variable name에 대해서 저장을 해 둠

![two](/img/MachineLearning/supervised/two.png)

- 지도학습을 할 것이 이게 의미가 있는지 사전에 확인을 할 수 있음, 지도학습의 결과를 내는게 맞는것인지 체크를 하는 것
- 그 전에 numeric data만을 뽑고 정규화를 시킬 것임, 이를 위해서 array형태로 받고 정규화를 시켜야함
![three](/img/MachineLearning/supervised/three.png)

- 그 다음 kmeans로 테스트 해볼 것임, 클러스터링이 잘 되었음을 알 수 있음
- input data만을 가지고 1~11을 했음
![four](/img/MachineLearning/supervised/four.png)


- 여기서 이를 crosstab을 통해서 kmeans로 클러스터링 한 것과 우리가 알고 있는 response variable인 heartdisease와 비교해볼 것임
![five](/img/MachineLearning/supervised/five.png)

- 한 쪽으로 어느정도 쏠려있음을 알 수 있음, 거의 2:1로 나누어짐을 알 수 있음, 특정 input data에 대해서 어느정도 데이터가 패턴을 가지고 있음을 알 수 있고 이를 바탕으로 패턴화되어 있으므로 지도학습을 쓰기 용이함을 알 수 있음
![six](/img/MachineLearning/supervised/six.png)

- 클러스터링을 했을 때 패턴을 보면 어느정도 결과값이 True / False와 연관성이 있음을 알 수 있음, 2:1, 3:1이 나오므로 지도학습을 해도 어느정도 유의미한 결과가 나옴을 알 수 있음, HeartDisease의 True False가 마냥 이분법적으로만 나뉘어지지 않으니깐
- 어느정도 input과 output의 연관성이 있음을 이해함

- 여기서 Training과 Validation 데이터를 구분할 것임, 이를 바탕으로 데이터를 바탕으로 업데이트를 할 수 있음
- 그 전에 random number generation을 통제할 것임, rng는 training, validation set을 나눌 것인데 하나의 경우 set을 하기 위해서 그 데이터를 확인하면서 정확도를 보기 위해서 rand가 계속해서 너무 랜덤하게만 나오게끔 할 수 없음
- training과 validation을 나눌 때 일정하게 유지시키고 하나의 데이터 셋에 대해서 accuracy를 확인하고 비교하기 위해서 rng random number를 고정시키는 것임
![seven](/img/MachineLearning/supervised/seven.png)

- 아래와 같이 비율로 나눠서 할 것임, validation 비율을 정해서 함, 이는 하나의 래퍼토리, 스크립화 된 내용임
- 8대 2로 나왔고 tridx를 통해서 part에서 training data가 무엇인지 확인함, 1과 0의 비율은 8대 2임
![eight](/img/MachineLearning/supervised/eight.png)

- 아래와 같이 training, validation data를 구분할 수 있음
![nine](/img/MachineLearning/supervised/nine.png)

- 그리고 다른 classifier를 할 때 모든 category를 활용하기 위해서 아래와 같이 training, validation 비율에 맞춰서 체크해주어야함
![ten](/img/MachineLearning/supervised/ten.png)

- 위처럼 랜덤하게 20%를 잡은것임, 여기서 결과가 매번 달라지지 않게 같은 값으로 통제해서 체크를 하기 위해서 rng를 사용하는 것임

## Nearest Neighbor Classification
- 아래와 같이 분류가 되었을 때, 새로운 데이터가 아래와 같이 들어왔을 때 반지름을 잡아주거나 제일 가까운 것을 체크함, 아무 옵션을 주지 않으면 가장 가까운 것으로 감
![eleven](/img/MachineLearning/supervised/eleven.png)
![twelve](/img/MachineLearning/supervised/twelve.png)

- 만일 노이즈가 많은 데이터의 경우 여기서 잘못 판단할 여지가 이런 경우는 위와 다르게 아주 많음, 파란색이 아닌 초록색을 고름
![thirteen](/img/MachineLearning/supervised/thirteen.png)

- 이럴 경우 가장 가까운 이웃을 선택할 때 k의 값에 따라 가장 가까운 이웃을 체크함, 그래서 k가 1일 때는 초록색이지만 3일 때는 노란색으로 예측을 함, 그만큼 체킹함
![fourteen](/img/MachineLearning/supervised/fourteen.png)

- 데이터 자체를 노이즈가 있어도 있는 그대로 봄, 데이터가 어떤지 어느정도 가정을 하는 것이 있기도함
- Nearest Neighbor, Decision Tree의 경우 데이터가 어떻든 상관없이 있는 그대로를 봄
- 이로 인해 노이즈에 약한 성질이 있음, 노이즈의 영향을 많이 받음 
- Navie의 경우 데이터에 대해 가정을 함
- Nearest는 매우 직관적임
- wide data -> 옆으로 쭉 늘어난 데이터, predict variable이 매우 많은 것, 이 때 cosine distance를 활용하는것이 좋음
- 결과랑 매칭을 시켜서 학습을 시키는 것임, 아래와 같이 데이터와 response variable을 넣어주면 됨
- 여기서 k의 값을 조절하고 싶다면, NumNeighbors를 활용해서 조절할 수 있음, 홀수를 주로 씀, 숫자가 커질수록 결과가 매우 떨어짐 -> 노이즈가 많으면 그 값을 늘려서 loss를 조절할 수 있음
- 아래와 같이 지도학습을 씀
![fifteen](/img/MachineLearning/supervised/fifteen.png)

- 그리고 이 학습 이후 loss에 대해서 확인할 수도 있음
- 아래와 같이 지도학습을 한 m을 가지고 validation data에 대한 loss를 확인할 수 있음, loss가 34%나 났으므로 정확도가 그리 높은건 아님을 알 수 있음
![sixteen](/img/MachineLearning/supervised/sixteen.png)

- 여기서 validation뿐 아니라 training data에 대한 loss 역시 봐야함, 아래와 같이 쓰면 됨, 굳이 data를 볼 필요없음
- 이를 확인하는 이유는 과적합 overfitting을 방지하기 위해서 꼭 봐야함
- training data에 대해서만 학습을 시켜서 호랑이를 체크하는 상황에서 백호가 들어와도 이를 false로 리턴해버리는 문제가 생겨버림
- 이러한 과적합은 아래와 같은 Nearest는 1이 나올 경우 과적합이 발생함
- 너무 overfitting이 되어 있는 것은 지양해야함
![seventeen](/img/MachineLearning/supervised/seventeen.png)

- 이제 Nearest Neighbor 방식으로 분류한 것을 predict을 할 것임, 그리고 validation data에 대한 response 역시 알고 있으므로 아래와 같이 HD 2개를 받아올 것임 데이터를
- 여기서 지도학습은 confusionchart를 많이 씀, 아래와 같이 True일 때, False를 한 경우 True를 한 경우를 보며 그 정도의 가치를 확인할 수 있음
![eighteen](/img/MachineLearning/supervised/eighteen.png)

- 아래와 같이 NumNeighbors의 수를 늘리면 이전의 방식보다 loss가 줄어듬을 알 수 있음, 그만큼 정확도가 좀 올라감을 알 수 있음
![nineteen](/img/MachineLearning/supervised/nineteen.png)

- 하지만 숫자가 높아진다고 마냥 좋은 것이 아님, 그만큼 training data에 대한 loss도 올라감
![twenty](/img/MachineLearning/supervised/twenty.png)

- 아래와 같이 옵션을 건드리면 Trainingdata에 대한 loss가 확연히 달라짐을 알 수 있음
![twentyone](/img/MachineLearning/supervised/twentyone.png)

## Decision Tree Classification
- 아래와 같이 Binary Decision이 나오게끔 물어봄, 데이터에게 그리고 데이터에 대해서 진행을 함
![twentytwo](/img/MachineLearning/supervised/twentytwo.png)

- 계속 물어보면서 스무고개를 하는것임, validate할 때 그 validate로 들어가는 것임
![twentythree](/img/MachineLearning/supervised/twentythree.png)

- 진행 시 아래와 같이 확실한 Yes or No로 나눠서함
![twentyfour](/img/MachineLearning/supervised/twentyfour.png)

- 그럼 다음 똑같은 방식으로 나눔
![twentyfive](/img/MachineLearning/supervised/twentyfive.png)
![twentysix](/img/MachineLearning/supervised/twentysix.png)

- 무조건 rectangular 방식으로만 나눔, nonlinear한 방식이 없음
![twentyseven](/img/MachineLearning/supervised/twentyseven.png)

- 하나의 예측할 데이터가 들어오면 아래와 같이 나오게 됨
![twentyeight](/img/MachineLearning/supervised/twentyeight.png)

- 하지만 노이즈가 항상 포함되어 있기 때문에 아래와 같이 나오게 됨, 노란색에 들어가야 할 것 같은데 아래와 같이 파란색이 나오는 overfitting의 문제가 생김
![twentynine](/img/MachineLearning/supervised/twentynine.png)

- 그러면 여기서 가지치기를 통해서 아래와 같이 일반화를 시켜야함(prune)
![thirty](/img/MachineLearning/supervised/thirty.png)
![thirtyone](/img/MachineLearning/supervised/thirtyone.png)

- 아래와 같이 코드를 활용해서 할 수 있음
![thirtytwo](/img/MachineLearning/supervised/thirtytwo.png)

- 그러면 이 부분이 상당히 과적합이 많이 됐고 가지가 많음을 알 수 있음
![thirtythree](/img/MachineLearning/supervised/thirtythree.png)

- 상당히 과적합된 것이므로 이를 prune할 것임(가지치기)
- 아래와 같이 동일한 방식으로 결과를 알 수 있음
![thirtyfour](/img/MachineLearning/supervised/thirtyfour.png)

- 이를 성능을 향상시키기 위해서 prune을 할 것임, 밑에서부터 3개를 가지치기 하기 위해서 아래와 같이함
![thirtyfive](/img/MachineLearning/supervised/thirtyfive.png)

- 아래와 같이 loss가 나아졌음을 알 수 있음
![thirtysix](/img/MachineLearning/supervised/thirtysix.png)

- 여기서 prune말고 다양한 옵션이 존재함, 노이즈 데이터가 많을 때 prune을 잘 사용하면 좋은 결과를 받을 수 있음
- 여기서 기본적으로 데이터는 numeric과 categorical 데이터가 다 있는데 knn은 이런식으로 섞여있는 데이터는 쓸 수 없음
- 여기서 Decision Tree의 경우 모든 데이터에 대해서 아래와 같이 활용할 수 있음
![thirtyseven](/img/MachineLearning/supervised/thirtyseven.png)

## Navie Bayes Classification
- 각각의 predictor variable이 독립적인 경우 매우 강함
- 아래와 같이 각각의 variable에 대해서 정규분포를 이루고 있다고 가정을 하면서 진행을 함
![thirtyeight](/img/MachineLearning/supervised/thirtyeight.png)

- 그리고 input 데이터가 생기는 경우 아래와 같이 각각의 Variable에 대해서 확률을 계산하여 알 수 있음, 그리고 확률이 높은쪽으로 넘어감
![thirtynine](/img/MachineLearning/supervised/thirtynine.png)

- 그리고 아래와 같이 각각의 variable에 대해서 독립적으로 정규분포를 이루고 있음을 알 수 있음, 옵션으로 변경을 할 순 있음
![fourty](/img/MachineLearning/supervised/fourty.png)
![fourtyone](/img/MachineLearning/supervised/fourtyone.png)

- 노이즈 데이터가 아래와 같이 있어도 정규분포의 큰 영향을 끼치지 않음
![fourtytwo](/img/MachineLearning/supervised/fourtytwo.png)

- 아래와 같이 코드를 씀
![fourtythree](/img/MachineLearning/supervised/fourtythree.png)

- 아래와 같은 loss가 나타남을 알 수 있음
![fourtyfour](/img/MachineLearning/supervised/fourtyfour.png)

- 모든게 섞여있는 데이터에서도 아래와 같이 나타남을 알 수 있음
![fourtyfive](/img/MachineLearning/supervised/fourtyfive.png)

- 아래와 같이 distributionname을 바꿀 수 있음
![fourtysix](/img/MachineLearning/supervised/fourtysix.png)

- 하지만 이러한 옵션을 건드릴 때 numerical과 categorical이 적용이 다른데 그러므로 무조건 일원화해서 적용시키기 어려움
- 그래서 아래와 같이 repmat을 통해서 array를 자동으로 생성하게끔 하여서 할 수 있음
- 이를 바탕으로 numerical과 categorical의 적용을 다르게 할 것임
![fourtyseven](/img/MachineLearning/supervised/fourtyseven.png)

- 그러면 아래와 같이 NormalDistributionNames이 지정한대로 바뀜
![fourtyeight](/img/MachineLearning/supervised/fourtyeight.png)

- 아래와 같이 변화가 있음을 알 수 있음
![fourtynine](/img/MachineLearning/supervised/fourtynine.png)

## Discriminant Analysis
- Naive Bayes와 유사함
- Navie Bayes, Discriminant, Support Vector Machine 이 3가지 분류기가 성능이 좋음
- 앙상블 → 다른 분류기들을 섞을 수 있음
- Naive Bayes는 각각의 predictor들이 independent함, Discriminant와는 다르게
- 하지만 데이터에서의 predictor들이 절대적으로 independent하진 않음
- Discriminant는 independent와 dependent를 구분하진 않음
- discriminant에서 quadratic을 항상 사용해야함, 메모리 사용이 많아도 여전히 빠르므로 주로 사용함
- 아래와 같이 response variable을 알고 있는 상황에서(clustering이 아니므로 이미 아래와 같이 나뉘어짐) normal distribution을 가정함
- 여기서 discriminant 타입이 기본적으로 linear로 되어있음, 이 linear는 각각의 공분산이 서로 같을때를 의미함, 아래와 같이 나뉘어짐
![fifty](/img/MachineLearning/supervised/fifty.png)

- 하지만 실제로 위와 같은 경우는 발생하지 않음, 3개가 다를 수 밖에 없음 그렇기 때문에 아래처럼 quadratic하게 나눔, 공분산이 같은 경우는 거의 없음
![fiftyone](/img/MachineLearning/supervised/fiftyone.png)

- 기본적으로 normal distribution을 가정하기 때문에 노이즈 데이터에 강함
- 아래와 같이 코드를 사용함, 원본이 아닌 quadratic을 활용함
![fiftytwo](/img/MachineLearning/supervised/fiftytwo.png)

## Support Vector Machines
- response variable이 2개로 나뉘어졌을 때 활용함, 그 이상을 다룰 때는 Multiclass Support Vector Machines을 씀
- Support Vector Machine은 2개로 나뉘어져 있을때 각각의 끝에서 먼 마진을 갖게끔 공간상의 plane을 아래와 같이 만듬
![fiftythree](/img/MachineLearning/supervised/fiftythree.png)

- 여기서 이러한 마진이 가장 많이 남는 쪽으로 잡음, 그리고 support vector를 잡음
![fiftyfour](/img/MachineLearning/supervised/fiftyfour.png)

- 노이즈가 많이 있을 경우 노이즈에 대해서 패널티를 줌, 그런 다음 마진이 더 남도록 plane을 잡고, 노이즈 데이터를 최대한 포함할 수 있도록 마진을 최대한 크게 잡음
![fiftyfive](/img/MachineLearning/supervised/fiftyfive.png)
![fiftysix](/img/MachineLearning/supervised/fiftysix.png)

- 하지만 아래와 같이 둘려싸여 있게 된다면 에러가 많다면 상당히 에러가 많은데 SVM은 PCA를 통해서 선형으로 바꾼 뒤 여기서 SVM을 하고 원상 복구시킴
![fiftyseven](/img/MachineLearning/supervised/fiftyseven.png)

- 아래와 같이 활용해서 쓸 수 있음
![fiftyeight](/img/MachineLearning/supervised/fiftyeight.png)

- 여기서 만일 nonlinear한 경우 아래와 같이 kernelfunction을 Gaussian으로 잡아주면 됨
![fiftynine](/img/MachineLearning/supervised/fiftynine.png)

## Multiclass Support Vector Machines
- 2개 binary categories에 대해서 작동하기 때문에 대부분 다 이 svm을 씀
- 기본적으론 아래와 같이 씀, Linear를 기본을 쓰기 때문에 굳이 SVM을 따로 쓸 필요는 없음
![sixty](/img/MachineLearning/supervised/sixty.png)

- 여기서 옵션을 활용하기 위해서는 아래와 같이 별도로 정의를 한 뒤 Learners를 통해서 사용해주어야 함
![sixtyone](/img/MachineLearning/supervised/sixtyone.png)

- MixedPredictors에 대해서도 아래와 같이 활용할 수 있음
![sixtytwo](/img/MachineLearning/supervised/sixtytwo.png)

- 베이스 데이터를 활용해서 어떻게 분류기를 활용해서 적용해서 내가 원하는 값을 볼 지에 대해서 이해할 필요가 있음