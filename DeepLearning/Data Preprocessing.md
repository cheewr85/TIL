### Data Preprocessing
- 광범위한 작업임, x데이터 y레이블을 합쳐진 것을 나눈다던가 이미지 형태를 하나의 데이터로 주어진다면 그 스프레드 시트의 데이터를 다양한 과정을 거쳐서 원하는 다루고자 하는 데이터를 샘플 이미지를 보고 학습의 퍼포먼스를 위해서 전처리를 해야할 수 있음
- 이런 모든 과정을 전처리 Data Preprocessing이라고 함
- 여기서 시리얼 데이터를 받은 경우도 있는데 이때 이를 CNN을 위해서 변환할 수도 있음, 이를 형태 변경들을 위해서 데이터를 변경처리 할 수도 있음
- Improving Network Performance에 측면에서 많이 활용을 함
- 데이터를 로드해서 확인 가능함
- 10000개의 레이블과 각각의 행이 하나의 observation이라면 3072개의 열을 가지고 있는 형태임
- 여기서 data, train_x, x, xData는 다 같은 의미고 y, label, class, yLabel, category도 같은 의미임

![one](/img/DeepLearning/Preprocess/one.png)

- xData의 특징을 보면 32x32의 color image임, 이는 3채널을 의미함 여기서 각각 1024 x 3을 하면 3072가 나옴 즉, 이는 RGB 채널임을 알 수 있음(32x32x3)
- 여기서 data 자체는 10000x3072임 근데 해석을 하면 xData가 위와 같다는 것이고 여기서 그러면 우리가 해석한대로 32x32x3x10000으로 Reshape을 해야함, 그래야 CNN에 사용할 수 있음
- 이 과정을 보면 permute 함수를 사용해서 reshape하고 permute하는 것임
- reshape은 아까 앞서 말했듯이 10 x 10이 있다면 이를 5 x 5 x 4로 바꾸는 것이고 permute은 array의 dimension을 치환하는 것임
- 예를 들어 3x4x2 행렬을 생성했을 때 이를 permute를 해서 permute(A, [3 2 1])을 하면 A가 3 x 4 x 2이였는데 permute [3 2 1]을 하면 3번째가 첫번째 즉 2가 첫 번째로 가고 3이 3번째로 가는 것임, [3 2 1]은 순서를 나타내는 것임
- permute를 하면 결국 3 x 4 x 2에서 2 x 4 x 3이 되는 것임
- 아래 예시를 보면 Element 역시도 치환이 아래와 같이 되는 것임

![one](/img/DeepLearning/Preprocess/two.png)
![one](/img/DeepLearning/Preprocess/three.png)
![one](/img/DeepLearning/Preprocess/four.png)

- 결국 dimension 자체를 바꾼다는 것임, 이것을 permute을 해서 실제로 3072 x 10000으로 바꿔 보는 것임, 최종적으로는 32 x 32 x 3 x 10000으로 해야하므로
- 이를 바꾸는 것은 10000 x 3072 x 1을  1 x 3072 x 10000으로 바꾸는 것임, 여기서 세미콜론을 치지 않으면 출력하는데 시간이 꽤 걸림

![one](/img/DeepLearning/Preprocess/five.png)

- 그 다음 데이터를 reshape을 할 것임, 해당 함수를 활용해서 행렬의 형태를 바꿀 수 있음, 하지만 만약 데이터 형태가 많고 예측이 가능할 경우 빈괄호를 넣으면 알아서 맞춰서 처리해줌

![one](/img/DeepLearning/Preprocess/six.png)

- 행렬에서 행은 항상 observation을 의미함, 중요한 파트는 열로 함, 그래서 reshape 역시 열 중심으로 함, 개수도 맞춰서 처리해야함, 빈 array 처리는 관심 없는것 무조건 맞춰야 하는 부분에만 신경써도 됨
- 실제 처리한다면 아래와 같이 처리하면 됨, 그리고 이미지를 볼 수 있음

![one](/img/DeepLearning/Preprocess/seven.png)

- 여기서 보면 이미지가 옆으로 돌아가 있음을 알 수 있음, 이는 데이터 reshape 과정에서 삐뚤어진 것임을 알 수 있음, 이를 보면 32 x 32 바뀌는 과정에서 옆으로 돌아간 것으로 보임

![one](/img/DeepLearning/Preprocess/eight.png)

- 즉, 3 x 10000은 잘 되었는데 32 x 32가 잘못된 것임, 그렇다면 위의 데이터에서 :, :, 1,1에서 (:,:) 부분을 전치시키면 됨 Transpose 근데 2차원이 아니기 때문에 Transpose를 직접할 수 없고 permute를 통해서 다시 처리할 수 있음
- 즉, 32 x 32 부분만을 바꾸기 위해서 dimension 자체를 permute를 통해서 바꾸는 것임, 그럼 아래와 같이 제대로 처리됨을 알 수 있음

![one](/img/DeepLearning/Preprocess/nine.png)

- 마찬가지로 yLabel도 변경하고 data 형태로 이미지에 대한 것을 가지고 있으므로 이를 training set, data set으로 구분할 것임(datastore를 일일이 다 받아서 할 수는 있으나 굳이 그렇게 하지 않아도 됨)
- yLabel도 역시 똑같이 나누어줄 수 있음, 일단 yLabel 자체가 categorical 한 게 아니고 그냥 단순하게 array로 되어 있으므로 이를 categorical로 바꿔줘야함, 그리고 이 category 타입을 확인하고 summary를 통해서 categories의 개수를 확인할 수 있음

![one](/img/DeepLearning/Preprocess/ten.png)

- 그 다음 train과 test로 data를 split 할 수 있음, imageDS를 쓴다면 splitEachLabel을 쓸 수 있지만 현재 데이터 셋은 시트형태로 주어졌으므로 이를 강제로 하나하나 이미지를 저장하고 imageDS를 쓸 수 있지만 너무 비효율적인 과정임 splitEachLabel은 반드시 imageDS인 경우에만 써야함
- 그래서 이 경우에는 기계학습에서 했던 것과 같이 cvpartition을 사용하면 됨, 데이터를 나누기 때문에
- 먼저 yLabel을 HoldOut 방식으로 test 데이터 비율을 입력해서 나눌 것임(0.2만큼 남긴다는 것)

![one](/img/DeepLearning/Preprocess/eleven.png)

- 그 다음 인덱스 값을 뽑기 위해서 pt에 training을 씌움, 그러면 training index를 뽑음, test를 하면 test index를 뽑음
- training을 한다면 여기서 train index 값만 10000개 중에서 참값으로 뽑아냄, train index만 1, test index는 0임

![one](/img/DeepLearning/Preprocess/twelve.png)

- 여기서 testindex는 굳이 뽑을 필요는 없음 왜냐하면 train index의 반대니깐
- 그리고 여기서 Train을 위해서 xData에서 앞서 뽑은 train index에 대해서만 뽑아두면 됨

![one](/img/DeepLearning/Preprocess/thirteen.png)

- test는 그 반대로 설정해서 해주면 됨

![one](/img/DeepLearning/Preprocess/fourteen.png)

- 이를 summary를 보면 비율에 맞게 나누어진 것을 확인할 수 있음

![one](/img/DeepLearning/Preprocess/fifteen.png)

- 여기서 training을 굳이 사용하지 않아도 되긴함, pt에 이미 training index, test index가 포함되어 있기 때문에
- 즉, pt.training에 대해서 위에서 작업한대로 training index가 있음, 그냥 사용할 수 있음
- 이를 그래서 아래와 같은 방식으로도 사용할 수 있음

![one](/img/DeepLearning/Preprocess/sixteen.png)

- 결과가 거의 똑같고 여기서 두 방식 중 편한것을 쓰면 됨 1번이 좀 더 직관적인 방식이긴 함
- 데이터를 통으로 주고 데이터 설명을 보고 줄 경우 그에 맞게 전처리를 잘해야함