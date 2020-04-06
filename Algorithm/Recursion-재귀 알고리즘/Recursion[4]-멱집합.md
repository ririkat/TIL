# Recursion 대표 문제[4] - 멱집합

### 멱집합

##### 문제 설명

임의의 집합의 모든 부분집합을 출력하라.

##### 풀이 코드

```java
public class PowerSet {
	private static char[] data= {'a','b','c','d','e','f'};
	private static int n=data.length;
	private static boolean[] include=new boolean[n];
	
	private static void ps(int k) {
		if(k==n) {//
			for(int i=0; i<n; i++) {
				if(include[i]) System.out.print(data[i]+" ");
			}
			System.out.println();
			return;
		}
		include[k]=false;
		ps(k+1); //data[k] 원소 포합하지 않는 원소들의 멱집합
		include[k]=true;
		ps(k+1); // data[k] 원소를 포함한 원소들의 멱집합
	}
	
	public static void main(String[] args) {
		ps(0);
	}

}
```

