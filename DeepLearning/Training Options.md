### Training Options
- Training Options을 계속 체크하면서 Network를 Train하면서 그 결과를 계속 체크할 것임
- 먼저 sgdm에 대해서 확인할 것임, 아래와 같이 설정을 해서 학습을 하면 Mini-batch가 NaN이 나옴을 알 수 있음

![one](/img/DeepLearning/Options/one.png)

- 여기서 한 번 InitialLearnRate를 건드려서 체크해 볼 것임, 그러면 loss가 떨어지고 testAcc이 올라간 것을 볼 수 있음

![one](/img/DeepLearning/Options/two.png)

- 0.001을 InitialLearnRate로 하면 계속 NaN이 나오고 0.0001이 나오면 Acc가 일정 수준 계속해서 나옴을 알수 있음, 하지만 계속 하다보면 0.0001을 해도 Acc이 0.84~0.93 즉 10% 정도 차이가 남 이는 학습이 충분히 진행이 되지 않음을 의미함
- 이런식으로 0.001과 0.0001의 차이가 나는 것은 MaxEpochs와 InitialLearnRate의 유의미한 의미가 있음을 말함
- 여기서 0.0001인 경우에 MaxEpochs를 늘리면 아래와 같이 나옴

![one](/img/DeepLearning/Options/three.png)

- 이를 계속해서 실행하다보면 90% 초반에서 중반이 계속 유지됨을 알 수 있음, 이를 통해서 MaxEpoch와 InitialLearnRate가 이러한 Acc와 Loss에 영향을 줌을 알 수 있음
- 여기서 sgdm, adam과 같은 알고리즘은 InitialLearnRate에 관련이 있음
- 딥러닝으로 하는 것은 Input과 Output을 Layer를 짜서, Network를 만들어서 문제와 답을 알고 있는 것을 서로 매칭, 연결 시켜주는 것임, 이러한 풀이과정을 만드는 것임
- 모르는 다른 Input이 들어와도 새로운 Output을 예측하는 것임
- 이러한 과정은 네트워크에 필터, weight와 값이 있고 튜닝, 학습을 시키면서 체크를 함 이러한 학습되는 과정은 입력이 들어왔을 때 출력을 알고 있고 가운데 풀이과정을 학습시켜야함

![one](/img/DeepLearning/Options/four.png)

- 여기서 Learnable Parameter를 계속 적당한 값으로 바꾸어가면서 Input과 Output을 열심히 매칭시킴, 그러면 Learnable Parameter들이 아래와 같이 계속 튜닝이 됨

![one](/img/DeepLearning/Options/five.png)

- 이런 과정을 거쳐서 하나의 Input을 넣었을 때 그 Output을 매칭하게끔 Parameter를 학습을 시키면 됨, 실제 Parameter는 무수히 많고 이를 계속 튜닝(학습)시켜야함
- 그 과정이 입력과 정답을 알고 있으므로 그 가운데 값, 매칭시키는 가운데 값을 역으로 튜닝시킴, 그 값은 결국엔 수학적으로 이루어지므로 최적값으로 결과와 가깝게 나오게끔 Loss Function을 활용함

![one](/img/DeepLearning/Options/six.png)
![one](/img/DeepLearning/Options/seven.png)

- 파라미터를 막 튜닝해서 첫번째 사진처럼 계속 조절을 하다가 두번째 사진처럼 결과가 나오게끔 튜닝하는 것임
- 최대한 가깝게 튜닝을 하는 것임, 두번째 사진처럼 하다가 결국에는 Loss 값 error의 차이를 더한 Total Error를 최소화하는 방향으로 튜닝이 되면 가장 학습이 잘됐다고 볼 수 있음

![one](/img/DeepLearning/Options/eight.png)
![one](/img/DeepLearning/Options/nine.png)

- 이런 Error를 Loss Function으로 계산을 함
- 이를 수학식으로 나타내지만 만약 모든 Parameter에 대해서 Loss를 가지고 전체 데이터 셋에 대해서는 구할 수가 없음, 훨씬 많은 Parameter에 대한 전체 데이터에 대한 Loss값, 즉, 모든걸 대변하는 Error 값은 한 번에 구할 수 없음
- 그러므로 아래와 같이 Loss Function에 맵을 그린 다음 하나하나 점점 Loss값이 낮아지게끔 해서 계산을 함, 이러면 해가 없을수도 있고 수학적 에러로 발산을 할 수 있음
- 발산하는 경우는 NaN이 되는 경우임

![one](/img/DeepLearning/Options/ten.png)

- 그래서 위처럼 모든 데이터셋 모든 계산을 다 할 수가 없기 때문에 이때 데이터를 쪼개는데 이를 Mini-Batch라고 함

![one](/img/DeepLearning/Options/eleven.png)

- 이 Mini-batch는 데이터를 몇 개의 Mini 사이즈로 쪼개는 것임, 여기서 이 각각 Mini-Batch, Batch를 하나씩 넣어주고 위에처럼 MiniBatch 3개를 전체데이터를 대변한다고 가정하고 파라미터를 튜닝을 함
- 그런 다음 그 파라미터에 대해서 Loss Function을 구함, 첫번째 Mini-Batch에 파라미터를 튜닝하고 Loss 최소화 값을 찾는것임, 시작점은 아무점에서 함(랜덤으로), Training Progress를 보면 급격하게 수렴하는것을 볼 수 있음, 처음엔 들쭉날쭉 하다가 낮아지는 방향으로(Loss 값이)

![one](/img/DeepLearning/Options/twelve.png)

- mini-batch에서 최소값이 나왔다고 하더라도 다른 값으로 확 바뀌게 하지 않는선에서 함, 하지만 그렇게 할수도 있긴함, InitialLearnRate를 위에서 했듯이 0.001로 한 경우
- 그런 경우 발산을 해버리는 것임, 파라미터가 갑자기 너무 높아져서
- 그래서 mini-batch에서의 낮아지는 방향으로 조금씩 나아가는 것임, 아래처럼(첫번째는 랜덤임), 기울기가 낮은 방향으로 Loss가 작아지게

![one](/img/DeepLearning/Options/thirteen.png)

- 걸음을 좁게하면 그렇게 될 것임 즉 InitialLearnRate를 너무 크게 잡으면 안된다는 것임, 물론 Batch 사이즈가 변경이 될 수록 즉 서로 다른 Batch에서 나온 것이 조금씩 다르긴 함

![one](/img/DeepLearning/Options/fourteen.png)

- Loss가 극단적으로 바뀌지 않아도 조금씩 바뀌긴 할 것임
- 그래서 결국 Loss Function 에서의 최적점을 찾을 것임

![one](/img/DeepLearning/Options/fifteen.png)

- 거기서 이제 Input을 넣으면 그 Input이 어떤 파라미터를 지나서 실제 값과 차이를 갖는 그 에러 값 Loss를 최소화하게끔 가운데 파라미터를 계속 튜닝하는 것임

![one](/img/DeepLearning/Options/sixteen.png)

- 그래서 옵션값으로 넣는 것은 파라미터를 튜닝할 때 어떤식으로 튜닝할 건지에 대해서 결정하는 것임 InitialLearnRate나 Mini-batch나
- 결국 결과값과 그 파라미터를 넣었을 때 결과값과 Prediction의 차이를 가지고 다시 파라미터를 튜닝을 함 이를 backpropagation이라고 함

![one](/img/DeepLearning/Options/seventeen.png)

- 이는 문제가 주어지면 결과를 내는게 아니라 랜덤하게 시작해서 파라미터를 지나 진짜값과 차이를 보고 파라미터를 튜닝하고 그 다음에 다음 데이터 셋에서 다시 이 과정을 반복하는 것임
- 아래와 같이 다양하게 걸을 수 있는데 여기서 규칙은 무조건 Loss가 작아지는 내리막으로 가는 것 이를 gradient descent 즉, stochastic gradient descent라고 함, sgd라고 함

![one](/img/DeepLearning/Options/eighteen.png)

- 이는 앞서 options에서 설정한 sgdm에서 sgd를 의미함, 여기서 이 폭을 크게 나갈건지 말것인지에 대해서 정하여서 학습을 하는 것임
- 수학식은 굳이 생각할 필요없음, 하지만 직접 layers를 설계해서 넣을려면 이 식을 만들고 계산을 해야함
- 이는 Reality(GT, Ground Truth)와 Prediction 사이의 Loss를 보면서 예측한 값과 그 차이를 보는것이 Loss임

![one](/img/DeepLearning/Options/nineteen.png)

- 결국 batch 값을 가지고 조금씩 나아가면서 가장 낮은 값으로 가는 것임 랜덤하게 시작을 했지만 얼마나 공격적으로 나아갈 지 혹은 살살갈 지 알 수 있음

![one](/img/DeepLearning/Options/twenty.png)
![one](/img/DeepLearning/Options/twentyone.png)

- 점점 작은 보폭으로 간다면 이상적으로 최적점으로 갈 수 있으나 시간이 많이 걸리게 됨, 단 보폭을 크게 하면 그 최적점을 찾는데 주변을 맴돌거나 결과적으로 못 찾을 수도 있음
- 그래서 처음에는 크게 나아갔다가 못 찾으면 만일 최적점을 못 찾으면 그 보폭을 작게할 수 있고 혹은 보폭을 크게 해도 방향전환을 적게 할 수도 있음, 그 보폭을 Learning Rate로 설정하는 것임
- 이를 momentum을 통해서 적용할 수 있음, 적당히 그 찾는거 전환을 조절

![one](/img/DeepLearning/Options/twentytwo.png)
![one](/img/DeepLearning/Options/twentythree.png)

- 그래서 점점 최적점으로 낮아지는데 그 방향전환을 적당히 꺾을 수 있게 관성을 주는 것을 sgdm 즉, momentum이 알고리즘에서 sgd + m이 되어 sgdm이 되는 것임 stochastic gradient descent이면서 momentum하게
- 그 momentum을 직접 결정, 조정할 수 있음
- 그리고 여기서 Epochs 즉, 위에서 mini-batch로 나눠서 활용하는 방식으로 전체 데이터 셋을 나누는 것을 몇 번 설정할지에 대한 것을 MaxEpochs를 통해서 결정하여 처리함, 이렇게 한 번 다 사용하는 것을 하나의 Epochs를 썼다고 함
- 그리고 InitialLearnRate 역시 중간에 값을 변경할 수 있고 처리할 수 있음
- 이 학습 과정을 본다면 아래와 같음

![one](/img/DeepLearning/Options/twentyfour.png)

- 여기서 Random이어서 처음엔 Acc이 엄청 낮고 급격하게 높아짐, 여기서 Learning Rate를 더 낮게 설정하면 좀 더 Acc이 올라가는 비율이 완만하게 증가함, 여기서 Learning Rate가 낮아도 Epochs를 적게 사용하면 이 완만하게 증가하는 것 때문에 결과가 채 다 끝나지 않을수도 있음, 이땐 Epochs를 더 해줘야함
- 여기서 Learning Rate에 대해서 스케줄링을 하여서 조절할 수 있음(Learning Rate는 첫번째 사진같이 Aggressive하게 Cautions 하게 갈 수 있음)

![one](/img/DeepLearning/Options/twentyfive.png)
![one](/img/DeepLearning/Options/twentysix.png)

- 보폭에 따라 낮은 값으로 가는것은 마찬가지임
- 여기서 Initial Learn Rate에 대해서 Epochs를 5번 사용했다면 이 Acc이 최고점인지 알 수 없음
- 아래와 같이 Epochs를 50번으로 늘려면 5번 했을때와 비교했을 때 변동은 계속 존재하더라도 점점 수렴하며 높아지는 모습임을 볼 수 있음, 점점 좋아짐

![one](/img/DeepLearning/Options/twentyseven.png)

- 점점 좋아지므로 이 Epochs를 더 높여야 할 수 있음, 이를 100까지도 진행해 볼 수 있음, 아래를 보면 50번을 넘어가면 점점 아예 수렴함을 볼 수 있음, 이를 바탕으로 최소 50번 이상은 해야함을 알 수 있음

![one](/img/DeepLearning/Options/twentyeight.png)

- 여기서 만약 Learn Rate를 올리면 100번을 해도 값이 수렴하지 않음을 알 수 있음, 이는 최적점 근처에서 계속 수렴하지 못하고 맴도는 상황이라고 이해하면 됨, 이럴 땐 Learn Rate를 낮춰야함
- 만약 여기서 Learn Rate를 더 낮춘다면 아래와 같이 Acc가 0.0001보다 더 완만하게 느리게 상승됨을 알 수 있음

![one](/img/DeepLearning/Options/thirty.png)

- 여기서 MiniBatch 사이즈를 즉 전체 데이터 셋을 그 만큼의 사이즈로 나눠서 연산할 수 있음 3000개를 200개로 나눈다면 15개의 Batch로 연산, 이렇게 Parameter를 업데이트 하는데 그럼 15개의 Batch만큼 15번 업데이트 하는 것임

![one](/img/DeepLearning/Options/twentynine.png)

- 그럼 MaxEpochs는 100이므로 전체 데이터셋을 쓰는 것이 15번 업데이트 하는 것이므로 15 x 100 = 1500번 계산되는 것임, 아래와 같이 보면 한 100번 정도 되야 수렴이 됨을 알 수 있음

![one](/img/DeepLearning/Options/thirtyone.png)

- 너무 수렴만 하면 overfiting이 될 수 있으므로 유의해야함
- iteration의 개수는 batch의 개수와 동일함 그래서 위와 같이 100(MaxEpochs) x 15(Batch) = 1500이 됨
- 그리고 위에서 Learn Rate를 바꾸면 에러가 발생함, 즉 보폭값을 낮추면 낮출수록 학습시간이 오래걸림을 알 수 있음, 여기서 그러면 학습시간을 빠르게 하면서 개선할 수 있는 방법이 있는데 gradient clipping을 활용할 수 있음
- 즉 하강값이 급격하게 위에서는 0.001 같은 경우 이런식으로 들쭉날쭉한 경우 gradient clipping 하강 상승값이 너무 크면 갑자기 뛰면 이를 아예 날려버리고 픽스해서 설정함
- 아래와 같이 쓸 수 있음, GradientThreshold 값을 정해줌, 강제로 gradient의 들쭉날쭉 하는 값을 교정해버림

![one](/img/DeepLearning/Options/thirtytwo.png)

- 이를 설정하고 돌리면 기울기가 크게 상승, 크게 하강한 경우 강제로 설정값을 바꿔버리는 것임, 계산을 하면 원래는 NaN이 되는 것이 아래와 같이 나옴

![one](/img/DeepLearning/Options/thirtythree.png)

- 아직 수렴을 안 했다는 것은 GradientThreshold이 값을 너무 크게 설정한 것이므로 다시 조정해주면 됨
- 이러면 학습시간과 결과를 동시에 잡을 수 있음, 1로 설정하니 어느정도 수렴이 됨을 알 수 있음

![one](/img/DeepLearning/Options/thirtyfour.png)

- 마지막으로 알고리즘을 본다면 파라미터의 개수가 굉장히 많고 어떤 파라미터에 대해서 gradient가 다 다르게 적용할 것임, 그래서 이를 알고리즘으로 적용하는 것임
- step, stride, Learning Rate 다 동일한 뜻임
- 급격하게 떨어지는 경우는 small step을 그리고 천천히 변하는 경우는 larger step을 사용함

![one](/img/DeepLearning/Options/thirtyfive.png)

- 그래서 이런 상황에 맞게 다르게 적용할 수 있는데 sgdm의 경우 momentum을 가지고 이런 step을 움직임
- RMSProp 같은 경우에는 과거의 history만을 가지고 gradient를 learning rate를 결정을 함

![one](/img/DeepLearning/Options/thirtysix.png)

- 이 두 가지를 모두 고려하는 것을 Adam이라고 함, momentum과 history를 다 사용함

![one](/img/DeepLearning/Options/thirtyseven.png)

- 결론적으론 RMSProp보다 sgdm을 더 많이 사용하긴 함, RMSProp은 과거의 영향을 많이 받아서 만약 그 경향성이 변동성이 매우 크면 똑같이 계속 크게 됨 history를 반영하므로, 너무 큰 변동성을 그대로 반영을 해버림
- 학습을 하면서 계속 Options을 건드리면서 해야함, 실제로는 매우 연산이 오래걸림
- Validation Data Set의 경우 Overfiting의 경우를 경계해야 하므로 이를 신경을 써야함
- 여기서 Loss도 낮고 Mini-BatchAcc가 높은데 즉, training data에 대해선 잘 나오는데 testAcc가 낮은 경우가 있음, 이러면 과적합임, 즉, training data를 너무 과하게 학습해서 training data에 대해서만 결과가 좋고 test data에 대해서는 일반적인 특징이 아닌 너무 과하게 학습을 해서 test에 대해서는 score가 낮게 나오는 것임
- 이를 위해서 Validation Data Set을 사용해야함
- 만약 일반적인 데이터를 통으로 사용한다면 아래와 같이 3개를 받아야함, 즉 data를 나눌 때 애초에 val data를 추가해서 받으라는 것

![one](/img/DeepLearning/Options/thirtyeight.png)

- Validation Data는 array 방식이든, cell 방식이든 어떤 방식이든 상관이 없음
- 여기서 그렇게 데이터를 만들고 옵션에다가 추가하면 됨 Validation Data와 Validation을 몇 번 할건지에 대해서 얼마나 자주 할 건지

![one](/img/DeepLearning/Options/thirtynine.png)

- 이를 실행하면 점선 그래프가 나오는데 이는 Validation data에 대한 accuracy 값임, training data 보다는 좀 낮고 그럼
- 아래와 같이 결과는 동일하게 나옴을 알 수 있음

![one](/img/DeepLearning/Options/fourty.png)

- 수렴을 안하면 Epochs를 더 올려주면 됨

## Training Options 추가
- 데이터를 로드하고 아래와 같이 해당 데이터에 대해서 볼 수 있음

![one](/img/DeepLearning/Options/fourtyone.png)
![one](/img/DeepLearning/Options/fourtytwo.png)
![one](/img/DeepLearning/Options/fourtythree.png)

- 위를 통해 패션잡화로 데이터가 이루어져 있고 그에 맞게 카테고리가 정해져 있음을 알 수 있음
- 이 카테고리 역시 find를 통해 인덱스 혹은 logical array로 뽑을 수 있음

![one](/img/DeepLearning/Options/fourtyfour.png)

- 그리고 데이터가 grayscale과 해상도가 떨어짐을 알 수 있음
- size함수를 통해 28x28x1임을 알 수 있음
- 데이터 자체만을 본다면 simple layer를 통해서 구분이 쉽게 가능함을 알 수 있음
- 시간 관계상 평가때 ValData를 안 한 것이지만 ValData는 무조건 있어야함 과적합을 볼 수 있고 이를 통해서 Training Options을 재수정할 수 있으므로
- 현재 쓰고 있는 데이터는 데이터가 복잡하지 않으므로 심플한 layer를 사용할 것임
- 여기서 validation data의 경우 test data는 절대 건드리면 안되므로 training 데이터를 활용하여 data를 구분할 것임
- pt1, pt2를 통해서 training, test data의 인덱스를 나눔, 아래와 같이 나눌 수 있음

![one](/img/DeepLearning/Options/fourtyfive.png)

- 하지만 굳이 test는 안써도 됨 `~training`이 test이므로 그래서 아래와 같이 씀

![one](/img/DeepLearning/Options/fourtysix.png)

- 여기서 또 다른 방식으로 training 함수를 쓰지 않고 cvpartition에서 이미 구분이 되어 있으므로 pt.training, pt.test로 그대로 사용해서 할 수 있음
- 대신 인덱스 값은 랜덤으로 계속 변할 수 있음
- 그 다음 간단하게 layer를 쓸 것임, 이전에 학습한 layer와 동일함, 단 여기서 디테일한 부분은 조금 다름
- 이전에 쓰던 것의 필터는 3x3인데 현재 쓰고 있는 데이터는 28x28인데 이 값에 대해서도 한 번쯤은 더 생각해봐야함, 일단 현재 데이터 셋에서는 적당한데 여기서 4x4 더 크게 가져가면 stride 값을 너무 크게 가져가게 됨, sliding 하는데 있어서 폭이 크거나 너무 과함

![one](/img/DeepLearning/Options/fourtyseven.png)

- 그 다음 기본적으로 알고 있는 옵션을 가지고 그대로 써주면 됨, Validation data는 항상 봐야함, 그런 데이터가 아닌 이상 거의 무조건 씀, 그리고 학습을 시키고 Validation 판단을 하면 됨

![one](/img/DeepLearning/Options/fourtyeight.png)
![one](/img/DeepLearning/Options/fourtynine.png)

- 일단 과적합이 되지 않고 Validation이 적절함을 알 수 있음, 그리고 어느정도 Acc이 Validation에서 평탄화 된 것을 알 수 있지만 이것 말고 Loss를 좀 더 눈여겨 봐야함, Loss는 점점 간격이 벌어지는 것을 위에서 알 수 있음
- 여기서 Acc는 평탄화가 되어 있는데 Loss를 보면 떨어질만한 여지가 있음 Val 기준으로, 충분히 사용을 했음에도 Val의 그래프가 Plateau가 Loss는 개선의 여지가 충분히 있음
- 그리고 민감도 측면에서 Loss가 좀 더 높음, 그 이유는 확실하게 알고 있어야함
- 일단 위의 그래프 상에선 개선의 여지 InitialLearnRate를 더 높일 수 있음
- 여기서 Acc은 0.73 정도 나옴

![one](/img/DeepLearning/Options/fifty.png)

- 여기서 학습률을 0.001로 높이면 아래와 같이 나옴을 알 수 있음

![one](/img/DeepLearning/Options/fiftyone.png)
![one](/img/DeepLearning/Options/fiftytwo.png)

- 여기서 학습률을 높이니깐 Plateau가 눈에 띄지 않음, 즉 개선의 여지가 존재함 여기서  InitialLearnRate를 더 조절을 해서 정확도를 높일 여지가 있음, 정확도 역시 좋아짐을 알 수 있음
- InitialLearnRate는 10의 배수 형태로 조절을 함 여기서 0.01로 높일 수 있음, 하지만 여기서는 살짝 이상한 부분이 감지됨, 그래도 정확도는 조금 더 올라가긴 함

![one](/img/DeepLearning/Options/fiftythree.png)
![one](/img/DeepLearning/Options/fiftyfour.png)

- 하지만 Acc 그래프에서 간격이 너무 많이 벌어짐, 그리고 Loss에서 Plateo가 이미 지나간 것임을 볼 수 있음, Acc에서 어느정도 수렴하는 것처럼 보이다가 Val 그래프와 간격이 벌어지면서 과적합이 일어나는 것을 보임
- 과적합이 일어나더라도 Acc이 좋으면 상관이 없긴함 하지만 과적합이 발생하면 Loss 값을 봐야함, Loss 민감도가 더 높기 때문에 가만 보면 30번 미만에서 아주 작은 Loss를 찍다가 그 이후에 Loss가 올라가는 것을 보임
- 이것은 이 부분에서 과적합이 발생하여 Val Loss가 증가하면서 Acc가 떨어지는것임을 알 수 있음
- 이를 보면 LearnRate가 크니 빠르게 수렴은 하는것을 볼 수 있음, 그렇기 때문에 민감도는 Loss가 더 높으므로 Accuracy보다도 Loss가 떨어지는 것을 먼저 보는것이 맞음, Acc비교보다 Loss를 보는게 나음
- MaxEpochs를 0.01에서 100번을 하면 아래와 같이 나옴

![one](/img/DeepLearning/Options/fiftyfive.png)

- 즉 위에서 말했듯이 0.01에서 50번을 할 경우 민감도가 높아서 정확도가 떨어지는 부분이었는데 100번을 할 경우 그 Loss가 높아지고 정확도가 떨어짐을 알 수가 있음
- 그래서 이 경우 MaxEpochs의 경우 20 ~ 30정도 선으로 맞추는 것이 좋음, 아래와 같이 0.01에서 27 정도가 적당함을 알 수 있음

![one](/img/DeepLearning/Options/fiftysix.png)

- 앞서 100번을 기준으로 왜 Loss 값이 민감도가 높고 높게 나오냐면 Acc의 경우 제대로 데이터를 맞출 경우 그 케이스가 반영이 됨 하지만 Loss는 Function에 의해서 구해지고 Loss는 score 값으로 같이 뽑히는 것이 있는데 아래와 같이 confidence값 즉 예측한 것을 어느정도 확신을 갖고 말할 수 있는지를 말함

![one](/img/DeepLearning/Options/fiftyseven.png)

- 여기서 scores에 대해서 Acc의 경우 예측만 맞으면 그것이 반영이 되서 Acc를 계산하지만 Loss의 경우 정확히 맞췄어도 위에서 본 scores값에 따라서 그 score 값이 낮다고 한다면 Loss가 늘어나는 것임, 하지만 Acc에서 맞추는것은 동일하지만 scores에 대해서 이게 맞다고 확신하는 자신감 score가 상대적으로 낮아지기 때문에 이게 Loss에 반영이 되서 Loss가 항상 Acc보다 민감한 것임
- 학습률이 너무 높으면 주변을 맴도는 값이 튀어버리는 현상이 일어남, 아래와 같이 NaN, undefined로 나오거나 아니면 값이 맴돌면서 안 나오는 경우가 있음

![one](/img/DeepLearning/Options/fiftyeight.png)

- 그래서 이럴 때는 InitialLeranRate를 낮추는 것이 맞음, 비슷하게 나오면 10의 배수로 계속 낮추면서 최대의 고정 적정 학습률을 찾는 것이 좋음
- 그 다음 MaxEpochs의 경우 위에서 100번을 했을 때의 case에서 20 ~ 30이 최적 값임을 알 기 때문에 그 때 끊어줘야 함을 알 수 있음, 그 이후 Loss가 증가하므로, 그리고 아래 표시한대로 차이가 벌어지기 시작하면 과적합임

![one](/img/DeepLearning/Options/fiftynine.png)

- 과적합이 난다고 무조건 잘못됐다고 할 순 없음, Acc의 영향을 안 끼치는 경우가 있기 때문임, 그래도 조심을 해야하는 것은 맞음, 어느정도의 차이가 있는것은 당연함
- valData는 과적합을 모니터링 하기 위해서 활용함, 여기서 나타나는 어느정도의 차이는 과적합이 시작함을 나타냄 10% 이내는 어느정도 인정함
- training의 flow chart는 아래와 같이 구성되어 있음

![one](/img/DeepLearning/Options/sixty.png)

- 위에서 설명했다시피 learn Rate를 조절해서 튀는 값 NaN을 조절하고 그 다음 loss가 줄어드는 상황에서 Epochs를 늘려서 학습을 더 시키고 이 값을 수렴하게함, 여기서 스케줄링으로 조절 할 수도 있음 → underfit한 상태인지 체크
- 여기서 과적합을 체크할 때 위의 과정을 다 거친후 과적합에 대해서 training data에 대해서 조절하거나 regularlization을 할 수 있음
- 여기서 아키텍처를 설계할 때 pretrained를 보고 모방하면서 해나가고 구글링하면서 비교대조를 하면서 해야함
- 여기서 과적합을 방지하기 위해서 dropout layer를 fullyConnected나 convolutional layer를 넣으면 됨
- 여기서 어느정도 수렴을 하는데 있어서 underfit 상태를 돌파하거나 병렬로 연결해서 다시 구성을 해서 처리할 수 있음
- 또 다른 옵션을 아래와 같이 테스트 해볼 수 있음, 과적합이 빨리 일어남을 알 수 있음

![one](/img/DeepLearning/Options/sixtyone.png)

- 아래와 같이 LearnRate에 대해서 조절을 해 줄 수 있음 - documentation 참조
- 여기서 과적합을 아래와 같이 어느정도 잡아줌을 알 수 있고 정확도도 올라감을 알 수 있음

![one](/img/DeepLearning/Options/sixtytwo.png)
![one](/img/DeepLearning/Options/sixtythree.png)

- 여기서 과적합을 더 잡기 위해서 Regularization을 건드릴 수 있음

![one](/img/DeepLearning/Options/sixtyfour.png)
![one](/img/DeepLearning/Options/sixtyfive.png)

- 여기서 이에 그치지 않고 layer을 더 깊게 짤 수도 있음, 아래와 같이 추가 레이어를 만들어 넣을 수 있음 단 주의할 점은 발전적인 방향으로 나가기 위해서는 위에서 filter개수에 대해서 20개 고정이 아니라 더 늘려주는 것이 좋음

![one](/img/DeepLearning/Options/sixtysix.png)

- 근데 큰 정확도의 차이는 나지 않음, 대략적으로 층만 쌓았기 때문임
- 여기서 좀 더 정교하게 디테일한 값을 아래와 같이 조절을 할 수 있음, filterSize 위주로 조절을 할 수 있음

![one](/img/DeepLearning/Options/sixtyseven.png)

- 여기서 오히려 정확도는 좀 더 올라감, 옵션을 건드리지 않았다는 가정하에
- 이런식으로 옵션을 계속 건드릴 수 있음, 과적합 방지 추가적으로 GradientThreshold 역시 만들 수 있음