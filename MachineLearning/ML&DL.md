## ML & DL
- Machine Learning과 Deep Learning은 어느정도의 차이가 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/dc806f41-027e-4afe-afa9-4f3d38f484a3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T052607Z&X-Amz-Expires=86400&X-Amz-Signature=37810840057baa352b9af899b82e475a833e7cfc9a675b48873ac5a472ba5b06&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

### Machine Learning
- 데이터를 찾아가는 부분에서 시작함 
- 각각의 특징들을 feature extraction, operator가 직접 뽑아야함
- 공정분야(조선업도 포함)에서도 많이 사용함, 분석을 해서 고칠점을 찾기 위해서 
- 유튜브 알고리즘, 오픈마켓에서 구매한 히스토리 분석등은 비지도 학습을 통해 클러스터링하여서 추천을 해주는 시스템임

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e06b195e-f8a3-4396-a473-4a1578a6c8ed/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T052753Z&X-Amz-Expires=86400&X-Amz-Signature=0390366b2bb11fedd7f907d02947ee10736a84f3cef6a2393db51f86ad0647fa&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

### Unsupervised Learning
- Clustering 사용 -> Grouping, Group에 특성을 나눔
- Clustering에 다양한 모델이 있고 제시됨(분류기,classifier) -> 다양한 방법론들
- 각각의 featur들을 variables, observation이라함
- Input을 했을때 별도의 특정 Output이 있진 않음

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/376bab8c-3356-4d16-bc36-8ee60661f0f2/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T052955Z&X-Amz-Expires=86400&X-Amz-Signature=493c9ff5ceb36aec921a25f63046db5619c239b9121a89323015a9645f06aaac&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

### Supervised Learning
- Input이 있으면 Output이 있음(예측을 함, response variable)
- Input은 Output을 예측하기 위해 넣는 데이터임
- Output은 지도학습을 통해 예측하고자 하는 결과임
- Output이 어떠한 카테고리를 가지고 있는가 확인을 할 수 있는데 이를 Classification이라 할 수 있고 숫자로 나온다면 Regression임
- Classification -> 다양한 feature를 통해서 카테고리를 예측함(스팸인지 아닌지, 암인지 아닌지, 심장병인지 아닌지)
- Regression -> temperature의 변화, 날씨예측, 연비효율 예측등 숫자로 표현 

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b2d755c5-9b4d-4d39-b0a9-4e73cf8bd1d1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T053309Z&X-Amz-Expires=86400&X-Amz-Signature=6a87e67c28b233d880e191b6895645023cf8bbe0ec23000221b094173d8381b5&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 다양한 방법론,분류기, classifier가 존재함

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c28558e8-dea0-40ca-8ad2-ab5942138df1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T053355Z&X-Amz-Expires=86400&X-Amz-Signature=1dab6742703fa03f73a09c9b05fb4a29d1963d841ba0d1b63b68d7a1ebb00323&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

### Classification의 예시
- 단순하게 Yes, No 즉 이분법적으로 구분할 경우 사용함
- Input 데이터를 가지고 Output의 데이터를 매칭시킴, 다양한 방법론 적용
- 영향을 많이 주는 특징에 대해서 뽑아놓고 그것을 모델로 다시 만들어서 함
- 위와 같이 학습을 시킨 후 모델을 통해서 33번째 데이터에 대해서 예측을 할 수 있음
- 모델을 만든뒤 예측하고자 하는 output 데이터에 대해서 feature 값을 입력하면 그 feature 값을 통해서 output 데이터를 예측하는데 이를 지도학습이라 함
- 위와 같은 카테고리화하는것은 classification임

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b74d53d5-fb76-4eeb-971b-8c236459298e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T053618Z&X-Amz-Expires=86400&X-Amz-Signature=4f00ffdcf8ff491555b62a8b8d2aedb046bc17986f15d7f077f57342dbbac64f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

### Regression의 예시
- output 데이터가 숫자화 된 것을 Regression 모델이라함 
- 위와 같이 자동차 연비 효율 예측할 수 있음 
- 각각의 feature를 observation에 대해서 입력을 하고 해당되는 observation의 output을 입력후 input과 output을 매칭시키면 모델이 나오는데 그 다음 그 모델을 새로운 observation에 대해서 예측할 수 있음 
- 위와 같은 숫자형태로 나오는 것을 regression이라함

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9b2035a6-9682-4fa3-9a3a-fdcf400ed22d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T053756Z&X-Amz-Expires=86400&X-Amz-Signature=80c84a74ea97a435414f289925865447e3b1c2bd0d5d9609cd9314ccdecac8bf&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

### Deep Learning
- feature selection을 할 필요없이 데이터만 넣으면 Deep Learning이 알아서 feature를 추출해서 그 특징으로 학습을 함 
- 데이터가 부족할 경우 feature selection이 힘들 수 있음, 이때 머신러닝을 활용하여서 feature를 뽑은 후 그 feature로 Deep Learning에 학습을 하게끔 할 수 있음 
- 대표적으로 얼굴인식, 암세포구분(이미지 기반), 음성, 텍스트 기반 분석등이 있음 

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b9d7a69c-2002-4cd1-a285-705336613f99/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T053921Z&X-Amz-Expires=86400&X-Amz-Signature=ac3bd961e1927d64c026e5b5aee776842769a66d33faf0939fcd81b236ab4e76&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

### CNN(Convolution Neural Network)
- 가장 많이 사용되는 딥러닝 분야, 이미지, 영상, 텍스트, 음성등 
- Input 데이터를 하면 3가지 layer를 통해서 알아서 추출하고 분류함, Output 데이터는 직접 입력해줘야함, 알아서 feature들을 뽑아서 학습을 함
- 이러한 Feature Detection은 위의 3개의 layer를 활용함

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/785635f2-e707-4848-b96e-859b0d54f9a5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T054116Z&X-Amz-Expires=86400&X-Amz-Signature=286ab47dfce41005057483c1036bb3d3aee19e3cdd8efe350a533666e30dbae6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6f8ec742-3e5a-4bfe-97e9-0868bdfbdcef/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T054126Z&X-Amz-Expires=86400&X-Amz-Signature=893223c3ea996bcd5657cfa9f3700ae901e328d32b96ad71e5f3c8ae926df515&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

### 예시
- 위와 같이 각각의 layer들이 활용됨 
- conv은 이미지에 대해서 convolution matrix를 활용함, 다양한 이미지 추출, 눈동자를 잘 추출하는 이미지를 선택함(output을 지정했으므로)
- ReLU 눈동자를 제외한 이미지를 다 0으로 만듬, 눈동자 특징을 강화시킴, 나머지는 어둡게 함 threshold 값 정해줌(0값 이하가 나오면 다 0으로 만듬)
- max pooling을 통해서 output이 확실히 나오게끔 더 강화시킴, 자동으로 extract 함
- 이러한 과정을 거쳐서 자동으로 눈동자를 구분해서 추출함 
- 이미지, 사운드, 텍스트, 이미지 기반 데이터가 딥러닝이 강점을 가지고 있음