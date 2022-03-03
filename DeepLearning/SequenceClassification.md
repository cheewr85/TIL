### SequenceClassification
- Sequence 즉, 시계열 이미지는 정적 Sequence는 동적임, 이를 Classification하는 것임
- 여태까지 진행한 이미지화를 아래와 같이 해서 CNN에 적용을 했음, 시간에 따라 추출된 이미지화를 spectrogram을 한 것임, 이는 시간에 따라 Amplitude를 구분한 것임

![one](/img/DeepLearning/Sequence/one.png)

- 여기서 이를 시간에 따른것에 집중해서 동적 데이터로 보고 분류를 할 수 있는데 이를 SequenceClassification이라고 함, 여기서 이를 LSTM을 활용할 것임, 아래와 같이 다른 부분이 존재함

![one](/img/DeepLearning/Sequence/two.png)

- 여기서 Sequence에 집중해서 LSTM을 쓰는 것임, 이전에 한 것에서 CNN 처리한 것이 아닌
- LSTM을 할 때 위의 것을 그대로 넣는 것이 아닌 시계열 주파수로 바꿔서 하기도 함, 하지만 시간이 오래걸림 그래서 LSTM을 그대로 쓰기 위해서 위의 데이터를 그대로 활용할 것임(정적 데이터를 시계열이라고 생각)
- 여기서 시간에 따른 sequence는 아래와 같은 특성을 가지고 생각을 함, 시간의 흐름에따라 입력받아서 글을 쓴 것에 대해서 알파벳이 어디에 위치하는지, 이뿐아니라 시간에 따른 생체신호 혹은 자율주행차의 부분에 대해서 시계열로 볼 수 있음
- 그리고 이 글을 누가 쓴 건지 알아 맞추는 것도 이에 해당함, LSTM, RNN을 활용하여서 학습을 시키고 어떤 글귀를 입력시키고 누가 썼는지에 대해서 Sequence Classifcation 뿐 아니라 다음 텍스트가 무엇이 나올지도 예측할 수 있음

![one](/img/DeepLearning/Sequence/three.png)
![one](/img/DeepLearning/Sequence/four.png)
![one](/img/DeepLearning/Sequence/five.png)

- 위처럼 생각할 수 있고 RNN에서(CNN과 같이) LSTM에 대해서 사용할 것인데 메모리가 많이 들어서 학습이 꽤 오래걸림 대신 정확도는 높음

![one](/img/DeepLearning/Sequence/six.png)
![one](/img/DeepLearning/Sequence/seven.png)
![one](/img/DeepLearning/Sequence/eight.png)

- RNN은 아웃풋이 하나하나 들어가서 그 바로 전에 아웃풋이 인풋으로 들어감, weight와 bias로 학습을 또 함

![one](/img/DeepLearning/Sequence/nine.png)

- LSTM의 경우 바로전 아웃풋만이 들어가는 게 아니라 하늘색 회색, 아웃풋이 나왔으면 그게 다 인풋으로 다시 들어감, 그래서 Internal Memory state를 가지고 있음, 이를 통해서 여태까지의 output을 계속해서 사용하여서 학습을 하는 것임
- 아웃풋으로 나가고 다시 state로 들어가서 다음 input에 학습되고 이런식으로 바로 직전것뿐 아니라 더 쓰임

![one](/img/DeepLearning/Sequence/ten.png)

- 그리고 weight, bias 뿐 아니라 이전의 output 값을 다 사용할 것인지 몇 개만 쓸 건지 체크하는 추가적인 parameter가 더 존재함, 이를 gate라고 함

![one](/img/DeepLearning/Sequence/eleven.png)

- 여기서 아래와 같이 알파벳의 경우 그 다음 알파벳이 무엇이 오냐고 고려할 때 Q와 E중에서 Q는 그 다음이 많지 않고 E는 그 다음이 많으므로 이 부분을 튜닝하여서 더 많은 이전 아웃풋 값을 활용할지 등을 고려해서 체크할 수 있음

![one](/img/DeepLearning/Sequence/twelve.png)

- 그 다음 output으로 나갈 때에 대해서도 추가적인 save와 focus라는 파라미터가 더 존재함
- 그래서 이 부분에 대해서 복합적인 state가 존재함을 알 수 있음

![one](/img/DeepLearning/Sequence/thirteen.png)

- bidirectionalLSTM은 철저하게 데이터의 augment 단어가 들어올 때 정방향, 역방향 이미지 augment를 여러개 해서 처리하듯이 처리를 해 줌, 이 결과를 합쳐서 결론을 냄 이렇게 하면 정확도가 매우 높아짐

![one](/img/DeepLearning/Sequence/fourteen.png)
![one](/img/DeepLearning/Sequence/fifteen.png)

- sequenceClassification 아래와 같이 이미지와 유사하게 Sequenece(단어)를 활용하여서 누가 썼는지 구분을 할 수 있음
- 이때 새로운 sentence를 주어주면 누가 말했는지 맞추는 것임, 한 단어씩 입력될 때마다 그 아웃풋에 대한 label이 나오는 것임, 그리고 다 입력됐을 때 결론을 도달하는 것

![one](/img/DeepLearning/Sequence/sixteen.png)
![one](/img/DeepLearning/Sequence/seventeen.png)
![one](/img/DeepLearning/Sequence/eighteen.png)

- 여기서 outputMode를 sequence로 할 것인가 last로 할 것인가 정함
- 일단은 last로 해주면 됨, sequence의 경우는 다음 단어가 무엇이 나올지 쭉 입력을 기반으로 해서 뒤쪽의 sequence를 예측하는 것임(주식 예측에 주로 사용됨) + 심전도 측정
- last를 해야 classification을 할 수 있음

![one](/img/DeepLearning/Sequence/nineteen.png)

- sequence data의 특성을 보면 아래와 같이 가짐, cell 형태의 행벡터로 받음, 하나의 행은 하나의 label을 가지고 이는 cell 형태로 활용을 함, sequence data는 거의 cell형태로 주로 다룸
- 여기서 zero peding을 조절해서 데이터를 처리할 수도 있음, 추가적으로
- 그리고 time step이 있고 그 다음 dimension이 존재함, 심전도 측정에서는 dimension이 매우 많이 있음

![one](/img/DeepLearning/Sequence/twenty.png)
![one](/img/DeepLearning/Sequence/twentyone.png)
![one](/img/DeepLearning/Sequence/twentytwo.png)

- 이전에 사용했던 악기에 대한 데이터를 활용해서 이미지를 sequence로 생각하고 할 것임
- 데이터는 XTrain을 보면 441하나의 row와 하나의 행은 3528의 sequence를 가지고 하나의 label을 가지고 있음(cell 데이터로 되어 있음)

![one](/img/DeepLearning/Sequence/twentythree.png)

- label의 값이 아래와 같이 되어 있음을 알 수 있음(GroundTruth값)

![one](/img/DeepLearning/Sequence/twentyfour.png)

- 샘플을 아래와 같이 들어볼 수 있음, 데이터 이해를 위해서 직접 들어보거나 데이터가 매우 짧을 수 있기 때문에, 여러개 데이터 동시에 섞어서 혹은 차례대로 들어서 그 이해도를 높이기 위해서 아래와 같이 들어보는 것임
- 1,2,3, 100 다 flute인데 조금 다른 소리임을 알 수 있음, 이런식으로 데이터 샘플을 들을 수 있음

![one](/img/DeepLearning/Sequence/twentyfive.png)

- 여기서 소리를 무작위로 몇 개를 뽑아서 합성한 다음에 연속적으로 들어볼 수 있음, 아래와 같이 스킬을 좀 써야함, 무작위로 정한 개수만큼 뽑기 위해서 randperm을 활용할 수 있음
- 그리고 아래와 같이 데이터에 직접 적용해서 랜덤하게 뽑을 수 있음, 여기서 x는 idx에서 가장 첫 번째 value 1x3에서 맨 앞 데이터를 뽑는 것임

![one](/img/DeepLearning/Sequence/twentysix.png)

- 이를 다 생성하기 위해서 array로 감싼 뒤 실행하면 일렬로 쭉 묶여서 나옴

![one](/img/DeepLearning/Sequence/twentyseven.png)

- 그리고 아래와 같이 plot을 그리고 wave가 나옴을 알 수 있음

![one](/img/DeepLearning/Sequence/twentyeight.png)

- 임의로 뽑아서 합성해서 소리를 합성하면 그 소리가 위의 plot처럼 이어져서 piano,piano,flute 소리가 남을 알 수 있음
- 그 다음 아래와 같이 간단하 LSTM layer를 직접 만들어서 활용할 수 있음, 수학적 식은 복잡하지만 CNN에 비해서 기본 layer를 써도 성능이 좋음, CNN에서는 평행하게 layer를 쌓고 나누는 방식을 했지만 LSTM에선 기본 layer도 충분한 성능을 보장함, tunnable parameter가 굉장히 많음, 그래서 epoch도 매우 높기 때문에 학습하는데 시간도 오래 걸림
- epoch가 250이어도 과적합이 일어나지 않음, 200이 적당했음, valData를 통해서 과적합을 확인하고 다 training으로 넘겨서 처리를 함 퍼포먼스를 위해서
- 그래서 LSTM은 파라미터 튜닝이 매우 중요함, 그만큼 많기 때문에, layer가 간단하더라도(그만큼 내용이 좀 적고 opts가 많음, 내가 결정할 게 많음)
- layer를 직접 짤 수도 있지만 디자이너를 활용함, 먼저 sequenceInputLayer를 넣어줌, InputSize sequence data의 dimension을 넣어주고 처리해줘야함(지금은 하나지만 dimension에 따라서 데이터를 보고 처리하면됨)
- 그 다음 lstmlayer, bilstmlayer를 쓸 수 있는데 bilstm을 사용할 것임, 데이터를 충분히 활용하기 위해서 bilstm은 parameter가 그만큼 많이짐(즉 trainingOption이 중요함), hidden unit을 100개로 상정함, output을 last로 함 그래야 예측이 아닌 Classification을 할 수 있음
- 그 다음 fullyConnected 동일하게 함 앞서 label로 categories가 3개 이므로 outputSize는 3개 설정함
- 그리고 softmax를 함, 그 다음 classificationlayer를 넣음, 그리고 이를 연결해주면 됨 그러면 아래와 같이 됨

![one](/img/DeepLearning/Sequence/twentynine.png)

- 그리고 export를 하여서 바로 workspace로 보낼 수 있음
- 코드로 따지면 아래와 같이 직접 쳐서 생성할 수 있음

![one](/img/DeepLearning/Sequence/thirty.png)

- 그리고 trainingOption과 trainNetwork를 하면 됨, 일단 이는 했다고 가정하에 결과값을 가지고 Evaluation을 아래와 같이 할 수 있음, 불러온 결과값 기준으로 아래와 같이 결과가 나옴을 알 수 있음

![one](/img/DeepLearning/Sequence/thirtyone.png)

- 위의 결과는 아주 좋은 결과이고 아래는 적당한 결과라면 아래와 같음을 알 수 있음

![one](/img/DeepLearning/Sequence/thirtytwo.png)

- GPU를 사용한다고 하여도 메모리를 많이 필요로 함