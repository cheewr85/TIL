### course 테이블과 review 테이블 만들기
- 각각 course, review 테이블에 대한 내용을 채워서 만듬
```sql
CREATE TABLE course_rating.course (
		id INT NOT NULL AUTO_INCREMENT,
		title VARCHAR(30) NULL,
		semester VARCHAR(6) NULL,
		maximum INT NULL,
		professor VARCHAR(10) NULL,
		PRIMARY KEY(id)
);
```
```sql
CREATE TABLE course_rating.review (
		id INT NOT NULL AUTO_INCREMENT,
		course_id INT NULL,
		star INT NULL,
		comment VARCHAR(500) NULL,
		PRIMARY KEY(id)
);
```

### course 테이블과 review 테이블 채워넣기
- INSERT INTO 문을 가지고 채워넣으면 됨
- 각각 필요한 값에 맞춰서 붙여넣으면 됨

### Foreign Key가 필요한 이유
- Foreign Key란 한 테이블의 컬럼 중에서 다른 테이블의 특정 컬럼을 식별할 수 있는 컬럼을 말함
- Foreign Key로 다른 테이블의 Primary Key를 참조한다고 표현함
- Foreign Key가 있는 테이블을 자식 테이블이나 참조하는 테이블이라고 하고 참조당하는 테이블을 부모 테이블, 참조당하는 테이블이라고 함

### Foreign Key 설정하기
- Foreign Key 설정은 토픽 1에서 한 것과 같음
- 추가적으로 On Update, On Delete 설정을 할 수 있음

### SHOW CREATE TABLE문으로 현재 테이블 어떻게 만들 수 있는지 보기
- 특정 테이블을 지금 바로 생성한다고 할 때 작성해야할 CREATE TABLE문이 뭔지를 보여줌
- 현재 상태의 테이블을 만들려면 CREATE TABLE문을 어떻게 써야하는지 바로 알 수 있음

### Foreign Key로 보장되는 참조 무결성
- 존재하지 않는 값을 추가될 일이 없게끔 방지할 수 있음

### 부모 테이블의 row가 삭제될 때 - RESTRICT 정책
- 그 row를 참조하는 자식 테이블이 부모 테이블이 삭제되면 애매하게 남아버림
- 이 부분의 처리를 고민해야함, 단 정답은 없지만 정책을 통해서 정할 수 있음
- 그 중 RESTRICT 정책은 자식 테이블이 하나라도 있다면 부모 테이블의 row가 삭제가 되지 않는 정책임

### 부모 테이블의 row가 삭제될 때 - CASCADE 정책
- CASCADE 정책은 부모 테이블 row를 삭제할 때 삭제가 잘 됨
- 여기서 이것을 참조하고 있던 자식 테이블의 row들도 같이 삭제됨

### 부모 테이블의 row가 삭제될 때 - SET NULL 정책
- 부모 테이블 row가 삭제됐을 때 그것을 참조하고 있던 자식 테이블의 row의 foreign key가 null이 됨
- 자식 테이블의 row는 남겨짐

### 부모 테이블의 row에서 참조당하는 컬럼이 갱신될 때는?
- 삭제할 때 On Delete였는데 갱신했을 때 On Update에서 역시 정책은 똑같음
- 논리는 똑같이 진행이 됨
- 각각 정책을 다르게 설정할 수 있음

### 논리적 Foreign Key, 물리적 Foreign Key
- 많은 테이블들이 Foreign Key를 매개로 해서 관계를 맺고 있음
- 어떤 테이블의 특정 컬럼이 Foreign Key로 설정되어야 할 것 같은데 Foreign Key로 설정되지 않은 경우를 보게 될 수 있음
- 개념상 논리적으로 성립하는 Foreign Key를 논리적 Foreign Key라고 함
- 실제로 특정 컬럼을 Foreign Key로 설정해서 두 테이블 간의 참조 무결성이 보장할 수 있게 됐을 때, 물리적 Foreign Key라고 함
- 왜 논리적으로만 설정하고 바로 물리적으로 하지 않을까?
- 성능적인 부분의 저하가 생길 수 있기 때문에
- 그리고 레거시 데이터의 참조 무결성이 이미 깨진 상태인데 이를 삭제하지 않고 남기기 위해서 굳이 물리적 Foreign Key로 바꾸지 않는 경우도 있음

### Foreign Key를 삭제하는 방법
- DROP FOREIGN KEY + (이름) 이를 통해서 테이블의 Foreign Key를 삭제할 수 있음

### 데이터베이스의 설계사항, 스키마
- 데이터베이스에 관한 모든 설계사항을 스키마라고 함, 데이터베이스에 어떤 테이블들이 있고, 각 테이블의 컬럼 구조와 각 컬럼의 데이터 타입 및 속성이 어떻게 되고, 테이블 간의 관계는 어떻게 되는지등과 같은 모든 사항 포함
- 개념적 스키마 - 하나의 조직, 하나의 기관, 하나의 서비스 등에서 필요로 하는 데이터베이스 설계사항을 의미함
- 물리적 스키마 - 데이터를 실제로 컴퓨터의 저장장치에 어떤 방식으로 저장할지를 결정하는 스키마임, 저장 스키마, 내부 스키마라고도 함, DBMS를 다룰 때 쓰는 개념