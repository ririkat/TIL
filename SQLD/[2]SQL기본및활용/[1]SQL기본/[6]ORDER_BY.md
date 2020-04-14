# ORDER BY

> SELECT문으로 검색된 데이터를 오름차순(**ASC**)이나 내림차순(**DESC**)으로 정렬 시킬 때 사용한다.
>
> Default값은 **Asc**ending(오름차순)으로써 ASC는 생략해도 되며, 문자는 알파벳 순서로 출력된다.
>
> ORDER BY절에 선택된 컬럼이 여러 개일 경우 앞(왼쪽)에 정의된 컬럼을 기준으로 먼저 분류한 후,
>
> 이후에 나열된 순서대로 분류한다.



### 기본 문법

------

```sql
1. SELECT empno FROM emp ORDER BY empno DESC -- 내림차순

2-1. SELECT empno FROM emp ORDER BY empno ASC -- 오른차순

2-2. SELECT empno FROM emp ORDER BY empno   -- ASC는 Default 값이라 생략해도 됨. 2번과 동일

3. SELECT job FROM emp ORDER BY empno  -- ORDER BY절에 지정된 컬럼이 SELECT절에 지정 안되도 됨
```



### ORDER BY 여러개

------

```sql
--A 내림차순 정렬
select A, B, C from EMP order by A desc;
 
--A 내림차순, B 오름차순 정렬
select A, B, C from EMP order by A desc, B;
```

