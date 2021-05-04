## Unsupervised Learning

## Roadmap
- [k-Means Clustering](#k-Means-Clustering)
- [Gaussian Mixture Model](#Gaussian-Mixture-Model)
- [Interpreting the Groups](#Interpreting-the-Groups)
- [Hierarchical Clustering](#Hierarchical-Clustering)

## k-Means Clustering
- k-Means와 Gaussian은 Cluster하고자 하는 그룹의 개수가 정해졌을 때 사용하는 방법
- 알고리즘을 통해서 몇 개의 cluster가 최적인지 알 수 있고 이를 바탕으로 비지도 학습을 할 수 있음
- clustering한 후 group을 visualization을 하여 제대로 되었는지 봄, 여기서 차원축소를 활용함
![one](/img/MachineLearning/Unsupervised/one.png)

- idx, g를 통해서 data가 어떤 group인지 clustering의 결과가 나오게끔 열벡터로 나타남

- k-Means를 할 때 우선 몇 개로 나눌것인지 나오는데 여기서 그렇게 하기 위해 임의로 center를 아래와 같이 지정함, 3개로 나눌것이므로 3개의 center
![two](/img/MachineLearning/Unsupervised/two.png)

- 그런 다음 center를 중심으로 그룹을 3개로 나눔
![three](/img/MachineLearning/Unsupervised/three.png)

- 여기서 group 사이의 거리가 같은 경우 위의 how to function을 바탕으로 본다면 distance 즉 그 사이의 거리를 option으로 설정하여 볼 수 있지만 기본값은 유클리드 기법이 기준임
- 첫번째 점은 우선 임의로 center를 아래와 같이 잡음
![four](/img/MachineLearning/Unsupervised/four.png)

- 그리고 그룹이 형성이 된 후 임의로 잡은 center에서 다시 새로운 center로 업데이트를 함, 그리고 그 업데이트한 center를 바탕으로 새로운 그룹으로 잡음
![five](/img/MachineLearning/Unsupervised/five.png)

- 그리고 다시 center를 바탕으로 그룹을 업데이트함
![six](/img/MachineLearning/Unsupervised/six.png)

- 이런 방식으로 계속해서 업데이트를 하면서 갱신을 함
![seven](/img/MachineLearning/Unsupervised/seven.png)

- 이러한 점으로 인해서 k-Means의 단점은 처음 잡힌 점이 터무니 없이 잡히게 된다면 때로는 발산을 하거나 터무니 없는 그룹으로 잡힐 수 있음
- 이러한 점을 해결하기 위해서 임의의 center를 여러번 반복해서 잡으면서 group을 잡으며 그 중 가장 즉 하나의 center에 대한 group의 길이의 평균값이 작은 것을 뽑으면 최적이 됨
- 아래와 같이 거리를 체킹을 하고 더 나은 것을 바탕으로 grouping을 함
![eight](/img/MachineLearning/Unsupervised/eight.png)
![nine](/img/MachineLearning/Unsupervised/nine.png)

- 그리고 아래와 같이 유클리드를 default로 그룹을 체킹을 함
![ten](/img/MachineLearning/Unsupervised/ten.png)

- 그 다음 해당 k-Means를 보기 위해서는 Dimensionality Reduction을 진행해야함, Visualization을 위해, 아래는 PCA 방식을 활용
- 위의 구한 식을 바탕으로 그대로 쓸 것이지만 marker, k-Means로 계산한 값을 표시를 할 것임
- 아래와 같이 group을 scatter3 함수로 표현
![eleven](/img/MachineLearning/Unsupervised/eleven.png)

- 여기서 만일 center를 잘못 잡으면 터무니 없이 나타나기도 함, 이를 아래와 같이 사용해서 방지할 수 있음 
- 5번 반복을 한 뒤 평균 center부터 observation이 제일 짧은 결과를 골라 아래와 같이 보여줄 수 있음
- k-Means에서 replicate 옵션은 거의 항상 씀
- c를 통해서 각 그룹의 center의 정도를 알 수 있음
![twelve](/img/MachineLearning/Unsupervised/twelve.png)

## Gaussian Mixture Model(GMM)
- Parameter의 영향을 많이 받음
- 다양한 옵션들을 통해서 결과가 희한하게 나올 수 있음
- k-Means는 어느정도 정형화 된 결과가 나오지만, Gaussian은 잘못 설정시 그 값이 상당히 이상하게 나올 수 있음
- GMM은 확률로 계산을 함(정규분포)
- 데이터가 아래와 같이 있을 경우 바깥으로 올라오는 정규분포를 그려 아래와 같이 나타냄 3차원 상에서 바깥부터 쭉 올라오는 형태로 확률로 계산이 됨
- 표준편차가 1 평균이 0 or 1인 데이터를 씌움, 정규분포 distribution을 만들어서 거기에 맞춰 grouping을 함
![thirteen](/img/MachineLearning/Unsupervised/thirteen.png)
![fourteen](/img/MachineLearning/Unsupervised/fourteen.png)

- k-Means는 거리기반, GMM은 확률기반임
- GMM은 Grouping의 확률이 모두 나타나는데 그 중 가장 높은 확률 부분의 group으로 들어가서 나옴, 처음엔 랜덤하기 때문에 발산하게 되는 경우도 있지만 Replicate를 통해서 반복을 하여 최적의 상태를 찾으면 됨
- 아래와 같이 하나의 데이터가 각 group에 속할 확률을 모두 파악할 수 있음, 세밀하게 조절하기 좋음
![fifteen](/img/MachineLearning/Unsupervised/fifteen.png)

- 처음에는 아래와 같이 엉뚱한 곳부터 시작하다가 점차 업데이트를 함
![sixteen](/img/MachineLearning/Unsupervised/sixteen.png)
![seventeen](/img/MachineLearning/Unsupervised/seventeen.png)

- 아래와 같이 발산할 수도 있음
![eighteen](/img/MachineLearning/Unsupervised/eighteen.png)

- 아래와 같이 Gaussian Model Distribution에 맞게 model을 생성한 후
![nineteen](/img/MachineLearning/Unsupervised/nineteen.png)

- 그 다음 해당 변수를 바탕으로 clustering에 아래와 같이 데이터를 활용함
![twenty](/img/MachineLearning/Unsupervised/twenty.png)

- 아래와 같이 코드를 통해서 distribution을 구함, 하지만 아래와 같은 경우 모든 부분에서 분포가 적합하지 않다고 나옴
![twentyone](/img/MachineLearning/Unsupervised/twentyone.png)

- 그러므로 처리할 때 튜닝옵션을 사용해야함, 정상적으로 처리가 됨
![twentytwo](/img/MachineLearning/Unsupervised/twentytwo.png)
![twentythree](/img/MachineLearning/Unsupervised/twentythree.png)

- 이러한 튜닝옵션을 설정해도 해당이 안될 떄도 있고 그리고 정상적으로 처리될 때도 있음, 처음 시작은 Random하게 시작하니깐

- 그리고 cluster 함수를 통해 그룹을 나눔
![twentyfour](/img/MachineLearning/Unsupervised/twentyfour.png)

- 그리고 Visualization을 위해 PCA를 활용, PCA를 자주 쓰는 이유는 쓰기 편하고 다양한 정보를 바깥쪽으로 뺄 수 있으므로 사용함
![twentyfive](/img/MachineLearning/Unsupervised/twentyfive.png)

- 여기서 GMM에서 위와 같이 직관적으로 쓸 수 있지만 또 다른 방식으로 확률을 받는 방식으로 쓰는 것이 좋음, 확률을 제공해주기 때문에
- 아래와 같이 probability는 무조건 받는 것이 좋음 결과를 명확하게 보여주고 cluster의 확률을 확실히 정해줌
![twentysix](/img/MachineLearning/Unsupervised/twentysix.png)

- 여기서 p로 확률을 받았고 아래와 같이 시각화를 해줄 수 있음
- 아래는 cluster1에 포함될 확률이고 즉 노란색이 그렇고 색깔이 점점 초록색과 파란색으로 될 수록 cluster2에 포함됨, 왜냐하면 어차피 cluster1에 포함될 확률이 p이면 cluster2에 포함될 확률은 1-p임
![twentyseven](/img/MachineLearning/Unsupervised/twentyseven.png)

## Interpreting the Groups
- Clustering 결과를 observation 별로 보고 clustering 별로 보고 어떻게 최적의 조건을 찾을지 파악할 수 있음
- group과 centroid를 설정한 kmeans와 Gaussian을 통한 group과 probability를 알 수 있음
- Gaussian은 Gaussian distribution을 씌운 다음에 Clustering을 진행함
- 우선 Kmeans의 observation당 variable로 나눠서 어떤 그룹에 속하는지 아래와 같이 시각화를 할 수 있음
- 각 observation이 어느 group에 포함되었는지 알 수 있음(17개의 variable, 선은 1112개의 좌표값을 나타냄)
- 각 variable당 좌표값이 어떤지 알 수 있음, 데이터가 어느정도 정형화되어 있다면 두 group이 나뉘어짐
![twentyeight](/img/MachineLearning/Unsupervised/twentyeight.png)

- labels의 각각의 xtick의 label을 확인할 수 있음
![twentynine](/img/MachineLearning/Unsupervised/twentynine.png)
![thirty](/img/MachineLearning/Unsupervised/thirty.png)

- 하지만 위와 같이 보면 보기 매우 힘듬, 그래서 옵션을 활용하여 좀 더 보기 편하게 설정함
- Quantile 0.25는 Medium값 기준으로 위로 0.25, 아래로 0.25를 의미함, 중간값을 기준으로 2번째 사진과 같이 잡음
- 진한 선을 기준으로 25%안에 들어오는 것의 경계면을 나타내는 것임, 위아래 경계를 두고 나타냄
![thirtyone](/img/MachineLearning/Unsupervised/thirtyone.png)
![thirtytwo](/img/MachineLearning/Unsupervised/thirtytwo.png)

- centroid 역시 알 수 있음
![thirtythree](/img/MachineLearning/Unsupervised/thirtythree.png)

- 때로는 비지도학습이어도 실제 그룹이 어디에 포함되는지 알 수 있음
- 그룹 결과를 이미 알고 있을 때, clustering의 퀄리티를 알 수 있음
- 이때 crosstab을 활용함, 각각의 group에 속할 확률을 알 수 있음
![thirtyfour](/img/MachineLearning/Unsupervised/thirtyfour.png)

- 아래와 같이 활용해서 쓸 수 있음
- 각각 앞의 숫자는 1번 그룹에 속한 개수, 뒤의 숫자는 2번 그룹에 속한 개수를 나타내는 것임
![thirtyfive](/img/MachineLearning/Unsupervised/thirtyfive.png)

- 이를 바 그래프로 사용하는것을 많이 씀, 아래와 같이 스택형식으로 쓸 수 있음
![thirtysix](/img/MachineLearning/Unsupervised/thirtysix.png)
![thirtyseven](/img/MachineLearning/Unsupervised/thirtyseven.png)

- 이를 반대로 쓸 수도 있음, 여기서는 cell형으로 넣어서 씀
![thirtyeight](/img/MachineLearning/Unsupervised/thirtyeight.png)

- clustering quality 역시 확인할 수 있음, evalclusters를 활용해서 quality를 판단할 수 있음
- 헷갈리면 다 작은따옴표로 통일해서 처리해도 상관없음
- silhouette 함수를 통해서 quality를 확인할 수 있음
- silhouette 함수는 아래와 같이 가운데 선을 기준으로 2번과 1번 그룹으로 나뉘어짐
- 파란색 면적이 오른쪽으로 많을수록 clustering의 quality가 좋은 것임 
- 아래의 사진을 비교했을 때 2개 그룹, 3개 그룹 비교시 두 번째 그룹의 퀄리티가 더 좋은 것임
- 그리고 올라가는 저 값들은 observation까지 얼마나 가까운지를 의미함, 오른쪽으로 값이 가까울수록 그만큼 퀄리티가 높다는 것을 의미함, 하지만 마이너스로 가까우면 그만큼 퀄리티가 안 좋다는 것을 의미함, 마이너스로 쭉 뻗으면 매우 안좋다는 것임
![thirtynine](/img/MachineLearning/Unsupervised/thirtynine.png)

- 아래와 같이 3개의 그룹으로 나올수도 있음
![fourty](/img/MachineLearning/Unsupervised/fourty.png)

- 아래와 같이 그룹을 계속 나눌 수 있음 
- 여기서 각각을 비교하면서 그 퀄리티를 체크하고 어떻게 나눌지 판단할 수 있음
- 근데 눈으로 파악했을 때 애매한 경향이 있음, 뭐가 더 나은지 판단하는 상황에서
![fourtyone](/img/MachineLearning/Unsupervised/fourtyone.png)
![fourtytwo](/img/MachineLearning/Unsupervised/fourtytwo.png)

- 여기서 자동으로 어떤게 나은지 체크 할 수 있음
- KList는 cluster의 개수를 의미함
- 검열한 cluster의 개수가 2,3,4,5 그리고 optimal한 것은 2개임을 의미함, 즉 아래와 같은 방식을 사용했을 때 최적의 방식이 2개의 group으로 나눴을 때임을 나타내줌
![fourtythree](/img/MachineLearning/Unsupervised/fourtythree.png)

- 여기서 평가하는 방법은 다양함
- Davis 방식은 최적값이 변하는 경우도 있음
- 아래의 방식을 토대로 2,5의 group이 나음을 알 수 있음
![fourtyfour](/img/MachineLearning/Unsupervised/fourtyfour.png)

## Hierarchical Clustering
- 데이터의 variable의 특성을 어느정도 완벽하게 알고 있을 경우 유용함
- 평이한 옵션을 활용하면 그에 맞게 평이하게 나옴, 하지만 옵션에 따라 세밀하게 구분을 할 수 있음
- linkage, dendrogram을 하고 cluster를 함, Gaussian에서의 cluster와 유사함, linkage로 유사성을 파악하고 dendrogram으로 유저가 보고 이를 통해 cluster를 함
- linkage에서는 데이터가 아무리 많아도 5개로 나타냄, 유사성이 아주 가까운 경우는 유사성으로 묶어서 나타냄, 아주 많은 경우는 그러지 않을 것임
- 여기서 1은 observation 1이 아님, 여기에 포함된 군집된, 너무 가까워서 하나로 군집되어 있는것을 의미함
- 아래의 dendrgram에서 1,2,3,4,5는 군집된 observation을 의미함, 4와 5는 적당한 유사성이 있지만 어느정도 떨어져 있음, (4,5), (1,2)의 차이는 세로축의 길이가 유사성을 나타냄, (1,2)가 묶이면 떨어져서 나중에 3으로 묶임
![fourtyfive](/img/MachineLearning/Unsupervised/fourtyfive.png)

- 이를 쓰기 위해서 데이터를 구분해서 쓸 것임 
- 그전에 statsnorm에서 정규화를 한 것은 zscore를 통해서 정규화 한 것임, 여기서 zscore는 표준정규분포를 만드는 것이었음
![fourtysix](/img/MachineLearning/Unsupervised/fourtysix.png)
![fourtyseven](/img/MachineLearning/Unsupervised/fourtyseven.png)

- 여기서 linkage를 하고 간단하게 보면 아래와 같이 나오게 됨, 상당히 이상하게 나옴
![fourtyeight](/img/MachineLearning/Unsupervised/fourtyeight.png)

- 이를 ward를 통해 서로간의 유사성을 다시 파악함, 어떻게 쪼갤 것인지 파악 가능함
![fourtynine](/img/MachineLearning/Unsupervised/fourtynine.png)

- 거리측정법을 cosine으로 바꾸고 아래와 같이 유사성 체크시 2개 혹은 3개로 쪼개는게 나음을 알 수 있음
![fifty](/img/MachineLearning/Unsupervised/fifty.png)

- 여기서 거리측정법을 최적으로 할 것이 무엇일지 고려를 할 때 그 변수간의 무엇이 나은지 doc을 통해 활용해서 정하면 됨
- 군집간 거리를 계산하는 알고리즘은 다양함
- 그 이후 아래와 같이 clustering을 확인을 할 수 있음
- medium을 기준으로 아래와 같이 그 정도를 확인할 수 있음
![fiftyone](/img/MachineLearning/Unsupervised/fiftyone.png)

- 하지만 여기서 위와 같이 처리해서 직접 보는 것 말고 evalclusters를 통해서 linkage였을 때 최적값을 찾을 수 있음
![fiftytwo](/img/MachineLearning/Unsupervised/fiftytwo.png)
