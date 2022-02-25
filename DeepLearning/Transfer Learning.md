### Transfer Learning
- Pretrained된 모델, 누군가가 이미 학습시켜놓은 모델을 인풋 데이터를 넣고 원하는 아웃풋 클래스 예측하도록 하는 것
- 이미 누군가 만들어놓은 것을 사용함 그 중 AlexNet 쓸 것임
- 어느정도 예측을 할 수 있음, 각각의 layer 역할, layer by layer의 네트워크 만들고 정확도 높이는지는 그 이후에 할 것임
- Transfer Learning은 윤곽을 잡는것임
- 여기서 alexnet을 사용하기 위해서 추가 에드온을 다운로드 한 뒤 아래와 같이 alexnet을 쓰면 결과가 나옴

![one](/img/DeepLearning/Transfer/one.png)

- 그러면 pretrained된 alexnetwork를 가져옴
- Alexnet은 아래와 같이 구성되어 있음

![one](/img/DeepLearning/Transfer/two.png)

- 먼저 Feature를 extract하는 파트와 그 다음 그걸 connect하는 파트로 나뉘어져있음
- input, output layer 사이에 아래와 같이 다양한 layer들이 들어가 있음

![one](/img/DeepLearning/Transfer/three.png)

- 일반적으로 이미지라고 불러져있는 2D-array에 최적화된 네트워크임
- 2D-layer라고 되어있는 것들은 전부다 받아서 Output 클래스를 예측할 수 있음
- 위처럼 크게 Input-layer, output-layer가 있고 그 사이에 feature를 extract하는 파트와 그 추출된 특징을 output 클래스와 연결해서 스코어로 만들어주는 파트로 되어 있음
- 그림이 RGB로 구성되어 있고, X축과 Y축으로 관련된 Red값이 무엇인지에 대한 2D-array로 구성됨 즉 컬러는 2D-array의 3 image RGB로 되어있어서 3개로 구성되어 있는 것임 m x n x 3 image에서 3은 채널이라고 함
- 만약 흑백이라면 그냥 채널이 1임
- 이 Alexnet은 2D-array라면 효율적으로 쓸 수 있음
- 어떠한 네트워크를 막론하고 CNN은 feature를 extract하는 파트(feature-extraction)와 얘를 output 클래스와 연결해주는 파트로 구성되어 있음, input-layer, output-layer 사이에
- 그래서 output에서 가장 높은 score에 대한 이미지를 예측하여 나타냄, 아래와 같이

![one](/img/DeepLearning/Transfer/four.png)

- 아래와 같이 우선 input에서 feature를 Convolution, Pooling, ReLU로 뽑아내고

![one](/img/DeepLearning/Transfer/five.png)

- 그 다음 Feature와 Output 클래스를 연결해주는 Fully Connected와 이를 스코어로 나타내주는 Softmax layer 그 다음 output으로 구성되어 있음
- Feature를 뽑는것은 Pretrained 네트워크를 사용함, 건드릴 요소가 없음 알아서 처리함
- 직접 건드릴 부분은 Fully Connected와 Softmax를 건드릴 것임
- Fully Connected layer는 나온 feature들을 Output 클래스와 연결시켜주는 역할을 함

![one](/img/DeepLearning/Transfer/six.png)

- 이러한 학습시키는 과정자체가 Weights(가중치)를 계속 학습을 시키면서 업데이트함, 업데이트 하는 과정을 학습이라고 함, 학습의 대부분의 시간이 소요됨

![one](/img/DeepLearning/Transfer/seven.png)

- Alexnet을 썼으므로 아래와 같이 어떤 layer가 있는지 쭉 확인할 수 있음, 25개의 layer가 있음

![one](/img/DeepLearning/Transfer/eight.png)

- 23 Fully Connected는 2~22까지 거친 추출된 특징을 output과 연결해주는 것임, 2~22는 특징을 추출하는 것임
- 마지막 25만을 통해서 학습을 진행할 수 있음
- 레이어를 뽑아서 저장할 수 있음, 첫번째 마지막 layer를 아래와 같이 변수로 뽑을 수 있음, 그리고 내부값을 건드려서 커스텀해서 사용할 수 있음
- InputSize를 보면 해상도를 알 수 있고 OutputSize를 보면 1000개의 카테고리로 분류할 수 있다(1000개중의 하나의 선택)고 알 수 있음
- 이런 부분에 대해서 커스텀해서 내가 쓸 데이터를 활용할 수 있음

![one](/img/DeepLearning/Transfer/nine.png)

- output class에 대해서 직접 확인할 수 있음, 1000개 중의 하나인 카테고리 파일임, 이 중 하나로 반드시 예측을 해서 나옴(스코어가 가장 높은 값으로)

![one](/img/DeepLearning/Transfer/ten.png)

- 기존에 있던 Pretrained는 Alexnet을 사용하는데 Input image를 넣고 원하는 Output class를 3가지 중 하나로 예측하고 싶다면 그때 Fully Connected를 변경하고 라벨링을 입력해서 커스텀 해주면 됨, 그런식으로 활용할 수 있음, 1번째 23 ~ 25번째 변경
- Input 데이터 넣을때 사진만 넣는것이 아닌 그와 관련된 라벨링 즉 이게 무슨 사진인지도 레이블링 값도 넣어줘야함
- 그리고 input size에 대해서도 227 227이어야 하는데 그럼 내가 넣으려는 이미지 역시 이 정도로 다운샘플링을 해줘야함
- 아래와 같이 이미지를 불러올 수 있음, 같은 폴더내에 이미지 파일이 있어야함

![one](/img/DeepLearning/Transfer/eleven.png)

- 그러면 이미지 파일에 대해서 쭉 array 형태 x,y값을 받아옴, 실제 데이터는 아래와 같음, 이 값은 사진을 분석할 때 맨 좌측 윗상단부터 시작하여 거기서 RGB에서 R에 해당하는 값을 나타냄, 그러면서 차례로 연결해서 보여주는 것을 나타냄, 좌표에 대해서

![one](/img/DeepLearning/Transfer/twelve.png)

- 이를 이미지 형태로 볼 수도 있음, 아래와 같이

![one](/img/DeepLearning/Transfer/thirteen.png)

- Alexnet에 input size가 227, 227임, 이를 볼 수 있음 그 다음 그것에 맞춰서 이미지 사이즈를 강제로 리사이즈해서 input size에 맞춰야함, 이미지 리사이즈를 할 때 하나의 input 값으로 227x227를 하기 위해서 array로 묶어줌

![one](/img/DeepLearning/Transfer/fourteen.png)

- 정상적으로 리사이즈 됐음을 알 수 있음
- 그 다음 이미지를 classify 할 수 있음, 이를 doc을 활용할 수 있음
- 가장 기본적인 형태로 활용가능함, 아래와 같이, 이를 Boston Bull로 예측했음을 알 수 있음

![one](/img/DeepLearning/Transfer/fifteen.png)

- 가장 높은 score로 boston bull로 한 것인데 이 score 역시 아래와 같이 볼 수 있음, 1000개의 카테고리에 대한 score를 알 수 있음

![one](/img/DeepLearning/Transfer/sixteen.png)

- 여기서 max 값을 뽑을 수 있고 그 값이 Boston Bull인 것임

![one](/img/DeepLearning/Transfer/seventeen.png)

- 이 과정은 아무것도 건드리지 않고 예측을 했을떄의 결과를 본 것임
- 이제 제대로 된 TransferLearning을 할 것인데 여기서 alexnet을 수정할 것임, 거기에 맞게 원하는 데이터를 넣어서 학습을 시키고 FullyConnected와 softmax를 수정을 해서 원하는 결과를 예측할 수 있게끔 연결을 해줄것임
- 2 ~ 22번은 그대로 사용함, pretrained 네트워크는 원하는 레이블링, ground truth(정답을 알려줌), 데이터를 넣어줄 것임, 레이블링 된 데이터를
- 학습을 위해서 포메나리안이면 그 폴더에 그와 관련된 사진을 쭉 넣을 것임, 레이블링을 하여서 이 레이블링 값을 닫고 받아서 뒤에까지 수정해서 제대로 예측하는지 볼 것임
- 앞에서 한 작업은 그냥 그대로 넣어서 예측만 한 것임 이제는 원하는 데이터를 input으로 넣고 원하는 결과를 얻을 것임
- 여기서 모든 데이터를 넣어버리면 속도가 느려짐, 메모리 상으로 다 불러올 필요가 없음, 메타데이터 파일 네임과 위치만 불러오고 레퍼런스 어떤 폴더에 어떤 이미지가 있는지 포맷과 위치만 불러와서 할 것임
- 그럴 때 image datastore를 사용함, 큰 데이터를 불러올 때 시간과 데이터를 쓸 필요없이, 메타데이터만 사용해서 이를 레퍼런스만 하는 것임, 필요하면 불러오고 필요없으면 레퍼런스만 하는 것임
- 근데 이는 직접 불러와서 처리하는 것이 아니기 때문에 이때 augmentedImageDatastore 함수를 통해서 이미지를 리사이징 할 것임 혹은 좀 더 복잡한 로직 이미지를 돌리거나 필터할 때 augmeter를 사용함
- 이를 도식화하면 일반적으로 아래와 같이 단순하게 불러왔음, 그대로 가져와서 예측만 함

![one](/img/DeepLearning/Transfer/eighteen.png)

- 만약 이미지가 무수히 많다면 데이터 시간 낭비이기 때문에 아래와 같이 단순하게 datastore를 통한 폴더상태, 폴더의 이름을 지정한 후에 그 데이터만 가져오게 처리를 함, 이 폴더는 레이블링, groundtruth임

![one](/img/DeepLearning/Transfer/nineteen.png)

- 아래와 같이 파일의 이름과 포맷같은 메타데이터만 Files가 저장을 함

![one](/img/DeepLearning/Transfer/twenty.png)

- 그럼 아래와 같이 메타데이터만을 저장을 하고 필요할 때만 불러와서 사용 하는 것임, 속도는 몇 백배 빠름

![one](/img/DeepLearning/Transfer/twentyone.png)

- 그리고 찾는다면 아래와 같이 사용함 근데 여기서 image datastore에서 간단한 전처리를 한 뒤 불러올수도 있음

![one](/img/DeepLearning/Transfer/twentytwo.png)

- 여기서 그런데 전처리를 할 때는 AugmentedImageDataStore 처리를 함, 리사이즈 할때도 사용함
- 근데 일단 데이터 자체가 아래와 같이 깨지거나 색깔이 없거나 밝기가 안맞는등의 문제가 있을 때 이런걸 Preprocessing(전처리)를 해줘야함

![one](/img/DeepLearning/Transfer/twentythree.png)

- 이 전처리는 augmentedImageDatastore를 사용해서 전처리를 해 줌
- 아래와 같은 활용을 함, 원본 이미지를 가져오는 것이 아닌 메타이미지를 가져와서 리사이징을 하고 바로 input 데이터로 넣을 수 있음

![one](/img/DeepLearning/Transfer/twentyfour.png)

- 하지만 여기서 더 복잡한 이미지 전처리가 필요할 때는 imageDataAugmenter를 사용함, 이는 하나의 입력해주는 옵션으로 생각해주면 됨, Augment를 써도 하나의 옵션 변수로 받고 처리해야함, 그 변경된 값을 다시 augmentedImageDatastore에 사용함 즉, imageDatastore을 그대로 쓰는 경우는 매우 드뭄

![one](/img/DeepLearning/Transfer/twentyfive.png)
![one](/img/DeepLearning/Transfer/twentysix.png)

- 하나의 옵션으로 활용하는 것뿐 직접 넣는것은 아님
- 불러오는 과정은 아래와 같이 처리함, imageDataStore에서 petImages 폴더를 기준으로 하위 폴더를 다 포함하고 LabelSource를 foldernames으로 나오게 함, 아래와 같이 Data가 쭉 저장됨

![one](/img/DeepLearning/Transfer/twentyseven.png)

- 영구적으로 추가한다면 Set Path에 추가하면됨
- 이렇게 저장하면 meta infomation만 저장되어 있음
- 사진을 보는 방법은 다양함, 그냥 폴더로 들어가서 봐도 됨, 혹은 matlab에서 앱에 있는 Image Browser를 통해서 볼 수도 있음
- Load해서 PetImage 폴더를 하면 모든 이미지를 쭉 볼 수 있음, Image Viewer를 통해서 볼 수 있음, 그리고 이미지 추출 등 편리한 UI를 활용할 수 있음
- 혹은 Image Labler에서 여러 사진 중 Boundary Boxing을 해서 Lablering을 직접 할 수 있음
- 아래와 같이 raw하게 할 것임 일반적으로 아래와 같이 코드를 쓰라고 나와 있을 것임

```matlab
imageAll = imtile(imageDS)
imshow(imageAll)
```

- 하지만 속도차가 나고 데이터가 많아서 이를 사용하지 않고 다른 함수를 쓸 것임
- 여기서 그래서 위와 같이 petImages 폴더를 다 하지 않고 나눌것임, 왜냐하면 그 폴더에 1300개 가량의 이미지가 있는데 이를 타일화하면 너무 많음
- Lucy만 체크를 할 것임, 아래와 같이 하위폴더를 두고

![one](/img/DeepLearning/Transfer/twentyeight.png)

- 그 파일을 보여줄 것임, 여기서 imtile이 아닌 montage를 활용해서 볼 것임, imtile은 훨씬 더 오래걸림

![one](/img/DeepLearning/Transfer/twentynine.png)

- 여기서 사이즈를 바꿔줘야함, 왜냐면 227 227이 input size이기 때문에, 아래와 같이 리사이즈 할 수 있음

![one](/img/DeepLearning/Transfer/thirty.png)

- 이미지를 바꿈, 이제 여기서 몇 몇 특성을 커스텀 할 것임, 그 전에 데이터를 한 번 clear 했기 때문에 layer를 저장해두면 됨
- 지금 상태는 input data layer는 바꾼 것임, 이제 2~22는 그대로 쓰고 23인 Fully Connected를 바꿀 것임
- 우선 기본적인 Output은 1000개임을 앞서 확인했었음, 여기서 이를 커스텀 할 때는 우리가 일단 Input data에 대해서는 petImages에 있는 것으로 레이블링을 했기 때문에 output 예측값 역시 이 petImages의 14개의 폴더의 레이블링이어야 함, 왜냐하면 이 데이터로 예측을 하려고 했기 때문에, 그래서 해당 폴더 레이블링으로 해야함
- 그 중 몇 개는 테스터 데이터로 쓸 것이므로 무작위로 80%만 뽑아서 시행할 것임, 나머지 20%는 하나를 던져서 무엇인지 판단하는 데이터로 쓸 것임
- 그래서 그에 맞게 fully connected를 레이블링 값으로 수정할 것임
- 도식화 한다면 아래 첫번째 그림처럼 된 것을 두 번째 그림처럼 바꾼다는 것임, 딱 뒷부분만 바꿔준다는 것임

![one](/img/DeepLearning/Transfer/thirtyone.png)
![one](/img/DeepLearning/Transfer/thirtytwo.png)

- 실제 코드로 구현한다면 아래와 같이 함, outputsize를 14개로 하고 그 다음 Classification Output 역시 refresh 해줌 같이 따라가는 것임, 아무것도 안 넣어주면 됨, 이러면 23, 25를 바꾼 것임

![one](/img/DeepLearning/Transfer/thirtythree.png)

- 그 다음 데이터를 준비하고 Training data와 Test data로 나눈 후 Training Options을 바꾸고 그 결과를 보면 됨
- imageDS를 이용해서 Training data와 Test data를 나누고 training data로 앞서 만든 network를 training 시키고 그 결과를 test data를 이용하여 visualization하고 결과를 confusionchart로 볼 것임
- 먼저 layers, net을 불러온 뒤 imageDS를 이용해서 전체 petImages를 불러와서 나눌 것임
- 먼저 아래와 같이 불러오면 됨, 앞서 작업한 방식과 동일하게

![one](/img/DeepLearning/Transfer/thirtyfour.png)

- 그런 다음 data set을 splitEachLabel 함수를 활용해서 나눔, imageDS를 불러오고 비율을 설정 0.8 즉 80%만 training으로 쓰고 20%는 test를 한다는 것임, 기본만 설정
- 각각 trainImage, testImage로 나눠서 받으면 됨

![one](/img/DeepLearning/Transfer/thirtyfive.png)

- 하지만 이미지의 크기가 크기 때문에 원래대로 raw하게 그대로 써버리면 이미지를 불러오고 처리할 때마다 속도가 점점 느려지게 됨, 하지만 imageDataStore를 사용한다면 meta 데이터만을 활용하기 때문에 그럴일이 없음
- augment를 활용해서 이미지 사이즈를 변형해줘야함, 아래와 같이

![one](/img/DeepLearning/Transfer/thirtysix.png)

- 이렇게 하면 사전작업은 모두 처리한 것이므로 아래와 같이 결과가 나옴

![one](/img/DeepLearning/Transfer/thirtyseven.png)

- 그런 다음 training options을 조정할 것임, 왜냐하면 trainNetwork 함수 사용시 data, layers와 함께 option이 필요함, data는 traindata, layers 즉 net에서 받은 layers를 수정한 것을 넣게됨, 여기서 추가적으로 option이 필요하기 때문에 training Option을 만들어줌
- 여기서 trainingOptions은 sgdm을 쓸 것임, 여기서 옵션 중 InitialLearnRate weight를 업데이트 할 때 학습시 업데이트할 때마다 한 걸음 나아간다고 할 때 그것을 정해주는 것임, 이를 설정해서 초기 세팅이 가능
- 그리고 plot으로 보기 위해서 training-progress를 볼 수 있음
- options과 관련해 그와 연관된 값이 쭉 뜸

![one](/img/DeepLearning/Transfer/thirtyeight.png)

- 그러면서 그 다음에 trainNetwork를 할 것임

![one](/img/DeepLearning/Transfer/thirtynine.png)

- 그러면 이제 학습되는 값(정확도)과 loss값 결과창이 아래와 같이 나옴

![one](/img/DeepLearning/Transfer/fourty.png)
![one](/img/DeepLearning/Transfer/fourtyone.png)

- 여기서 Epoch와 mini-batch에 대해서 계속 나옴
- mini-batch는 학습을 통해서 layers에서 가중치를 업데이트하는데 최소 사이즈임, 매 미니 배치마다 올라감, 로스는 떨어짐
- mini-batch가 그런 주기를 설정하는 것임, 앞서 설명한 options에서 InitialLearnRate를 조정하면 mini-batch의 값이 들쭉날쭉할 수 있음
- 하지만 처음 실행시 그 실행 시간이 현저히 오래 걸림 왜냐하면 Single-CPU를 사용하기 때문에 GPU를 사용하게 된다면 현저히 빠르게 돌릴 수 있음, 이는 Addon을 써서 사용하면 됨(parallel computing toolbox 사용), 이러면 자동으로 GPU와 multi를 사용해서 씀, GPU를 자동으로 인식해서 씀
- 여기서 학습률 조정 계획도 변경할 수 있음
- 위처럼 학습을 한 뒤 끝나면 아래와 같이 나옴

![one](/img/DeepLearning/Transfer/fourtytwo.png)

- 위처럼 일련의 과정을 통해서 training을 하면 됨
- 그 다음 test data를 통해서 퍼포먼스를 확인할 수 있음, classify를 통해서 처리를 먼저 함
- 그런 다음 ground truth 실제 값을 볼 수 있음, 여기서 meta-information에서 폴더 정보에 대해서 Labels로 넣어줬기 때문에 이 값이 ground truth 값으로 처리할 수 있음, 그러면 해당 값들이 처리되서 나옴

![one](/img/DeepLearning/Transfer/fourtythree.png)

- 그런 다음 그 값을 비교를 하면 됨, 여기서 testPred와 testGT를 array 끼리 비교를 해서 true, false인 1과 0으로 나타낼 수 있음
- 여기서 이 합을 구하면 맞은 개수를 알 수 있음, 그런 다음, 이 합을 array의 개수로 나누면 raw한 방법으로 정확도를 구할 수 있음

```matlab
**sum(testPred == testGT) / 270 % Prediction Accuracy**
```

- 좀 더 정석적인 방법으로 한다면 nnz, 0 값이 아닌게 몇 개인지 확인을 하고 이를 numel을 통해서 총 개수를 나누면 됨

![one](/img/DeepLearning/Transfer/fourtyfour.png)

- 그 다음 이를 시각화 할 수 있음, confusionchart를 활용해서

![one](/img/DeepLearning/Transfer/fourtyfive.png)
![one](/img/DeepLearning/Transfer/fourtysix.png)

- prediction시 클래스와 실제 클래스인 경우 이게 맞는 경우가 파란색이고 안 맞은 경우는 다른색깔임, 즉, 대각선인 경우 맞은 개수임, 그 외는 다르게 예측한 경우임