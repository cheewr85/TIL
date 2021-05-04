## DataProcessing
- 저장되어 있는 Data를 바탕으로 해당 정보를 가공 활용함
- 농구선수들의 스탯과 정보를 활용
![one](/img/MachineLearning/Data/one.png)
![two](/img/MachineLearning/Data/two.png)

- Variable을 추가해 FullName을 만들 것
- UseFirst가 비어있는 경우가 있는데 여기서 UseFirst를 채우고 FirstName과 LastName을 합쳐서 FullName을 만들고 새로운 Variable을 생성해서 저장함
- FirstName을 추출해서 저장, 비어있는 선수들 존재
![three](/img/MachineLearning/Data/three.png)

- 여기서 비어있는 선수들을 채워주기 위해서 indexing을 활용하여 idx에 저장함, 여기서 이름이 있는 선수들은 0, 없는 선수들은 1로 logical array 형태로 저장됨
![four](/img/MachineLearning/Data/four.png)

- 여기서 idx에 비어있는 선수를 찾아둠, 그 다음 firstname(idx)를 통해 비어있는 칸 추출, {}는 cell일 때 사용
![five](/img/MachineLearning/Data/five.png)

- 그 칸을 playerinfo에서 firstname을 채우면 됨. useFirst를 채우기 위한 작업
- 테이블 내에서 변환이 가능하지만 변수를 위와 같이 바깥으로 빼고 여러 함수를 적용시켜서 응용함
- Cell에서 통하지 않는 함수들이 있기 때문에, 비어있으면 FirstName의 똑같은 index number를 넣어서 그 값을 넣어주면 됨
- 이를 통해 비어있는 칸을 채움
![six](/img/MachineLearning/Data/six.png)

- 여기서 fullname 사용시 strcat 즉 수평적으로 합치는 것을 활용함
- firstname은 변수를 통해 lastname은 별도로 추출하지 않았으므로 playerinfo 자체를 활용
![seven](/img/MachineLearning/Data/seven.png)

- 하지만 이름은 중간에 띄어주니깐 그 부분을 추가함, Cell이므로 중괄호를 쓰고 중간에 띄어쓰기를 통해 아래와 같이 활용하면됨, Cell이므로 빈공간을 Cell로 만들어야함
![eight](/img/MachineLearning/Data/eight.png)

- fullname을 last column에 추가하면 됨, 해당 데이터가 새롭게 추가됨
![nine](/img/MachineLearning/Data/nine.png)

- playerinfo에서 height와 weight 데이터를 가져올 것임
- 아래와 같이 모든 데이터를 테이블 형태로 추출함
![ten](/img/MachineLearning/Data/ten.png)

- 테이블도 큰 형태의 Cell로 볼 수 있음, Cell에서 그 안에 내용만 가져올 때는 아래와 같이 Cell 표시를 활용하여 array형태로 가져옴
![eleven](/img/MachineLearning/Data/eleven.png)

- 여기서 playerinfo에서 필요한것만 사용할것임, 그래서 아래와 같이 처리를 해서 필요한 데이터만 가져와서 playerinfo를 대체할 수 있음, 위에서 사용한 데이터가 덮어씌어져서 새롭게 추출함
![twelve](/img/MachineLearning/Data/twelve.png)

- 여기서 array형태로 덮어씌울 수 있는지 확인을 해보면
![thirteen](/img/MachineLearning/Data/thirteen.png)

- 실행이 안됨을 알 수 있음, 위에서 height_weight 와는 다르게 데이터 type이 다르므로 저장을 할 수 없는것임, 다른 데이터형을 합칠 수 없음, array형태는 반드시 double형만을 가지고 있어야하므로 불가능함

- stats데이터중 1990년 이후의 값만을 가져올 것인데, idx로 저장시 아래와 같이 1990이후인 값에 대해서는 1, 아닌 값은 0으로 logical array로 저장됨
![fourteen](/img/MachineLearning/Data/fourteen.png)

- 여기서 1990이후인 선수들만 필요하므로 그 값을 바꿔두면 아래와 같이 갱신됨을 알 수 있음
![fifteen](/img/MachineLearning/Data/fifteen.png)

- 실제로는 raw data를 그대로 둔 상태에서 다른 변수 name을 사용함, 위와 같은 방식으로 처리하진 않음
- stats에서 postseason 데이터 24~42 column을 삭제할 것임
![sixteen](/img/MachineLearning/Data/sixteen.png)


- 이를 통해 stats에서 postseason 데이터는 다 [], 즉 void 처리 다 날려버림
![seventeen](/img/MachineLearning/Data/seventeen.png)

- Categorical data는 위의 데이터에서는 position이 될 수 있음, 즉 C,P,F 각각의 포지션
- 여기서 하나만 있는것이 아닌 C-F등 같이 뛸 수 있는 값도 있음
- 이것은 단순한 문자열인데 이것을 의미있는 데이터로 만들 수 있음
![eighteen](/img/MachineLearning/Data/eighteen.png)

- 여기서 pos을 categorical하게 바꿀 수 있음
![nineteen](/img/MachineLearning/Data/nineteen.png)

- 여기서 위와 비교를 해보면 문자열을 의미하는 ('')가 사라짐, 'F-C'->F-C
- 이것은 문자열이 아닌 Categorical이라고 함, 여기서 Categorical로 바꾼다는 것은 남성/여성을 예를 들면 그 데이터 자체가 남성/여성으로 분류를 할 수 있게됨
- 즉 Category, class를 나누는 것임, 의미없는 문자를 Male/Female로 나눴다는 것
- 이렇게 Categorical하게 어떻게 바뀌었는지 보게 된다면 아래와 같이 구분됨을 알 수 있음
- 모든 데이터가 12개의 카테고리로 나뉘어져 있음을 알 수 있음
![twenty](/img/MachineLearning/Data/twenty.png)

- 여기서 category가 2개가 의미가 없다고 생각하고 강제로 변환을 시킨다면 아래와 같이 바꿀 수 있음
- 왜 이런식으로 하냐면 아주 정형화된 잘 정돈된 데이터를 활용한다고 할 때 카테고리가 우리가 가지고 있는 데이터가 같지 않을 경우 이를 그 잘 정돈된 데이터에 변환하기 위해서 카테고리를 강제로 변환해야하는 경우도 있음
- 여기서 아래와 같이 positions의 7개의 category로 변환하게 되는 경우 이에 해당되지 않는 경우도 있는데 이는 그냥 버리는 것으로 처리를 함
![twentyone](/img/MachineLearning/Data/twentyone.png)

- 하지만 여기서 강제로 그 category를 바꾸면 아래와 같이 이에 해당되지 않는 경우는 undefined가 됨
![twentytwo](/img/MachineLearning/Data/twentytwo.png)

- 여기서 아래와 같이 다시 category를 확인하면 7개의 category만이 있는것을 알 수 있음(undefined 제외)
- 여기서 undefined는 삭제하도록 할 것임
![twentythree](/img/MachineLearning/Data/twentythree.png)


- 그전에 stats 데이터를 정리를 할 것임, 원하는 데이터만을 갖게끔 더 줄일 것임
- 데이터가 확 줄어듬
![twentyfour](/img/MachineLearning/Data/twentyfour.png)

- 대부분의 데이터들이 Time을 기반으로 되어 있는데 이것을 사람당으로 아래와 같이 Time기반을 바꿀 수 있음
- Time 기반이므로 Id가 중복되서 나타남
![twentyfive](/img/MachineLearning/Data/twentyfive.png)

- 이를 grouping을 할 수 있음, 여기서 아래와 같이 처리한다면 playerID를 기준으로 grouping하여서 활용할 수 있음, 아래는 평균값을 의미함
- stats에서 동일한 playerID를 합쳐서 mean값을 아래와 같이 구함
![twentysix](/img/MachineLearning/Data/twentysix.png)

- 아래와 같이 sum을 구함, 여기서 @sum을 활용해도 됨
![twentyseven](/img/MachineLearning/Data/twentyseven.png)

- 여기서 100game 미만을 제거할 것임, idx 즉 sum_GP가 100미만인 값을 logical array로 저장해둔다음, 이 부분을 void 처리를 하여 없애면 아래와 같이 나오게 됨
- 위의 데이터와 비교한다면 100 미만의 값이 싹 사라짐, 노이즈로 간주해서 없앰
- 최소한의 기준을 잡아야하기 때문에 없앰, groupCount 역시 없앨 것임
![twentyeight](/img/MachineLearning/Data/twentyeight.png)

- 여기서 sum_이 꼭 필요한 값은 아님, 이 부분을 지울 것임
- 여기서 새로운 부분은 stats를 쓰게 되면 그 밑의 다양한 변수들이 나오게 되는데 이 중에서 해당 특성과 VariablesName을 입력하면 아래와 같이 해당 Name이 쭉 나오게 됨, VariableName을 뽑을 수 있음
![twentynine](/img/MachineLearning/Data/twentynine.png)

- 여기서 이렇게 뽑은 name에서 sum을 아래와 같이 교체할 것임
![thirty](/img/MachineLearning/Data/thirty.png)

- playerinfo는 bioID와 totalstats등 연도별로 구분을 함, 여기서 bioID와 playerID가 다른 변수지만 내용이 같음, 이 두 데이터를 합치는데 유의미한 방법을 활용할 수 있음
- innerjoin -> 두 개의 데이터 그룹에서 교집합을 찾아서 교집합에 쭉 이어붙여 주는 것임, 교집합에 포함되지 않은 것은 날아감
- outerjoin -> 합집합의 의미
- 아래와 같이 bioID와 playerID가 같은 교집합 부분에서 data를 저장함
- 아래와 같이 data를 이와 관련되게 쭉 합쳐놓음, playerinfo는 5061 totalstats 1117의 데이터를 가지고 있었음, 이를 합치게 되면 data는 1117이 됨
![thirtyone](/img/MachineLearning/Data/thirtyone.png)

- 이제 그 둘을 스무스하게 합쳐서 모든 데이터가 들어가 있으므로 missing data를 삭제할 것임(undefined와 같은 데이터)
- 여기서 각 열당 missing data의 합을 구할 수 있음
![thirtytwo](/img/MachineLearning/Data/thirtytwo.png)

- 여기서 missingdata에서 rmmissing 즉, missingdata를 remove하는 함수를 활용하여 할 수 있음
![thirtythree](/img/MachineLearning/Data/thirtythree.png)

- 하지만 여기서 undefined 먼저 찾은 뒤 이를 data에서 삭제하는 로직을 아래와 같이 활용할 수 있음
- 아래의 undefined가 사라지게 할 것임
![thirtyfour](/img/MachineLearning/Data/thirtyfour.png)

- 아래의 로직을 활용하여 undefined가 사라짐을 알 수 있음
![thirtyfive](/img/MachineLearning/Data/thirtyfive.png)

- rmmissing을 활용해도 됨

- Explore data 즉, visualization을 하여 데이터를 볼 수 있음
- 아래와 같이 boxplot을 통해서 data.pos를 기준으로 height에 대해서 아래와 같은 형태로 데이터를 전체적으로 볼 수 있음
![thirtysix](/img/MachineLearning/Data/thirtysix.png)

- 여기서 scatter에서 rebounds를 나타내지만 points도 같이 나타냄
- 하지만 동시에 나오므로 큰 차이가 없음
![thirtyseven](/img/MachineLearning/Data/thirtyseven.png)

- 추가적으로 data position으로 나누어서 rebounds오 points를 구분할 수 있음, categorical을 활용하여 알아서 나누어줌, x는 rebounds, y는 points 알아서 gscatter를 하여 position 별로 구분할 수 있음
![thirtyeight](/img/MachineLearning/Data/thirtyeight.png)

- 여기서 좀 더 의미있게 나눌 필요가 있음, Guard는 사실상 Rebounds의 개념이 크게 작용하지 않으므로
- Normalizing, 정규화 즉, 의미있는 데이터로 나눈다는 것인데, 어떠한 의미이냐면 쉬운 국어시험 90점과 어려운 수학시험 90점은 동일선상에서 보기 힘듬, 이를 의미있게 구분하기 위해서 정규화를 시킴
- 여기서 데이터를 총 리바운드, 총 포인트는 큰 의미가 없음, 즉 GamePlayed에 따라서 나누면 그만큼의 효율을 체크함
- 이 scatter를 보면 player한 게임수와 각 data를 나눈것이 큰 차이가 없음, 즉 큰 의미가 있다고 볼 수 없음, 게임 played 수는 큰 의미가 없음
![thirtynine](/img/MachineLearning/Data/thirtynine.png)

- 그렇다면 뛴 시간만큼으로 변환해서 체크를 해볼 수 있음, 분당 득점, 분당 리바운드로 계산
- 조금 더 Guard, Center등의 분기점이 의미있게 나뉘어져 있음
![fourty](/img/MachineLearning/Data/fourty.png)

- Normalizing, 정규화, 일반적인 방법은 평균과 표준편차가 나와 있고 평균은 0, 표준편차는 1로 즉 쉬운 국어 90 어려운 수학 90에서 같은 동일선상에서 비교하기 위해 Normalizing을 함
- statsnorm을 통해서 데이터를 동일선상에서 볼 수 있게끔 표준 정규화를 시킴, 아래와 같이
![fourtyone](/img/MachineLearning/Data/fourtyone.png)
