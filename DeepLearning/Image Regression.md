### Image Regression
- Output 값이 어떠한 Discrete 즉, 고양이 강아지 등으로 나뉘는게 아니고 Continuous Value로 나오는 것을 말함 Continuous reponse value
- 이미지에서 아래와 같이 각도 클래스, 카테고리가 아닌 아래와 같이 연속성있는 숫자로 나오는 것
- 이런 특징을 이용해서 얼굴이 몇 도 틀어져 있는지 등을 예측할 수 있음

![one](/img/DeepLearning/ImageRg/one.png)

- 현재 사용하고 아래의 값은 RGB 값을 강제로 돌리는 것, 변형
- 원본에서 얼마나 RGB가 바뀌었는지 예측하고 그것을 기준으로 변환을 할 것임 GroundTruth 값도 있음, 변경된 RGB를 확인하여서 정확도를 체크할 것임
- 정확도를 나타내는 척도가 RMSE를 쓸 것임, 여기서 예측된 데이터를 실제 이미지 RGB를 변경해서 원본의 자연색에 가까운지 체크할 것임
- 위의 예시처럼 Output이 아닌 Response로 많이씀, 하나의 숫자값으로 나옴, 아래의 사용값은 Response Variable이 3개임
- 해당 데이터는 imageDS와 동일하게 파일 위치와 이미지 그리고 그 값이 나옴(RGB로), 테이블 형태로 되어 있음

![one](/img/DeepLearning/ImageRg/two.png)
![one](/img/DeepLearning/ImageRg/three.png)

- 이 데이터를 볼 수 있음, cell 형태로 씌워서 볼 수 있음, 여기서 RGB가 같은 이미지라도 왜곡되어 있음을 알 수 있음

![one](/img/DeepLearning/ImageRg/four.png)
![one](/img/DeepLearning/ImageRg/five.png)

- 여기서 데이터 기준으로 table을 보면 RGB가 Color 부분에서 값이 각각 왜곡되어 있음을 알 수 있음

![one](/img/DeepLearning/ImageRg/six.png)

- 여기서 Transfer Learning을 할 것인데, alexnet을 사용할 떄 Image Regression에 맞게 설정을 할 것임, fullyConnectedLayer을 교체하고 softmax, classification을 삭제해주고 Regression을 추가하면 됨

![one](/img/DeepLearning/ImageRg/seven.png)

- 그 전에 데이터를 미리 준비해둬야함, 사이즈는 227x227x3이고 alexnet Input도 동일해서 이미지 리사이즈 할 필요는 없음, 하지만 변경한다고 가정하고 처리해봄, 현재 예시에는 필요는 없음,생략해도 됨
```matlab
trainds = augmentedImageDatastore([227 227], trainingData);
testds = augmentedImageDatastore([227 227], testData);
```
- 그 다음 layers를 변경하면 됨, fullyConnected 변경은 RGB이므로 output은 3으로 하면 됨 만약 Continuous 한 경우에는 2로 바꾸면 됨, 그 다음 softmax와 output을 바꿔주면 됨, 빈 배열로 여기서 굳이 end 아니고 직접 그 layer 층을 입력해도 됨
- 여기서 layers가 fullyConnected만 남아있으므로 새로 layers를 만들어야 하므로 아래와 같이 기존 layer에다가 regression을 추가하면 됨
- 여기서 end를 썼으므로 한 번 실행시킬때마다 layers가 사라짐, 그러므로 잘 확인하고 해야함

![one](/img/DeepLearning/ImageRg/eight.png)

- train은 동일함, options 생성하고 trainNetwork를 진행하면 됨, 다른점은 layers밖에 없음
- Image Regression은 RGB값을 원상복귀 시키는데도 활용이 되고 화질 향상에도 사용되고 이미지 기울기를 파악하고 복구시키는데도 쓰임
- 여기서 그래프가 Acc가 아닌 RMSE 값이 나옴, Loss값도 매우 중요함, Loss가 떨어지는 것을 봐야함, 여기서 과적합이 되는 즉 Loss가 올라간다고 보일 때 거기서 멈추고 조정하는게 중요함, Validation도 무조건 확인해야함, 계속 떨어진다고 해도 과적합 있을 수 있음 이때 Validation을 봐야함

![one](/img/DeepLearning/ImageRg/nine.png)
![one](/img/DeepLearning/ImageRg/ten.png)

- 여기서 Evaluate도 하면 됨, 방법만 다르지 방식은 유사함, predict를 함, GT값은 testData가 table 형태의 Color를 가져오면 이 값이 GT 값임, err 값은 참에서 예측값을 빼주면 됨
- rmse의 경우 err을 각각 제곱을 하고(마이너스를 없애기 위해) mean값을 구하고 sqrt값을 씌우면 됨, 각각 rgb 값에 대해서 나오는 것임

![one](/img/DeepLearning/ImageRg/eleven.png)

- 이 값을 바탕으로 하나의 이미지를 선택해서, 그 값을 불러와서 network를 통해서 개선을 할 수 있음, 여기서 아래와 같이 본다면 좀 붉은빛을 띄는 것을 알 수 있음

![one](/img/DeepLearning/ImageRg/twelve.png)

- 여기서 correctColor를 보게 되면 function script로 이미지를 넣고 그 rgb값을 넣으면 rgb를 업데이트해서 보정을 하게 됨
- 여기서 testPred의 즉, network가 예측한 첫번째 행을 가지고 그 값을 저장한 뒤 이미지를 보정할 것임, 여기서 해당 함수를 불러온 뒤 이미지를 넣고 보정할 rgb 값을 넣어주면 됨

![one](/img/DeepLearning/ImageRg/thirteen.png)

- 그럼 아래와 같이 보정이 됨, 어느정도 붉은빛이 사라짐

![one](/img/DeepLearning/ImageRg/fourteen.png)

- 그 뿐만 아니라 아래와 같이 imageNum을 통해서 원하는 이미지를 가지고 보정을 할 수 있음

![one](/img/DeepLearning/ImageRg/fifteen.png)

### Spectrogram
- CNN을 이용하되 이미지가 아닌 소리 데이터를 활용함 Spectogram 즉, 음성 데이터지만 이미지화해서 저장을 하면 CNN을 사용할 수 있음, 시간에 따라서 이미지 크기를 저장할 수 있음
- 그 시간에 음에 대한 주파수 대역까지도 저장할 수 있음, 음역대등
- 이를 Spectrogram으로 이미지화를 할 수 있음, 음성의 크기 뿐 아니라 그 각각의 이미지 대역폭을 저장할 수 있음
- 아래와 같은 과정을 거침
- 이런식으로 spctrogram을 사용해서 CNN을 거쳐서 체크를 할 수 있음

![one](/img/DeepLearning/ImageRg/sixteen.png)
![one](/img/DeepLearning/ImageRg/seventeen.png)

- 여기서 소리를 보면 아래와 같이 각각의 주파수가 있음을 알 수 있음, 여기서 동시에 누르면 이 주파수 대역이 합쳐지면 마치 2번째 사진과 같이 노이즈가 있는것처럼 하나로 합쳐짐을 알 수있음
- 여기서 역으로 주파수 분석을 하면 2번째 사진이 1번째 사진처럼 이룬다는 것을 알 수 있게됨

![one](/img/DeepLearning/ImageRg/eighteen.png)
![one](/img/DeepLearning/ImageRg/nineteen.png)

- 이런식으로 어떤 주파수가 들어오면 그 대역대별로 즉 분석해서 나누고 그것을 이미지화 하는 것임, 그리고 그 각각의 주파수 대역대에서 어떤게 사운드가 가장 큰 지, 어떤 주파수의 Contribution이 가장 큰 지 볼 수 있음

![one](/img/DeepLearning/ImageRg/twenty.png)

- 아래처럼 건반을 누를 때에도 소리가 다양하게 나타나고 그 다음 여기서 동시에 주파수 분석을 하고 Contribution을 보면 아래와 같이 볼 수 있음

![one](/img/DeepLearning/ImageRg/twentyone.png)

- 위의 방식도 꽤 복잡함, 이를 시간에 따라서 아래와 같이 시간에 따라 눌렀을 때 주파수 대역을 파악할 수 있음

![one](/img/DeepLearning/ImageRg/twentytwo.png)

- 여기서 Contribution이 높으면 바를 노란색으로 칠하고 길이는 다 똑같이 하면 아래와 같이 나타남
- 즉, 이런식으로 각각의 건반을 누를때 일정한 바 길이를 가진 Contribution을 알 수 있음

![one](/img/DeepLearning/ImageRg/twentythree.png)

- 이를 다 합치면 아래와 같이 되고 이를 Spectrogram이라고 함, 아래를 보면 낮은 음역대일 때 Contribution이 높으므로 Frequency가 낮을 때 노란색임을 알 수 있음, 음에 따라 다르게 나타남을 알 수 있음

![one](/img/DeepLearning/ImageRg/twentyfour.png)
![one](/img/DeepLearning/ImageRg/twentyfive.png)

- 사이렌, 천둥번개 등도 아래와 같이 표현이 가능함

![one](/img/DeepLearning/ImageRg/twentysix.png)

- 직접 오디오 데이터를 가져와서 할 수 있음, 여기서 시간에 따른 데이터, 샘플링 Frequency로 데이터를 읽어서 두 개의 아웃풋의 저장함
- 시간에 따라서 2개의 데이터가 있는데 대부분 하나로 나타남

![one](/img/DeepLearning/ImageRg/twentyseven.png)

- sound 함수를 통해서 직접 들을 수 있음

![one](/img/DeepLearning/ImageRg/twentyeight.png)

- 이를 plot을 보면 1번째 열, 2번째 열이 아래와 같이 나타남을 알 수 있음

![one](/img/DeepLearning/ImageRg/twentynine.png)

- 여기서 두 줄을 다 써도 되지만 편의상 1번째 열만 쓸 것임, 그렇다고 y(:,1)만 실행해도 소리가 달라지지 않음

![one](/img/DeepLearning/ImageRg/thirty.png)

- 여기서 이를 주파수 분석을 위해서 Spectrogram 함수로 볼 것임

![one](/img/DeepLearning/ImageRg/thirtyone.png)

- 여기서 좀 더 자세히 보기 위해서 ylim을 걸어서 볼 수 있음, 여기서 음에 따라 차이가 있음을 알 수 있음

![one](/img/DeepLearning/ImageRg/thirtytwo.png)

- 이제 이 데이터를 가지고 학습을 시켜서 처리를 할 수 있음, 데이터가 많고 다양한 데이터를 학습시켜 활용할 수 있음
- 이를 이미지화 하기 위해서 colorbar, powerbar를 다 없애야함, 즉 주변을 다 없애야함, hold on 위에 있는 figure를 잡고 처리를 함
- 그러면 이제 이 이미지화 된 것을 가지고 이 형태의 Spectrogram을 활용해서 CNN을 해서 이미지 Classification을 적용할 수 있음

![one](/img/DeepLearning/ImageRg/thirtythree.png)
