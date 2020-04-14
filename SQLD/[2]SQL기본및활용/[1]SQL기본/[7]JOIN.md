# JOIN

>  \- JOIN은 각 테이블간에 공통된 걸럼(조건)으로 데이터를 합쳐 표현하는 것이다.
>
>  \- JOIN에는 크게 INNER JOIN, OUTER JOIN이 있다.



▶ 예제 테이블을 통해 이해해보자.

TABLE 1) MEM : 회원테이블 (회원번호, 이름, 이메일, 부서번호)

![img](https://t1.daumcdn.net/cfile/tistory/9952083359A678B422)

TABLE 2) DEPART : 부서테이블 (부서번호, 부서명)

![img](https://t1.daumcdn.net/cfile/tistory/9956893359A678BD16)



### SELECT FROM을 이용한 조인

------

**1.1)** **회원 테이블과 부서 테이블의 조인**

-  DEPART_ID가 공통 컬럼
-  MEM테이블의 DEPART_ID와 DEPART테이블의 DEPART_ID를 연결하여 준다.

```sql
SELECT MEM.MEM_ID, MEM.NAME, MEM.DEPART_ID, DEPART.DEPART_NAME
FROM   MEM, DEPART
WHERE MEM.DEPART_ID = DEPART.DEPART_ID;
```

![img](https://t1.daumcdn.net/cfile/tistory/995E6E3359A678CD21) 



**1.2)** **이때 테이블명이 긴 경우 일일이 그 테이블 명을 다 써주지 않고 별칭을 쓸 수 있다.**

```sql
SELECT A.MEM_ID, A.NAME, A.DEPART_ID, B.DEPART_NAME
FROM  MEM A, DEPART B
WHERE A.DEPART_ID = B.DEPART_ID;
```

**결과는 동일**

![img](https://t1.daumcdn.net/cfile/tistory/99C2583359A678DB2B)



### ANSI 표준 조인 (JOIN 절을 이용한 명시적 조인)

------

- **문법**

JOIN절을 명시적으로 선언하여 질의문을 작성할 수 도 있다.

```sql
SELECT 컬럼이름1, 컬럼이름2, ㆍㆍㆍ
FROM  테이블명1
JOIN  테이블명2
ON    테이블명1.컬럼명 = 테이블명2.컬럼명;
```

위의 쿼리를 이렇게 바꿔 작성할 수 있다.

```sql
SELECT A.MEM_ID, A.NAME, A.DEPART_ID, B.DEPART_NAME
FROM  MEM A
JOIN  DEPART B
ON   A.DEPART_ID = B.DEPART_ID
```



### 질의문 사용한 JOIN

------

**3.1)** **회원 테이블과 부서 테이블의 조인 (특정 회원 조회 EX) NAME이 갓동수’ 인 회원)**

**3.1.1) SELECT FROM을 이용한 조인에 AND로 조건을 추가하여 조회 가능하다.**

```sql
SELECT A.MEM_ID, A.NAME, A.DEPART_ID, B.DEPART_NAME
FROM  MEM A, DEPART B
WHERE A.DEPART_ID = B.DEPART_ID AND A.NAME = '갓동수'
```

![img](https://t1.daumcdn.net/cfile/tistory/9942FA3359A678EB20)

**3.1.2) ANSI** **표준 쿼리에서는 WHERE 문을 추가하여 조건 조회가 가능하다.**

```sql
SELECT A.MEM_ID, A.NAME, A.DEPART_ID, B.DEPART_NAME
FROM MEM A
JOIN DEPART B
ON A.DEPART_ID = B.DEPART_ID
WHERE A.NAME = '갓동수';
```

![img](https://t1.daumcdn.net/cfile/tistory/9942B53359A678F428)



### 3개 이상(다중) 테이블 조인

------

 TABLE Name = MOD_MEM_LOG : 회원정보 변경로그 (회원번호, 변경시간)

![img](https://t1.daumcdn.net/cfile/tistory/9989113359A6790208)

**4.1)** **회원 테이블과 부서 테이블의 조인 후 그 회원의 회원 수정 기록을 알고 싶다.**

MEM_MOD_LOG 테이블을 추가하고, 공통 컬럼을 연결 시켜준다.

**첫번째 방법) SELECT, FROM 절**

```sql
SELECT A.MEM_ID, A.NAME, A.DEPART_ID, B.DEPART_NAME, C.LOG_TIME
FROM   MEM A , DEPART B, MEM_MOD_LOG C
WHERE  A.DEPART_ID = B.DEPART_ID
**AND   A.MEM_ID = C.MEM_ID
AND    A.NAME = '갓동수';
```

![img](https://t1.daumcdn.net/cfile/tistory/995B003359A6790D24)



**두번째 방법) ANSI표준쿼리**

```sql
SELECT A.MEM_ID, A.NAME, A.DEPART_ID, B.DEPART_NAME, C.LOG_TIME
FROM   MEM A
JOIN   DEPART B
ON     A.DEPART_ID = B.DEPART_ID
JOIN  MEM_MOD_LOG C
ON   A.MEM_ID = C.MEM_ID
WHERE A.NAME = '갓동수';
```

![img](https://t1.daumcdn.net/cfile/tistory/99F09E3359A6791721)



### OUTER JOIN (LEFT,RIGHT,FULL OUTER JOIN)

------

EQUI JOIN 문장들의 한 가지 제약점은 그것들이 조인을 생성하려 하는 두개의 테이블의 

두개 컬럼에서 공통된 값이 없다면 테이블로부터 데이터를 반환하지 못한다는 것이다.

- 정상적으로 저인 조건을 만족하지 못하는 행들을 보기위해 OUTER JOIN을 사용한다. 

- OUTER JOIN 연산자는 "(+)"이다.

-  조인시킬 값이 없는 조인측에 "(+)"를 위치 시킨다.

- OUTER JOIN 연산자는 표현식의 한 편에만 올 수 있다.

  

**EX1 ) ‘사자’님의 회원 정보를 조회해보겠다. (부서명 까지 조인)**

```sql
SELECT A.MEM_ID, A.NAME, A.DEPART_ID, B.DEPART_NAME
FROM   MEM A, DEPART B
WHERE  A.DEPART_ID = B.DEPART_ID AND    A.NAME = '사자';
```

![img](https://t1.daumcdn.net/cfile/tistory/992D933359A679220B)

위와 같은 정보가 나오는 것을 알 수 있다.



**EX2) 그럼 '사자'님의 회원정보 수정 기록을 알기 위해 조인을 해보자.**



```sql
SELECT A.MEM_ID, A.NAME, A.DEPART_ID, B.DEPART_NAME, C.LOG_TIME
FROM  MEM A, DEPART B, MEM_MOD_LOG C
WHERE A.DEPART_ID = B.DEPART_ID AND  A.MEM_ID = C.MEM_ID AND  A.NAME = '사자';
```

![img](https://t1.daumcdn.net/cfile/tistory/992BAC3359A679301D)

아무런 결과가 나오지 않는다.

그 이유를 살펴보면 ‘사자’님은 한번도 회원정보를 수정한 적이 없기 때문이다.

![img](https://t1.daumcdn.net/cfile/tistory/99595A3359A6794217)

회원 정보 수정 로그 (사자 MEM_ID : 0000000003)

회원 정보 수정 로그가 없더라도 회원 기본 정보를 보고 싶다면 **이때** **OUTER 조인을 사용하면 된다.**



▶ **5.1) ORACLE에서의 OUTER조인**

간단하게 말하여 데이터가 없을 수도 있는 쪽 JOIN 컬럼에 (+)를 추가하여 OUTER JOIN이 가능하다.

```
SELECT A.MEM_ID, A.NAME, A.DEPART_ID, B.DEPART_NAME, C.LOG_TIME
FROM   MEM A, DEPART B, MEM_MOD_LOG C
WHERE  A.DEPART_ID = B.DEPART_ID AND   A.MEM_ID = C.MEM_ID(+) AND    A.NAME = '사자';
```



![img](https://t1.daumcdn.net/cfile/tistory/99B8843359A679642D)

위와 같이 회원정보 변경 이력이 없더라도 나머지 조인에 의한 결과행은 보여지도록 된다.



▶ **5.2) ANSI** **표준 쿼리의 OUTER JOIN**

-   ANSI 표준에서의 OUTER JOIN은 LEFT, RIGHT OUTER 조인 2가지가 있다.

  

 **5.2.1) LEFT OUTER JOIN**

이전의 JOIN ON 절에서 JOIN 앞에 **LEFT OUTER**를 붙여주면 된다.

```sql
SELECT A.MEM_ID, A.NAME, A.DEPART_ID, B.DEPART_NAME, C.LOG_TIME
FROM   MEM A
JOIN   DEPART B
ON     A.DEPART_ID = B.DEPART_ID
LEFT  OUTER JOIN MEM_MOD_LOG C
ON  A.MEM_ID = C.MEM_ID
WHERE A.NAME = '사자';
```

![img](https://t1.daumcdn.net/cfile/tistory/9946443359A679702B)

 

▶ **5.3) FULL OUTER JOIN**

양쪽 테이블에 다 Outer Join을 거는 것을 TWO-WAY OUTER JOIN 또는 FULL OUTER JOIN 이라 한다.



출처: https://goddaehee.tistory.com/62 [갓대희의 작은공간]