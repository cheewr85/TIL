### Sequence Length
- Sequence 데이터는 Serial 데이터 시간에 따라서 측정 즉, 최소한 어떤 데이터가 있을 때 time step이 아니더라도 앞과 뒤의 데이터가 동시에 측정된게 아님 즉 정적인게 아님
- 그래서 Sequence가 time step이 있다고 함

![one](/img/DeepLearning/SequenceLen/one.png)

- 하지만 여기서 위와 같이 길이가 다 다를 수 있음, 이전의 쓴 데이터 그리고 Serial 데이터는 왠만해서는 그 길이가 다름, 무작정 길이를 커스텀해서 일원화 시킬 수 없음, 데이터가 삭제되서 중요한 데이터가 사라질 수 있기 때문에 그래서 이를 zero pedding을 함 즉, 0을 넣어서 쭉 길이를 맞춤
- 0 자체를 데이터로 인식해서 학습을 함, 하지만 이렇게 하면 위의 그림에서 0,2 같은 경우 0자체가 큰 영향을 끼침, 그러므로 데이터 전처리와 사전 작업을 매우 잘 해야함
- 위의 데이터는 9개 기준으로 Mini-Batch가 나뉘어져 있음, 비율로만 보면 알 수 있듯이 하나의 group으로 잡고 튜닝이 가능함, 하지만 zero pedding이 너무 많이 들어가 있어서 학습의 큰 영향을 끼칠 확률이 높음
- 그래서 이것을 전처리를 해줄 필요가 있음
- 먼저 할 수 있는 것은 아래와 같이 데이터를 sorting을 해주는 것임

![one](/img/DeepLearning/SequenceLen/two.png)

- 길이 순서대로 sorting을 하는 것임, 여기서 Mini-Batch가 첫 데이터와 같다면 첫 데이터보다는 낫다는 것을 알 수 있음, 여기서 shuffle을 never로 해야함, 그래야 sorting한 것이 섞이지가 않음
- 대부분의 데이터는 길이가 다름 그래서 전처리를 잘해야하는데 shuffle도 never로 해줘야함
- 그리고 sorting과 더불어서 아래와 같이 mini-batch 사이즈를 조절해서 처리를 할 수 있음, 2번째는 9개인데 이를 6으로 줄여서 zero-pedding 조절이 가능함

![one](/img/DeepLearning/SequenceLen/three.png)

- 근데 너무 많이 batchsize를 조절하면 시간이 오래걸림

![one](/img/DeepLearning/SequenceLen/four.png)

- 하지만 여기서 앞서 말했듯이 아예 자르는 경우도 택할 수 있음, 하지만 이 경우가 더 값이 좋을 수 있음, 아래와 같이 shortest로 조절도 가능함

![one](/img/DeepLearning/SequenceLen/five.png)

- 하지만 여기서 음성은 이렇게 자를 수 없음, 그게 중요한 데이터가 있을 수 있기 때문에, 그래서 zero pedding을 많이 쓰긴함, 전체적인 특징이 묻어나오는 소리의 경우는 잘라서 쓰기도 함, 하지만 그런 경우는 많지는 않음
- 여기서 하나의 문장이 누가 이야기 한 것인지 예측을 할 수도 있음, 특정 작가가 쓴 글을 계속 주고 문장을 주고 누가 말했는지 예측을 하게끔 할 수 있음, 문자가 무엇인지 체크하는데 있어서 categorical 데이터를 numeric으로 변환을 해서 처리할 수 있음
- 그렇다고 numeric으로 막 바꾸어서도 안됨

![one](/img/DeepLearning/SequenceLen/six.png)

- 어떻게 바꿀 것이냐면 기계학습에서는 여러가지 predictor와 observation이 있다고 할 때, color가 아래와 같이 3가지와 size의 numeric이 있다고 할 때, color를 숫자로 바꾼다는 것을 직관적으로 생각할 수 있음

![one](/img/DeepLearning/SequenceLen/seven.png)

- 하지만 이렇게 바꿔버리면 실제로 network가 인식할 때 아래와 같이 차이 즉 distance가 나게 되는데 categorical에서는 옆의 그림과 같이 동일하게 되어 있는데 이렇게 1차원적으로 생각하면 같은 길이가 아닌 distance 차이가 나버림, 동일하게 바라보질 못함, 거리 개념을 넣어버린 것임

![one](/img/DeepLearning/SequenceLen/eight.png)

- 그러면 이것을 바꿀 때 categories를 활용하면 3개가 나오는데 여기서 3개의 빈 array를 생성해서 이 값을 각각 3개의 색마다 빈 array를 생성해서 아래와 같이 1을 채우되 각각의 참 거짓으로만 숫자를 표현하는 것임
- matlab에서도 실제로 dummy variable을 사용해서 바꿀 수 있음, 2번째 그림과 같이 변환이 되는 것임, 즉 하나의 column이 3개의 column으로 나뉘어지는 것임, 이를 dummy variable이 추가되었다고 해서 나타냄

![one](/img/DeepLearning/SequenceLen/nine.png)
![one](/img/DeepLearning/SequenceLen/ten.png)

- 이러한 방식을 딥러닝에서도 똑같이 적용을 하는 것임, 아래와 같이 Dummy Variable로 알파벳을 생성이 가능함, a,b,c,t 4개의 categories가 있으므로 그 categories 만큼 dummy variable을 만드는 것임
- 이러면 어떠한 정보의 손실도 생기지 않을 수 있음

![one](/img/DeepLearning/SequenceLen/eleven.png)

- 실제 코드를 아래와 같이 활용가능함, 우선 문자를 저장하고 그 다음 이 값을 그대로 하는것이 아니라 조금 더 쉽게 하기 위해서 uint8(사이즈가 작은)로 변환을 함

![one](/img/DeepLearning/SequenceLen/twelve.png)

- 공백도 포함해서 32로 변환함 총 18칸의 수를 num으로 변환함 각 알파벳마다 같은 값임(공백포함)
- 그리고 이를 categorical로 바꿀 것임, 말 그대로 categorical 데이터로 바꾸는 것임(uint8로)

![one](/img/DeepLearning/SequenceLen/thirteen.png)

- 그 다음 이를 dummy variable로 바꿔주면 됨, 하지만 한가지 알아야 할 것은 위에 까지는 row 행 벡터로 받았지만 dummy variable의 경우 column 열 벡터로 받음, 그래서 이를 transpose를 아래와 같이 해줘야함, 그리고 dummyvar 함수를 쓰면 됨, 그 다음 원래대로 복구하면 됨

![one](/img/DeepLearning/SequenceLen/fourteen.png)

- categorical로 다 바꾸고 이를 categories가 7개로 구성됨을 알고 그 다음 dummy로 바꾸면 앞서 설명한대로 바뀐 것을 알 수 있음, 공백은 첫 부분이 그것을 의미함을 알 수 있음, 그리고 각각 1이 해당하는 row가 해당 알파벳임을 위의 이론에서 나온 예제 그림처럼 나타남을 알 수 있음
- 각각 대응됨을 알 수 있음

![one](/img/DeepLearning/SequenceLen/fifteen.png)

- 이는 알파벳 7개임을 감안하고 한 것임
- 하지만 실제로 하게 된다면 알파벳 26개와 하나의 빈칸으로 총 27개임(대문자를 제외하고), 여기서 아래와 같이 27개에 대해서 실제 dummy variable을 생성하는게 맞음 알파벳으로 여기서 그러면 이를 적용하기 위해서 categorical로 바꿀 때 2번째 parameter로 넣어서 처리할 수 있음 즉, 전체 category를 vocab으로 받아서 거기에서 categorical로 변환하는데 전체 categories는 vocab을 알리는 것임

![one](/img/DeepLearning/SequenceLen/sixteen.png)

- 그러면 아래와 같이 바뀜을 알 수 있음 즉, 27개의 열 vocab이라는 전체 categories를 넣어줬기 때문에 전체에 대해서 dummyvar을 생성한 것임

![one](/img/DeepLearning/SequenceLen/seventeen.png)

- 만약 text 데이터가 categorical 혹은 숫자형이지만 sequence의 길이가 다를 경우 dummyvar를 시키거나 숫자형은 sequence Length가 다르기 때문에 적절하게 데이터를 전처리 해줘야함
- 숫자형에서 sequence Length가 다를 경우 전처리를 해줘야 하는 것임
- 사용할 데이터들은 숫자형 데이터들임(dimension인 12임, inputSize가 12)

![one](/img/DeepLearning/SequenceLen/eighteen.png)

- 하지만 dimension인 동일하지만 sequence length가 12, 10, 11, 9 등 다 다름

![one](/img/DeepLearning/SequenceLen/nineteen.png)

- 이를 그대로 학습시키면 퍼포먼스가 매우 떨어짐, 그래서 전처리를 해줘야함
- 그 전에 이 데이터에 대해서 무엇인지 생각해볼 수 있음
- 대표적으로 스마트폰의 Gyro, 그리고 Accel 가속도에 대한 것이 각각 센서 값을 동시에 받을 수 있음, 이는 아래와 같이 tiem step 기준으로 데이터 측정이 진행이 됨, 아래와 같은 경우는 6개의 dimension의 데이터가 됨
- 이를 걷는 것, 뛰는 것, 등산 등 그 상황에 따라 데이터가 다르게 측정되서 쌓이고 지정될 것임, 이러한 sequence data를 받을 수 있고 이게 대표적임
- 자동차는 아래의 dimension보다 더 많은 값을 측정해서 하고 dimension이 훨씬 많아짐, 위에서 예시 자료도 그런것과 유사한 것임

![one](/img/DeepLearning/SequenceLen/twenty.png)

- 그럼 그에 맞게 데이터 전처리를 할 수 있음
- 왜냐 만약 sequence length가 아래와 같이 다르면 우선 pedding으로 맞춰주긴 하지만 그 학습 주기인 mini-batch등 업데이트를 하긴 함, 아래와 같이

![one](/img/DeepLearning/SequenceLen/twentyone.png)

- 하지만 여기서 pedding은 pedding인지 모르고 network에서 학습을 함 그래서 퍼포먼스가 떨어짐 그렇기 때문에 pedding을 줄이기 위해서 전처리를 함
- 그래서 먼저 아래와 같이 sorting을 먼저 함(shuffle을 never로 반드시 해야함)

![one](/img/DeepLearning/SequenceLen/twentytwo.png)

- 그리고 mini-batch를 더 줄일 수 있음 아래와 같이 그런데 이게 단순히 퍼포먼스 향상보다는 학습에도 영향을 끼칠 수 있기 때문에 잘 고려해야함
- mini-batch가 너무 작으면 튜닝할 파라미터가 작아서 각각의 iteration에 대해서 들쭉날쭉 될 수 있음, 그리고 반대로 너무 크면 GPU의 메모리에 부담이 가서 에러가 날 수 있음
- 그래서 이 값을 건드리는데 있어서는 매우 조심히 잘 다뤄야함

![one](/img/DeepLearning/SequenceLen/twentythree.png)

- 이런식으로 퍼포먼스를 향상 시킬순 있음
- 먼저 이런식으로 데이터를 전처리 할 것임, sorting을 먼저 할 것임
- observation의 개수를 뽑음, height로 50개의 데이터를 뽑음, 여기서 만약 맨 처음의 12x7의 데이터를 뽑을려면 cell 형태로 뽑고 해당 데이터에서의 height도 뽑을 수 있음

![one](/img/DeepLearning/SequenceLen/twentyfour.png)

- length도 똑같이 12가 뽑히는데 여기서 length는 아래 그림에서 12x7에서 그 중 큰 값인 12를 뽑는 것임 height와 같이 그냥 observation이 12개여서 뽑는게 아닌 그래서 만약 12x14가 되면 length는 14가 뽑힘, 이는 취지에 맞지 않음

![one](/img/DeepLearning/SequenceLen/twentyfive.png)

- 여기서 numel를 하면 위의 기준으로 12x7 총 element의 개수가 뽑힘
- 그래서 일반적으론 height의 값으로 쓰는게 나음
- Xtrain은 하나의 열벡터이기 때문에 length나 height나 같은 값이 나오긴함, 그렇다고 해도 기본은 height로 하는게 맞음, 일반적으로 많이 쓰기도 하고
- 그런 다음 for문을 통해서 i값을 뽑아서 sequenceData가 아래와 같이 나타나게 됨 반복해서

![one](/img/DeepLearning/SequenceLen/twentysix.png)

- 여기서 1로 고정을 하면 똑같은 값이 50번 나오는 것임

![one](/img/DeepLearning/SequenceLen/twentyseven.png)

- 어쨌든 i기준으로 size함수를 통해서 이 크기를 뽑을 수 있음, 여기서 2번째 값만 뽑으면 되니깐 아래와 같이 그 값만 뽑아줄 수 있음

![one](/img/DeepLearning/SequenceLen/twentyeight.png)

- 이것을 array 형태로 행벡터로 만들어줄 수 있음, 반복문이기 때문에 점점 커지는 것임, 그럼 1x50의 행벡터가 됨

![one](/img/DeepLearning/SequenceLen/twentynine.png)

- 여기서 속도 문제가 생기기도 함 계속 업데이트를 반복문마다 해버려서 그래서 정석으론 memory free allocation을 해줘야함, 0으로 다 채우는 것임, 이미 메모리 상에 그 크기만큼 잡아버리는 것임, 그러면 속도가 훨씬 나아짐

![one](/img/DeepLearning/SequenceLen/thirty.png)

- 이렇게 값을 뽑은 다음 바그래프로 아래와 같이 보임을 알 수 있음 바 형태로 각각의 observation의 길이가 나타낼 수 있음(sorting 하기 전에)

![one](/img/DeepLearning/SequenceLen/thirtyone.png)

- 그 다음 높은 값에서 낮은 순으로 데이터 정렬을 할 수 있음
- 일단 기본 sort를 쓰면 낮은순에서 높은순으로 정렬이 됨
- 여기서 옵션을 쓸 수 있음 높은 값에서 낮은값으로

![one](/img/DeepLearning/SequenceLen/thirtytwo.png)

- 여기서 바 그래프 형태를 보면 아래와 같음을 알 수 있음

![one](/img/DeepLearning/SequenceLen/thirtythree.png)

- 여기서 중요한 것은 sorted 된 값을 Xtrain에 업데이트 하는게 중요함, 인덱스 값도 같이 뽑아서
- 그 값 뿐 아니라 label 값 역시 업데이트 해야함, 그래서 sorting 뿐 아니라 idx에 대한 값을 array로 뽑아야함
- 그 다음 업데이트를 하기 위해서 인덱스 값을 입력하면 우리가 sorting 한 값으로 정렬이 됨

![one](/img/DeepLearning/SequenceLen/thirtyfour.png)

- 이 결과물을 보면 원하는대로 sorting 됨을 알 수 있음
- 근데 이 바 차트 기준으로 mini-batch 사이즈를 함부로 잡을 수 없음, pedding 관점에서 보면 10개가 적당해 보이긴 함
- pedding 관점에서만 본다면 10개보다 더 적게 하는게 나아보이긴 함

![one](/img/DeepLearning/SequenceLen/thirtyfive.png)

- 그렇다고 이렇게 mini-batch를 눈대중으로 할 수가 없음, sorting 하는 것 만으로도 학습의 퍼포먼스를 크게 높이기 때문에 일단 mini-batch는 기본 디폴트로 한 뒤 낮은 순으로 조절하는게 좋음, 그리고 train시 shuffle은 반드시 never를 해야함

![one](/img/DeepLearning/SequenceLen/thirtysix.png)

- 그리고 pedding이 들어가기 때문에 똑같이 test data에서 prediction 할 때도 pedding이 들어것을 가지고 해줘야함, 그래서 test data에 대해서 똑같은 방식으로 sorting을 해줘야함, test data도 똑같이 height를 통해서 하고 for문으로 진행하고 sorting을 똑같이 해 줌

![one](/img/DeepLearning/SequenceLen/thirtyseven.png)

- 그 다음 predict 할 때 단순하게 classify에 net 하고 Xtest를 했지만 여기서는 뒤에 옵션 값을 추가로 넣어줘야함

![one](/img/DeepLearning/SequenceLen/thirtyeight.png)

- mini-batch, sequenceLength를 위와 같이 옵션을 정확하게 입력을 해주는게 중요함