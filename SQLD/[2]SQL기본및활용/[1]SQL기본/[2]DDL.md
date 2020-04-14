# DDL

> 테이블과 같은 데이터 구조(관계 (테이블) View, 인덱스 , 저장 프로시저 등)를 정의하는데 사용되는 명령어들로 그러한 구조를 생성하거나 변경하거나 삭제하거나 이름을 바꾸는 데이터 구조와 관련된 명령어



### CREATE

------

데이터베이스, 테이블, 유저 등 전체적인 데이터 구조를 생성할 때 사용 하는 문법

- **CREATE TABLE 기본 문법**

  컬럼이 N개인 테이블 생성 문법

  ```sql
  CREATE TABLE 테이블명
  (
      컬럼명1 데이터타입(사이즈),
      컬럼명2 데이터타입(사이즈),
      컬럼명3 데이터타입(사이즈),
      ...
      컬럼명N 데이터타입(사이즈)
  );
  ```

- **CREATE TABLE + 제약조건 추가**

  제약조건은 CREATE문 안에서 추가하는 방법과 ALTER문을 이용해 추가하는 방법 2가지가 있다.

  ```sql
  CREATE TABLE 테이블명
  (
      컬럼명1 데이터타입(사이즈),
      컬럼명2 데이터타입(사이즈),
      컬럼명3 데이터타입(사이즈) CONSTAINT_NAME, --제약조건을 추가할 열의 데이터타입 뒤에 추가하면 된다.
      ...
      컬럼명N 데이터타입(사이즈)
  );
  ```

  - CONSTRAINT 옵션

    - **NOT NULL** - NULL값이 들어가지 않아야 한다. 

      컬럼명1 데이터타입(사이즈) NOT NULL

    - **UNIQUE** - 반드시 a unique value 하나가 있어야 한다. 

      컬럼명1 데이터타입(사이즈) UNIQUE

    - **PRIMARY KEY** - NOT NULL과 UNIQUE의 조합. 유일하게 구분되어지는 키값이다.

      컬럼명1 데이터타입(사이즈) PRIMARY KEY

    - **FOREIGN KEY** - 다른테이블에서 매치되는 데이터를 찾을 수 있는 참조키 값이다. 

      컬럼명1 데이터타입(사이즈) FOREIGN KEY REFERENCES 참조테이블명(참조테이블의PK)

    - **CHECK** - 값이 정해진 조건에 충족하는지 체크

      CHECK IN (A,B,C) : A,B,C만 가능

    - **DEFAULT** - 아무것도 안쓰면 default 값을 갖는다. 

      DEFAULT 기본값 : 기본값 지정



### ALTER

------

데이터 구조를 변경할 때 사용하는 문법

- **기본 문법**

  ```sql
  ALTER TABLE 테이블명
  [변경 구문]
  ```

  **변경 구문에 들어갈 수 있는 구문**

  - DROP : 컬럼이나 제약조건 삭제
  - ADD : 컬럼이나 제약 조건 추가
    - ADD COLUMN [컬럼명] [데이터타입]
    - ADD CONSTRAINT [제약조건명] [제약조건]  (적용컬럼명)
  - MODIFY(컬럼명1 데이터타입, ...,컬럼명N 데이터타입) : 컬럼 수정 (=ALTER COLUMN)
  - RENAME COLUMN [A] TO [B]: 컬럼명 수정(A->B)



### DROP

------

데이터 구조를 삭제할 때 사용하는 문법

- **기본 문법**

  ```sql
  DROP TABLE 테이블명 [CASCADE CONSTRAINT];
  ```