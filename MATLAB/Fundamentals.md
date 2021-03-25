## Fundamental

## Roadmap
- [Variables & Expressions](#Variables-&-Expressions)
- [Array](#Array)
- [Indexing](#Indexing)
- [Statistical operation](#Statistical-operation)
- [Plot](#Plot)
- [Logical operator & Functions](#Logical-operator-&-Functions)
- [Cell Array](#Cell-Array)



## Variables & Expressions
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/101b023c-6a4c-4163-b3ca-b8736176de04/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T004312Z&X-Amz-Expires=86400&X-Amz-Signature=c641e9d45694442eafc1a93a62195cd02cffc0747f24bbae7d5120428ec16738&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 명령창에서 작업 처리를 함
- 작업공간 : 변수들을 저장하는 공간(RAM 상에 저장됨), 휘발성으로 날아감 
- 따로 저장을 하기 위해서는 save 명령어 사용(저장되어 있지 않고 변수를 불러오면 에러가 뜸)
- MATLAB 경로에 추가를 하게 된다면 자동으로 load를 할 수 있음
- 기본적인 명령어
	- clc : 써 있는 명령창 정리가 됨
	- clear : 작업공간에 있는 내용이 정리가 됨
	- ';' : 세미콜론을 붙이게 되면 반복적으로 입력한 값을 보여주지 않음
- 변수 사용시 대소문자 구분을 할 수 있고 무조건 알파벳으로 시작해야함, '_' 도 사용 가능
- 변수값 입력시 갱신 가능, pi, sin 등 다양한 수학적 표현이 자동으로 저장되어 있음
- doc을 입력하면 공식문서가 뜨는데 이를 통해 모르는 부분에 대해서 직접 찾아볼 수 있음
- 라이브 스크립트 실행시 작업공간에도 자동으로 실행됨
```MATLAB
% Enter value to vaiable
a=3*5
a=3*5; % semiconlon(;) to suppress any output

% Update variable
a=a+1;

% Variables start with alphabet and include alphabet, numbers, _
% Variables:Case sensitive
s=3;
S=4;
a=pi;
a=sin(pi/2);
a=sqrt(4);

% save Filename VariableName, load Filename
save('MatlabVariables.mat') % save MatlabVariables.mat, command 방식임(함수 방식 x)
save('MatlabVariables.mat','a') % 특수한 변수만 저장
save('MatlabVariables.mat')
load('MatlabVariables.mat') % 저장한 파일을 그대로 열 수 있음

% Documentation always with you
doc save % documentation for 'save' function 
```

## Array
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c8b2c91d-99d6-4c26-80c8-a3b8c899ea1b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T005444Z&X-Amz-Expires=86400&X-Amz-Signature=75e9cbf0a9893b7304852f0fd861419d2ee1599474063394673da7f9386d3bf2&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- Array는 배열임, 위와 같이 선언하여 생성
- 데이터를 다루고 머신러닝, 딥러닝을 할 때 데이터를 다룰 때 숫자 데이터는 대부분 클러스터, 테이블로 들어옴, 그 테이블로 들어오기 때문에 Cell Array 학습이 필요함 
- Array에서 기본은 열벡터임, 배열에는 vector가 포함됨
- 위의 예시는 행 array, 행 vector라고 함

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/864128fc-b07c-420d-8e9e-f3691716cdcf/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T005646Z&X-Amz-Expires=86400&X-Amz-Signature=adeb4494c7ade15b3c6cdfee19a8711a7ec20b239534a71a44365a0db84c07aa&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 2차원 배열은 위와 같이 만듬(Array라고 함, 2x2, vector라고 하지 않음)\

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/53f10b17-6ac9-42d9-8f22-592ee406c466/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T005722Z&X-Amz-Expires=86400&X-Amz-Signature=a60970842e29d1d2a922f72acb5070bc770bac00878fdf13ebced43758dc2ac5&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 열벡터는 위와 같이 생성됨, 열 array 열 vector
- a=[1 2], a=[1,2], a=[1, 2] 모두 같은 표현임, 스페이스바만 쓰는 것은 element가 많아지면 다 콤마를 쓸 수 없어서

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5932fba8-330d-428b-abf8-be804840f3bb/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T005853Z&X-Amz-Expires=86400&X-Amz-Signature=f5c48b5f78533943b522910a9c5feee851b97d0c6322c6265e0af1813f246787&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/873f2f03-af5c-4a6b-87a7-ddeeb966ae44/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T005910Z&X-Amz-Expires=86400&X-Amz-Signature=f88bc2f69446e62c5412ec255c31e7b049bb6d37ff6414b006ee26664d6bc533&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 수식을 활용하여서 사용할 수도 있고 두 vector를 합쳐서 하나의 vector로 만들 수도 있음 

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/29ddeaeb-671e-472f-bf1e-ac58a3d270cf/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T005956Z&X-Amz-Expires=86400&X-Amz-Signature=2356557bd83fa0123ae2571709ae52a44a38c7786d2d06771ef78e6870cb2524&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a09a35b3-38e6-46eb-a33a-c9c2a476d3bc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T010006Z&X-Amz-Expires=86400&X-Amz-Signature=55bc1bc1d4d8f2392733c1489a18780300273040b128312edb54899e96d91fea&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 1~50까지 생성한다고 숫자를 다 일일이 입력해 줄 필요는 없음, 위와 같이 입력해서 만들수도 있음 
- 숫자의 크기를 다르게하여 증가시킬 수도 있음 

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c0d0dfea-eac8-4009-861d-ab25a8a17790/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T010101Z&X-Amz-Expires=86400&X-Amz-Signature=8e1684955397a8062c75bcff7b0f4837e6894c4807d087d63c6b8bc60a484c8e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0a9459c3-02c1-4334-9098-1cad4de5f4d1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T010111Z&X-Amz-Expires=86400&X-Amz-Signature=9ec4a8d29a6ee44fa26601dbbe6b96b60e3b756e66cb847c55a43a85d587157c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- linspace를 사용하여서 위와 같이 첫 값 끝 값을 알고 몇 개로 나눠야할 지 알 때 사용할 수 있음

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/975c848c-f18c-4797-9d46-c2f16a7f3316/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T010206Z&X-Amz-Expires=86400&X-Amz-Signature=d514957aa67cba7122b1f0c79afb8edf8f06c618807dcbfc72772efbdf38cad0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 숫자를 랜덤하게해서 vector를 생성할 수 있음 nxn을 기준

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c0f644c0-348a-4444-993f-270762361c40/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T010236Z&X-Amz-Expires=86400&X-Amz-Signature=0bf2830bf1bea5e8d449b229f793034da709b875ef11cec28c09edce34edb47c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 0 vector도 생성가능함

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5635a5ec-bcbb-4cc8-a9ad-cd0b4342ff21/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T010303Z&X-Amz-Expires=86400&X-Amz-Signature=9a2cc797fe3d4071401a73f1e5da4c2a04570773ed568f80bbf711ad9d4943ac&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 주로 행벡터를 많이 씀(공간의 제약으로 인해서, 간단하게 사용할 수 있으니깐)
- 여기서 행벡터를 열벡터로 '를 사용해서 위처럼 간단하게 바꿀 수 있음
```MATLAB
% Use square bracket to create
a=[1 2] % row vector
a_1=[sin(pi/2), sqrt(4)]
a_2=[sin(pi/2), sqrt(4)]

b=[3 4]
c=[5; 6] % column vector

% Concatenate
d=[a b]
e=[a; b]

% create a vector from 1 to 50, 1 increment
a=1:50 % a=[1:50], create a vector from 1 to 50, 1 increment
a_1=1:2:50 % 2 increment
a_2=1:5:50 % 5 increment

b=linspace(0,10,10)
% create an array with random and zero values
c_1=rand(1)
c_2=rand(2)
c_3=rand(3)
c_4=rand(4)
c_5=zeros(4)

%transpose
a=a'
```


## Indexing
- Indexing은 크게 Linear indexing, Row column indexing, Logical Indexing 3가지가 있음
- Linear indexing
	- 데이터의 기본은 열임(사용시 행으로 생성되긴함, 데이터를 덜 잡아먹어서), 열이 기본 feature를 나타냄
	- 체킹을 할 때 아래 예시를 보면 1->6->11->16->2.... 과 같은 순으로 체크를 함
	- 소괄호로 표현함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6939236a-f95d-4b0a-baa8-1eb36f0ef23e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T011020Z&X-Amz-Expires=86400&X-Amz-Signature=f306be2f2e471c93635528965359da084da00b45e6d72423a7a9e24a688ecb1b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- Row column indexing
- linear indexing과 유사해 보이지만 반드시 콤마를 써야함
- 행이 많을 경우에는 아래와 같이 직접 입력하지 않고 뽑을 수도 있음 
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8be3e2c5-04c0-4a62-b321-e364bf517abd/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T011126Z&X-Amz-Expires=86400&X-Amz-Signature=1e4dca638575b0b88c2eb16c129411a36f39983606c9ecf77343918956dcebcf&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fbb2df24-9e58-4109-b3e2-14a96c5fe9a4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T011137Z&X-Amz-Expires=86400&X-Amz-Signature=ed8337d82cd9b55f5d6d8f25f4a55700a7a7e56362c1be2570be8f2cd412ad8a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- (:)은 전체를 의미함(all), 아래와 같이 전체 해당 부분을 뽑을 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ec0ff9e0-f248-4b1b-8ba7-992fc26778f6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T011218Z&X-Amz-Expires=86400&X-Amz-Signature=121578c2a5d9f3d6eb8b01a1ac1600358871715ece5bc8adfc9e5df32811aa7d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 인덱싱 내에서 아래와 같이 대괄호를 통해서 특정행과 열을 뽑을 수 있음 
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6bde0250-47de-4a38-847e-62754b1457c2/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T011317Z&X-Amz-Expires=86400&X-Amz-Signature=4a39fea0190a3e11a9d9c5092fb55dc96613b5900d33263b761798af266765a7&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/688978bd-eacd-4f71-ac33-63c464549114/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T011327Z&X-Amz-Expires=86400&X-Amz-Signature=e5b998d262f95b3c2c4bbd6bd41b4bfe40451b14ce66b1e345d7c3ba90fa24bd&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 아래와 같이 특정 부분에 대해서 indexing을 명확하게 위치를 나타내서 뽑을 수 있음 
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/384c76df-56dd-4aea-9704-632cc1f4f9c5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T011400Z&X-Amz-Expires=86400&X-Amz-Signature=ab51dc16bf5265315c2f8962ecc944931717d3e272a55acb20fe7713e26d4938&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- Element 계산
- 덧셈, 뺄셈은 동일하게 처리하면 되나 곱셈의 경우 행렬 곱셈의 정의를 적용함
- 즉 곱셈을 하면 dot product로 행렬의 곱셈의 맞게 변환후 계산을 해야함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/22ba4009-92ef-4e73-b950-1ea4c5853c60/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T011435Z&X-Amz-Expires=86400&X-Amz-Signature=014924748827a518805b4f95650da76f667fc2b91f3bcc11fae3f1f203836336&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4a5c5c9a-2094-42cb-8d75-f125b21bad7c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T011502Z&X-Amz-Expires=86400&X-Amz-Signature=c8d8064ba275ec50def2c6a0689384c63ea3abbb712e796c1cc189527ccde9c2&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 만일 여기서 element간의 곱셈, 나눗셈을 하기 위해서는 아래와 같이 표현함
- element의 의미로 '.'를 사용함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ef4cc4a2-e8ec-46c6-ace6-227d7c106714/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210312%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210312T011611Z&X-Amz-Expires=86400&X-Amz-Signature=36599a9e45742c774af03eeb010d1d4588b499ade7dd245243f1d83b5f431ad5&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- logical indexing
- 논리적인 조건을 입력해서 인덱싱을 하는 방법
- 아래와 같이 논리적인 조건을 입력하면 a가 10보다 큰 값에 대해서 큰 값인 경우 1, 아닌 경우 0으로 logical array로 나타남
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c678bf7a-01b0-4724-ab83-7217415dbccc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T220632Z&X-Amz-Expires=86400&X-Amz-Signature=0bd3a9a3f5ac223d0b133b67a38e5bb8013a4fcb30be1d6b3ba0a96729714e90&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/11dfc152-5b4e-4f3c-907b-36b3b91660e9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T220653Z&X-Amz-Expires=86400&X-Amz-Signature=bc54684540fd54aca6c6280851f667436f9bbc47a680f3ec3eb6be654947cf0e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 logical array가 아닌 그 값을 뽑고 싶다면 아래와 같이 해당 값만을 뽑을 수 있음
- 열 기준으로 뽑기 때문에 11 12 13... 순이 아닌 11 16 12 17 ... 순으로 뽑힘
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0ede46e0-c8b0-4c09-a7ce-15f1d2bef5bb/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T220802Z&X-Amz-Expires=86400&X-Amz-Signature=86850d3e42112c043cd177cfedac0d8f12e4d0a21ac917dd8b53b2ae5c30b86c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 위와 같이 하지 않고 row column값까지 같이 뽑아서 할 수도 있음, 여기서 뽑아낸 값은 linear indexing 값임, 즉 해당 값이 있는 위치를 뜻함 
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4d68888d-a3a2-4581-bd37-64880e8fb353/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T220853Z&X-Amz-Expires=86400&X-Amz-Signature=009a483cc1239cd6fce543381baceb83266bc7aea8fd8e79e29cf2b9db431864&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 할당되는 변수를 row, column이라고 설정하여 찾으면 row와 column number를 알 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/23544aac-77b7-4730-a156-7a0d9cecc7be/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T220932Z&X-Amz-Expires=86400&X-Amz-Signature=a8a0109a5d002bc8e5ad16d50edf4413b47980012134dd414814ed8ad0735562&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 합치고 싶다면 array로 다시 합칠 수 있음
- 이를 통해 3행 1열 4행 1열등 한 눈에 볼 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a3301220-e5c7-4ba0-b356-cefd9fca67dc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T221012Z&X-Amz-Expires=86400&X-Amz-Signature=f3dc323f0722bd5daf1d504e2f134622403f95b3295280d2cbc358fd783b8229&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 만약 이를 이용해서 조건을 2개 이상 체크해서 확인하기 위해서는 아래와 같이 써야함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/031b5b61-dda1-4ec3-9a32-5ba662bbb223/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T221046Z&X-Amz-Expires=86400&X-Amz-Signature=cd090412845da2c918ed29490b2cc216bc39153d5662ac4c2b1225129b3b2352&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 logical indexing을 아래와 같이 써서 답을 구할 수도 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/81e5c284-b1b3-4402-bfc3-95d6a8971b12/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T221115Z&X-Amz-Expires=86400&X-Amz-Signature=6501c0f01a51064dda7f02438240f67fee58e751b332b50570cbd1d10e0803ac&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 아래와 같이 값을 직접 입력해서 넣을 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/31a6e224-9def-434b-a3c6-a4323c52bf1d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T221228Z&X-Amz-Expires=86400&X-Amz-Signature=74ed1b5507f72e7b6c07dddae892fadd93ea5e62e20ea4516ce90e3ddaf4c2e0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

## Statistical operation
- MATLAB의 문법을 활용하여 값에 대해서 유의미한 값을 직접 추출할 수 있음
- max
- max값을 아래와 같이 추출할 수 있음, 하나만 추출되는 것이 아닌 각각 열에 대한 max값이 추출됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9f0782a2-0e1e-4417-a0a6-0919c5d9d821/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T221716Z&X-Amz-Expires=86400&X-Amz-Signature=ff37833edb85dfe373c4bcd0e9ce4d173e9fb7bc98394cab7389cfc0bcf77b15&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 가장 큰 max 값 하나만 추출하려면 아래와 같은 작업을 해야함, 이렇게 되는 이유는 데이터가 기본적으로 하나의 열(feature)에 대해서 나타나는 것이므로 열을 기준으로 하기 때문에 그 열에서의 max 값을 뽑아냄, 각각의 열은 각각 다른 variable이기 때문임
- 예를들어 각각의 feature는 국어, 수학, 영어 점수라면 각각 다른 속성이기 때문에 그 영역에서 max값을 구하는 것임, 그 중 값이 큰 것을 찾는것은 별개의 문제임, 그래서 max 값은 하나의 열에서 작동을 함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8231db50-2059-4076-a270-76b221af7f3a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T221931Z&X-Amz-Expires=86400&X-Amz-Signature=8c5e0788290a87ead8af6be21e595b665dbd2956987a56fb7f1f48cfa07e27e7&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 하나의 feature에서의 max값과 별개로 max값을 뽑기 위해서는 아래와 같이 처리를 해주면 됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7abc4769-7208-47e7-b679-5d7a8d2b0a54/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T222011Z&X-Amz-Expires=86400&X-Amz-Signature=100e4b051fde17403fa86ed9d7d15b9f5d0c57f2f54e4f49ef212f10ee847061&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- find값과 마찬가지로 max 역시 index 값을 뽑아줄 수 있음
- 아래와 같이 처리한다면 max값과 그 max값이 위치한 열에 대해서 index를 뽑을 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/256bdcff-3878-4702-b524-03f6eea2ce35/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T222051Z&X-Amz-Expires=86400&X-Amz-Signature=91766fcc71a5a72e690ae4ca3e808645065faa0f3f5cd175ce6ea657fcaf7824&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- sort
- sort함수를 통해 아래와 같이 sort를 해 줄 수 있음, 기본적으로 오름차순 방향으로 sorting을 해줌
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a692fb65-c41b-4c23-b0dd-7797603735f1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T222126Z&X-Amz-Expires=86400&X-Amz-Signature=38fb3227f55e29ac69f099d6f991faa0c718bcbdc5df088552a8156552afa40f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 내림차순으로 하고 싶다면 아래와 같이 입력하게 된다면 내림차순으로 정렬을 함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2034edb2-1eb7-4ce7-9f3c-7b0d3f09c272/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T222157Z&X-Amz-Expires=86400&X-Amz-Signature=8b7ec6aebf4bde1604e57d4b248779f6c4f4ad1af508dc83451a17c92ddaa971&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 단순하게 정렬을 하는 것이 아니라 정렬전 index 순서 역시 아래와 같이 나타낼 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/20b98689-0e91-427d-b3a6-85f28862844c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T222235Z&X-Amz-Expires=86400&X-Amz-Signature=b062c81134a7655bc7b2ee320e6b56799b183e8e24437c5aaced36141c8d0c35&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- size, numel, length
- 사이즈의 개수를 체크할 수 있음
- 아래와 같이 행과 열의 개수를 알 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b657eb6c-fa26-4ffa-85f0-eadebd839003/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T222307Z&X-Amz-Expires=86400&X-Amz-Signature=3ae29c113ee4ff2244cfd81bf0453494ebf635d93144e1367f11a05cd85e5f8d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 그리고 총 element의 개수도 체크할 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f4790aef-809c-4a70-bb93-569261b2f2be/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T222330Z&X-Amz-Expires=86400&X-Amz-Signature=811233e748adb9ed51d9584086314134eabde2f49309d295318de5942d1dc005&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 추가적으로 옆으로 변수가 몇 개가 있는지 알 수 있음
- 열이 기본이기 때문에 length는 열을 기준으로 나타냄
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1774f7c2-5b77-4f0a-aabd-0260e3eebb99/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T222430Z&X-Amz-Expires=86400&X-Amz-Signature=9496c12fa7abf4a82fc66774e50ace2b6e6ac11f16eeedf369a661a694901fb1&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 위처럼 다양한 사이즈를 체크하는법을 아는 것이 좋음

## Plot
- 다양한 plot을 그릴 수 있음 doc plot을 통해서 더 많은 정보를 알 수 있음
- 아래의 주소를 참고하여 코드와 document를 참고할 수 있음
- https://kr.mathworks.com/products/matlab/plot-gallery.html
- 사용할 데이터는 아래와 같이 excel에 있는것을 MATLAB 외부에서 열기를 통해서 볼 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ffc823e5-e709-4f66-878f-efc01ccc00f5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T222704Z&X-Amz-Expires=86400&X-Amz-Signature=6b8a25d6164778ca717dca76a77da87dd2dac67897c8426491afcb41d92d32d9&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 데이터를 불러오는 방법은 다양하게 있음, 테이블 전체 다 불러오는 것, 파일 자체내용을 다 불러올 수 있음, 값들만 array로 불러오는 것도 있음
- 하지만 주로 데이터 사용시 하나하나 variable이 중요함, 기본은 array로 값만을 불러오는 것이지만 variable을 위해서 테이블 전체를 불러올 것임
- 불러오기를 할 때 큰따옴표("")를 권장함, 무조건 쓸 것
- open을 하게 되면 아래와 같이 데이터에 대한 내용이 테이블 전체로 불러와서 나옴
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b4da1284-1d04-4e99-93c3-2186c7ab35d4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T222842Z&X-Amz-Expires=86400&X-Amz-Signature=878652fd270bda728f94290d1af6f8d605981381c22c8456ceec2a1e467eee63&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b0b88534-6caf-48c6-8285-9b0ee2860e92/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T222852Z&X-Amz-Expires=86400&X-Amz-Signature=4ae6c9295ec7a34d0df741f42c2b6b9661a270c7ae67eb3697d3e1e277e67396&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 위와 같이 테이블 형식으로 나오면 데이터를 어떻게 불러올지 UI창으로 열려서 나옴, 옵션을 조정해서 가져올 수 있음
- 해당 창에서 아래와 같이 체크를 한 뒤 설정을 하고 값을 불러온다면 해당 테이블이 2번째와 같이 불러와진 것을 알 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d722f5f6-9138-4317-9a9b-878e754a4bad/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T222950Z&X-Amz-Expires=86400&X-Amz-Signature=d226639acf9d25e952f1d1958488c5d5396176d09e6e5f07031ac852db4c807a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/67a64d5c-b7b1-4e32-a6f6-b87ac6a73763/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T223000Z&X-Amz-Expires=86400&X-Amz-Signature=0652ee924ff4fff58a6c222919c558450f6e40cdaa9cdcb67f14850901fa6fc0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 하지만 보통 위와 같이 UI를 통해서 하진 않음, 아래와 같이 체크를 하고 설정을 한 뒤 스크립트 생성을 누른다면 2번째 사진과 같이 해당 테이블을 불러오는데 필요한 코드가 생성됨(범위에서 해당 값에 대한 범위를 파악함), 이를 그대로 복사 붙여넣기해서 사용해도 됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/40e5ae97-8f17-4d7c-8e1f-a519f9a99471/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T223110Z&X-Amz-Expires=86400&X-Amz-Signature=3b4aae7f3c11585cc32898f5bebfd5356b3b592570cfda668c3b9185e5eb7127&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/22b8af5d-6826-4803-b9b4-46dbc8acf4dc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T223125Z&X-Amz-Expires=86400&X-Amz-Signature=f1afa1a79bea33cd779968581db283254c62eb4ab9a651308c3d204cbb23bd2c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 그러므로 데이터를 불러올 때 모르겠으면 open만 알고 있다면 위와 같이 활용할 수 있음
- 그리고 불러올 수 없는 값에 대해서 어떤식으로 처리할지에 대해서도 설정을 아래와 같이 할 수 있음(blank, 특정 숫자로 할 것인지), 비어있는 셀과 char으로 된 셀에 대해서
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/897d5c60-4b52-4a64-9eb0-9e90de442385/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T223350Z&X-Amz-Expires=86400&X-Amz-Signature=7a7a93830ae33b82e015bb840a2f9c5def66785f3889bc83a844551cf74d4973&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 테이블 형식으로 불러올 때 굳이 변수 이름 행 5번째라고 써 있는 부분에 대해서까지 체크를 하지 않고 아래와 같이만 체크를 하고 불러오게 된다면 자동으로 변수 이름 행이 5번째줄로 설정했으므로 추가되서 나타남
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c678911a-c019-4de6-8888-7ec99c7fb381/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T223447Z&X-Amz-Expires=86400&X-Amz-Signature=68a2d769a58d2297ddca57ec7de9fda99e6a53214b6c04875c487c6e7da3fe74&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2ad8d92d-af1d-413c-91fe-b52c7a64d691/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T223457Z&X-Amz-Expires=86400&X-Amz-Signature=1a716cad6a553bdd01e6639f5f73b6e57b0257e27521cde5dec372742a5bab52&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 이를 open 형태가 다른 형태로도 불러올 수 있음
- 먼저 xlsread를 통해서 number array형태로 만들고 불러올 수 있음 하지만 권장되는 방식은 아님(시간도 오래걸리고 무겁기 때문에)
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ee25db5c-4c14-4636-8bd6-406db83cb436/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T223545Z&X-Amz-Expires=86400&X-Amz-Signature=ca0beb555add2dde571d66548bb901bfa43bda9767b7b4615778a2d21f089924&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 테이블 형태로도 아래와 같이 불러올 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/68ab9cd2-9cf8-450c-8023-1c2955b543d0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T223610Z&X-Amz-Expires=86400&X-Amz-Signature=dddf9a1f3027e270a18bab24fd5dce6ad142a7f4f958afd6209506a14324c797&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 기본적으로 주석들을 제거를 하짐나 주석의 범위를 설정해줄 수 있음
- 아래와 같이 A:5부터 K:24를 불러오게끔 설정을 2번째 사진과 가팅 할 수 있음
- 여기서 옵션에 대응하는 값은 2번째 사진과 같이 하나씩 대응됨(옵션-값)
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5252953d-9a2c-4358-a988-7b57bb5621df/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T223711Z&X-Amz-Expires=86400&X-Amz-Signature=19e7e544b100c0397b61352a15b6b4a2ff351c15b0670a8abd2323d0e16f9ac6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9bca80fe-73a4-45d1-891b-81e66c616ed0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T223748Z&X-Amz-Expires=86400&X-Amz-Signature=5d9a409ec6c2d2ca31d30ebcb1a3078abc9705fc338c2fbe4b7fa70ed4b4866a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 보고 싶은 데이터를 확인하는 법은 아래와 같이 사용하면 됨
- 하지만 테이블로 설정해서 해당 값이 아닌 해당 테이블 전체가 나옴, 테이블에서 element만 뽑아내기 위해서는 아래와 같이 사용해선 안됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4bf97b9f-4d62-4dc1-a3b9-1bc81a5b43da/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T223839Z&X-Amz-Expires=86400&X-Amz-Signature=00ba51e5d1fbec969b3751e4da09caead6412cc5473c676aecc42f115b93f456&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- cell을 배우면 더 간단하게 할 수 있지만 테이블에서 데이터만 가져오는 값은 아래와 같이함(테이블 형식이 아닌 element 형태)
- 아래와 같이 보면 테이블이 아닌 element형태로 가져왔음을 알 수 있음, 즉 element만 보기 위해선(.)을 사용하면 됨(. 를 element의 의미로 쓰임)
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0f9b6b51-b0d0-4b9a-b902-4949ebe52da7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T223950Z&X-Amz-Expires=86400&X-Amz-Signature=236cde95c211a08ad3e79c41d41f2268ce516752a47cc659736276156e841c32&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/cc1742f1-43fe-4b3b-b7c0-de47f5ca6a37/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T224000Z&X-Amz-Expires=86400&X-Amz-Signature=d6d114964bec5f015d0b54ccdcfff1c4656e16aec788d42a3868940780c00ef5&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7cef42ea-4794-40d9-b72e-41cbe5dac39a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T224008Z&X-Amz-Expires=86400&X-Amz-Signature=f7147fc14893ac558c0d6b2a0f11c61f9e059c08334151cc36cf4c579d4980d2&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 아래와 같이 데이터를 모은 뒤 plot을 활용할 수 있음, 하지만 NaN 값이 있는 경우 numberic값이 아니어서 plot을 그릴 수 없음, 이 부분을 처리해야함, Numeric값이 있어야함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a3636dff-59e4-4ab0-b1c6-5653d68a864e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T224103Z&X-Amz-Expires=86400&X-Amz-Signature=6a3f541bf9e313fcd8dbcd502d5c579559c0fe56b95870cdc1bbed138875d9ba&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 NaN값은 여태까지의 해당 열의 평균값을 집어넣어 줄 것인데 이를 위해서 logical indexing과 isnan메소드를 통해서 NaN인지 파악해야함
- ~ 은 부정을 의미함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/60a0067d-19a6-4a36-ba6c-b6626638c977/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T224155Z&X-Amz-Expires=86400&X-Amz-Signature=521d1c84e4a158e1020b58e521f4bbd456c2798d4152402b0bad328d3b97a1f1&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b3e898a0-786d-42c7-8f18-3e37f6749c74/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T224216Z&X-Amz-Expires=86400&X-Amz-Signature=f8fd20ece0cc5565e0c9280cc4208ca0057f11d1f4307d349a8c629bf7eb18f3&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- NaN에다가 평균값을 넣을 것인데 여기서 Au에서 아래와 같이 처리한다면 NaN이 아닌 값이 추출이 됨
- 그리고 2번째 사진과 같이 평균을 냄
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0abb9f0d-bd53-4be0-b3f4-e1ec7c0658f5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T224337Z&X-Amz-Expires=86400&X-Amz-Signature=e3fa1c9af93695ed525a672aaa7b34bbb517724e759b1d16f6e46621ee42f8f6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a9dac7cb-d25a-4b93-b65a-3bbae76daaec/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T224358Z&X-Amz-Expires=86400&X-Amz-Signature=a3f010860cf964b0cf64ffd67c9ef38ca4f04a155c778f44344ef0406a7edd6d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 그 다음 isnan을 검색한 뒤 해당 부분에 그 값을 넣어주면 됨, 그러면 평균값이 NaN에다가 들어가게됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1d358014-0613-434b-b005-e4ccf26356ae/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T224442Z&X-Amz-Expires=86400&X-Amz-Signature=ae70d991e50aea9e4bf037d1c8e18f09dab056c0ac157b0d2cad0d0ef3aca94d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 하나씩 차근차근 과정을 밟아나가면서 해도 됨
- plot은 상당히 쉬움 plot을 쓰면 됨, 아래와 같이 나오게 됨
- 원하는 데이터 입력후 여러가지 옵션을 ""와 함께 넣을 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/18461de3-d08b-4f23-95e4-67b15148177d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T224532Z&X-Amz-Expires=86400&X-Amz-Signature=f140bc98a41ffba32d0716470b0fc5162453fdad815fc38c3ea098a026f8dfaa&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 위와 같은 plot이 아닌 Year로 바꾸기 위해서는 아래와 같이 작성하면 X축을 바꿀 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5ef292f7-68c5-400f-af8f-d0b55e47ad20/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T224611Z&X-Amz-Expires=86400&X-Amz-Signature=f14737cb9604b34089fab2b992ca21f62665155ae6a5eb443fa7821608e8fd47&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 어떤 데이터를 갖고 있는지 명확하게 갖고 있게끔 아래와 같이 처리할 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/79d8d9e5-aa26-4de3-9dc1-9340a846493c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T224635Z&X-Amz-Expires=86400&X-Amz-Signature=c809019fe253e099c8b693fd3e5b37769abd9ee76ae3e164f2a81ce2bec3d964&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/afa4e1ee-06ee-42fd-a9cb-07fb7882a51e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T224644Z&X-Amz-Expires=86400&X-Amz-Signature=6f2605c160885550c2c1ee9c49994ca5daa86ddbf77812fab85ac602ff0ad713&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 그리고 색깔도 바꿀 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/40d6473e-ea5f-4ff5-8443-b46b9cbe75a5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T224705Z&X-Amz-Expires=86400&X-Amz-Signature=54ea5bb065350427d35f3b5b7bb304acd7218a1504e936dcc2871557eb7700e0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 선을 희미하게 연결하기 위해서 아래와 같이 처리할 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/577e3b04-ca83-4933-87d3-92343ba53da9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T224732Z&X-Amz-Expires=86400&X-Amz-Signature=ff321f8836d0e6f2f5e300dcf323e0baa20755d89d24315b05fef56df3850a54&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 또 새로운 plot을 그릴 때 같이 합쳐서 쓰기 위해서 아래와 같이 처리할 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/32740838-3444-4252-8c58-d308f2dc2f12/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T224812Z&X-Amz-Expires=86400&X-Amz-Signature=01806586370c2f46ca45f45e6713132d172b3fef184c57dddc4979e67e2537a0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e2632ca4-8fa3-4e0d-904e-9ce705b8d356/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T224821Z&X-Amz-Expires=86400&X-Amz-Signature=fd8bb0ff7027e9d21e0163ec1986c579cbe7c221545c730383662d904d39eb37&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 다른 plot으로 그리고 싶다면 아래와 같이 해제를 할 수 있음
- hold on, off 사용함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/78e9136c-5dd0-4a53-a8fd-4b2a89d5ddd2/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T224847Z&X-Amz-Expires=86400&X-Amz-Signature=c4805a7fe0828e292aec302e0a959e84be3d3d3cff966f69362a28fccadfc61d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 추가적으로 figure 명령어를 사용해서 연산속도를 빠르게 할 수 있음, 자동화, 알고리즘 등 실행속도를 즉 메모리 공간을 확보할 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b8829fe0-2a7f-49cd-aeed-388d23c13b46/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T224922Z&X-Amz-Expires=86400&X-Amz-Signature=5814a07c322f31835d9e3ab044c0ffc109e2bc6f644abd61d67f7c6fd6568c13&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 그냥 스크립트에서 쓸 경우 새로운 창이 뜸
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/27159eb0-485f-4162-99e1-db8d8270fdb9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T224941Z&X-Amz-Expires=86400&X-Amz-Signature=8f1d16ad2e4ecb7449a9b2d28fdc255b6980cbf0d53906bf3e1c2502cab2e95d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 위와 같이 다양한 옵션을 사용할 수 있음
- 추가적으로 그래프의 legend, x,y축 표시등을 처리할 수 있음 
- 먼저 title을 달 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1b628711-a981-45ca-8768-f2c5ce3e2e8d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T225022Z&X-Amz-Expires=86400&X-Amz-Signature=218976b4884b14a4b26be575381149f85e016d15d49097dbe1d23421d99563c3&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 추가적으로 폰트크기, 색깔등 다양한 옵션을 사용할 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/98eb64e1-ac14-407f-94af-751685e75f2b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T225053Z&X-Amz-Expires=86400&X-Amz-Signature=59cf5c7f633b1613004a0c7dbda722b8c9b53020cc2de24964cd80421f642a0a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- label 설정도 추가할 수 있음 
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7fb7ff07-57c6-4d1b-8d25-c3db17b58156/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T225112Z&X-Amz-Expires=86400&X-Amz-Signature=2e6365d40424c67d68d1963fc32e7784b384e7870de238bbde7a7c510a99d0b6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- limit도 바꿀 수 있음, 즉 1~8 범위를 바꿀 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8c1bec4c-234c-40d4-ad77-6d9858c4a82f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T225141Z&X-Amz-Expires=86400&X-Amz-Signature=84d16e157766a3b2447901d01e554d5571a2516aa53ec0e6a2873b753eceb872&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">


- 이러한 설정은 plot을 다 그린 다음에 데코레이션 같은 느낌임
- 그리고 legend 즉, 범례를 아래와 같이 추가할 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/834647d4-7f55-4f87-ad82-2f77916d4513/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T225221Z&X-Amz-Expires=86400&X-Amz-Signature=4c34e9d4dfe149c132016c07799b052d33fcd80d9b14bace3b7fbefc80d3a625&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 하지만 legend가 아래와 같이 값을 가리는 경우가 생기는데 2번째 사진 이후처럼 위치를 바꿔줄 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/327cbd6b-edcb-41f6-9dbf-893b512ad10a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T225252Z&X-Amz-Expires=86400&X-Amz-Signature=28fff8669e8778985a4fa590dd4dd917132c797d84d039cc1d12c504552ea1b2&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/42187cff-8220-4127-96a3-f55438f82d52/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T225318Z&X-Amz-Expires=86400&X-Amz-Signature=760e859e290260bbf59ac8a3ec9e496d0a311076ea0845ddc60a7959648df9dc&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/478f9c24-5b29-44f8-a755-34f01198d24a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T225329Z&X-Amz-Expires=86400&X-Amz-Signature=62df4fd693ccb2bac59653af8c2a318ebb67cc0f231867fa9287b549f2d9fbca&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/45034b29-dfee-4641-b588-9d60e8767cc7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210318%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210318T225337Z&X-Amz-Expires=86400&X-Amz-Signature=5c9e6de53497d726249da0897b13c31f88890d6c1c752507c3cc488a64c15509&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 하나의 plot의 여러개를 그리되 겹치지 않게 아래와 같이 테이블 형태로 그릴 수도 있음(Subplot)
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/253e995b-6a33-4f21-8c59-e3141a146440/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T045719Z&X-Amz-Expires=86400&X-Amz-Signature=062924dc9a140ed393be802eb799c189a7983ece2fe3ce9354d01506ac173626&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 각각 title, legend, label등을 붙이고 설정할 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/46ef14d7-be81-4b0c-bd01-9095845583be/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T045747Z&X-Amz-Expires=86400&X-Amz-Signature=2a064f0446d6c86a3936406f0d776e90179082cf1f3dd20cf84ae335c11160b4&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 그 수치를 비교하기 위해서 lim을 동일하게 해주는 것이 일반적임, 같은 scale에서 비교를 해주기 때문에 subplot이라도 각각 lim을 동일하게 줘서 활용을 하여 비교를 함

## Logical operator & Functions
- Logical operator는 위에서 실습함 find함수와 isnan함수가 해당됨
- web(fullfile(docroot, "matlab/logical-operations.html"))을 통해서 해당 내용을 자세하게 알 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/79eea74b-81e3-41bc-82da-1dcf88f7ce8e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T050055Z&X-Amz-Expires=86400&X-Amz-Signature=89ae1f9b5b722839cb3cb43a86b6dc9f61cc7983df382550224cc6b7fd4ff1db&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- Short-Circuit은 많이 접한 개념이지만 Array에서는 쓰이지 않음, 머신러닝에서는 Array 데이터를 사용하므로 Short-Circuit은 많이 사용 안하고 일반 Logical Operator를 많이 사용함
- any함수 -> 어떤 array가 nonzero인지, 0값이 하나라도 있는지 묻는 값, 0이 하나라도 있으면 0 반환함, 그게 아니면 1 반환
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f40e99c6-1821-4e5e-8db7-b6bc853101f0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T050217Z&X-Amz-Expires=86400&X-Amz-Signature=d6fad4fce159844534df5074df7059662a1f9ed4b3b8a55cbfa19809701019a8&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 만일 그냥 any(gasprices)를 할 경우 에러가 뜸, 데이터를 보고 다룰 때는 테이블 형식으로 다루지만 데이터 프로세싱을 할 때(실제 numeric 데이터를 다룰 때)에는 테이블 데이터에서 array만을 가지고 사용하기 때문임(직접 사용해야함)
- Numeric Data가 아닌 경우는 Cell Array에서 다룸
- all함수 -> 모든 element가 0이 아닌지 묻는 것 0이 아니면 1값 반환 모두 element가 0이면 0반환
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3f856d2a-2cdb-4e28-8eee-f8ef83a9673f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T050346Z&X-Amz-Expires=86400&X-Amz-Signature=510c45910b96c49f34a672a04e22c4e05e666c8655751cca20f3a6eec31d599a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 이를 응용해서 아래와 같이 쓸 수 있음 아래와 같이 쓰면 Germany의 값이 France보다 큰 값이 하나라도 있다면 0을 출력함 해당 조건이 맞지 않으므로
- 이 기준은 같은 observation에 대해서만 비교함, 즉 1번째는 1번째끼리 2번째는 2번째끼리 비교하는 것임
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6d187dd0-d08b-4e64-8cdb-1b43761c6499/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T050445Z&X-Amz-Expires=86400&X-Amz-Signature=38dc318a5797529c01fa92ec9cc7d602f6ff1c95a9d1aa3a38dcb0b27671965a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 실제 표상에서 1행부터 12행까지 France가 더 크므로 아래와 같이 코드를 변경하여서 값이 달라질 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/15488d26-4a50-4f44-a3ee-94143a8d54b9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T050516Z&X-Amz-Expires=86400&X-Amz-Signature=38c7677b8b6b3024ad1123660b282b7d4cfa2944c151ce5c2ad8e5f7dab37e43&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/24a2f57b-a8b6-409a-bd99-dd5ce960de41/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T050529Z&X-Amz-Expires=86400&X-Amz-Signature=d4809cb5b16b569d81b823d1f5a3c76b71733172de14d02d5c78353c94e178fc&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 추가적으로 any 역시 응용할 수 있음, 아래와 같이 쓴다면 큰 값이 하나라도 있기 때문에 1을 반환함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/dfd6bcd2-c2c0-4763-a211-6eb980a2ddaf/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T050552Z&X-Amz-Expires=86400&X-Amz-Signature=56c719863cefce08c5099d689dc04008a5c4e8e4caca04f148c4786afc1c7c5b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/22bb462e-d0d9-4ebb-a075-233cd267d392/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T050602Z&X-Amz-Expires=86400&X-Amz-Signature=22e11db5dc545c779f71caae52d0e4c9abf7755f7788b6683b8314dd25f60859&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 단순하게 아래와 같이 코드를 짠다면 그 값을 비교했을 때 해당 조건이 맞는 경우 1 아닌 경우 0으로 나타나서 array로 쭉 나타남(하나하나를 비교)
- 위에서 봤듯이 1~12는 더 크므로 1로 나머지는 0이 나옴
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b6a4f62b-9a1c-4213-8e76-5d79f46ffc8c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T050659Z&X-Amz-Expires=86400&X-Amz-Signature=07fb79429ba9cc653fd26d8ef8e5720d2aa8f57d4817ccd0a23c2bfc6d0204bb&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">


- nnz -> 0이 아닌 개수를 카운터함
- 12개가 나옴 크기 비교상 1~12까지 더 커서 1이므로 12개임
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e8b73a04-acc4-4123-aa3a-8681322bdf6b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T050753Z&X-Amz-Expires=86400&X-Amz-Signature=096aa101c7dcf8c621bbe4cc23c46ff6b0b41ff65c4d1e6bc584477988e47be0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">


## Cell Array
- CarSpec에 관한 데이터 테이블임, 여러가지 데이터가 혼재되어 있음
- 테이블 클래스는 기본적으로 문자형 데이터를 쓸 수 없으나 하나의 방법으로 문자형 데이터를 숫자형과 같이 아래와 같이 Make Model 아래 값을 넣을 수 있음, Cell Array로 이해해도 괜찮음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1bf368c9-bf02-4cfc-a807-e2b203452fa5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T051012Z&X-Amz-Expires=86400&X-Amz-Signature=8507d8be33f646bbf1f3fa761e29cf78cc994ead37f8c0372e946ccf532d928a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 아래와 같이 테이블로 불러올 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3a29e159-a2b3-407c-b93f-e10504e2749e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T051030Z&X-Amz-Expires=86400&X-Amz-Signature=9404f6a2c6ffbbad2d0624d57f6368f5410617f0b620869512dab0126391b431&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 아래처럼 그 값을 불러올 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/23ecbedf-b490-4b7b-bacd-8d10de0236d4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T051049Z&X-Amz-Expires=86400&X-Amz-Signature=03fcfd1e8d599421cb71e5d6b47748cf042fbd99cda30a9bad86fa5937456ee5&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 문자형의 경우 EngineSize처럼 element 값이 뜨는 것이 아닌 중괄호 표시가 포함되어 있음, 이것이 Cell Array임
- 테이블은 숫자형만을 다룸, 여기서 그러면 아래와 같은 형식으로 문자가 들어감 즉, Cell이라는 공간에 문자가 들어가고 거기서 101이라고 해당하는 값이 그대로 Make의 1번째 부분에 들어가게 되는것임, C언어에서 포인터의 개념과 유사함
- 문자형 데이터는 직접적으로 들어가지 않고 해당 주소넘버가 들어가서 그 데이터를 볼 수 있음, 여기서 주소넘버는 알 수 없음, 그래서 문자형이 마치 숫자형처럼 위처럼 중괄호에 묶여서 나타남
- 숫자도 Cell 형태로 넣을 수 있음, 그리고 아예 다른 Array를 통째로 넣을 수 있음
- 결과적으로 형태는 {}(중괄호)안에 나타난 형태로 나옴
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6e55b9de-d174-4e32-aa88-c44aa7c63322/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T051317Z&X-Amz-Expires=86400&X-Amz-Signature=8799504c026d14f1723fce767ba9e19af89c1182daafb18a458ef5c750d1e625&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9ffb9b51-4b2e-4ccb-b1d2-8d96b4296ef7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T051325Z&X-Amz-Expires=86400&X-Amz-Signature=57e9cb90f69a1948ccdcd412f84c8eba70159a96fd9899566e55e5814ee20f40&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 plot을 응용할 수 있음, 그냥 plot을 쓴다면 선형이더라도 아래와 같은 형태로 나타남
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c59d5f9e-f02b-4b95-83ec-0b6d68d0a289/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T051349Z&X-Amz-Expires=86400&X-Amz-Signature=ddf6bc6dea6ba82b2186dc2de70b09c46f3507747210d04f1d8658de29abb471&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 위와 같은 형태는 알아볼 수 없기 때문에 분포로써 나타내기 위해서 scatter를 쓸 수 있음, 머신러닝에서 grouping할 때 많이 씀
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d391103f-9e19-4448-966a-79e5823ec481/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T051420Z&X-Amz-Expires=86400&X-Amz-Signature=4852b01ad348b4dcc6aaa2b19cbf9034f83b2538c02fc82fcb531c5d693afee0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5ee4e44e-9b29-42c4-91e1-65a0d76ab21a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T051428Z&X-Amz-Expires=86400&X-Amz-Signature=81e65d661504c1f417143b9c94726b5d6213fdbb11e5420063d9e8dd9d38697b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- element 계산을 통해서 정규화를 할 수 있음, 여기서 그 값을 위해 matrix 나누기인 요소 나누기는 아래와 같이 시행하면 됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7c079980-4e9d-43e9-864e-16304a50020b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T051501Z&X-Amz-Expires=86400&X-Amz-Signature=e9a289649eb949f25b32c69d3fdbf76689b579e635aca12a1ec7f83ada3bcc9b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 아래와 같이 코드를 치게 된다면 새로운 부분을 추가하여서 해당 계산값을 집어넣을 수 있음(Variable 생성)
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7b2b4db6-1432-4d0e-ba6b-8ea6991ae377/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T051532Z&X-Amz-Expires=86400&X-Amz-Signature=8cb9e44017e0b41cf7a88f9d91f98051c2faab101193b7d9d9f1e87a9cfc565a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 최대값을 찾을 수 있음, 여기서 index number observation도 알 수 있음(13번째의 최대값 존재)
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/511ecf99-ba5e-4847-8d33-60580c789346/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T051611Z&X-Amz-Expires=86400&X-Amz-Signature=1f97ee0598b0e849da9d52756a9e595a5b037278504efeefefadf6c10acc6fab&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 아래와 같이 코드를 친다면 cell형태로 나오게 됨(table처럼 나옴)
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/541256da-e24a-47a1-85e2-836d12d37ec0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T051637Z&X-Amz-Expires=86400&X-Amz-Signature=d2371b23b16a9fa7a5e6515ab4c9019925ce6f04de19d033e956745d3e3ec13c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 idx를 활용하여서 코드를 사용하면 table형태가 아닌 cell array형태로 나옴, cell에 갇힌 상태에서 cell을 통째로 가져옴
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/aa892261-153f-4be6-9062-2b30321989ac/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T051709Z&X-Amz-Expires=86400&X-Amz-Signature=1faf3d26e3d4eaec862358e34745df4d7120b7fe7e5fe0fb3d7287c95af76e2b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 그냥 문자열 자체만을 뽑고 싶다면 아래와 같이 {}를 활용하여 값을 뽑으면 문자열만 나오게 됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8162b0b0-40b5-4ba7-923a-8a0791bc5183/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T051744Z&X-Amz-Expires=86400&X-Amz-Signature=1ff9682f7dc2b8744a9b767bb28a552fe68f592190afe18bed62f75c144c0510&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- CarSpecs에서 하나의 row를 조건을 걸어서 아래와 같이 정렬을 할 수 있음
- 그러면 PtW을 기준으로 기존의 CarSpecs라는 Table이 내림차순 정렬이 된 byPtW가 생성됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3063c7d1-1b38-4c72-bf42-d4637e7e9929/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T051834Z&X-Amz-Expires=86400&X-Amz-Signature=a6e03994d75786beff9e5e5438d2e539899638ff15fa9662c732f758d53a6e10&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/329e5d1b-5183-4290-b794-f7a532bc6891/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T051842Z&X-Amz-Expires=86400&X-Amz-Signature=d2a5697d9317f799f004fb2a85b8b544e88925e09ecb4c38b3d3d749372ee472&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 그리고 정렬한 값을 볼 수 있음, 아래와 같이 코드를 활용하여 정렬 기준 1~5의 순위에서 1,2,end 즉 Make행, Model행, PtW행을 뽑아서 나타낼 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/53519bc7-2c10-4cb0-83b6-8135a17e27d4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T051933Z&X-Amz-Expires=86400&X-Amz-Signature=68a92dea7e21e604c73d1a7378124435c06d27dc449b55bc71d96d13b346df4c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">


- 다양한 방식으로 나타낼 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e0c3ad41-112b-4161-8024-36f5cb582fac/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T052012Z&X-Amz-Expires=86400&X-Amz-Signature=d5cffae1d1d015e8570a3c153f9774a9fef3eb453d9b11d03a891c1f77b57b13&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/eaf597be-6470-4a65-9c97-41836f1b1529/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T052021Z&X-Amz-Expires=86400&X-Amz-Signature=d5753638f4d343902059466cdf3f7cb14c9d357e91c933801023809d942af7e6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 다양한 방식을 활용해서 직접 해보는 것이 좋음, 여기서 자동으로 sorting을 하고 복잡하게 꼬여있을 경우 Variable Name만을 가지고 뽑아서 하는 경우가 필연적으로 생기게 됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/cbe87f3c-d78f-4ddf-90f1-da1bbee8f8ea/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T052104Z&X-Amz-Expires=86400&X-Amz-Signature=14b39b019999ee8bf3bf20313da6461b6604f92461e473826e97744df5549f62&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 여기서 머신러닝 모델만을 가지고 모델을 뽑아내서 그 모델을 가지고 다른 모델을 비교할 때는 첫번째 방법으로 충분하지만 완전 자동화 형태에서 데이터는 테이블 형태로 받아오게 되는데 column의 name위치가 어디에 있을지 모르고 그에 따라 길이도 달라지기 때문에 그 상황에선 뒤죽박죽하게 되는데 여기서 변수명은 바뀌지 않기 때문에 변수명으로 뽑아서 활용하는 측면이 더 나을 수 있음(비지도학습과 클러스터링을 하여서)
- table도 cell과 똑같이 생각해도 됨
- 그러면 아래와 같이 그 값을 볼 때 원래는 테이블로 나오지만 아래와 같이 처리를 하여 그 값 자체를 {}를 활용하여 뽑을 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/80f89979-c351-43b1-aa72-4cea9d8c25fb/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T052323Z&X-Amz-Expires=86400&X-Amz-Signature=cef4e01dfc1cbc90d6c7aca2b38b8154744f769a8d23296716ea68f20cfb5016&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
