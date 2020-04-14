# Recursion(재귀) 알고리즘 개념

### 재귀 알고리즘

- 재귀 함수를 사용하여 문제를 해결하는 알고리즘 기법
- 재귀함수 : 자기 자신을 다시 호출하는 함수
- **구조** 
  - **baseCase** : 적어도 하나의 recursion에 빠지지 않는 경우가 존재해야 한다.
  - **Recursive case** : baseCase가 아닐 때, 수행되어야하는 case.
  - 단, recursion을 반복하다 보면 결국 **base case로 수렴**하도록 설정해야한다.



------

### 기본 예제

**1. 팩토리얼 (Factorial)**

- 0! = 1

- n! = n\*(n-1)\*...\*1 (n>0)

- **n!=n\*(n-1)!**

  ```java
  import java.io.*;
  class Main {
  	public static void main(String[] args) throws Exception {
  		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
  		int input = Integer.parseInt(br.readLine());
  		
  		System.out.print(factorial(input));
  		
  	}
  	
  	public static long factorial(int n){
  		if(n==0){
  			return 1;
  		}
  		return n*factorial(n-1);
  	}
  }
  ```

  

**2. 피보나치 수**

- f0=0

- f1=1

- **fn=fn-1+fn-2** (n>1)

  ```java
  import java.io.*;
  class Main {
  	public static void main(String[] args) throws Exception {
  		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
  		int input = Integer.parseInt(br.readLine());
  		
  		long sum=0;
  		for(int i=0; i<=input; i++){
  			sum+=fibonacci(i);
  		}
  		System.out.print(sum);
  	}
  	
  	public static long fibonacci(int n){
  		if(n==0) return 0;
  		if(n==1) return 1;
  		return fibonacci(n-1)+fibonacci(n-2);	
  	}
  }
  ```



**3. 최대공약수 (GCD)**

- 두 개 이상의 정수의 공통 약수 중에서 최댓값

- **유클리드 호제법**을 이용한 풀이 (Recursion)

  - m>=n인 두 양의 정수 m,n

  - m이 n의 배수이면 gcd(m,n)=n

  - otherwise, gcd(m,n)=gcd(n,m%n) 이다.

    ```java
    class Solution {
      public int solution(int m, int n) {
          return gcd(m,n);
      }
        
       public int gcd(int m, int n){
            if(m<n){//큰 값이 m이 되도록 설정.
                int tmp=m;
                m=n;
                n=tmp;
            }
            if(m%n==0)return n;
            return gcd(n,m%n);
        }
    }
    ```



