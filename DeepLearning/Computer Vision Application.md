### Computer Vision Application
- Object Detection
- 얼굴 인식, 자율 주행차 등 구분을 하는 것
- 먼저 데이터를 불러와서 씀, 기존과는 살짝 다른 데이터 형태임, 레이블과 좌표값처럼 나와 있는게 있음

![one](/img/DeepLearning/Computer/one.png)

- 이 좌표값은 아래의 사진에서 바운딩 박스의 좌표값(x,y) 그리고 박스에 가로, 세로 길이를 뜻함

![one](/img/DeepLearning/Computer/two.png)

- 컴퓨터 비전에서 CNN이 쓰이는 것은 위의 4가지 방식으로 쓰임, Semantic Segementation이 제일 어려움, 영역 전체를 차지해서 나타냄, 레이블링하기 까다롭고 시간이 오래걸림 주로 자율 주행차에서 많이 쓰임
- 여기서 이 부분은 바운딩 박스까지 같이 학습을 시켜야함, 그리고 Object Detection을 해야함
- Object Detection을 하기 위해서 데이터 전처리의 일반적인 과정을 거쳐야함 물론 Pretrained Network를 가져와서 쓸 것임, 이 petImage는 week3에서 한 petImages를 활용한 것임
- 여기서 이미지를 하나 불러올 때 imageFileName은 cell 형태로 되어있기 때문에 이 값을 가져올 때 아래와 같이 가져와서 내용을 불러와야함(여기서 week3의 petImages를 추가해둬야 이미지를 볼 수 있음)

![one](/img/DeepLearning/Computer/three.png)

- 여기서 위에서 설명했듯이 바운딩 박스와 레이블링에 대해서 Image에 넣을 수 있음, Object Detection을 위해서
- 여기서 Madeline의 첫번째 사진이므로 아래와 같이 레이블과 cell형태로 지정해줘야함(그래야 그 값만 나옴)
- 그리고 이미지 안에다가 Annotation을 아래와 같이 추가하여 바운딩 박스를 둘 수 있음, 이미지 먼저 넣고 그 다음 바운딩 박스 위치, 그다음 레이블과 옵션을 넣으면 됨
- 그러면 아래와 같이 바운딩박스가 쳐지는 것을 알 수 있음, 레이블과 바운딩 박스를 같이 체크됨

![one](/img/DeepLearning/Computer/four.png)

- 이러면 Object Detection을 predict하기 위한 학습 데이터로 쓸 수 있음
- 사이즈가 490x653x3인데 여기서 Pretrained를 쓸려면 데이터를 변환해야 하는데 리사이즈 할 경우 바운딩 박스의 위치와 사이즈도 리사이즈도 같이 되야함
- 즉 Ground Truth 위에서 테스트로 쳐 본 실제 데이터 역시 리사이즈할때 전처리를 같이 해줘야함, 박스의 위치와 크기도 변하므로
- 먼저 imageDataStore를 활용해서 해 볼 것임, 불러오는 것은 imageFileName을 불러오고 바운딩 박스 역시 불러와야 함(box label datastore), 여기서 바운딩 박스는 TBL 즉 테이블 형태로 넣어주면 됨(boxLabelDatastore의 경우), 레이블과 바운딩 박스의 위치가 테이블 형태로 되어 있으므로 테이블 형태로 집어넣어야 함(cell을 벗기면 array 형태가 날라감)
- 그 다음 그 두개를 합친 후(combine) 그 전체 크기를 리사이즈(resize)하고 보면 됨, 아래와 같이 함, 리사이즈의 경우 transform(transfrom datastore를 위한 것을 씀)을 통해서 할 것임 scaleGT라는 지역함수를 활용해서 쓸 것임(왜냐하면 합친 datastore를 가지고 있어서 augmentedImageDatastore를 쓸 수 없음)

![one](/img/DeepLearning/Computer/five.png)
![one](/img/DeepLearning/Computer/six.png)

- 이미지와 바운딩 박스를 핸들링 하는데 주로 실습한 것임, 왜냐하면 Object Detection은 위와 같은 방식으로 해야함, 기존에 단순히 했던 Image처리와는 다르게
- 이를 preview로 볼 수 있음, datastore에 들어가 있는것을 미리 볼 수 있음, 여기서 바운딩 박스 처리 역시 동일하지만 newGT 즉, preview를 통해서 확인했을 때 각각 1,2,3에 이미지, 바운딩박스 위치, 레이블링이 들어가 있기 때문에 이를 응용하면 됨(행이 하나라서 1,1로 안 쓴 것임)

![one](/img/DeepLearning/Computer/seven.png)

- Object Detection은 Image Classification + a임, Semantic Segmentation 역시 그럼

### R-CNN
- R-CNN을 통해서 직접 학습시켜서 Detection을 할 수 있음
- Matlab 앱에서 Image Labeler가 있음, 직접 이미지 레이블링을 할 수 있음
- import → File or workspace를 통해서 직접 가능
- 이미지 데이터 스토어를 직접 만들어서 할 수 있음

![one](/img/DeepLearning/Computer/eight.png)

- 그러면 이 저장된 imageDatastore에 있는 파일들이 아래와 같이 쭉 나옴

![one](/img/DeepLearning/Computer/nine.png)

- 여기서 label을 누르면 직접 달 수 있음, 그럼 아래와 같이 추가됨

![one](/img/DeepLearning/Computer/ten.png)
![one](/img/DeepLearning/Computer/eleven.png)

- 이런식으로 바운딩 박스를 직접 만들고 export 할 수 있음, 그리고 아래와 같이 직접 바운딩박스를 누르고 직접 체크하면 됨, 하나하나 만들 수 있음

![one](/img/DeepLearning/Computer/twelve.png)

- 여기서 Object Detection이 아닌 Segmantaion을 위한 픽셀 역시 만들 수 있음
- 그리고 아래와 같이 Export 역시 가능함, 이를 저장 가능함

![one](/img/DeepLearning/Computer/thirteen.png)
![one](/img/DeepLearning/Computer/fourteen.png)

- GT 값을 이와 같이 export해서 뽑을 수 있음, 이런식으로 Image Labeler 사용할 수 있음, 이외에도 다양한 Video 앞서 설명한 컴퓨터 비전 관련한 요소들 앱으로 활용가능함
- R-CNN의 경우 욜로라고 말함, Object Detection에 가장 많이 쓰임, 3개의 다른 타입이 있고 영상에 쓸 것인지 이미지에서 할 것인지에 따라서 그 사용 범주가 다름
- CNN은 이미지 input size를 조정을 해줘야 하지만 R-CNN의 경우는 함수를 사용해서 학습하므로 굳이 imageInputSize도 필요가 없음, 그저 학습만 시켜주면 됨
- 아래와 같이 먼저 옵션을 설정해서 함, 여기서 R-CNN을 할 경우 MiniBatchSize는 항상 1로 해줘야함, 매순간 Weight와 Bias를 업데이트 할 수 있게끔 1로 설정해줘야함(필수사항임)
- 그리고 RCNN을 하면 됨 그리고 데이터를 그대로 넣을 것임, 이미지만 학습하는게 아니기 때문에, 이미지 바운딩박스 레이블을 포함해야 하므로 그 다음 alexnet 등 다양한 pretrainedNetwork와 options을 쓰면 됨

![one](/img/DeepLearning/Computer/fifteen.png)

- 시간이 오래걸리므로 일단 학습된 데이터를 기준으로 처리함
- 먼저 testImages 즉 비교하기 위한 값으로 testImages의 Ginny 값을 불러옴, 그리고 나서 detect 함수를 통해서 detector에 있는 네트워크와 dogim를 비교해 볼 것임, 여기서 detect에서 바운딩박스, score, labels을 뽑을 수 있음

![one](/img/DeepLearning/Computer/sixteen.png)

- 이제 이 부분을 Visualization 즉 뽑은 데이터를 시각화해서 처리를 하는 것이 중요함, 바운딩 박스를 치고 체크를 하는 것, 앞서 했듯이 바운딩 박스를 처리함
- labels(categorical) 역시 cell 변수와 동일하게 취급해서 처리할 수 있음 → cellstr 활용해서 처리할 수 있음, str과 같이 처리함

![one](/img/DeepLearning/Computer/seventeen.png)

- 여기서 바운딩 박스 말고도 몇 %의 score(confidence)를 가지고 확신하는 것인지 체크를 할 수 있음, 위에서 나온 scores 값에 대해서
- 여기서 scores 역시 넣을 수 있음, 여기서 label에서 score를 추가해서 만들 것임 바운딩 박스에서 레이블링으로 그대로 cell을 활용해서 쓰면 됨, 반복문을 통해서 데이터를 넣을 것임, 여기서 string으로 바꿔서 넣어줘야함

![one](/img/DeepLearning/Computer/eighteen.png)

- 그리고 이 값을 그대로 바운딩 박스로 레이블링과 함께 넣어주면 됨

![one](/img/DeepLearning/Computer/nineteen.png)

- False positive - 잘못되서 레이블링을 잡는 경우가 있음, Confidence가 낮게끔, 이때 Threshold 임계값을 둬서 그 값이 넘어가지 못하면 바운딩 박스를 안 나오게 할 수 있음
- 아래와 같이 기준을 잡고 해당 하는 부분만 뽑을 수 있음

![one](/img/DeepLearning/Computer/twenty.png)

- 그러면 직관적으로 이 값을 labelScores에도 적용을 하여서 넣으면 됨, 즉 이렇게 하면 Threshold 값을 넘어가면 바운딩 박스를 치고 Threshold가 낮으면 안 치게 할 수 있음

![one](/img/DeepLearning/Computer/twentyone.png)
