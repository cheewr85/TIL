### Training Option
- LSTM의 Training의 option을 조정해서 할 수 있음
- 직접 하는건 데이터가 오래걸리기 때문에 어떻게 튜닝을 하는지 보는게 좋음, CNN에도 역시 적용할 수 있음
- LSTM에서는 parameter tuning이 더 중요하게 작용함
- sequence length 역시 중요하게 작용을 함
- 우선 아래와 같이 옵션을 설정하여서 학습을 시켜볼 것임, CNN 보다 Max Epochs를 높게 해도 과적합이 일어날 확률이 적음
- 여기서 plateto 값을 기준으로 이 Max Epochs를 줄이면서 적용을 할 수 있음, 우선 InitialLearnRate는 0.1로 적용을 할 수 있음

![one](/img/DeepLearning/SeqOptions/one.png)

- 0.1 기준으로는 아래와 같이 Loss는 NaN이 뜨고 제대로 학습이 안된 것을 알 수 있음

![one](/img/DeepLearning/SeqOptions/two.png)
![one](/img/DeepLearning/SeqOptions/three.png)

- 그 다음에는 InitialLearnRate를 0.01로 낮출 수 있음 대부분 1/10로 나누는게 정석임
- 이를 LearRateDropFactor라고도 하는데 LearnRate 스케줄링시 얼마만큼 떨어뜨릴것인가를 하는 부분임
- 우선 0.01로 했을 때 adam은 아래와 같이 나옴

![one](/img/DeepLearning/SeqOptions/four.png)

- sgdm의 경우는 조금 다른 것을 알 수 있음

![one](/img/DeepLearning/SeqOptions/five.png)

- sgdm의 경우 Momentum이 들어가고 adam의 경우 이 값이 없고 GradientDecayFactor가 들어감을 알 수 있음
- 여기서 이 값을 건드리지 않고 sgdm과 adam에 동일하게 들어가는 options에 대해서 튜닝을 하여서 값을 조절할 것임
- 그리고 성능 향상에 있어서 튜닝을 하는데 있어서 아래와 같이 가이드를 생각할 수 있음, 물론 이것을 모두 적용시키는 일반화는 시킬 수가 없음

![one](/img/DeepLearning/SeqOptions/six.png)

- 0.1일 때 NaN 그리고 갑자기 튀는 spike가 나타나면 learn Rate를 낮추는 것이므로 0.01로 낮춰서 한 것임, 아래와 같이 꾸준히 Loss가 떨어지고 Spike가 없음을 알 수 있음

![one](/img/DeepLearning/SeqOptions/seven.png)

- 아래와 같이 상승과 올라가는 과정이 반복되고 결론적으로 spike와 loss가 확 튀는걸 볼 수 있음, 그리고 어느정도 pleato한 부분이 나옴, 향상될 수 있음을 생각할 수 있음

![one](/img/DeepLearning/SeqOptions/eight.png)

- 근데 이 값이 options의 절대적인 것을 알려줄 수 없음, 랜덤하게 나오기 때문에 항상 똑같은 결과물로 나오는 것이 아니기 때문에, 그러면 training을 여러번 해서 어느정도 확인을 해야함
- 예측을 보면 아래와 같이 나옴 썩 좋은 것은 아님

![one](/img/DeepLearning/SeqOptions/nine.png)

- 두 번째로 학습을 했을 때 첫번째와 비교해서 NaN이 나오고 무의미한 결과로 수렴이 되버림

![one](/img/DeepLearning/SeqOptions/ten.png)

- 세 번째에도 역시 이와 유사하게 training이 제대로 되지 않은 경우가 있음, 이러면 options의 조정이 필요함 dropvector 즉 LearnRate를 1/10 줄일 필요 있음, 0.001로 함

![one](/img/DeepLearning/SeqOptions/eleven.png)

- 이렇게 하면 경향도 천천히 떨어지고 NaN이 안 뜨고 계속 상향됨을 기대하면서 계속 진행을 할 것임, 결과는 하지만 아래와 같음

![one](/img/DeepLearning/SeqOptions/twelve.png)

- 변동성이 좀 있긴함, 그래도 개선의 여지가 있으므로 MaxEpochs를 더 늘릴수도 있음, 그래도 변동성과 Spike 발생이 조금 문제가 됨
- 이러면 LearnRate를 조금 더 낮추고 MaxEpochs를 대폭 늘리면 안정적이긴 하나 시간이 매우 오래 걸릴 것임
- 여기서 그러면 Gradient 값을 잡아서 변동성을 안 생기게 할 수 있음 굳이 LearnRate와 Epochs를 건드리지 않고
- 왜냐하면 계속 비슷한 경향성이 나타낼 확률이 높음, 그래서 해당 options은 유지한채로 GradientThreshold 값을 잡아줄 수 있음

![one](/img/DeepLearning/SeqOptions/thirteen.png)

- 이 결과는 아래와 같음을 알 수 있음

![one](/img/DeepLearning/SeqOptions/fourteen.png)

- 첫 번째와 비교했을 때 어느정도 변동성을 잡고 spike가 줄긴 했고 좀 나아지긴 했지만 엄청 만족스러운 결과치는 아님, 조금 더 나아진 정도임
- 여기서 일단 GradientThreshold로 잡아주고 학습속도가 느리므로 LearnRate를 조금 더 올리는걸로 해볼 수 있음

![one](/img/DeepLearning/SeqOptions/fifteen.png)

- 결과는 아래와 같이 나옴, 일단 학습속도가 빨라지긴 했으나 spike가 여전히 튀긴함, Threshold 1도 많이 잡은것임, 더 잡기 힘듬

![one](/img/DeepLearning/SeqOptions/sixteen.png)

- 여기서도 중간의 변동성이 아쉬운것은 마찬가지임, 갑자기 값이 떨어지므로 그렇다고 Epochs를 중간에 끊어서 변동성 이전의 부분으로 하는것은 꼼수이고 본질적인 해결책이 되지 못함, 저런 변동성을 잡아줘야함, 갑자기 떨어지는 부분을 파라미터 튜닝을 해서 안정적으로 나오게 해야함
- 해당 옵션이 일관성이 있게 보이는지 보기 위해 몇 번 돌려서 볼 수 있음, 하지만 에러가 나왔음

![one](/img/DeepLearning/SeqOptions/seventeen.png)

- 이는 일관성이 좀 떨어지는 것을 의미함 Threshold를 여기서 더 올려볼 수 있음, 위에서 LearnRate를 올리면 나아지긴 하나 Threshold를 조절해볼 것임 5로

![one](/img/DeepLearning/SeqOptions/eighteen.png)

- 하지만 에러가 또 뜬 것을 알 수 있음, Threshold는 큰 영향을 끼치지 못한 것을 알 수 있음

![one](/img/DeepLearning/SeqOptions/nineteen.png)

- 그 에러가 나타나는 부분이 50 ~ 60 사이임을 알 수 있음, LearnRate가 0.001이면 Drop이 더 빨리 발생할 것임
- 여기서 그렇다면 0.005와 Threshold를 1로 고정하고 조정해야함을 알 수 있음
- 이를 이제 그러면 LearnRate Schedule이 Constant 즉 고정되어 있음을 알 수 있는데 이를 일정 시간이 지나면 값을 조절해서 정확도를 유지하는 수준에서 LearnRate만 낮추는 것임
- 이를 LearningRate Scheduling이라고 함, 아래와 같이 튜닝할  수 있음, Schedule을 하고 Period를 정해주면 됨, Period가 의미하는 것은 60 Epochs가 지나고 LearnRate를 떨어뜨린다는 것을 이야기 하는 것임, 여기서 떨어뜨리는 것은 기본값이 0.1인 LearnRateDropFactor를 통해서 조절을 함

![one](/img/DeepLearning/SeqOptions/twenty.png)

- 이를 진행해보면 결과가 아래와 같이 나옴을 알 수 있음, 어느정도 안정적이게 나옴을 알 수 있음

![one](/img/DeepLearning/SeqOptions/twentyone.png)

- 그래도 한 번 정도 더 돌려서 확인을 해봐야 하긴 함, 만일 비슷하면 일관성이 있음을 알 수 있음
- 여기서 아래와 같이 한 번 더 했을 때 일관성있게 다시 나옴을 알 수 있음, spike가 갑자기 튄 게 있지만 어느정도 안정성이 있음을 알 수 있음

![one](/img/DeepLearning/SeqOptions/twentytwo.png)

- 여기서 볼 것은 이렇게 trainingOptions을 통해서 튜닝을 잘하여서 초반보다 전체적인 퍼포먼스와 변동성 부분에 있어서 많이 나아짐을 알 수 있음
- 여기서 schedule에서 60 epochs에서 0.001, 0.0001씩 0.1씩 떨어지는 것을 알 수 있음, 이렇게 튜닝이 됨