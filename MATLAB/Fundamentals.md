## Fundamental

## Roadmap
- [Variables & Expressions](#Variables-&-Expressions)
- [Array](#Array)
- [Indexing](#Indexing)

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