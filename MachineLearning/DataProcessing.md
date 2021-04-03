## DataProcessing
- 저장되어 있는 Data를 바탕으로 해당 정보를 가공 활용함
- 농구선수들의 스탯과 정보를 활용
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f24e777a-92f6-4673-8ca4-ef67f7a3b901/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T112850Z&X-Amz-Expires=86400&X-Amz-Signature=3bfa1701a35f1ac6b9da85aaaa7eaa15ce7c0ff46ecc5d91f12908af33888756&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3d4682e6-a02a-4752-a703-043521f97a4e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T112909Z&X-Amz-Expires=86400&X-Amz-Signature=0b980c989783f3ad2ad9b18dd4cd29bf62cfb55ef23a559136c5a5a5f53922f9&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- Variable을 추가해 FullName을 만들 것
- UseFirst가 비어있는 경우가 있는데 여기서 UseFirst를 채우고 FirstName과 LastName을 합쳐서 FullName을 만들고 새로운 Variable을 생성해서 저장함
- FirstName을 추출해서 저장, 비어있는 선수들 존재
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/75c36d43-f2be-4e65-b0db-d29c22b9dfef/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T113055Z&X-Amz-Expires=86400&X-Amz-Signature=5f918260834a4b803475e1cb6a3fe622559db23e7d68ad096ea512f3ef462114&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 비어있는 선수들을 채워주기 위해서 indexing을 활용하여 idx에 저장함, 여기서 이름이 있는 선수들은 0, 없는 선수들은 1로 logical array 형태로 저장됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/54f3b36e-1be6-4506-81c6-d5636423cef0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T113137Z&X-Amz-Expires=86400&X-Amz-Signature=eaedaf8f2343861653be7a3075ae06a6a90d888029d6cf419cb742303008d72f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 idx에 비어있는 선수를 찾아둠, 그 다음 firstname(idx)를 통해 비어있는 칸 추출, {}는 cell일 때 사용
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a8988206-24a1-4048-b77c-2695dcbbfefa/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T113217Z&X-Amz-Expires=86400&X-Amz-Signature=3c7942e4542cbc96ffb564ee6210aa7d1f3d37072bd26c185bc28a0cd844bde6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 그 칸을 playerinfo에서 firstname을 채우면 됨. useFirst를 채우기 위한 작업
- 테이블 내에서 변환이 가능하지만 변수를 위와 같이 바깥으로 빼고 여러 함수를 적용시켜서 응용함
- Cell에서 통하지 않는 함수들이 있기 때문에, 비어있으면 FirstName의 똑같은 index number를 넣어서 그 값을 넣어주면 됨
- 이를 통해 비어있는 칸을 채움
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2b513b6d-c16d-4022-a452-075cdf31d38c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T113335Z&X-Amz-Expires=86400&X-Amz-Signature=55b7b7c4e1d2462166ba88e2158a0f27aed00c2864a672aef15c16ba3c33f1fa&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 fullname 사용시 strcat 즉 수평적으로 합치는 것을 활용함
- firstname은 변수를 통해 lastname은 별도로 추출하지 않았으므로 playerinfo 자체를 활용
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/802a985f-824e-4f82-99dd-5d72085d4cf7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T113420Z&X-Amz-Expires=86400&X-Amz-Signature=6a6505ddea7bb751a51de8ca6dd3befd309e597efe119504f06e42fbc113f615&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 하지만 이름은 중간에 띄어주니깐 그 부분을 추가함, Cell이므로 중괄호를 쓰고 중간에 띄어쓰기를 통해 아래와 같이 활용하면됨, Cell이므로 빈공간을 Cell로 만들어야함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f165cf89-8ac4-4bc7-8a89-8633065b04ab/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T113500Z&X-Amz-Expires=86400&X-Amz-Signature=0a98c3b36398efb129636f505f021deb0b7a1f0dd0ff774d2f4d59deb4bdaea0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- fullname을 last column에 추가하면 됨, 해당 데이터가 새롭게 추가됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0f30b695-7408-42a7-873e-e1dfbfaa734c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T113523Z&X-Amz-Expires=86400&X-Amz-Signature=d5e4c73f108f6c2e4e2e5c1c32ba7bc52cfc209f8f395b890b35d35608164171&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- playerinfo에서 height와 weight 데이터를 가져올 것임
- 아래와 같이 모든 데이터를 테이블 형태로 추출함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/51acda94-ad82-4885-911f-370f454b155b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T113600Z&X-Amz-Expires=86400&X-Amz-Signature=f79be11e1a9698d4807b9ed5e071ea70ae4526041273093382ddb1b0a00aa24a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 테이블도 큰 형태의 Cell로 볼 수 있음, Cell에서 그 안에 내용만 가져올 때는 아래와 같이 Cell 표시를 활용하여 array형태로 가져옴
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/46442f44-8f73-48b3-b8a5-45a3e8454121/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T113637Z&X-Amz-Expires=86400&X-Amz-Signature=daf5d152c8dfb337ddc4884d55605f7ebb1db9409a1b3e7f410c3ed5e1f4a044&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 playerinfo에서 필요한것만 사용할것임, 그래서 아래와 같이 처리를 해서 필요한 데이터만 가져와서 playerinfo를 대체할 수 있음, 위에서 사용한 데이터가 덮어씌어져서 새롭게 추출함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3a262dea-d548-4914-8be0-0f0477e0427d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T113719Z&X-Amz-Expires=86400&X-Amz-Signature=6739802bf5047f03e1db7af40201235617ece7695a3fa731b46a190d17e93056&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 array형태로 덮어씌울 수 있는지 확인을 해보면
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/92c82d0c-f4b6-4295-9082-78b28cf5e06c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T113747Z&X-Amz-Expires=86400&X-Amz-Signature=cb84f057ac724275c0da4cd4ee23af7e70f2db6282be166b703e412f05afa1d0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 실행이 안됨을 알 수 있음, 위에서 height_weight 와는 다르게 데이터 type이 다르므로 저장을 할 수 없는것임, 다른 데이터형을 합칠 수 없음, array형태는 반드시 double형만을 가지고 있어야하므로 불가능함

- stats데이터중 1990년 이후의 값만을 가져올 것인데, idx로 저장시 아래와 같이 1990이후인 값에 대해서는 1, 아닌 값은 0으로 logical array로 저장됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4636489f-3c1c-42bf-a4de-c2d69cd87a9d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T113908Z&X-Amz-Expires=86400&X-Amz-Signature=a0e106270b461e1e615ed5de996370723a36349a718ea694b231f2945cd06a35&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 1990이후인 선수들만 필요하므로 그 값을 바꿔두면 아래와 같이 갱신됨을 알 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a1ffe1da-c06d-41ba-b8de-e11258ee109d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T113934Z&X-Amz-Expires=86400&X-Amz-Signature=14f4900009936e482500bc77524bcb8c19a4108bd6fe1e04d23f869f662d9fb6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 실제로는 raw data를 그대로 둔 상태에서 다른 변수 name을 사용함, 위와 같은 방식으로 처리하진 않음
- stats에서 postseason 데이터 24~42 column을 삭제할 것임
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6421d57e-f937-4018-8f6c-c21d45622708/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T114024Z&X-Amz-Expires=86400&X-Amz-Signature=084468798c04df528476ecdaf89fec7f8cf8f48e268995758716d8cadacb83e3&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 이를 통해 stats에서 postseason 데이터는 다 [], 즉 void 처리 다 날려버림
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b31a4b99-8026-449c-9b82-b8b1fe2ccb9c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T114109Z&X-Amz-Expires=86400&X-Amz-Signature=89b3d3aa429bb7e112f29381738eacc44b26c7d53b7cdd5fde39073618f276b3&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- Categorical data는 위의 데이터에서는 position이 될 수 있음, 즉 C,P,F 각각의 포지션
- 여기서 하나만 있는것이 아닌 C-F등 같이 뛸 수 있는 값도 있음
- 이것은 단순한 문자열인데 이것을 의미있는 데이터로 만들 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/aec96769-f4ac-49cd-846c-fd0b17904388/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T114210Z&X-Amz-Expires=86400&X-Amz-Signature=ab0d21913050d8f514164b6b9b6146833d15872b81473d580238b828b1e99e40&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 pos을 categorical하게 바꿀 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/558a22d8-ce03-4419-9b02-5d00a700693b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T114234Z&X-Amz-Expires=86400&X-Amz-Signature=38c1b60fa5cd84bf159c6f27e62f97cb7a273173c05ee8e68a2b16aa38291ebd&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 위와 비교를 해보면 문자열을 의미하는 ('')가 사라짐, 'F-C'->F-C
- 이것은 문자열이 아닌 Categorical이라고 함, 여기서 Categorical로 바꾼다는 것은 남성/여성을 예를 들면 그 데이터 자체가 남성/여성으로 분류를 할 수 있게됨
- 즉 Category, class를 나누는 것임, 의미없는 문자를 Male/Female로 나눴다는 것
- 이렇게 Categorical하게 어떻게 바뀌었는지 보게 된다면 아래와 같이 구분됨을 알 수 있음
- 모든 데이터가 12개의 카테고리로 나뉘어져 있음을 알 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e8e85de4-604d-44a1-ae0f-cee5e8859844/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T114429Z&X-Amz-Expires=86400&X-Amz-Signature=3032f9101ab5883921c1591a285a13930fd7847bb4178124baf48161f680fbb7&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 category가 2개가 의미가 없다고 생각하고 강제로 변환을 시킨다면 아래와 같이 바꿀 수 있음
- 왜 이런식으로 하냐면 아주 정형화된 잘 정돈된 데이터를 활용한다고 할 때 카테고리가 우리가 가지고 있는 데이터가 같지 않을 경우 이를 그 잘 정돈된 데이터에 변환하기 위해서 카테고리를 강제로 변환해야하는 경우도 있음
- 여기서 아래와 같이 positions의 7개의 category로 변환하게 되는 경우 이에 해당되지 않는 경우도 있는데 이는 그냥 버리는 것으로 처리를 함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/00fac1ef-ad5d-41eb-a34b-f90f6eeed6dd/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T114613Z&X-Amz-Expires=86400&X-Amz-Signature=c141c3b99e584f5ee777575199fe4964eb5a7d98778dcefe23068b2ce8cb9795&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 하지만 여기서 강제로 그 category를 바꾸면 아래와 같이 이에 해당되지 않는 경우는 undefined가 됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b7d9c060-0783-40b5-a4b0-bbf319a73249/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T114650Z&X-Amz-Expires=86400&X-Amz-Signature=ff409042ccd53f5c5c03ae9f83a9d68a7d446810a252f20fdda1d0ee47627e79&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 아래와 같이 다시 category를 확인하면 7개의 category만이 있는것을 알 수 있음(undefined 제외)
- 여기서 undefined는 삭제하도록 할 것임
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/cb8ff309-bfc6-4e9a-8e77-e93611f13af9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T114742Z&X-Amz-Expires=86400&X-Amz-Signature=6a96b6e9ef05aa53ff3bbb9c864dd3f1fc5f3bc5f78a806f8160fb054b493d9d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">


- 그전에 stats 데이터를 정리를 할 것임, 원하는 데이터만을 갖게끔 더 줄일 것임
- 데이터가 확 줄어듬
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/02b6c593-555b-4dc4-88f4-326e875bd4b8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T114814Z&X-Amz-Expires=86400&X-Amz-Signature=0ece87acf98352d19796a5509db0bfb0ac22e574012826642be0a2539f734c20&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 대부분의 데이터들이 Time을 기반으로 되어 있는데 이것을 사람당으로 아래와 같이 Time기반을 바꿀 수 있음
- Time 기반이므로 Id가 중복되서 나타남
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fd008c9a-5633-4c15-9da6-34329b96f8dc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T114909Z&X-Amz-Expires=86400&X-Amz-Signature=3ec664f54f6ed4899ba9e47336e1c65399eefce6e0e0a9eb0271e17b0d4ca7b7&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 이를 grouping을 할 수 있음, 여기서 아래와 같이 처리한다면 playerID를 기준으로 grouping하여서 활용할 수 있음, 아래는 평균값을 의미함
- stats에서 동일한 playerID를 합쳐서 mean값을 아래와 같이 구함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5b672ebb-bac4-4bf2-883b-9f8d06da4141/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T115001Z&X-Amz-Expires=86400&X-Amz-Signature=5358ada953ea554d502deefeba27eda18606b524ab8256ed388c6c7cdc1227fa&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 아래와 같이 sum을 구함, 여기서 @sum을 활용해도 됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9a5c5e66-8036-4ad1-850e-7aef41b17d70/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T115025Z&X-Amz-Expires=86400&X-Amz-Signature=831020033c3823a409a6cfb42b61f5d7c0285b92cccf2b2eb459a966c8ff57ac&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 100game 미만을 제거할 것임, idx 즉 sum_GP가 100미만인 값을 logical array로 저장해둔다음, 이 부분을 void 처리를 하여 없애면 아래와 같이 나오게 됨
- 위의 데이터와 비교한다면 100 미만의 값이 싹 사라짐, 노이즈로 간주해서 없앰
- 최소한의 기준을 잡아야하기 때문에 없앰, groupCount 역시 없앨 것임
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/dea19514-837f-4c38-9d08-3f4a1a9d19f0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T115135Z&X-Amz-Expires=86400&X-Amz-Signature=8be23ba6e23a640183a53b3e158b2bb002552a8543a8e33cc5040bd784dc64bc&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 sum_이 꼭 필요한 값은 아님, 이 부분을 지울 것임
- 여기서 새로운 부분은 stats를 쓰게 되면 그 밑의 다양한 변수들이 나오게 되는데 이 중에서 해당 특성과 VariablesName을 입력하면 아래와 같이 해당 Name이 쭉 나오게 됨, VariableName을 뽑을 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/398741e3-4566-4685-aadd-ca7a3e8f771e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T115232Z&X-Amz-Expires=86400&X-Amz-Signature=ca0d7e645d2dc7893a00984586c2c68727bcb034072ca8fd47d8549047aebcda&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 이렇게 뽑은 name에서 sum을 아래와 같이 교체할 것임
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/698b7ff4-be97-47c2-8160-47ac34b967a8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T115255Z&X-Amz-Expires=86400&X-Amz-Signature=72bfc8bf82467015ff1a50399817e88038b52aa6ad846104066b80148ba98d0d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- playerinfo는 bioID와 totalstats등 연도별로 구분을 함, 여기서 bioID와 playerID가 다른 변수지만 내용이 같음, 이 두 데이터를 합치는데 유의미한 방법을 활용할 수 있음
- innerjoin -> 두 개의 데이터 그룹에서 교집합을 찾아서 교집합에 쭉 이어붙여 주는 것임, 교집합에 포함되지 않은 것은 날아감
- outerjoin -> 합집합의 의미
- 아래와 같이 bioID와 playerID가 같은 교집합 부분에서 data를 저장함
- 아래와 같이 data를 이와 관련되게 쭉 합쳐놓음, playerinfo는 5061 totalstats 1117의 데이터를 가지고 있었음, 이를 합치게 되면 data는 1117이 됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4bf704a6-1010-439a-9630-2a00ab116d29/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T115511Z&X-Amz-Expires=86400&X-Amz-Signature=f88efa1a13e28057b0ce65a54873d5939de6251bc59f6e306dc513fda69bbfe7&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 이제 그 둘을 스무스하게 합쳐서 모든 데이터가 들어가 있으므로 missing data를 삭제할 것임(undefined와 같은 데이터)
- 여기서 각 열당 missing data의 합을 구할 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f783edee-2aff-4ac7-8227-f1e9196b2e79/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T115555Z&X-Amz-Expires=86400&X-Amz-Signature=8c0043f967d7ee0d9dce229280c097c1a46871826a4fc622aadbc98eed2bfbd2&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 missingdata에서 rmmissing 즉, missingdata를 remove하는 함수를 활용하여 할 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/773f8855-9c1f-45fe-a4f5-a7b8cdd31e4c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T115625Z&X-Amz-Expires=86400&X-Amz-Signature=c3e7fb91115aa27621ab36e2f5439a31401004f38497f11e9df0914f66d42b22&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 하지만 여기서 undefined 먼저 찾은 뒤 이를 data에서 삭제하는 로직을 아래와 같이 활용할 수 있음
- 아래의 undefined가 사라지게 할 것임
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ccd27d3a-29a4-4cb7-b9e5-f99a59924bfc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T115700Z&X-Amz-Expires=86400&X-Amz-Signature=543c08daa6be562c7f686a2e6c2e565507222ca4a7edca7794314e4db96f2076&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 아래의 로직을 활용하여 undefined가 사라짐을 알 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c5740def-a974-434b-a65b-df6334be40fd/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T115723Z&X-Amz-Expires=86400&X-Amz-Signature=1d5ce1176f229771d325a1acf9ee89bc77f44e0cf21bade210e044a9041fe7ae&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- rmmissing을 활용해도 됨

- Explore data 즉, visualization을 하여 데이터를 볼 수 있음
- 아래와 같이 boxplot을 통해서 data.pos를 기준으로 height에 대해서 아래와 같은 형태로 데이터를 전체적으로 볼 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/84835ee2-3aeb-40d6-a360-14fc55c77227/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T115816Z&X-Amz-Expires=86400&X-Amz-Signature=734b9ca9a36e1f60136a13ec7ea939fa2accb8b789b13f03221d36c6714872af&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 scatter에서 rebounds를 나타내지만 points도 같이 나타냄
- 하지만 동시에 나오므로 큰 차이가 없음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/065f58a1-ef9b-467b-bfb4-d22a6be2d612/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T115848Z&X-Amz-Expires=86400&X-Amz-Signature=0fbb88476187f3f51911b095de9c84822693fdb6debb0dfb2495928aa2a8eaea&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 추가적으로 data position으로 나누어서 rebounds오 points를 구분할 수 있음, categorical을 활용하여 알아서 나누어줌, x는 rebounds, y는 points 알아서 gscatter를 하여 position 별로 구분할 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e0bb224a-0c6d-417c-8998-ee7aebe6a855/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T115945Z&X-Amz-Expires=86400&X-Amz-Signature=cc74ef4b1aca7f1a4eeb3e1c9f62ef55263ccddeb4d09a330999d20f08aacd3e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 좀 더 의미있게 나눌 필요가 있음, Guard는 사실상 Rebounds의 개념이 크게 작용하지 않으므로
- Normalizing, 정규화 즉, 의미있는 데이터로 나눈다는 것인데, 어떠한 의미이냐면 쉬운 국어시험 90점과 어려운 수학시험 90점은 동일선상에서 보기 힘듬, 이를 의미있게 구분하기 위해서 정규화를 시킴
- 여기서 데이터를 총 리바운드, 총 포인트는 큰 의미가 없음, 즉 GamePlayed에 따라서 나누면 그만큼의 효율을 체크함
- 이 scatter를 보면 player한 게임수와 각 data를 나눈것이 큰 차이가 없음, 즉 큰 의미가 있다고 볼 수 없음, 게임 played 수는 큰 의미가 없음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d0070666-d9de-41e2-aa2f-b00e757643e3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T120152Z&X-Amz-Expires=86400&X-Amz-Signature=7f7df9552a0c1c264a04057904f024459503d751b547ca062d187b8d1d0e74d2&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 그렇다면 뛴 시간만큼으로 변환해서 체크를 해볼 수 있음, 분당 득점, 분당 리바운드로 계산
- 조금 더 Guard, Center등의 분기점이 의미있게 나뉘어져 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6c94730b-53a6-4eb1-bbd7-bbc1b4409f8c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T120232Z&X-Amz-Expires=86400&X-Amz-Signature=f413d9912616ae70edcf04f1bbbcff0cb12f6844400389971900ee9910eccf20&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- Normalizing, 정규화, 일반적인 방법은 평균과 표준편차가 나와 있고 평균은 0, 표준편차는 1로 즉 쉬운 국어 90 어려운 수학 90에서 같은 동일선상에서 비교하기 위해 Normalizing을 함
- statsnorm을 통해서 데이터를 동일선상에서 볼 수 있게끔 표준 정규화를 시킴, 아래와 같이
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c2e59a61-3fc6-4915-8908-d1a4fa80e6a9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T120333Z&X-Amz-Expires=86400&X-Amz-Signature=d2d25bfa5aee849f778c1ba03b6e2c2aaaf197f174a5fd5ab07d06f82f20da7c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
