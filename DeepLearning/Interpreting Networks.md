### Interpreting Networks
- 지나가면서 이미지가 어떻게 변하는지 알아볼 것임
- Convolution, ReLU, Max Pooling Layers 등
- 이미지가 기본적으로 2D-array이지만 각각의 layer를 지나갈 때 어떻게 변하는지는 추상적으로 밖에 알 수 없음
- 하지만 이러한 결과물에 대해서 즉, layer를 지날때마다 filter 들이 씌워지고 그 결과를 볼 것임, 이는 수학적인 모델에 좀 더 가깝게 됨
- 각각의 feature extraction을 하였는데 각각 layer를 지날 때 어떤 형식으로 바뀌고 feature extraction이 되는것인지 볼 것임
- 점진적으로 나갈수록 수학적인 모델에 가까워 질 것임
- 이미지에 대해서 어느정도 보기 쉽게 뽑아낼 수 있음
- 여기서는 Alexnet이 아닌 squeezenet을 써볼 것임

![one](/img/DeepLearning/Interpreting/one.png)
![one](/img/DeepLearning/Interpreting/two.png)
![one](/img/DeepLearning/Interpreting/three.png)

- 여기서 채널은 3개임에 집중해야함, 이 채널은 RGB로 볼 수 있음
- 각각의 이미지를 뽑아보면 흑백이미지이지만 이를 합쳐두면 컬러이미지가 되는 것임
- 실제 컴퓨터 입력에선 image가 array 형태로 수학식이 적용되어서 보임
- layer는 68계층이 있는데 이를 좀 더 쉽게 볼려면 아래와 같이 가능함

```matlab
analyzeNetwork(net)
```

![one](/img/DeepLearning/Interpreting/four.png)

- squeezenet의 경우 alexnet보다 좀 더 복잡한 계층구조를 가지고 있음, convolution, ReLU, maxPooling등
- 이 구조를 쭉 따라가다 보면 FullyConnected가 없을 볼 수 있음, 여기서 pool10이 이를 대신함, 이는 overfiting에서 좀 더 자유로움
- 이런식으로 자세하게 해당 network에 대해서 분석하여 볼 수 있음
- 여기서 좀 더 볼 부분은 Activation을 봐야함, 이 의미는 network layers 사이에서 이동되는 정보들임, 어떤 함수를 써서 사이에 정보가 어떻게 전달되는가를 Activation을 볼 수 있음
- 어떤 채널 형태로 전달될 때 하나의 layer에서 나올 때 그 layer에서 나오는 output에 대해서 Activation이라고 하고 볼 수 있음
- 하나의 필터를 거치면 그 결과는 채널의 저장이 됨 위에서 보이는 113x113x64에서 64 이 숫자에서
- Activation은 하나의 layer에서 나오는 결과물임, 본질적인 output은 아님, 어떠한 값이 나오는지 activation 함수를 통해서 볼 수 있음
- 먼저 convolution layer가 어떻게 되어 있는지 아래와 같이 봄

![one](/img/DeepLearning/Interpreting/five.png)

- Hyperparameter는 set predetermined, 학습하면서 바뀌지 않는 값이고 learnable parameter는 학습하면서 계속 바뀌는 것임
- 여기서 NumChannel은 layer에 들어오는 채널이 3이라는 것, 하지만 필터가 64개니깐 빠져나오는 채널은 64개가 되어서 마지막이 64임
- 정보가 아래와 같이 layer마다 넘어감, 화살표는 infomation이어도 layer를 통과해서 나온 결과, activation 값임, 어떠한 정보들이 활성화 되는지 보기 때문에

![one](/img/DeepLearning/Interpreting/six.png)

- 아래처럼 컬러가 있는 모양이라도 2D 형태로 나타내야 하기 때문에 3개의 채널로 나눈것임, RGB 값으로 나타내는 것이므로(RGB 형태의 3채널 2D array로)

![one](/img/DeepLearning/Interpreting/seven.png)
![one](/img/DeepLearning/Interpreting/eight.png)

- 그리고 필터에 따라서 아래와 같이 바뀌게 됨

![one](/img/DeepLearning/Interpreting/nine.png)
![one](/img/DeepLearning/Interpreting/ten.png)

- 이런식으로 필터를 거치면서 그 결과를 Activation이라고 함, 그래서 이 과정에서 어떠한 feature를 잘 뽑으면 특징들을 잘 추출할 수 있음을 의미함

![one](/img/DeepLearning/Interpreting/eleven.png)
![one](/img/DeepLearning/Interpreting/twelve.png)

- 넣는값이 이미지 데이터여서 위와 같이 하지만 CNN은 이미지를 넣고 그 이미지를 하나의 layer의 몇 번째 filter를 거쳐서 어떻게 나오는지 눈으로 보기 쉽게 처리할 수 있음
- CNN은 이미지만을 위한 용도는 아님
- 여기서 Feature Extraction에서 어떤 기능으로 뭘 하는지 눈으로 확인하기 위해서 이미지를 넣어서 보는 것임, 아래와 같이 feature들이 나오게 되면

![one](/img/DeepLearning/Interpreting/thirteen.png)

- 앞에서 먼저 layer를 봤으므로 그 다음 어떤 정보가 보이는지 알 수 있음, 아래와 같이 net과 image를 넣고 해당 layer인 conv1을 넣으면 그러면 conv1이 64개의 채널을 가지고 있음을 알 수 있음

![one](/img/DeepLearning/Interpreting/fourteen.png)

- 이 array는 하지만 숫자로 보아서 큰 의미를 알 수가 없긴 함, 64개 채널의 array가 있기 때문에, 여러가지가 있음을 추측만 가능함
- 이 결과를 직접 볼 수 있음 montage를 썻지만 imtile을 써도 됨

![one](/img/DeepLearning/Interpreting/fifteen.png)

- 위처럼 64개의 하나의 결과물을 하나의 필터를 거친 결과물을 볼 수 있음, 순서대로 1~8 / 9~16 순으로 감
- 첫번째 필터를 거친 것이 첫번째(1,1)의 activation임
- 여기서 몇 개는 확실하게 보이는게 있음, 눈만 보이던가, 눈과 입만 보이던가, 이러한 결과물은 수학적으로 convolution하면 나오는 것임
- 보통 완전 흑백으로 보진 않고 gray scale로 아래와 같이 봄, 여기서 의미는 아무 없는 matrix 행렬 형태를 gray 형태로 본다는 것을 의미함, 그럼 좀 익숙한 회색조 이미지로 볼 수 있음

![one](/img/DeepLearning/Interpreting/sixteen.png)

- 왼쪽위부터 오른쪽으로 차례대로 쭉 나아감, 각각 channel 1, 2... 가 됨
- 하나의 filter를 씌울 때도 왼쪽에서 오른쪽으로 씌움 순서가
- 근데 특정 filter는 특징들이 나타나게끔 눈에 두드러지게 나오게 하는것들이 있음
- 하얀색으로 나오면 positive strong, 검은색이면 negative strong임, 검은색에서 밝은 색으로 추출하는 필터를 사용시 특정 부분이 그렇게 보임 혹은 가로선으로 하는 필터가 있음
- grayscale에서도 역시 이를 볼 수 있음, 아래와 같이 나옴을 알 수 있음

![one](/img/DeepLearning/Interpreting/seventeen.png)
![one](/img/DeepLearning/Interpreting/eighteen.png)
![one](/img/DeepLearning/Interpreting/nineteen.png)

- ReLU를 씌우면 밝은 것만 살아남고 불필요한것을 날림 그 다음 maxPooling을 씌우는 로직으로 됨
- ReLU에서는 양의 값은 그대로 두고 음의값을 0으로 바꿔버림, 하얀색만 놔두고 애매한것은 다 0으로함 maxPooling을 씌우면 강제로 다운 샘플링함, 추출된 특징을 강제화 시키기 위해서, 그러면 눈에 확 띄니깐 아래와 같이 진행이 됨

![one](/img/DeepLearning/Interpreting/twenty.png)
![one](/img/DeepLearning/Interpreting/twentyone.png)

- 그 다음 봐볼 것은 앞서 actvn1을 통해서 activation으로 64개의 layer를 값으로 받았고 그 중 channel 41을 봐볼 것임, 해당 데이터를 뽑아볼 수 있음

![one](/img/DeepLearning/Interpreting/twentytwo.png)

- 그리고 이를 mat2gray를 통해서 변환을 해서 볼 수 있음

![one](/img/DeepLearning/Interpreting/twentythree.png)

- 하지만 그 전에 이미지 리사이즈를 할 것임, 원래 이미지 사이즈와 동일하게 볼 것임, 앞서 정의한 sz 변수 활용, 그 다음 이미지를 볼것임, 여기서 imshow와 montage를 써도 되지만 원본 이미지와 나란히 비교해서 볼 것이므로 다르게 쓸 것임
- 여기서 비교할 때 cell 형태로 묶어줘야함, 왜냐하면 image와 actvn1_ch41이 숫자형태로 되어있기 때문에, 나란히 보여주기 위해서 cell 형태로 묶어줘야함

![one](/img/DeepLearning/Interpreting/twentyfour.png)

- 그 다음 channel 22에서도 볼 수 있음

![one](/img/DeepLearning/Interpreting/twentyfive.png)

- 위처럼 activation의 output 값을 눈으로 확인가능, 하나하나 확인해서 layer를 짤 때 어떤 필터를 써서 결과가 나오는지 알기 위해서 볼 수 있음
- 위에서 쓴 채널을 보면 대략적으로 사진을 보고 channel 22의 경우 ReLU, Max Pooling을 하면 입이 추출될 것 같다는 것을 짐작할 수 있음
- 하지만 이제 알아볼 Deeper Layer Activations에서는 Layer가 깊어질수록 현재 볼 Layer는 35번째인데 이는 충분히 필터를 많이 거치고 ReLU, MaxPooling을 지나가고 크기가 작아진 결과인데 점점 알아보기가 힘들어짐
- 즉, Deeper Layer 뒤로 갈 수록 점점 보기 힘들고 블랙박스라고 함, 어떤 특징이 들어가는지 알기 힘듬, 딥러닝에서는 explainable이라고 함, 이 특징을 알기 위한 기법의 의미로써 말함
- 하지만 이를 블랙박스가 아닌 사람이 이해하고 알기 쉽도록 필터의 특징도 확실하게 알도록 그렇게 할 수 있는 기법이 꽤 많이 나옴
- 먼저 Deeper Layer를 추출할 것임, 통으로 다 볼 수 있음, 48개의 채널과 쭉 나오는 것을 알 수 있음

![one](/img/DeepLearning/Interpreting/thirty.png)

- 하지만 montage로 봤을 때 점점 알아보기가 힘듬, 사람 얼굴을 찾기 어려움, 여기서 보고자 하는 것은, positive strong(흰색)을 본다면 눈만 나타나는 것들이 있음, 그 채널이 47인데 그 channel을 볼 수 있음
- 이 추출 과정을 위에서 한 것처럼 채널을 뽑고 mat2gray한 뒤, 리사이즈해서 montage로 나란히 볼 수 있음

![one](/img/DeepLearning/Interpreting/thirtyone.png)

- 35번째 layer에서 activation은 위와 같은데 거의 알아보기 힘들지만 눈만 나타나는 특징을 추측할 수 있음, 이를 학습시킨다면 눈에다가 레이블링을 하고 학습을 시킨다면 35번째 layer에서 activation값에서 위의 예시가 weight가 매우 크게 나올 것임 눈만 높기 때문에, 그러면 네트워크가 이를 인식하고 처리할 것임
- MaxPooling layer는 현재 network에서는 제외임
- 그럼 이제 위처럼 처리한 뽑은 layer에서 ReLU가 어떻게 나오는지 볼 수 있음, ReLU를 뽑고 똑같이 해당 채널을 뽑고 mat2gray 처리를 하고 리사이즈 하고 montage 처리하는 과정은 똑같음, 여기서 한 번 이전에 추출한 값도 비교할 수 있음, 아래는 2x2인데 이를 1x3으로 보기 편하게 처리 가능

![one](/img/DeepLearning/Interpreting/thirtytwo.png)
![one](/img/DeepLearning/Interpreting/thirtythree.png)

- 3번째 사진은 모든 음수값들이 0으로 바뀌면서 눈의 특징이 더 눈에 띔을 알 수 있음
- 그 다음에 Pooling해서 다운샘플링 되면 그 특징이 더 극대화됨, 이런식으로 특징을 추출하고 이 특징들을 바탕으로 학습을 진행함
- 학습을 할 때는 이 특징과 레이블링값, ground truth 값, 라벨링 값 혹은 output class값으로 즉, 레이블링값과 연결시키면서 계속 학습을 하면서 weight값을 체크하면서 학습을 함