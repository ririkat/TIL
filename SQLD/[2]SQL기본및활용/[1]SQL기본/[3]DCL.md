# DCL/TCL



### DCL - 데이터 제어어

------

- **GRANT : 객체 권한 부여**

  ```sql
  GRANT object_privilege[column]
  ON	object
  TO	{user[.user]|role|PUBLIC}
  [WITH GRANT OPTION]
  ```

  - object_privilege : 부여할 객체권한의 이름

  - object : 객체명

  - user, role : 부여할 사용자 이름과 다른 데이터 베이스 역할 이름

  - PUBLIC : 객체 권한, 또는 데이터베이스 역할을 모든 사용자에게 부여할 수 있다.

  - WITH GRANT OPTION : 권한을 부여 받은 사용자도 부여 받은 권한을 다른 사용자 또는 역할로 부여할 수 있게 된다.

  - **모든 권한 주기**

    ```sql
    GRANT CONNECT,DBA,RESOURCE TO username;
    ```

    

- **REVOKE : 객체 권한 회수**

  ```SQL
  REVOKE {privilege[.privilege]|ALL}
  ON object
  FROM {user[.user]|role|PUBLIC}
  [CASCADE CONSTARINTS]
  ```

  - 객체 권한의 철회는 그 권한을 부여한 부여자만이 수행할 수 있다.

  - CASCADE CONSTARINTS : 이 명령어의 사용으로 참조 객체 권한에서 사용 된 참조 무결성 제한을 같이 삭제 할 수 있다.

  - WITH GRANT OPTION : 객체 권한을 부여한 사용자의 객체 권한을 철회하면, 권한을 부여받은 사용자가 부여한 객체 권한 또한 같이 철회되는 종속철회가 발생한다.

    

- **operation**: 권한을 부여할 때 사용 가능한 연산을 나타낸다.

  - **SELECT**: 테이블 정의 내용을 읽을 수 있고 인스턴스 조회가 가능. 가장 일반적인 유형의 권한.
  - **INSERT**: 테이블의 인스턴스를 생성할 수 있는 권한.
  - **UPDATE**: 테이블에 이미 존재하는 인스턴스를 수정할 수 있는 권한.
  - **DELETE**: 테이블의 인스턴스를 삭제할 수 있는 권한.
  - **ALTER**: 테이블의 정의를 수정할 수 있고, 테이블의 이름을 변경하거나 삭제할 수 있는 권한.
  - **INDEX**: 검색 속도의 향상을 위해 칼럼에 인덱스를 생성할 수 있는 권한.
  - **EXECUTE**: 테이블 메서드 혹은 인스턴스 메서드를 호출할 수 있는 권한.
  - **ALL PRIVILEGES**: 앞서 설명한 7가지 권한을 모두 포함.

  

### TCL - 트랜잭션 제어어

------

논리적인 작업의 단위를 묶어 DML에 의해 조작된 결과를 작업단위(Transaction)별로 제어하는 명령어

- **COMMIT** : 트랜잭션단위 저장

- **ROLLBACK** : 트랜잭션단위 취소

- **SAVEPOINT** : ROLLBACK할 때 트랜잭션 단위가 아니라 일부만 ROLLBACK하고 싶을 때 사용하는 포인트 지점

  ```sql
  DML구문1
  SAVEPOINT A
  DML구문2
  SAVEPOINT B
  DML구문3
  SVAEPOINT C
  --1) ROLLBACK
  --2) ROLLBACK A
  --3) ROLLBACK B
  --4) ROLLBACK C
  ```

  1) DML 구문 1,2,3 모두 취소

  2) DML 구문 2,3 취소

  3) DML 구문 3 취소

  4) DML 전체 취소X