## Unsupervised Learning

## Roadmap
- [k-Means Clustering](#k-Means-Clustering)
- [Gaussian Mixture Model](#Gaussian-Mixture-Model)
- [Interpreting the Groups](#Interpreting-the-Groups)
- [Hierarchical Clustering](#Hierarchical-Clustering)

## k-Means Clustering
- k-Means와 Gaussian은 Cluster하고자 하는 그룹의 개수가 정해졌을 때 사용하는 방법
- 알고리즘을 통해서 몇 개의 cluster가 최적인지 알 수 있고 이를 바탕으로 비지도 학습을 할 수 있음
- clustering한 후 group을 visualization을 하여 제대로 되었는지 봄, 여기서 차원축소를 활용함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9de2016a-13a9-40da-b90a-d35c2a704cd9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T025135Z&X-Amz-Expires=86400&X-Amz-Signature=a8c6f9e73679ea6e1a31ef45c928cb1e7abc568709607872e3b300adc4b59a96&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- idx, g를 통해서 data가 어떤 group인지 clustering의 결과가 나오게끔 열벡터로 나타남

- k-Means를 할 때 우선 몇 개로 나눌것인지 나오는데 여기서 그렇게 하기 위해 임의로 center를 아래와 같이 지정함, 3개로 나눌것이므로 3개의 center
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/629f3165-3e3b-447f-91f1-3ca1648f2b1f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T025236Z&X-Amz-Expires=86400&X-Amz-Signature=27a00537535d560fa166d3c37e0f464899bfac0495fd80a33b7fee67c2394728&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 그런 다음 center를 중심으로 그룹을 3개로 나눔
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b41ac034-c4a0-4e82-8678-b63ffe97a883/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T025256Z&X-Amz-Expires=86400&X-Amz-Signature=edda79f53bce35661e1d50c0381cd4a2705eb8918edf7e57097a39ac29e11149&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 group 사이의 거리가 같은 경우 위의 how to function을 바탕으로 본다면 distance 즉 그 사이의 거리를 option으로 설정하여 볼 수 있지만 기본값은 유클리드 기법이 기준임
- 첫번째 점은 우선 임의로 center를 아래와 같이 잡음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2b3db0eb-5a08-4770-a143-049e52bdc8ec/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T025346Z&X-Amz-Expires=86400&X-Amz-Signature=a21067616b078adfc3172232b73897e0d6d76bb86e63c420af5ca709b98aded7&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 그리고 그룹이 형성이 된 후 임의로 잡은 center에서 다시 새로운 center로 업데이트를 함, 그리고 그 업데이트한 center를 바탕으로 새로운 그룹으로 잡음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c300299b-a413-4e07-856e-b86a1e88d52f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T025422Z&X-Amz-Expires=86400&X-Amz-Signature=a2f47fd2604bf83cce5245dfa6265b81edfd118ea0fd596de8818859bd7a7941&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 그리고 다시 center를 바탕으로 그룹을 업데이트함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ff684c62-73e3-4566-9cee-21b1e77fa8c6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T025438Z&X-Amz-Expires=86400&X-Amz-Signature=9b8aa0ec6c95103a7154d5cf4b0e73dc679d0a499c0a613b6ee5544a9dae1022&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 이런 방식으로 계속해서 업데이트를 하면서 갱신을 함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1ba04dcb-9faf-4f2b-adac-992737d028e3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T025454Z&X-Amz-Expires=86400&X-Amz-Signature=2652b48cd6926d424c6d2b87897679f779409b8d5319784519ee93c289df05ee&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 이러한 점으로 인해서 k-Means의 단점은 처음 잡힌 점이 터무니 없이 잡히게 된다면 때로는 발산을 하거나 터무니 없는 그룹으로 잡힐 수 있음
- 이러한 점을 해결하기 위해서 임의의 center를 여러번 반복해서 잡으면서 group을 잡으며 그 중 가장 즉 하나의 center에 대한 group의 길이의 평균값이 작은 것을 뽑으면 최적이 됨
- 아래와 같이 거리를 체킹을 하고 더 나은 것을 바탕으로 grouping을 함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/20557c21-22e5-45b9-b430-a09e5b58ebc4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T025616Z&X-Amz-Expires=86400&X-Amz-Signature=cb0ad150f3dde69734960685c949012c258e87f7d570a4ad4f693ce3ad0d394c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fbbd184a-80ff-4816-9346-c8403785d997/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T025623Z&X-Amz-Expires=86400&X-Amz-Signature=6a0005fcaab742d1d4d385516cfa2d96b174a7bd9ca4090ebd89fbf61c37563f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 그리고 아래와 같이 유클리드를 default로 그룹을 체킹을 함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/63807749-31a0-4bd5-8637-33876f0798d5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T025644Z&X-Amz-Expires=86400&X-Amz-Signature=0833782f681c92229a9642515c8d818ec1c5120e82de6a5a10f82f91e8abc281&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 그 다음 해당 k-Means를 보기 위해서는 Dimensionality Reduction을 진행해야함, Visualization을 위해, 아래는 PCA 방식을 활용
- 위의 구한 식을 바탕으로 그대로 쓸 것이지만 marker, k-Means로 계산한 값을 표시를 할 것임
- 아래와 같이 group을 scatter3 함수로 표현
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2460b679-77c5-415f-ba21-3525eaaae9c2/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T025808Z&X-Amz-Expires=86400&X-Amz-Signature=6dd3f665b5da05a6472ff25c7749377067799a8a3d0ff0ef5806314be0e1f3ae&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 만일 center를 잘못 잡으면 터무니 없이 나타나기도 함, 이를 아래와 같이 사용해서 방지할 수 있음 
- 5번 반복을 한 뒤 평균 center부터 observation이 제일 짧은 결과를 골라 아래와 같이 보여줄 수 있음
- k-Means에서 replicate 옵션은 거의 항상 씀
- c를 통해서 각 그룹의 center의 정도를 알 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7b96d3b7-637f-45b6-88d6-34d78b485260/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T025926Z&X-Amz-Expires=86400&X-Amz-Signature=2aa20234d87979b39b0345b5066bcf919a6721f0f6ca0f8b399482b0fb697dd3&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

## Gaussian Mixture Model(GMM)
- Parameter의 영향을 많이 받음
- 다양한 옵션들을 통해서 결과가 희한하게 나올 수 있음
- k-Means는 어느정도 정형화 된 결과가 나오지만, Gaussian은 잘못 설정시 그 값이 상당히 이상하게 나올 수 있음
- GMM은 확률로 계산을 함(정규분포)
- 데이터가 아래와 같이 있을 경우 바깥으로 올라오는 정규분포를 그려 아래와 같이 나타냄 3차원 상에서 바깥부터 쭉 올라오는 형태로 확률로 계산이 됨
- 표준편차가 1 평균이 0 or 1인 데이터를 씌움, 정규분포 distribution을 만들어서 거기에 맞춰 grouping을 함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0edeafcc-95d5-4e71-a923-8866dd7b1ab3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T030118Z&X-Amz-Expires=86400&X-Amz-Signature=478d242e1a0ac2fe9621f9388ecfff78f4658e2fb9d49ce17a8615aec11814f0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2b005a3e-4c04-43b3-9119-0ed53af7c01d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T030127Z&X-Amz-Expires=86400&X-Amz-Signature=29b5b383073d002256db845cdd6a8a6f232303f2a607f31caeb172718c9c560b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- k-Means는 거리기반, GMM은 확률기반임
- GMM은 Grouping의 확률이 모두 나타나는데 그 중 가장 높은 확률 부분의 group으로 들어가서 나옴, 처음엔 랜덤하기 때문에 발산하게 되는 경우도 있지만 Replicate를 통해서 반복을 하여 최적의 상태를 찾으면 됨
- 아래와 같이 하나의 데이터가 각 group에 속할 확률을 모두 파악할 수 있음, 세밀하게 조절하기 좋음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5f7dacd9-d59a-4799-8020-6eeb50023a25/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T030327Z&X-Amz-Expires=86400&X-Amz-Signature=96a53893bb3e5478d6fbe5f0abc6dacda8733d0971e9890048177892f6237115&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 처음에는 아래와 같이 엉뚱한 곳부터 시작하다가 점차 업데이트를 함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5d386e70-4c47-4057-b6f9-b6b692991b03/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T030356Z&X-Amz-Expires=86400&X-Amz-Signature=3579d57685fa696a713a21ab5126be7412d37e5b54cf9faa7e6c56f026e0def0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5231dbbf-3e76-4db5-9ff8-6df10ed5a49f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T030403Z&X-Amz-Expires=86400&X-Amz-Signature=f9ff6db1d1918ce50cf92692f8e1178f54545b23486499abdf7086560448e041&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 아래와 같이 발산할 수도 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c85665b2-0703-40d0-a378-f51638c19398/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T030418Z&X-Amz-Expires=86400&X-Amz-Signature=199758393626a592730c6edeab50b7329338baf9b4cbc2d6602a0281376782c7&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 아래와 같이 Gaussian Model Distribution에 맞게 model을 생성한 후
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e11ab8bc-f096-4f03-8d55-56e528356ec7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T030449Z&X-Amz-Expires=86400&X-Amz-Signature=197d1c5c48cbb75b8e1a674b6cdbfd866e1583cf6ff4365c6cef3c8350c78980&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 그 다음 해당 변수를 바탕으로 clustering에 아래와 같이 데이터를 활용함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/32afeeb0-59d5-4c34-af35-ac51486c5f3d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T030511Z&X-Amz-Expires=86400&X-Amz-Signature=71bee29dc14210e736b587117f5d5760e1e56ae009e9861fc53adc810c3f828f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 아래와 같이 코드를 통해서 distribution을 구함, 하지만 아래와 같은 경우 모든 부분에서 분포가 적합하지 않다고 나옴
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d139eaeb-b08b-4ee2-b340-6040ad2b062e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T030544Z&X-Amz-Expires=86400&X-Amz-Signature=1cd73961db10080be796879f043f45f36546dd9655abb62e7c6ced6cbf5474b3&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 그러므로 처리할 때 튜닝옵션을 사용해야함, 정상적으로 처리가 됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/08265f7f-2e94-4543-b8fe-54a376d3133b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T030610Z&X-Amz-Expires=86400&X-Amz-Signature=f4baa3de9329e0069949cb847b87fc3a8ce4ff209acfef8a44d51cbdb00a2dd2&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a2ffa550-fd38-4c15-bfff-eb9f9a0f0d4b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T030618Z&X-Amz-Expires=86400&X-Amz-Signature=66c4f8f32ee286261ebb3f7fa299722aba7e5fdd1afb90f7932e39139e94699f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 이러한 튜닝옵션을 설정해도 해당이 안될 떄도 있고 그리고 정상적으로 처리될 때도 있음, 처음 시작은 Random하게 시작하니깐

- 그리고 cluster 함수를 통해 그룹을 나눔
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0d288dce-d10e-48aa-820a-5689f0e27582/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T030704Z&X-Amz-Expires=86400&X-Amz-Signature=8db0186851f432d3dc6f57e8b0abea17b848a4e6f7c5becacf0e36de060bb2b2&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 그리고 Visualization을 위해 PCA를 활용, PCA를 자주 쓰는 이유는 쓰기 편하고 다양한 정보를 바깥쪽으로 뺄 수 있으므로 사용함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5d1cfaec-e838-4007-96f5-721103553ade/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T030741Z&X-Amz-Expires=86400&X-Amz-Signature=4ebac83e4a6b46dc021eeb4892060ba3fd0514bfdfdc20ce7001f1291bde6d19&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 GMM에서 위와 같이 직관적으로 쓸 수 있지만 또 다른 방식으로 확률을 받는 방식으로 쓰는 것이 좋음, 확률을 제공해주기 때문에
- 아래와 같이 probability는 무조건 받는 것이 좋음 결과를 명확하게 보여주고 cluster의 확률을 확실히 정해줌
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3c29ed6f-2bad-4cc6-9d05-a057badb8933/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T030835Z&X-Amz-Expires=86400&X-Amz-Signature=196b7376190c4999ea863b22281a781de8d40ba1fe817364ed083414acff5f9c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 p로 확률을 받았고 아래와 같이 시각화를 해줄 수 있음
- 아래는 cluster1에 포함될 확률이고 즉 노란색이 그렇고 색깔이 점점 초록색과 파란색으로 될 수록 cluster2에 포함됨, 왜냐하면 어차피 cluster1에 포함될 확률이 p이면 cluster2에 포함될 확률은 1-p임
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f88af8a0-a969-40c8-9dbc-5e4b0cb5b5c8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210407%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210407T030951Z&X-Amz-Expires=86400&X-Amz-Signature=26989033309822d017691476d232f2214937249ee1c3a4055c6f6a07706045fb&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

## Interpreting the Groups
- Clustering 결과를 observation 별로 보고 clustering 별로 보고 어떻게 최적의 조건을 찾을지 파악할 수 있음
- group과 centroid를 설정한 kmeans와 Gaussian을 통한 group과 probability를 알 수 있음
- Gaussian은 Gaussian distribution을 씌운 다음에 Clustering을 진행함
- 우선 Kmeans의 observation당 variable로 나눠서 어떤 그룹에 속하는지 아래와 같이 시각화를 할 수 있음
- 각 observation이 어느 group에 포함되었는지 알 수 있음(17개의 variable, 선은 1112개의 좌표값을 나타냄)
- 각 variable당 좌표값이 어떤지 알 수 있음, 데이터가 어느정도 정형화되어 있다면 두 group이 나뉘어짐
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/dc5d26cf-e7bd-4a0e-824c-3042631e4635/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T080344Z&X-Amz-Expires=86400&X-Amz-Signature=01b05f98510c1d85e4476f285d028ca901af5a27fa4f95dc4650b7b59d5e346e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- labels의 각각의 xtick의 label을 확인할 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/39bef6d5-a795-4177-ae8d-0980e8aedb16/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T080407Z&X-Amz-Expires=86400&X-Amz-Signature=6fd553258e4bd297bbe34a0f6330e3a19218a3184a09bbfd629cb28a93ef4b91&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1ad1058a-a16e-4e9f-aba1-0c880387b51d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T080415Z&X-Amz-Expires=86400&X-Amz-Signature=4a055a37e2c4b46a80b6a24cd266668df9b70b79cf90e2f0a5bc5885b0680c21&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 하지만 위와 같이 보면 보기 매우 힘듬, 그래서 옵션을 활용하여 좀 더 보기 편하게 설정함
- Quantile 0.25는 Medium값 기준으로 위로 0.25, 아래로 0.25를 의미함, 중간값을 기준으로 2번째 사진과 같이 잡음
- 진한 선을 기준으로 25%안에 들어오는 것의 경계면을 나타내는 것임, 위아래 경계를 두고 나타냄
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/87247624-ba22-4e01-ab25-96eb93ead968/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T080516Z&X-Amz-Expires=86400&X-Amz-Signature=304397c8ca8628a254d5589cfd5a92bef001b6981c35367d897969a4cd379218&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8a8e141f-859b-4e70-aff4-e39381882215/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T080524Z&X-Amz-Expires=86400&X-Amz-Signature=a704c135ee676611cd8f0873a4f7d8b505cd983a28c2e303d89654c816ae134e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- centroid 역시 알 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ff292004-3f8c-4428-a5b5-5ef4b5e33a4b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T080540Z&X-Amz-Expires=86400&X-Amz-Signature=51eda86a42cf52b3e8fc1d51e9fd22f749f081ea67d1a0063583c8007fad68a3&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 때로는 비지도학습이어도 실제 그룹이 어디에 포함되는지 알 수 있음
- 그룹 결과를 이미 알고 있을 때, clustering의 퀄리티를 알 수 있음
- 이때 crosstab을 활용함, 각각의 group에 속할 확률을 알 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/51ddc1df-f8df-4964-b57e-3dac467b2e30/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T080649Z&X-Amz-Expires=86400&X-Amz-Signature=5e8275a9280488dbc5643056a5d663c73aeb743c8e80cac2f9b7c557ef5f8a8f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 아래와 같이 활용해서 쓸 수 있음
- 각각 앞의 숫자는 1번 그룹에 속한 개수, 뒤의 숫자는 2번 그룹에 속한 개수를 나타내는 것임
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b42b2db8-8bbb-4aab-b0c8-d168a9c90985/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T080723Z&X-Amz-Expires=86400&X-Amz-Signature=42fcbf56b7248402f038767b9f66fcc24c489bc13db6cea70c19976274b4dec5&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 이를 바 그래프로 사용하는것을 많이 씀, 아래와 같이 스택형식으로 쓸 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8d945e33-0eee-4560-b5cb-fdecff0cdee4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T080742Z&X-Amz-Expires=86400&X-Amz-Signature=25eb9f6347c048efa187e521d05435f70d784ea38003b047fc6d912ca4ecd8eb&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/64b8c6ef-9908-4a72-a8ac-77282b4e7c9e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T080751Z&X-Amz-Expires=86400&X-Amz-Signature=7509c5205f05af46389673dd17c61e15595f8551176e5930e7a3b7ca97ede4a2&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 이를 반대로 쓸 수도 있음, 여기서는 cell형으로 넣어서 씀
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0b8e4610-a306-4102-9065-83e5f8882a83/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T080815Z&X-Amz-Expires=86400&X-Amz-Signature=4df573d01298fbadb58e63270b67e093a22a328ae0b11d0fb0b8008305f2a935&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- clustering quality 역시 확인할 수 있음, evalclusters를 활용해서 quality를 판단할 수 있음
- 헷갈리면 다 작은따옴표로 통일해서 처리해도 상관없음
- silhouette 함수를 통해서 quality를 확인할 수 있음
- silhouette 함수는 아래와 같이 가운데 선을 기준으로 2번과 1번 그룹으로 나뉘어짐
- 파란색 면적이 오른쪽으로 많을수록 clustering의 quality가 좋은 것임 
- 아래의 사진을 비교했을 때 2개 그룹, 3개 그룹 비교시 두 번째 그룹의 퀄리티가 더 좋은 것임
- 그리고 올라가는 저 값들은 observation까지 얼마나 가까운지를 의미함, 오른쪽으로 값이 가까울수록 그만큼 퀄리티가 높다는 것을 의미함, 하지만 마이너스로 가까우면 그만큼 퀄리티가 안 좋다는 것을 의미함, 마이너스로 쭉 뻗으면 매우 안좋다는 것임
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/90ac8860-98cd-4757-94a1-f8aa56109c71/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T081109Z&X-Amz-Expires=86400&X-Amz-Signature=00240396090cde0fc2050db129b1ad04fbf263bd2238765160426d866d1da6b1&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 아래와 같이 3개의 그룹으로 나올수도 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9e2ad779-07a3-4e6f-8b6d-ca8b97d45e70/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T081126Z&X-Amz-Expires=86400&X-Amz-Signature=27e10f277ab0e7d98cec17e9f334824d638a87927124d6bcc5fbc65cc45d2549&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 아래와 같이 그룹을 계속 나눌 수 있음 
- 여기서 각각을 비교하면서 그 퀄리티를 체크하고 어떻게 나눌지 판단할 수 있음
- 근데 눈으로 파악했을 때 애매한 경향이 있음, 뭐가 더 나은지 판단하는 상황에서
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e202b271-ea7d-4f06-aee9-ef12d0bc2b81/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T081205Z&X-Amz-Expires=86400&X-Amz-Signature=3d335cb63bd98b61bb6ab5740225dd1a5a62b872402d921cf3241a3d50c1a7b3&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/45ba5745-8e09-4607-8c14-422faf9f3221/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T081214Z&X-Amz-Expires=86400&X-Amz-Signature=c20dbfd90be5724333ba7df7152e3623c4d66b93adf94b477ac8c6c32edd448f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 자동으로 어떤게 나은지 체크 할 수 있음
- KList는 cluster의 개수를 의미함
- 검열한 cluster의 개수가 2,3,4,5 그리고 optimal한 것은 2개임을 의미함, 즉 아래와 같은 방식을 사용했을 때 최적의 방식이 2개의 group으로 나눴을 때임을 나타내줌
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f347aa0e-a9ef-4ffe-b9e4-14d2295e546f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T081318Z&X-Amz-Expires=86400&X-Amz-Signature=98f4bfb980a650f6907d20c23f060a7fb48239b104e9612f6671520702dd5483&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 평가하는 방법은 다양함
- Davis 방식은 최적값이 변하는 경우도 있음
- 아래의 방식을 토대로 2,5의 group이 나음을 알 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3b44795f-f8bb-4413-bd1b-77a7e44f835d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T081353Z&X-Amz-Expires=86400&X-Amz-Signature=3fc6350ba2ccbc2f0e74bc20a8b99421b720700b2a9cb001064280d59043662e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

## Hierarchical Clustering
- 데이터의 variable의 특성을 어느정도 완벽하게 알고 있을 경우 유용함
- 평이한 옵션을 활용하면 그에 맞게 평이하게 나옴, 하지만 옵션에 따라 세밀하게 구분을 할 수 있음
- linkage, dendrogram을 하고 cluster를 함, Gaussian에서의 cluster와 유사함, linkage로 유사성을 파악하고 dendrogram으로 유저가 보고 이를 통해 cluster를 함
- linkage에서는 데이터가 아무리 많아도 5개로 나타냄, 유사성이 아주 가까운 경우는 유사성으로 묶어서 나타냄, 아주 많은 경우는 그러지 않을 것임
- 여기서 1은 observation 1이 아님, 여기에 포함된 군집된, 너무 가까워서 하나로 군집되어 있는것을 의미함
- 아래의 dendrgram에서 1,2,3,4,5는 군집된 observation을 의미함, 4와 5는 적당한 유사성이 있지만 어느정도 떨어져 있음, (4,5), (1,2)의 차이는 세로축의 길이가 유사성을 나타냄, (1,2)가 묶이면 떨어져서 나중에 3으로 묶임
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/de9232d3-38b9-4e71-a080-b048e27c9103/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T081735Z&X-Amz-Expires=86400&X-Amz-Signature=aa26e179a5def4e3d3470d8e600abddc934f659b71f1f2fa66c30a13b0d35e29&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 이를 쓰기 위해서 데이터를 구분해서 쓸 것임 
- 그전에 statsnorm에서 정규화를 한 것은 zscore를 통해서 정규화 한 것임, 여기서 zscore는 표준정규분포를 만드는 것이었음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a92a6cc0-5fc7-40ef-a06c-f36df054c9c5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T081813Z&X-Amz-Expires=86400&X-Amz-Signature=9179a329b60a0ba92084abe42c061be21d20c9f6fbd8a4ce56f367d3c6e8ef74&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e018b9de-723a-4c75-b2b4-e2e57c7abce6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T081821Z&X-Amz-Expires=86400&X-Amz-Signature=549f7148d0a6724940186cbbbb04187e1cbd18bf0b013a8788a45d3b088f498a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 linkage를 하고 간단하게 보면 아래와 같이 나오게 됨, 상당히 이상하게 나옴
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9bfe6e9b-1f7c-4984-89dc-c7500a8629e8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T081848Z&X-Amz-Expires=86400&X-Amz-Signature=ef1bd130cd0e97d7310cc30653fdf752f0f335d659aa475776d77a0c439c1a6a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 이를 ward를 통해 서로간의 유사성을 다시 파악함, 어떻게 쪼갤 것인지 파악 가능함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1df4192c-51d1-4a0b-afd6-e779d7720a50/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T081910Z&X-Amz-Expires=86400&X-Amz-Signature=b0b411f18485af9fe1589a8fe749a5e5bd337ab214fbe4c5162cbc8c95607a7f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 거리측정법을 cosine으로 바꾸고 아래와 같이 유사성 체크시 2개 혹은 3개로 쪼개는게 나음을 알 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5ec31923-ef06-4879-a5c9-86bc6d6ec12a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T081937Z&X-Amz-Expires=86400&X-Amz-Signature=c12a94c854daaff1aa2ebbb2c036fba26e340187ff82d0ed2f72174426bd6171&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 거리측정법을 최적으로 할 것이 무엇일지 고려를 할 때 그 변수간의 무엇이 나은지 doc을 통해 활용해서 정하면 됨
- 군집간 거리를 계산하는 알고리즘은 다양함
- 그 이후 아래와 같이 clustering을 확인을 할 수 있음
- medium을 기준으로 아래와 같이 그 정도를 확인할 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f1fe7885-dfe5-41d6-9683-3adc163c2b95/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T082053Z&X-Amz-Expires=86400&X-Amz-Signature=406c92afa26c9fab809581c6014110984004e077543150205e287248c9e3dd11&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 하지만 여기서 위와 같이 처리해서 직접 보는 것 말고 evalclusters를 통해서 linkage였을 때 최적값을 찾을 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ebf8835f-0e85-4d65-8d92-8e486bf6be81/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T082123Z&X-Amz-Expires=86400&X-Amz-Signature=b69d384ee256b0c1b412ebab57b1113d893cc65fb2e3e37f759504ae8cf29ea7&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
