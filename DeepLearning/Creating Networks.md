### Creating Networks
- 직접 layer by layer를 설계하고 학습하고 원하는 output을 뽑을 수 있게 할 것임
- fromscratch 아무것도 없는 상태에서 설계하고 학습시킬 것임
- Network를 적용할 수 있는 방법은 아래와 같이 3가지임

![one](/img/DeepLearning/Creating/one.png)

- Pretrained Network는 어떠한 수정 없이 그대로 사용하는 것임, 하지만 원하는 output class를 예측할 수 없음, 그래서 원하는 예측을 위해서는 Pretrained network를 일부 수정해서 Transfer Learning으로 사용함
- 하지만 Transfer Learning을 전부 다 적용할 수 없음, 이런 경우 Training from scratch 즉 직접 설계를 해야함, 하지만 많은 경우에 있어서 Pretrained, Transfer Learning을 사용하는게 좋음, 시간과 노력을 작게 하고 중상이상의 퍼포먼스를 얻을 수 있음, 이미지 분류에 있어서
- 하지만 모든 경우에서 Transfer Learning을 사용할 수 없으므로 직접 설계하는 것임
- Pretrained와 Transfer 같은 경우 아래와 같이 미리 설계가 되어있고 이를 활용함

![one](/img/DeepLearning/Creating/two.png)
![one](/img/DeepLearning/Creating/three.png)

- 만약 FullHD 데이터 1920 x 1080 사이즈가 있으면 다운샘플링 하면 되지만 만약 구글 위성데이터 혹은 구글 위성 데이터에서 사람 건물 등을 추출하고 싶다면? 이는 픽셀 사이즈가 너무 작아서 업샘플링을 해도 데이터 손실이 크고 퍼포먼스가 떨어짐, 아래와 같이, 그런 경우 적용을 하면 안됨

![one](/img/DeepLearning/Creating/four.png)

- 혹은 특정 사이즈의 데이터가 있다면 다운 샘플링을 하면 되지만 너무 작은 경우 퍼포먼스가 떨어지고 아니면 3채널이 RGB가 아닌 추가적인 다른 이미지가 있는 다채널 4~5채널인 경우 적용하기 어려움, 여기서 걍 2채널을 날려도 되긴 하지만 중요한 정보가 날라갈 수 있음
- 위의 2가지 경우 Training from scratch를 써야함, layer를 하나하나 빌드해가면서 설계해야함
- 가장 대표적으로 자율주행차의 경우 RGB + Rider가 있음, 이 경우 Rider를 날릴 수 없어서 매우 중요함 혹은 적외선, 수중 음향 탐지의 경우 활용해야함
- layer를 일단 빌드를 하면 training하는 방법은 동일함
- 가장 큰 차이점은 network가 가지고 있는 feature extraction을 그대로 사용하고 앞 뒤 layer만 수정하지만 scratch의 경우 다 만들어야 함
- 이러한 layer가 어려운 것은 매우 많은 layer가 존재함, 이를 어떻게 배치하고 써야하는지 감을 잡기 어려움, 그런 점이 가장 어려움

![one](/img/DeepLearning/Creating/five.png)

- 하지만 그래도 처음부터 끝까지 layer by layer를 다 쌓는 경우는 극히 드물다, 가지고 있는 데이터와 비슷한 유형의 데이터를 pretrained data가 있으므로 그것을 참고를 해서 분석해서 활용하여 모방을 하고 데이터에 맞게 최적화 시킬 수 있음
- 아래와 같이 미리 설계된 것을 보고 활용, 어떻게 layer를 설계할지 feature extraction을 할 지 ReLU를 어떻게 할 지등, 참고를 하는 것

![one](/img/DeepLearning/Creating/six.png)

- 예제로 사용할 데이터는 위성 이미지임, 맨땅인지, 숲인지, 빌딩인지 등을 파악, RGB 이미지임 사이즈는 28x28임 사이즈가 너무 작아서 기존 Transfer Learning 하기 어려움 더군다나 적외선 채널이 추가되서 RGB 채널만 가지고 하기 힘듬
- RGB+적외선 채널 4채널임, OUTPUT LAYER는 6개 사이즈는 28X28임
- 먼저 데이터를 불러옴

![one](/img/DeepLearning/Creating/seven.png)

- 그리고 데이터를 잠깐 들여다보면 아래와 같음 이는 사이즈와 label을 확인할 수 있음

![one](/img/DeepLearning/Creating/eight.png)

- 507번째 이미지를 gray scale로 볼 것임 왜냐하면 적외선이 있기 때문에, 여기서 건드리는 데이터는 무조건 TrainData임
- 매우 작고 깨지는 것을 볼 수 있음, 위성이미지기 때문에, label은 building임

![one](/img/DeepLearning/Creating/nine.png)

- 기본적인 layer by layer로 아래의 기본 layer를 활용할 것임, 앞서 실습했던 layer들과 역할이 같음

![one](/img/DeepLearning/Creating/ten.png)

- 이 layer들을 가지고 구성을 해 볼 것임, 이를 column vector로 한 줄 짜리 한 열을 가지고 있는 1-D array를 통해 만들면 됨, 주어진 layers 설계 조건대로 만듬 input은 28x28x4를 array로 묶어서 나타내고, column이므로 세미콜론 활용
- covolution2dlayer에서 filtersize와 filter 개수를 넣으면 됨
- 그리고 순차적으로 argument가 없는 것은 없는대로 있는건 그에 맞는 조건대로 넣어주면 됨
- 아래와 같이 만들면 layer가 끝임

![one](/img/DeepLearning/Creating/eleven.png)

- 이를 analyzeNetwork를 통해서 만든 layer를 볼 수 있음

![one](/img/DeepLearning/Creating/twelve.png)

- 간단한 경우는 위처럼 layer by layer를 짜면 되지만 만약 parallel하거나 복잡한 layer 같은 경우는 코드하나로 짜기가 만만치 않음 특히 from scratch의 경우
- 그래서 여기서 Apps에서 Deep Network Designer가 있음, 이를 통해서 Blank Network를 가지고 직접 설계할 수 있음, 혹은 직접 가져와서 수정해도 됨

![one](/img/DeepLearning/Creating/thirteen.png)

- 드래그 앤 드랍으로 설계할 수 있음, 간단하게 데이터와 내용을 채워서
- 위에서 코드로 짠 생각을 한 layer by layer를 단순하게 로직을 짜서 할 수 있음
- 이렇게 짜고 아래처럼 export를 하거나 코드로 나오게 하거나 입력을 해서 parameter를 쓰거나 할 수 있음

![one](/img/DeepLearning/Creating/fourteen.png)

- 그리고 training의 경우 이전에 했던것과 같이 동일하게 할 수 있음 아래처럼 그리고 학습을 시켰음

![one](/img/DeepLearning/Creating/fifteen.png)

- 그 다음 classify와 evaluate할 수 있음
- 추가적으로 accuracy가 몇 인지 나타낼 수 있어야함, 직접 계산을 하는 것

![one](/img/DeepLearning/Creating/sixteen.png)

- 전체적인 퍼포먼스가 나쁘지 않다는 것을 알 수 있음
- 빌딩에 대해서는 개선이 필요함을 알 수 있음
- 각 layer들이 어떤 역할을 하는지에 대한 아키텍처를 아래와 같이 볼 수 있음
- fullyConnectedLayer가 들어가게 되면 이를 Classical Neural Network라고 함

![one](/img/DeepLearning/Creating/seventeen.png)

- NonClassical은 fullyConnect와 다른게 들어감, 일반적으로 위와 같이 되어있음
- 2번과 같은 일련의 과정이 진행됨 먼저 imageInputLayer은 아래와 같이 이미지가 숫자형태로 2-D array로 됨 아래는 하나의 채널만 봄

![one](/img/DeepLearning/Creating/eighteen.png)

- 즉 네트워크의 input size를 정의하고 input image를 normalize함, 크게 크기를 정의하고 정규화하는데 디폴트 값은 평균값을 계산하고 각각 데이터에서 평균값을 뻄으로써 normalize함, 그래서 평균 0값 주변으로 center화 할 수 있음
- convolution2dlayer에서는 학습에서 가장 큰 영향을 미치고 feature extraction 용도로 그리고 학습 과정을 통해서 가중치값을 계속 업데이트함 아래와 같이

![one](/img/DeepLearning/Creating/nineteen.png)

- sliding filter라고 하는데 이는 네트워크 상에서 위와 같은 2x2를 그대로 포개서 그대로 더하는 것임, 위의 예시 기준으로 7 * 1 + 14 * 0 + 13 * 0 + -5 * 1 = 2가 됨, 이런식으로 포개지면서 계속 계산되면서 결과값이 나오는것을 의미함, 한칸씩 이동함 14, -9, -5, -3 근데 이 이동하는 칸도 직접 설정해줄 수 있음
- 이는 CNN 구조에서 가장 key part임 → image classification에서 가장 최적화되어 있음
- filter size를 결정하면 weight 값은 최적의 filter를 뽑아내기 위해서 바뀌긴 함, filter weight와 bias 값은 learnable parameter 이므로 size만 정해주면 뉴런이 하나의 filter를 가지고 있으므로 계속 업데이트 함
- pretrained의 경우 filter가 다 학습되어 있으므로 알아서 activation하면 보여짐
- convolution은 spatial structure 이미지 classification에 최적화되어 있음
- relu layer는 아래와 같음

![one](/img/DeepLearning/Creating/twenty.png)

- 이는 간단함, 마이너스 값을 다 0으로 해서 어두운 색 검은색으로 만드는 것임, 특징들을 드러나게 하기 위해서 positive 값만 남겨둠
- 그 다음 maxPoolingLayer는 다운 샘플링 하는 것임, 일반적 특징들을 뽑아냄

![one](/img/DeepLearning/Creating/twentyone.png)

- 위에서 relu의 결과에서 [3 3]이면 3x3에서 최대값을 따서 결과를 뽑아서 다운샘플링 하는 것임
- 그다음 fullyConnected에서는 클래스와 예측하고자 하는 output 클래스를 넣어줌

![one](/img/DeepLearning/Creating/twentytwo.png)

- 즉 추출한 특징들을 연결시켜줌
- 그 다음 softmax에서는 normalized exponential function을 이용해서 normalized 된 score로 변경을 해 줌, 다 더하면 1이 나옴 실제로는 0.999이지만 즉 min scale normalize해서 나옴 수학적 equation임

![one](/img/DeepLearning/Creating/twentythree.png)

- 마지막 classificationLayer는 해당 값과 이미지를 연결시켜줌, 제일 높은 것을 연결해줌

![one](/img/DeepLearning/Creating/twentyfour.png)

- 이렇게 뉴런을 업데이트 하는 개념인데 각각 Layer에는 뉴런이 있고 모든 뉴런들이 아래와 같이 연결되어 있음, 노드들이 일반적인 네트워크에서는 아래와 같이 연결되어 있음

![one](/img/DeepLearning/Creating/twentyfive.png)

- 그리고 아래와 같이 각 데이터들이 연결된게 받고 데이터를 학습하고 똑같이 넘기는 과정이 진행됨

![one](/img/DeepLearning/Creating/twentysix.png)
![one](/img/DeepLearning/Creating/twentyseven.png)

- 그럼 하나의 실제 뉴런에서는 아래와 같이 양쪽에서 들어와도 weight라는 filter의 value가 곱해지고 더해진다음 그값에 bias 값을 더해서 learnable parameter로 학습이되고 업데이트가 되는 값이고 그 값자체를 또 transfer function을 받게 계산을 해서 전달을 함

![one](/img/DeepLearning/Creating/twentyeight.png)

- 이런식으로 계산을 하면서 필터 값을 알아서 업데이트 됨

![one](/img/DeepLearning/Creating/twentynine.png)

- 뉴런을 묘사해서 하는 것임, 실제로 존재하는게 아닌

![one](/img/DeepLearning/Creating/thirty.png)

- 그래서 filter 값은 이미 학습된 업데이트 된 값임을 의미함
- 그리고 Convolution Layer의 경우 spatial structure라고 하였는데 이미지를 2-D array를 그대로 받아와서 아래와 같이 사용을 함, 근데 사실 편하게 할려면 아래와 같이 풀어버리면 됨

![one](/img/DeepLearning/Creating/thirtyone.png)

- 하지만 풀 수가 없는게 이미지는 spatial structure를 단순히 풀어서 하면 정보가 손상되기 때문에 2-D array layer로 받아야하는데 그런것에 가장 최적화 된 것이 Convolution이므로 아래와 같이 하는 것임
- 즉 2-D array를 보존하고 채널에 맞게 개수를 설정해서 계산함, 그대로 입력

![one](/img/DeepLearning/Creating/thirtytwo.png)

- 그 다음 각 채널별로 계산을 하고 아래와 같이 넘겨주고 넘겨주는 작업을 함

![one](/img/DeepLearning/Creating/thirtythree.png)
![one](/img/DeepLearning/Creating/thirtyfour.png)

- 2-D array로 할 수 있는게 중요한 것임
- CNN은 아래와 같고 그러면서 feature들을 뽑는 것임

![one](/img/DeepLearning/Creating/thirtyfive.png)

- Filter의 경우도 말 그대로 Filter로 생각하면 됨, 아래와 같이 특정 이미지가 지나가면 선이 진해졌다가 옅어짐, 그러면서 특징이 추출이 되는 것임

![one](/img/DeepLearning/Creating/thirtysix.png)

- 실제로 본다면 아래와 같이 세로방향에서 슬라이딩 필터이므로 쭉 진행하면서 특징들을 뽑음

![one](/img/DeepLearning/Creating/thirtyseven.png)

- 가장 두드러지게 나오는 곳이 얼룩말에서 세로 방향 줄무늬가 가장 큰값이 나타난 특징으로 밝은색으로 나올 것임

![one](/img/DeepLearning/Creating/thirtyeight.png)

- 그러면서 아래와 같이 추출될 것임

![one](/img/DeepLearning/Creating/thirtynine.png)

- 그 필터값은 학습되면서 weight bias 값이 계속 업데이트 됨

![one](/img/DeepLearning/Creating/fourty.png)

- 그러면 이것을 그대로 씌워서 계산을 아래와 같이 진행함

![one](/img/DeepLearning/Creating/fourtyone.png)
![one](/img/DeepLearning/Creating/fourtytwo.png)
![one](/img/DeepLearning/Creating/fourtythree.png)

- 그 계산이 되서 마지막으로 하나의 값이 나오는 것이고 그 값이 끝나면 아래와 같이 옆으로 진행됨

![one](/img/DeepLearning/Creating/fourtyfour.png)
![one](/img/DeepLearning/Creating/fourtyfive.png)

- 칸 이동에 대해서는 커스텀을 해서 할 수 있음, 어쨌든 이 방식으로 쭉 진행을 해서 아래와 같이 나올 것임

![one](/img/DeepLearning/Creating/fourtysix.png)

- 수학적인 계산을 하는 것임, 그래서 아래와 같이 결과가 나오는 것임

![one](/img/DeepLearning/Creating/fourtyseven.png)

- 세로 필터를 썻으므로 아래와 같은 결과가 나오는 것임, vertical이 눈에 띔

![one](/img/DeepLearning/Creating/fourtyeight.png)

- 이런식으로 계속 학습하면서 아래와 같이 weight 값 bias 값을 업데이트함, 특징들이 잘 추출될 수 있도록 각 뉴런들이 필터를 이용해서 특정한 특징들을 추출하는 용도로 학습을 하는 것

![one](/img/DeepLearning/Creating/fourtynine.png)

- 어떠한 feature들을 선택하느냐는 필터에 의해서 결정되고 학습을 통해서 업데이트가 됨
- 결국 위의 filter가 아래와 같이 하나의 weight으로 나타남, 하나의 array가 됨

![one](/img/DeepLearning/Creating/fifty.png)

- 그런식의 과정이 아래와 같이 feature가 되고 나타나게 되는 것임, 이게 convolution layer가 하는 일임

![one](/img/DeepLearning/Creating/fiftyone.png)

- 아래와 같이 red channel을 뽑으면 결과는 다음과 같음

![one](/img/DeepLearning/Creating/fiftytwo.png)

- 이를 3x3 filter를 만들어서 적용해볼 것임, 이는 우리가 이미 알고 있는 filter를 가지고 학습을 통해서 train 된 filter 하나를 뽑아와서 씀(kernel라고도 부름 filter = kernel)
- 이를 blur 시켜서 흐릿하게 만드는 것을 만들어서 적용하면 아래와 같음, ones 1의 값에 1/9을 곱해서 수치를 떨군 값임 `blurKernel`
- 이 변수에 2D convolution을 적용하면 됨

![one](/img/DeepLearning/Creating/fiftythree.png)

- 만약 이 값을 `imshow(blurConv)` 를 쓰면 아무것도 안 보임 이를 `imshow(rescale(blurConv))` 를 통해서도 볼 수 있긴함
- 하지만 rescale하지 않고 아래와 같이도 가능함, 알아서 rescale해서 보여줌

![one](/img/DeepLearning/Creating/fiftyfour.png)

- 여기서 edges를 weight, bias를 업데이트 했다는 가정하에 edgeKernel을 직접 만들어서 적용할 수 있음

![one](/img/DeepLearning/Creating/fiftyfive.png)

- 이러면 edge들이 추출된 것을 알 수 있음
- 그리고 이미 학습되서 Train 된 filter를 가져와서 어떤 역할을 하는지 아래와 같이 weight 값을 볼 수 있음, 감을 잡을 수 있음, 그러면 그 filter를 씌우고 원하는 대로 activation이 나타나는지 알 수 있음
- filter 확인이 큰 의미는 지니고 있지 않지만 눈으로 확인할 수 있는 filter를 뽑는다면 의도되는대로 되는지 알 수 있음

![one](/img/DeepLearning/Creating/fiftysix.png)

- 위의 꽃들을 보면 보라색 꽃, 빨간색 꽃, 갈색등 그런 특징적인 색깔을 뽑는 filter를 알 수 있을 것 같음
- GoogleNet으로 확인해볼 것임

![one](/img/DeepLearning/Creating/fiftyseven.png)
![one](/img/DeepLearning/Creating/fiftyeight.png)

- 144개의 신경망이 되어 있음을 알 수 있음 maxpooling, relu, 등등 다양하게 존재함
- stride와 padding들이 들어있는것도 있음
- 하지만 때로는 maxPooling이 아닌 averagePooling 처럼 평균값을 내서 하는 것도 있음
- 해당 array의 평균을 내서 결과를 뽑아냄
- Weight Size는 Filter Size에 동일하고 channel은 3개라서 weight에도 그대로 반영되고 numfilter가 64라서 그대로 weight에 반영되어 나가는 것을 아래에서 확인할 수 있음

![one](/img/DeepLearning/Creating/fiftynine.png)

- bias는 1x1x64 즉 각 output에 대해서 하나씩 들어간다는 것을 알 수 있음
- Stride에서는 Sliding Filter 적용시 몇 칸씩 이동할지 하는 것이고 Padding 사이즈는 zero padding을 넣는 것임 즉, 원본 데이터에서 아래와 같이 375로 들어가 있는데

![one](/img/DeepLearning/Creating/sixty.png)

- 변환시 377로 들어가 있음을 알 수 있음, 즉 zero padding 이미지의 양쪽에 0을 추가한 것임 만약 paddingSize가 [3 3 3 3]이라면  위, 아래, 좌, 우에 3개씩 0을 넣겠다는 것임, 이미지 사이즈가 작을 경우 의미는 있으나 큰 경우는 의미가 없긴 함

![one](/img/DeepLearning/Creating/sixtyone.png)

- 이전 설계한 network에서는 하나도 안 넣은것을 볼 수 있음

![one](/img/DeepLearning/Creating/sixtytwo.png)

- 마지막으로 DilationFactor는 filter에 padding 처럼 0을 추가하는 것, 보는 영역을 확대하려고 하는 것임, 0이 들어가서 연산량은 의미가 없음
- 결국 weight 값은 filtersize + numchannels + numfilters의 hyperparameter의 조합임
- 그러면 아래와 같이 나오는 것임

![one](/img/DeepLearning/Creating/sixtythree.png)

- 여기서 색들이 들어간 필터는 어느정도 의미가 있음
- 우선 weights를 아래와 같이 볼 수 있음

![one](/img/DeepLearning/Creating/sixtyfour.png)

- 7x7x3을 하나의 이미지로 받고 학습된 최종 필터 값을 위처럼 나옴
- 여기서 특별한 filter 11번째를 뽑아내볼 것임

![one](/img/DeepLearning/Creating/sixtyfive.png)

- 매우 작은 형태로 RGB 형태로 나옴을 볼 수 있음, 그말은 즉 filter가 위에서 본 꽃들이 있는 이미지를 슬라이딩 하면서 쭉 지나가면서 필터가 붉은색 이미지를 뽑아냈다고 생각할 수 있음
- 이를 실제로 activation으로 한 번 볼 수 있음, 11번째 필터를 지났을 때 activation을 본 것임

![one](/img/DeepLearning/Creating/sixtysix.png)

- 어느정도 붉은색 관련된 색깔 즉 11번째 필터에서 보이는 것만 한 부분이 특징으로 추출되어 빛나는 것을 볼 수 있음
- 이때 ReLu를 지나면 회색들은 다 0으로 되고 MaxPooling 하면 추출된 특징들이 극대화 될 것임
- filter를 직접 눈으로 확인하고 특징들이 어떻게 추출되는지 알 수 있게됨