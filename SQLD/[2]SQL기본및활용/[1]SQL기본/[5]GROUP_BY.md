# GROUP BY

> GROUP는 특정 컬럼을 기준으로 집계를 내는데 사용된다.



### 기본 문법

------

```sql
SELECT [GROUP BY 절에 지정된 컬럼1] [GROUP BY별로 집계할 값] 
FROM [테이블 명] 
GROUP BY [ 그룹으로 묶을 컬럼 값 ];
```



### HAVING절 사용

------

> WHERE가 테이블의 조건이라면,
>
> HAVING은 GROUP BY로 집계된 값들의 조건임.

```sql
SELECT [GROUP BY 절에 지정된 컬럼1] [GROUP BY별로 집계할 값] 
FROM [테이블 명] 
GROUP BY [ 그룹으로 묶을 컬럼 값 ]
HAVING [조건 추가] ;
```



### GROUP BY 여러개

------

여러 컬럼을 그룹화 할 경우 GROUP BY절에 나열된 컬럼들의 값이 모두 같아야 같은 그룹으로 묶인다.

```
SELECT [GROUP BY 절에 지정된 컬럼1][GROUP BY 절에 지정된 컬럼2] [GROUP BY별로 집계할 값] 
FROM [테이블 명] 
GROUP BY [그룹으로 묶을 컬럼 값1],[그룹으로 묶을 컬럼 값2];
```

