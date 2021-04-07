## Dimensionality Reduction

## Roadmap
- [Multidimensional scaling](#Multidimensional-scaling)
- [Principal Component Analysis](#Principal-Component-Analysis)
- [Practice](#Practice)

## Multidimensional scaling
- Dimensionality Reduction을 하는 이유는 아래와 같은 데이터를 한 번의 시각화해서 보기 어려움이 있기 때문임
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/acb1cde5-b255-4960-91eb-c89635584ece/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T020241Z&X-Amz-Expires=86400&X-Amz-Signature=322b4956cde339f03dc82f34d362af1b70e745fea42aa73f873b1af42258fb21&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 위의 자료는 17차원임, 1112x17의 데이터이므로, 여기서 차원을 축소하여서 시각화할 수 있음, 하지만 축소시 데이터 손실이 발생함
- 차원 축소에 있어서 하나의 방식 중 하나가 Multidimensional scaling임
- 아래의 사진과 같이 차원이 많다면 Visualization을 할 수 없음, 그러므로 차원 축소를 해서 Visualization을 해줘야함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/aa105cfe-981b-4cbc-8048-8f99482d6840/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T020449Z&X-Amz-Expires=86400&X-Amz-Signature=e26cd2e264c5a810e3b72653e851ba4e52330a03ae43c6ebc959005d306d7813&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ec83ca69-eb86-4834-b7f1-6525c6060f9a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T020456Z&X-Amz-Expires=86400&X-Amz-Signature=31fd797b38e8eea044a9f76f5849a442a0114098fcfb9fa704cfb4c280a74073&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 차원 축소는 정보를 최소한으로 유지하면서 연산량을 축소시켜 빠르게 하기 위해서 사용함
- 그리고 비지도학습을 해서 클러스터링(=그룹화)를 함 -> 변수가 많고 차원이 많음, 눈으로 확인 못함 -> 차원 축소를 통해서 시각화하여 확인 가능
- 차원 축소의 Key
	- 신뢰성 유지, 데이터가 가지고 있는 정보를 손실이 없는 선에서(어느정도 손실이 있더라도 최대한) 최소한으로 줄여야함, 그래서 3차원을 지향함(2차원은 더 줄이는 것이므로)
	- 새로운 좌표축 생성시 그 좌표축은 서로 90도를 나타내야함
- 위의 사진과 같이 새로운 방식의 축으로 표현, 여기서 차원 축소가 단순히 observation을 잘라서 하는 것이 아닌 아예 새로운 변수로 차원을 생성하는 것임
- 여기서 Multidimensional scaling은 Pair-wise-distance 즉, 각 observation의 쌍거리를 유지시키는 선에서 이동을 함
- 아래와 같이 각 쌍들의 거리를 유지시키는 선에서 좌표축을 이동시킴, 여기서 쌍거리를 유지시키는데 필요없는 차원이 있으면 제거를 함
- 아래와 같이 차원이 계산되고 n일 경우 n(n-1)/2가 쌍거리를 유지시키는 선에서의 차원의 수임, 즉 쌍거리 유지의 문제가 없다면 해당되지 않는 차원은 제외시킴
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8c8df945-0f24-4a1d-bf56-fe45efe065dd/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T021337Z&X-Amz-Expires=86400&X-Amz-Signature=6c59ffadb93acad34c973fe9911688d8a60021e021b0223fa0ee4e844512875b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

## Principal Component Analysis
- Principal Component Analysis(PCA)의 경우 N차원이면 N차원을 선형결합을 통해서 새로운 N차원으로 나타냄
- 이에 따르면 Scaling은 17차원을 위에 계산한바와 같이 줄이면 16차원, PCA는 17차원을 거의 17차원으로 새로운 좌표축으로 나타내게 됨, 여기서 차원 축소가 거의 의미가 없어보이지만 이 축소는 사용자의 몫임
- 즉 아래와 같이 데이터가 주어진다면 여기서 기존의 x1,x2,x3 축을 통해서는 명확하게 이 데이터가 어떤 좌표축에 근접해서 표현되는지 알 수 없음
- 하지만 이를 아래와 같이 데이터 신뢰성을 유지하고 각각의 90도에 맞춘 새로운 좌표축을 형성했을 때 Pareto 그래프에서 보듯이 새로운 좌표축을 바탕으로 데이터가 어떻게 형성되었는지 알 수 있음
- 그러면 결과적으로 퍼센티지가 낮은 좌표축은 없앨 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d1aba9ec-f3ae-43d3-b5fd-a5a4bb7a2cbe/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T021903Z&X-Amz-Expires=86400&X-Amz-Signature=69c976cdc0760a28c7c2c85b786f8269cbfee29050e9fe1fdd5cca017beddf77&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 위의 사진과 같이 좌표축에 대해서 어떻게 남기고 활용을 할 지 직접 확인할 수 있고 이를 바탕으로 사용자가 어떤것을 없앨지 알 수 있음
- PCA의 경우 eigenvalue 값을 바탕으로 함, 아래와 같이 82%가 데이터를 나타낸다면 이를 기점으로 나머지를 5% 데이터 loss를 감수하고 해당 부분의 데이터를 끌어올리면 그만큼 82% 데이터의 표현도가 올라가는데 이런식으로 차원을 줄여나가는 것을 사용자가 직접 확인하는 것임
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/62176cb2-46f4-4756-abb7-41ac5bce5ebc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T022050Z&X-Amz-Expires=86400&X-Amz-Signature=766fbed12d08ffa91725f90cc3b6248d1cb644f7a6477f6ab86b5af1e21c9ecc&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

## Practice
- Multidimensional Scaling을 아래와 같이 사용함, 현재 사용할 stats에서 pair-wise-distance를 계산을 함, observation 기준으로 (1112*1111)/2가 됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/00088ca1-c366-4932-9450-a54dbea5ec24/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T022227Z&X-Amz-Expires=86400&X-Amz-Signature=059bd000aacf62034bbafc0cfe806240800393f63e9824d2700720a7318f49e0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">


- 그리고 아래와 같이 Classical Multidimensional Scaling을 실행함, observation은 동일하게 1112개 17차원으로 변환됨, 차원은 줄지 않음
- 여기서 중요한 것은 eigenvalue 값인데 Pareto Chart를 통해서 중요도를 확인함, 즉 새롭게 생성된 차원에서의 중요도를 나타냄
- 여기서 Pareto 차트를 잘 보면 위에서 설명한대로 해당 선 그래프가 하나의 차원을 줄일때마다 그만큼의 그 데이터 값이 올라가는 것인데 그래프 상 3차원일때 약 85%정도의 데이터를 나타냄을 알 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f4260c89-f865-4c58-a76b-ab7f30d8509f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T022414Z&X-Amz-Expires=86400&X-Amz-Signature=b50eee3f86bb9974c287cdd2e6f3b6b5bb4d6c2a88322f569acd9d14d296fd47&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 이를 바탕으로 3차원으로 표현, 새로운 3차원으로 표현을 했는데 17개 중 앞의 3개만을 가지고 그림, 여기서 데이터 손실은 당연히 있음 하지만 Pareto Chart에서 봤듯이 85%이상의 데이터를 가지고 있음을 암
- 이는 철저하게 Visualization을 위해서 사용하는 것임
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/76dbb715-3632-4269-90d6-71708f519af4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T022524Z&X-Amz-Expires=86400&X-Amz-Signature=b5128b38d03be42d0b102e35aefab41817afeeb7d9cea10eee7b24a7adb6e57f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- PCA
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/efc1e5f0-300d-49bb-8866-d285e704387c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T022542Z&X-Amz-Expires=86400&X-Amz-Signature=98b773ea3ead288efafd9ccaeea9f688828b78f64f655e91206fe5236f1ae7ee&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 위와 같이 한 줄의 코드로 활용, 2번째 score를 pexp, 각 component가 몇 %를 설명하는지 사용할 것임
- data를 집어넣어 pca를 진행하는데 pcs, pca를 할 때 몇 차원으로 변환할지 나타내는 것이고 data는 pcs matrix를 통해서 scrs data로 바뀜, pexp는 각각의 component에 의해서 설명되는 것이 몇 %인지 나타내는 것임
- 아래와 같이 기존의 component를 새로운 차원으로써 설명을 함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/903d30ad-cafd-480b-b3c9-b38154ef3520/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T022734Z&X-Amz-Expires=86400&X-Amz-Signature=4111345dcff1ed4e1a73e0e4f2937849c5bcd8f369875d7b33632b149b1058ed&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c8204749-e2a4-4464-bcd6-473ffde2d539/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T022742Z&X-Amz-Expires=86400&X-Amz-Signature=ef565a6a3dfc6c0fb2657f9d348ef2d1639a6b3cb637ba331ea0071ebb3f4bbe&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 실제 코드를 아래와 같이 활용함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b500a2ee-571d-4d02-9eb2-e4d83a2de83f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T022824Z&X-Amz-Expires=86400&X-Amz-Signature=a661a5329fab3c9f9bc45f10f35326588e92cde06d6da6e1cfcbe0f4e7a0f49a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 위와 같이 pcs는 17차원을 그대로 변환한 것이므로 17차원을 나타내고 scrs는 statsnorm의 데이터를 받아서 scrs로 17차원으로 다시 나타내고 pexp, 각각의 새롭게 정의된 17개의 component에 의해서 데이터가 몇 % 설명이 가능한지 나타냄
- 여기서 pexp를 보면 위의 scaling과 같이 3차원 정도에서 49+27+6 약 90%정도의 데이터를 나타냄을 알 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a2849fc6-1474-495b-9853-bd975ac34c65/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T022949Z&X-Amz-Expires=86400&X-Amz-Signature=1ee40284053f8633999404881aa51aaecb8ba24fc1de4134f2fca67683752c14&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 아래와 같이 3차원으로 나타나서 보임, 다시 차원을 줄임
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/98c6aa37-c91b-4787-8661-c47623b718ba/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T023013Z&X-Amz-Expires=86400&X-Amz-Signature=bba2dc47fe31dd1518c7bc75e4a6aae246e6676679a5b8a1a1314c1e2344fbfc&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 2개의 차원은 굉장히 똑같고, 유클리드 방법을 사용하면 어느것을 써도 상관없음
- 클러스터링을 할 때 비지도학습할 때 PCA와 Multidimensional을 통해서 제대로 Clustering이 되었는지 봐야하기 때문에 봐서 확인을 하기 때문에 차원 축소가 중요함
