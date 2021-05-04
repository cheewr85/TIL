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
![one](/img/MATLAB/Fundamentals/one.png)

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
![two](/img/MATLAB/Fundamentals/two.png)


- Array는 배열임, 위와 같이 선언하여 생성
- 데이터를 다루고 머신러닝, 딥러닝을 할 때 데이터를 다룰 때 숫자 데이터는 대부분 클러스터, 테이블로 들어옴, 그 테이블로 들어오기 때문에 Cell Array 학습이 필요함 
- Array에서 기본은 열벡터임, 배열에는 vector가 포함됨
- 위의 예시는 행 array, 행 vector라고 함

![three](/img/MATLAB/Fundamentals/three.png)


- 2차원 배열은 위와 같이 만듬(Array라고 함, 2x2, vector라고 하지 않음)

![four](/img/MATLAB/Fundamentals/four.png)


- 열벡터는 위와 같이 생성됨, 열 array 열 vector
- a=[1 2], a=[1,2], a=[1, 2] 모두 같은 표현임, 스페이스바만 쓰는 것은 element가 많아지면 다 콤마를 쓸 수 없어서

![five](/img/MATLAB/Fundamentals/five.png)
![six](/img/MATLAB/Fundamentals/six.png)


- 수식을 활용하여서 사용할 수도 있고 두 vector를 합쳐서 하나의 vector로 만들 수도 있음 

![seven](/img/MATLAB/Fundamentals/seven.png)
![eight](/img/MATLAB/Fundamentals/eight.png)


- 1~50까지 생성한다고 숫자를 다 일일이 입력해 줄 필요는 없음, 위와 같이 입력해서 만들수도 있음 
- 숫자의 크기를 다르게하여 증가시킬 수도 있음 

![nine](/img/MATLAB/Fundamentals/nine.png)
![ten](/img/MATLAB/Fundamentals/ten.png)

- linspace를 사용하여서 위와 같이 첫 값 끝 값을 알고 몇 개로 나눠야할 지 알 때 사용할 수 있음

![eleven](/img/MATLAB/Fundamentals/eleven.png)


- 숫자를 랜덤하게해서 vector를 생성할 수 있음 nxn을 기준

![twelve](/img/MATLAB/Fundamentals/twelve.png)


- 0 vector도 생성가능함

![thirteen](/img/MATLAB/Fundamentals/thirteen.png)


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
![fourteen](/img/MATLAB/Fundamentals/fourteen.png)


- Row column indexing
- linear indexing과 유사해 보이지만 반드시 콤마를 써야함
- 행이 많을 경우에는 아래와 같이 직접 입력하지 않고 뽑을 수도 있음 
![fifteen](/img/MATLAB/Fundamentals/fifteen.png)
![sixteen](/img/MATLAB/Fundamentals/sixteen.png)


- (:)은 전체를 의미함(all), 아래와 같이 전체 해당 부분을 뽑을 수 있음
![seventeen](/img/MATLAB/Fundamentals/seventeen.png)

- 인덱싱 내에서 아래와 같이 대괄호를 통해서 특정행과 열을 뽑을 수 있음 
![eighteen](/img/MATLAB/Fundamentals/eighteen.png)
![nineteen](/img/MATLAB/Fundamentals/nineteen.png)


- 아래와 같이 특정 부분에 대해서 indexing을 명확하게 위치를 나타내서 뽑을 수 있음 
![twenty](/img/MATLAB/Fundamentals/twenty.png)


- Element 계산
- 덧셈, 뺄셈은 동일하게 처리하면 되나 곱셈의 경우 행렬 곱셈의 정의를 적용함
- 즉 곱셈을 하면 dot product로 행렬의 곱셈의 맞게 변환후 계산을 해야함
![twentyone](/img/MATLAB/Fundamentals/twentyone.png)
![twentytwo](/img/MATLAB/Fundamentals/twentytwo.png)


- 만일 여기서 element간의 곱셈, 나눗셈을 하기 위해서는 아래와 같이 표현함
- element의 의미로 '.'를 사용함
![twentythree](/img/MATLAB/Fundamentals/twentythree.png)


- logical indexing
- 논리적인 조건을 입력해서 인덱싱을 하는 방법
- 아래와 같이 논리적인 조건을 입력하면 a가 10보다 큰 값에 대해서 큰 값인 경우 1, 아닌 경우 0으로 logical array로 나타남
![twentyfour](/img/MATLAB/Fundamentals/twentyfour.png)
![twentyfive](/img/MATLAB/Fundamentals/twentyfive.png)


- 여기서 logical array가 아닌 그 값을 뽑고 싶다면 아래와 같이 해당 값만을 뽑을 수 있음
- 열 기준으로 뽑기 때문에 11 12 13... 순이 아닌 11 16 12 17 ... 순으로 뽑힘
![twentysix](/img/MATLAB/Fundamentals/twentysix.png)


- 여기서 위와 같이 하지 않고 row column값까지 같이 뽑아서 할 수도 있음, 여기서 뽑아낸 값은 linear indexing 값임, 즉 해당 값이 있는 위치를 뜻함 
![twentyseven](/img/MATLAB/Fundamentals/twentyseven.png)


- 할당되는 변수를 row, column이라고 설정하여 찾으면 row와 column number를 알 수 있음
![twentyeight](/img/MATLAB/Fundamentals/twentyeight.png)


- 여기서 합치고 싶다면 array로 다시 합칠 수 있음
- 이를 통해 3행 1열 4행 1열등 한 눈에 볼 수 있음
![twentynine](/img/MATLAB/Fundamentals/twentynine.png)


- 만약 이를 이용해서 조건을 2개 이상 체크해서 확인하기 위해서는 아래와 같이 써야함
![thirty](/img/MATLAB/Fundamentals/thirty.png)


- 여기서 logical indexing을 아래와 같이 써서 답을 구할 수도 있음
![thirtyone](/img/MATLAB/Fundamentals/thirtyone.png)

- 아래와 같이 값을 직접 입력해서 넣을 수 있음
![thirtytwo](/img/MATLAB/Fundamentals/thirtytwo.png)


## Statistical operation
- MATLAB의 문법을 활용하여 값에 대해서 유의미한 값을 직접 추출할 수 있음
- max
- max값을 아래와 같이 추출할 수 있음, 하나만 추출되는 것이 아닌 각각 열에 대한 max값이 추출됨
![thirtythree](/img/MATLAB/Fundamentals/thirtythree.png)


- 여기서 가장 큰 max 값 하나만 추출하려면 아래와 같은 작업을 해야함, 이렇게 되는 이유는 데이터가 기본적으로 하나의 열(feature)에 대해서 나타나는 것이므로 열을 기준으로 하기 때문에 그 열에서의 max 값을 뽑아냄, 각각의 열은 각각 다른 variable이기 때문임
- 예를들어 각각의 feature는 국어, 수학, 영어 점수라면 각각 다른 속성이기 때문에 그 영역에서 max값을 구하는 것임, 그 중 값이 큰 것을 찾는것은 별개의 문제임, 그래서 max 값은 하나의 열에서 작동을 함
![thirtyfour](/img/MATLAB/Fundamentals/thirtyfour.png)


- 하나의 feature에서의 max값과 별개로 max값을 뽑기 위해서는 아래와 같이 처리를 해주면 됨
![thirtyfive](/img/MATLAB/Fundamentals/thirtyfive.png)


- find값과 마찬가지로 max 역시 index 값을 뽑아줄 수 있음
- 아래와 같이 처리한다면 max값과 그 max값이 위치한 열에 대해서 index를 뽑을 수 있음
![thirtysix](/img/MATLAB/Fundamentals/thirtysix.png)


- sort
- sort함수를 통해 아래와 같이 sort를 해 줄 수 있음, 기본적으로 오름차순 방향으로 sorting을 해줌
![thirtyseven](/img/MATLAB/Fundamentals/thirtyseven.png)


- 내림차순으로 하고 싶다면 아래와 같이 입력하게 된다면 내림차순으로 정렬을 함
![thirtyeight](/img/MATLAB/Fundamentals/thirtyeight.png)


- 여기서 단순하게 정렬을 하는 것이 아니라 정렬전 index 순서 역시 아래와 같이 나타낼 수 있음
![thirtynine](/img/MATLAB/Fundamentals/thirtynine.png)


- size, numel, length
- 사이즈의 개수를 체크할 수 있음
- 아래와 같이 행과 열의 개수를 알 수 있음
![fourty](/img/MATLAB/Fundamentals/fourty.png)


- 그리고 총 element의 개수도 체크할 수 있음
![fourtyone](/img/MATLAB/Fundamentals/fourtyone.png)


- 추가적으로 옆으로 변수가 몇 개가 있는지 알 수 있음
- 열이 기본이기 때문에 length는 열을 기준으로 나타냄
![fourtytwo](/img/MATLAB/Fundamentals/fourtytwo.png)


- 위처럼 다양한 사이즈를 체크하는법을 아는 것이 좋음

## Plot
- 다양한 plot을 그릴 수 있음 doc plot을 통해서 더 많은 정보를 알 수 있음
- 아래의 주소를 참고하여 코드와 document를 참고할 수 있음
- https://kr.mathworks.com/products/matlab/plot-gallery.html
- 사용할 데이터는 아래와 같이 excel에 있는것을 MATLAB 외부에서 열기를 통해서 볼 수 있음
![fourtythree](/img/MATLAB/Fundamentals/fourtythree.png)


- 데이터를 불러오는 방법은 다양하게 있음, 테이블 전체 다 불러오는 것, 파일 자체내용을 다 불러올 수 있음, 값들만 array로 불러오는 것도 있음
- 하지만 주로 데이터 사용시 하나하나 variable이 중요함, 기본은 array로 값만을 불러오는 것이지만 variable을 위해서 테이블 전체를 불러올 것임
- 불러오기를 할 때 큰따옴표("")를 권장함, 무조건 쓸 것
- open을 하게 되면 아래와 같이 데이터에 대한 내용이 테이블 전체로 불러와서 나옴
![fourtyfour](/img/MATLAB/Fundamentals/fourtyfour.png)
![fourtyfive](/img/MATLAB/Fundamentals/fourtyfive.png)


- 위와 같이 테이블 형식으로 나오면 데이터를 어떻게 불러올지 UI창으로 열려서 나옴, 옵션을 조정해서 가져올 수 있음
- 해당 창에서 아래와 같이 체크를 한 뒤 설정을 하고 값을 불러온다면 해당 테이블이 2번째와 같이 불러와진 것을 알 수 있음
![fourtysix](/img/MATLAB/Fundamentals/fourtysix.png)
![fourtyseven](/img/MATLAB/Fundamentals/fourtyseven.png)


- 하지만 보통 위와 같이 UI를 통해서 하진 않음, 아래와 같이 체크를 하고 설정을 한 뒤 스크립트 생성을 누른다면 2번째 사진과 같이 해당 테이블을 불러오는데 필요한 코드가 생성됨(범위에서 해당 값에 대한 범위를 파악함), 이를 그대로 복사 붙여넣기해서 사용해도 됨
![fourtyeight](/img/MATLAB/Fundamentals/fourtyeight.png)
![fourtynine](/img/MATLAB/Fundamentals/fourtynine.png)

- 그러므로 데이터를 불러올 때 모르겠으면 open만 알고 있다면 위와 같이 활용할 수 있음
- 그리고 불러올 수 없는 값에 대해서 어떤식으로 처리할지에 대해서도 설정을 아래와 같이 할 수 있음(blank, 특정 숫자로 할 것인지), 비어있는 셀과 char으로 된 셀에 대해서
![fifty](/img/MATLAB/Fundamentals/fifty.png)


- 여기서 테이블 형식으로 불러올 때 굳이 변수 이름 행 5번째라고 써 있는 부분에 대해서까지 체크를 하지 않고 아래와 같이만 체크를 하고 불러오게 된다면 자동으로 변수 이름 행이 5번째줄로 설정했으므로 추가되서 나타남
![fiftyone](/img/MATLAB/Fundamentals/fiftyone.png)
![fiftytwo](/img/MATLAB/Fundamentals/fiftytwo.png)


- 이를 open 형태가 다른 형태로도 불러올 수 있음
- 먼저 xlsread를 통해서 number array형태로 만들고 불러올 수 있음 하지만 권장되는 방식은 아님(시간도 오래걸리고 무겁기 때문에)
![fiftythree](/img/MATLAB/Fundamentals/fiftythree.png)

- 테이블 형태로도 아래와 같이 불러올 수 있음
![fiftyfour](/img/MATLAB/Fundamentals/fiftyfour.png)


- 기본적으로 주석들을 제거를 하짐나 주석의 범위를 설정해줄 수 있음
- 아래와 같이 A:5부터 K:24를 불러오게끔 설정을 2번째 사진과 가팅 할 수 있음
- 여기서 옵션에 대응하는 값은 2번째 사진과 같이 하나씩 대응됨(옵션-값)
![fiftyfive](/img/MATLAB/Fundamentals/fiftyfive.png)
![fiftysix](/img/MATLAB/Fundamentals/fiftysix.png)


- 보고 싶은 데이터를 확인하는 법은 아래와 같이 사용하면 됨
- 하지만 테이블로 설정해서 해당 값이 아닌 해당 테이블 전체가 나옴, 테이블에서 element만 뽑아내기 위해서는 아래와 같이 사용해선 안됨
![fiftyseven](/img/MATLAB/Fundamentals/fiftyseven.png)


- cell을 배우면 더 간단하게 할 수 있지만 테이블에서 데이터만 가져오는 값은 아래와 같이함(테이블 형식이 아닌 element 형태)
- 아래와 같이 보면 테이블이 아닌 element형태로 가져왔음을 알 수 있음, 즉 element만 보기 위해선(.)을 사용하면 됨(. 를 element의 의미로 쓰임)
![fiftyeight](/img/MATLAB/Fundamentals/fiftyeight.png)
![fiftynine](/img/MATLAB/Fundamentals/fiftynine.png)
![sixty](/img/MATLAB/Fundamentals/sixty.png)


- 아래와 같이 데이터를 모은 뒤 plot을 활용할 수 있음, 하지만 NaN 값이 있는 경우 numberic값이 아니어서 plot을 그릴 수 없음, 이 부분을 처리해야함, Numeric값이 있어야함
![sixtyone](/img/MATLAB/Fundamentals/sixtyone.png)


- 여기서 NaN값은 여태까지의 해당 열의 평균값을 집어넣어 줄 것인데 이를 위해서 logical indexing과 isnan메소드를 통해서 NaN인지 파악해야함
- ~ 은 부정을 의미함
![sixtytwo](/img/MATLAB/Fundamentals/sixtytwo.png)
![sixtythree](/img/MATLAB/Fundamentals/sixtythree.png)


- NaN에다가 평균값을 넣을 것인데 여기서 Au에서 아래와 같이 처리한다면 NaN이 아닌 값이 추출이 됨
- 그리고 2번째 사진과 같이 평균을 냄
![sixtyfour](/img/MATLAB/Fundamentals/sixtyfour.png)
![sixtyfive](/img/MATLAB/Fundamentals/sixtyfive.png)


- 그 다음 isnan을 검색한 뒤 해당 부분에 그 값을 넣어주면 됨, 그러면 평균값이 NaN에다가 들어가게됨
![sixtysix](/img/MATLAB/Fundamentals/sixtysix.png)


- 하나씩 차근차근 과정을 밟아나가면서 해도 됨
- plot은 상당히 쉬움 plot을 쓰면 됨, 아래와 같이 나오게 됨
- 원하는 데이터 입력후 여러가지 옵션을 ""와 함께 넣을 수 있음
![sixtyseven](/img/MATLAB/Fundamentals/sixtyseven.png)


- 여기서 위와 같은 plot이 아닌 Year로 바꾸기 위해서는 아래와 같이 작성하면 X축을 바꿀 수 있음
![sixtyeight](/img/MATLAB/Fundamentals/sixtyeight.png)


- 어떤 데이터를 갖고 있는지 명확하게 갖고 있게끔 아래와 같이 처리할 수 있음
![sixtynine](/img/MATLAB/Fundamentals/sixtynine.png)
![seventy](/img/MATLAB/Fundamentals/seventy.png)


- 그리고 색깔도 바꿀 수 있음
![seventyone](/img/MATLAB/Fundamentals/seventyone.png)


- 선을 희미하게 연결하기 위해서 아래와 같이 처리할 수 있음
![seventytwo](/img/MATLAB/Fundamentals/seventytwo.png)


- 여기서 또 새로운 plot을 그릴 때 같이 합쳐서 쓰기 위해서 아래와 같이 처리할 수 있음
![seventythree](/img/MATLAB/Fundamentals/seventythree.png)
![seventyfour](/img/MATLAB/Fundamentals/seventyfour.png)


- 여기서 다른 plot으로 그리고 싶다면 아래와 같이 해제를 할 수 있음
- hold on, off 사용함
![seventyfive](/img/MATLAB/Fundamentals/seventyfive.png)


- 여기서 추가적으로 figure 명령어를 사용해서 연산속도를 빠르게 할 수 있음, 자동화, 알고리즘 등 실행속도를 즉 메모리 공간을 확보할 수 있음
![seventysix](/img/MATLAB/Fundamentals/seventysix.png)


- 그냥 스크립트에서 쓸 경우 새로운 창이 뜸
![seventyseven](/img/MATLAB/Fundamentals/seventyseven.png)


- 위와 같이 다양한 옵션을 사용할 수 있음
- 추가적으로 그래프의 legend, x,y축 표시등을 처리할 수 있음 
- 먼저 title을 달 수 있음
![seventyeight](/img/MATLAB/Fundamentals/seventyeight.png)


- 여기서 추가적으로 폰트크기, 색깔등 다양한 옵션을 사용할 수 있음
![seventynine](/img/MATLAB/Fundamentals/seventynine.png)


- label 설정도 추가할 수 있음 
![eighty](/img/MATLAB/Fundamentals/eighty.png)


- limit도 바꿀 수 있음, 즉 1~8 범위를 바꿀 수 있음
![eightyone](/img/MATLAB/Fundamentals/eightyone.png)


- 이러한 설정은 plot을 다 그린 다음에 데코레이션 같은 느낌임
- 그리고 legend 즉, 범례를 아래와 같이 추가할 수 있음
![eightytwo](/img/MATLAB/Fundamentals/eightytwo.png)


- 하지만 legend가 아래와 같이 값을 가리는 경우가 생기는데 2번째 사진 이후처럼 위치를 바꿔줄 수 있음
![eightythree](/img/MATLAB/Fundamentals/eightythree.png)
![eightyfour](/img/MATLAB/Fundamentals/eightyfour.png)
![eightyfive](/img/MATLAB/Fundamentals/eightyfive.png)
![eightysix](/img/MATLAB/Fundamentals/eightysix.png)


- 하나의 plot의 여러개를 그리되 겹치지 않게 아래와 같이 테이블 형태로 그릴 수도 있음(Subplot)
![eightyseven](/img/MATLAB/Fundamentals/eightyseven.png)

- 여기서 각각 title, legend, label등을 붙이고 설정할 수 있음
![eightyeight](/img/MATLAB/Fundamentals/eightyeight.png)


- 그 수치를 비교하기 위해서 lim을 동일하게 해주는 것이 일반적임, 같은 scale에서 비교를 해주기 때문에 subplot이라도 각각 lim을 동일하게 줘서 활용을 하여 비교를 함

## Logical operator & Functions
- Logical operator는 위에서 실습함 find함수와 isnan함수가 해당됨
- web(fullfile(docroot, "matlab/logical-operations.html"))을 통해서 해당 내용을 자세하게 알 수 있음
![eightynine](/img/MATLAB/Fundamentals/eightynine.png)


- Short-Circuit은 많이 접한 개념이지만 Array에서는 쓰이지 않음, 머신러닝에서는 Array 데이터를 사용하므로 Short-Circuit은 많이 사용 안하고 일반 Logical Operator를 많이 사용함
- any함수 -> 어떤 array가 nonzero인지, 0값이 하나라도 있는지 묻는 값, 0이 하나라도 있으면 0 반환함, 그게 아니면 1 반환
![ninety](/img/MATLAB/Fundamentals/ninety.png)


- 만일 그냥 any(gasprices)를 할 경우 에러가 뜸, 데이터를 보고 다룰 때는 테이블 형식으로 다루지만 데이터 프로세싱을 할 때(실제 numeric 데이터를 다룰 때)에는 테이블 데이터에서 array만을 가지고 사용하기 때문임(직접 사용해야함)
- Numeric Data가 아닌 경우는 Cell Array에서 다룸
- all함수 -> 모든 element가 0이 아닌지 묻는 것 0이 아니면 1값 반환 모두 element가 0이면 0반환
![ninetyone](/img/MATLAB/Fundamentals/ninetyone.png)


- 이를 응용해서 아래와 같이 쓸 수 있음 아래와 같이 쓰면 Germany의 값이 France보다 큰 값이 하나라도 있다면 0을 출력함 해당 조건이 맞지 않으므로
- 이 기준은 같은 observation에 대해서만 비교함, 즉 1번째는 1번째끼리 2번째는 2번째끼리 비교하는 것임
![ninetytwo](/img/MATLAB/Fundamentals/ninetytwo.png)


- 여기서 실제 표상에서 1행부터 12행까지 France가 더 크므로 아래와 같이 코드를 변경하여서 값이 달라질 수 있음
![ninetythree](/img/MATLAB/Fundamentals/ninetythree.png)
![ninetyfour](/img/MATLAB/Fundamentals/ninetyfour.png)


- 추가적으로 any 역시 응용할 수 있음, 아래와 같이 쓴다면 큰 값이 하나라도 있기 때문에 1을 반환함
![ninetyfive](/img/MATLAB/Fundamentals/ninetyfive.png)
![ninetysix](/img/MATLAB/Fundamentals/ninetysix.png)


- 여기서 단순하게 아래와 같이 코드를 짠다면 그 값을 비교했을 때 해당 조건이 맞는 경우 1 아닌 경우 0으로 나타나서 array로 쭉 나타남(하나하나를 비교)
- 위에서 봤듯이 1~12는 더 크므로 1로 나머지는 0이 나옴
![ninetyseven](/img/MATLAB/Fundamentals/ninetyseven.png)



- nnz -> 0이 아닌 개수를 카운터함
- 12개가 나옴 크기 비교상 1~12까지 더 커서 1이므로 12개임
![ninetyeight](/img/MATLAB/Fundamentals/ninetyeight.png)



## Cell Array
- CarSpec에 관한 데이터 테이블임, 여러가지 데이터가 혼재되어 있음
- 테이블 클래스는 기본적으로 문자형 데이터를 쓸 수 없으나 하나의 방법으로 문자형 데이터를 숫자형과 같이 아래와 같이 Make Model 아래 값을 넣을 수 있음, Cell Array로 이해해도 괜찮음
![ninetynine](/img/MATLAB/Fundamentals/ninetynine.png)


- 아래와 같이 테이블로 불러올 수 있음
![onehun](/img/MATLAB/Fundamentals/onehun.png)

- 아래처럼 그 값을 불러올 수 있음
![onehunone](/img/MATLAB/Fundamentals/onehunone.png)


- 여기서 문자형의 경우 EngineSize처럼 element 값이 뜨는 것이 아닌 중괄호 표시가 포함되어 있음, 이것이 Cell Array임
- 테이블은 숫자형만을 다룸, 여기서 그러면 아래와 같은 형식으로 문자가 들어감 즉, Cell이라는 공간에 문자가 들어가고 거기서 101이라고 해당하는 값이 그대로 Make의 1번째 부분에 들어가게 되는것임, C언어에서 포인터의 개념과 유사함
- 문자형 데이터는 직접적으로 들어가지 않고 해당 주소넘버가 들어가서 그 데이터를 볼 수 있음, 여기서 주소넘버는 알 수 없음, 그래서 문자형이 마치 숫자형처럼 위처럼 중괄호에 묶여서 나타남
- 숫자도 Cell 형태로 넣을 수 있음, 그리고 아예 다른 Array를 통째로 넣을 수 있음
- 결과적으로 형태는 {}(중괄호)안에 나타난 형태로 나옴
![onehuntwo](/img/MATLAB/Fundamentals/onehuntwo.png)
![onehunthree](/img/MATLAB/Fundamentals/onehunthree.png)


- 여기서 plot을 응용할 수 있음, 그냥 plot을 쓴다면 선형이더라도 아래와 같은 형태로 나타남
![onehunfour](/img/MATLAB/Fundamentals/onehunfour.png)


- 위와 같은 형태는 알아볼 수 없기 때문에 분포로써 나타내기 위해서 scatter를 쓸 수 있음, 머신러닝에서 grouping할 때 많이 씀
![onehunfive](/img/MATLAB/Fundamentals/onehunfive.png)
![onehunsix](/img/MATLAB/Fundamentals/onehunsix.png)


- element 계산을 통해서 정규화를 할 수 있음, 여기서 그 값을 위해 matrix 나누기인 요소 나누기는 아래와 같이 시행하면 됨
![onehunseven](/img/MATLAB/Fundamentals/onehunseven.png)


- 아래와 같이 코드를 치게 된다면 새로운 부분을 추가하여서 해당 계산값을 집어넣을 수 있음(Variable 생성)
![onehuneight](/img/MATLAB/Fundamentals/onehuneight.png)


- 최대값을 찾을 수 있음, 여기서 index number observation도 알 수 있음(13번째의 최대값 존재)
![onehunnine](/img/MATLAB/Fundamentals/onehunnine.png)


- 아래와 같이 코드를 친다면 cell형태로 나오게 됨(table처럼 나옴)
![onehunten](/img/MATLAB/Fundamentals/onehunten.png)


- 여기서 idx를 활용하여서 코드를 사용하면 table형태가 아닌 cell array형태로 나옴, cell에 갇힌 상태에서 cell을 통째로 가져옴
![onehuneleven](/img/MATLAB/Fundamentals/onehuneleven.png)


- 여기서 그냥 문자열 자체만을 뽑고 싶다면 아래와 같이 {}를 활용하여 값을 뽑으면 문자열만 나오게 됨
![onehuntwelve](/img/MATLAB/Fundamentals/onehuntwelve.png)


- CarSpecs에서 하나의 row를 조건을 걸어서 아래와 같이 정렬을 할 수 있음
- 그러면 PtW을 기준으로 기존의 CarSpecs라는 Table이 내림차순 정렬이 된 byPtW가 생성됨
![onehunthirteen](/img/MATLAB/Fundamentals/onehunthirteen.png)
![onehunfourteen](/img/MATLAB/Fundamentals/onehunfourteen.png)


- 그리고 정렬한 값을 볼 수 있음, 아래와 같이 코드를 활용하여 정렬 기준 1~5의 순위에서 1,2,end 즉 Make행, Model행, PtW행을 뽑아서 나타낼 수 있음
![onehunfifteen](/img/MATLAB/Fundamentals/onehunfifteen.png)



- 다양한 방식으로 나타낼 수 있음
![onehunsixteen](/img/MATLAB/Fundamentals/onehunsixteen.png)
![onehunseventeen](/img/MATLAB/Fundamentals/onehunseventeen.png)


- 다양한 방식을 활용해서 직접 해보는 것이 좋음, 여기서 자동으로 sorting을 하고 복잡하게 꼬여있을 경우 Variable Name만을 가지고 뽑아서 하는 경우가 필연적으로 생기게 됨
![onehuneighteen](/img/MATLAB/Fundamentals/onehuneighteen.png)

- 여기서 머신러닝 모델만을 가지고 모델을 뽑아내서 그 모델을 가지고 다른 모델을 비교할 때는 첫번째 방법으로 충분하지만 완전 자동화 형태에서 데이터는 테이블 형태로 받아오게 되는데 column의 name위치가 어디에 있을지 모르고 그에 따라 길이도 달라지기 때문에 그 상황에선 뒤죽박죽하게 되는데 여기서 변수명은 바뀌지 않기 때문에 변수명으로 뽑아서 활용하는 측면이 더 나을 수 있음(비지도학습과 클러스터링을 하여서)
- table도 cell과 똑같이 생각해도 됨
- 그러면 아래와 같이 그 값을 볼 때 원래는 테이블로 나오지만 아래와 같이 처리를 하여 그 값 자체를 {}를 활용하여 뽑을 수 있음
![onehunnineteen](/img/MATLAB/Fundamentals/onehunnineteen.png)

