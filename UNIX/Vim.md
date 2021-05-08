## Vim

### 텍스트 에디터 Vim
- CLI 환경에서 사용할 수 있는 에디터는 Vim임
- 키보드로만 사용해야함, CLI에서 가장 보편적인 에디터임

### Vim의 4가지 사용 모드

![one](/img/UNIX/Vim/one.png)

- 어떤모드에 있는지에 따라 다르게 해석됨

![two](/img/UNIX/Vim/two.png)

- 3가지 모드에서 하나의 모드로 갈때는 항상 일반모드를 거쳐서 가야함

### Vim 입력 모드
- vim을 입력하면 아래와 같이 실행할 수 있음
- 가장 처음은 일반모드임

![three](/img/UNIX/Vim/three.png)

- i를 누르면 아래와 같이 입력모드로 바뀜

![four](/img/UNIX/Vim/four.png)
![five](/img/UNIX/Vim/five.png)

- esc를 누르면 다시 일반모드로 돌아감
- 다시 입력모드로 갈 때 a키를 누르면 커서가 한 칸 뒤로 간 뒤 입력모드로 바뀜

![six](/img/UNIX/Vim/six.png)

- 맨 앞에 커서를 옮기고 입력모드로 바꾸기 위해서는 대문자 I를 사용해서 할 수 있음
- 한 번에 맨 마지막으로 가는 것은 대문자 A를 사용해서 커서가 맨 뒤로 가고 입력모드로 바꿈
- 소문자 o(open)를 누르면 커서를 다음 줄로 옮기고 입력 모드로 전환함
- 대문자 O 사용시 문장이 있는 기준으로 아래와 같이 처리되고 입력모드가 됨

![seven](/img/UNIX/Vim/seven.png)
![eight](/img/UNIX/Vim/eight.png)

### Vim 명령 모드
- 명령모드로 가기 위해서는 :(콜론) 키를 입력해야함

![nine](/img/UNIX/Vim/nine.png)

- 명령모드에서 저장을 할 수 있음 w(write)를 이용해서 저장할 수 있음

![ten](/img/UNIX/Vim/ten.png)
![eleven](/img/UNIX/Vim/eleven.png)

- 위처럼 저장이 된 것임 위의 뜻은 5줄의 121개의 글자가 저장됨을 의미함
- 여기서 나가려면 명령모드에서 q를 입력해서 나갈 수 있음

![twelve](/img/UNIX/Vim/twelve.png)
![thirteen](/img/UNIX/Vim/thirteen.png)

- 저장한 exercise 파일도 존재함

![fourteen](/img/UNIX/Vim/fourteen.png)

- 여기서 vim을 통해서 해당 파일을 다시 열 수 있음

![fifteen](/img/UNIX/Vim/fifteen.png)
![sixteen](/img/UNIX/Vim/sixteen.png)

- 아래와 같이 입력모드에서 추가한 내용을 저장하기 위해서는 입력모드에서 일반모드로 넘어간 다음 명령모드로 가야함 즉 아래의 상태에서 esc를 눌러 일반모드로 간 뒤 콜론을 통해서 명령 모드로 넘어가서 저장해야함

![seventeen](/img/UNIX/Vim/seventeen.png)
![eighteen](/img/UNIX/Vim/eighteen.png)
![nineteen](/img/UNIX/Vim/nineteen.png)

- 여기서 지금 저장할 때는 굳이 파일명을 안해줘도 됨 이미 저장하였으므로

![twenty](/img/UNIX/Vim/twenty.png)
![twentyone](/img/UNIX/Vim/twentyone.png)

- 이제 저장과 동시에 Vim을 끄는 방법은 아래와 같음

![twentytwo](/img/UNIX/Vim/twentytwo.png)

- 만일 아래와 같이 작성한 문장을 반영하지 않고 처리하기 위해서 그냥 종료를 하면 에러메시지와 함께 반영이 안됨
- 여기서 반영을 하지 않고 그냥 종료하기 위해서는 느낌표를 써야함

![twentythree](/img/UNIX/Vim/twentythree.png)

- 반영이 안되고 저장됨을 알 수 있음

![twentyfour](/img/UNIX/Vim/twentyfour.png)

- 명령모드에서 텍스트 검색을 하기 위해서는 /(슬래시) 키를 통해서 명령모드로 가고 텍스트 검색을 해야함
- 그러면 찾고자 하는 단어에 첫번째 문자에 가게됨
- 여기서 그 다음 내용을 검색하기 위해서 n을 누르면 그 다음 검색 내용으로 이동함

![twentyfive](/img/UNIX/Vim/twentyfive.png)
![twentysix](/img/UNIX/Vim/twentysix.png)

- 여기서 대문자 N을 입력하게 되면 이전 검색 내용으로 이동함

![twentyseven](/img/UNIX/Vim/twentyseven.png)

- 텍스트 치환 모드가 존재함 특정 텍스트를 다른 텍스트로 바꾸는 기능임, 콜론 키로 명령모드로 가고 s(subtitute) 명령어 사용함
- 아래와 같이 처리한다면 첫번째 줄에 있는 like를 찾아서 love로 바뀌게 됨

![twentyeight](/img/UNIX/Vim/twentyeight.png)

- 모든 단어를 바꾸기 위해서는 % 기호를 씀 그 범위를 파일 전체로 하는것을 의미함

![twentynine](/img/UNIX/Vim/twentynine.png)
![thirty](/img/UNIX/Vim/thirty.png)

- 하지만 첫번째 단어만이 love로 바뀌고 두 번째 단어는 바뀌지 않음, 이 모든것을 바꾸기 위해서는 옵션을 활용해야함

![thirtyone](/img/UNIX/Vim/thirtyone.png)
![thirtytwo](/img/UNIX/Vim/thirtytwo.png)

- 여기서 특정 #만 바꾼다면 바꾸지 않을 것과 바꿀 것을 확인해야함
- 여기서 c는 confirm을 의미함, 사용자가 바꿀 것에 대해서 하나씩 확인하면서 바꾸게 됨
- 그러면 아래와 같이 하나씩 하나씩 확인하면서 바꿀 수 있음

![thirtythree](/img/UNIX/Vim/thirtythree.png)
![thirtyfour](/img/UNIX/Vim/thirtyfour.png)

### Vim 일반모드
- 일반모드에서 커서를 이동하려면 키보드에 방향키를 이동하는 방법과 알파벳키를 통해서 이동할 수 있음

![thirtyfive](/img/UNIX/Vim/thirtyfive.png)

- 내가 원하는 칸 수만큼 해당 방향으로 이동하기 위해서 아래와 같이 숫자 + 알파벳키를 사용하면 됨

![thirtysix](/img/UNIX/Vim/thirtysix.png)

- 여러 줄 이동시 현재 커서가 어디에 있는지 아는게 중요함
- 컨트롤 g키를 통해서 어디에 위치하는지 아래와 같이 알 수 있음

![thirtyseven](/img/UNIX/Vim/thirtyseven.png)

- 숫자 0을 누르면 커서가 그 줄의 첫 번째 칸으로 가고 $ 표시를 누르면 커서가 그 줄의 마지막 칸으로 이동함
- 파일의 맨처음으로 가려면 gg를 입력하면 됨 마지막 줄로 가기 위해서는 대문자 G를 입력함
- 수정을 위해서 일반모드에서 커서를 빨리 움직이는걸 알아야함
- 텍스트 삭제는 x를 삭제하면 됨

![thirtyeight](/img/UNIX/Vim/thirtyeight.png)

- 여러 칸을 한 번에 삭제하기 위해서는 숫자 + x를 쓰면 됨

![thirtynine](/img/UNIX/Vim/thirtynine.png)

- 줄단위, 문장 통째로 삭제하기 위해서는 소문자 dd를 누르면 됨
- 여러 문장을 삭제하기 위해서는 숫자 + dd를 누르면 됨
- 만일 삭제한것을 복구하기 위해서는 이전 작업을 취소하는 소문자 u(undo)를 누르면 이전 작업을 취소할 수 있음

![fourty](/img/UNIX/Vim/fourty.png)

- 어떤 작업을 하기 이전상태로 돌아갈 수 있음

### Vim 비주얼 모드
- 원하는 영역만큼 텍스트 블록 지정이 가능함 v를 눌러서 들어갈 수 있음, 방향키를 누르면 원하는 만큼 블록을 지정할 수 있음

![fourtyone](/img/UNIX/Vim/fourtyone.png)

- 블록 지정을 통해서 해당 텍스트를 삭제, 복사-붙여넣기, 잘라내기를 할 수 있음
- 아래와 같이 x를 통해서 삭제를 할 수 있음, 삭제 이후 일반모드로 변함

![fourtytwo](/img/UNIX/Vim/fourtytwo.png)

- 복사-붙여넣기도 할 수 있음, 복사를 위해서 소문자 y(yank)키를 누름
- 복사를 하면 자동으로 일반모드로 감

![fourtythree](/img/UNIX/Vim/fourtythree.png)

- p(paste)를 통해서 복사한 내용을 붙여넣기 할 수 있는데 소문자 p의 경우 커서 다음 칸에 붙여넣고 대문자 P의 경우 커서 이전 칸에 붙여넣음
- 소문자 p

![fourtyfour](/img/UNIX/Vim/fourtyfour.png)

- 대문자 P

![fourtyfive](/img/UNIX/Vim/fourtyfive.png)

- 그 다음 대문자 V를 누르면 줄 단위로 블록 지정을 할 수 있음, 방향키로 해도 무조건 줄단위로 지정됨

![fourtysix](/img/UNIX/Vim/fourtysix.png)

- 잘라내기도 유사함, 여기서 아래와 같이 지정하고 d(delete)를 누르면 해당 문장이 삭제됨, 하지만 Vim은 삭제된 문장을 일시적으로 기억함, 그래서 다른 위치로 이동한 다음에 붙여넣기를 하면 잘라내기가 됨, 붙여넣기는 p를 이용함

![fourtyseven](/img/UNIX/Vim/fourtyseven.png)
![fourtyeight](/img/UNIX/Vim/fourtyeight.png)
![fourtynine](/img/UNIX/Vim/fourtynine.png)

