# Quick Sort (빠른정렬)

- ### pivot으로 하나의 값 지정 (분할)

- ### 각 부분을 순환적으로 정렬 (정복)




### pseudocode

```pseudocode
quickSort(A[], p, r) ▷ A[p....r]을 정렬한다
{
	if(p<r) then {
		q <- partision(A,p,r); 		// 1. 분할
		quickSort(A,p,q-1);	// 2. 왼쪽 부분 배열 정렬
		quickSort(A,q+1,r);	// 3. 오른쪽 부분 배열 정렬
	}
}
partition(A[],p,q,r)
{
	//배열 A[p..r]의 원소들을 A[r]을 기준으로 양쪽으로 재배치
	//A[r]이 자리한 위치를 return 한다.
	pivot <- A[r];
	i<-p-1;
	for j<-p to r-1						//1
        if(A[j]<=pivot) then
            i<-i+1;
            exchange A[i] and A[j];		//1 - 작은 부분, 큰 부분 분류
    exchange A[i+1] and A[r];			// pivot을 작<=pivot <=큰 위치로 옮김.
    return i+1; // pivot의 위치 반환.
}
```



### JAVA 코드

```java
package swmtest;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;

public class quickSort {
	static int[] arr;
	public static void main(String[] args) throws Exception {
		//입력
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int n = Integer.parseInt(br.readLine());//배열 크기
		String[] s=br.readLine().split(" ");
		arr=new int[n];//정렬할 배열
		for(int i=0; i<n; i++) {
			arr[i]=Integer.parseInt(s[i]);
		}

		qSort(0,n-1);

		//출력
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
		for(int i=0; i<n; i++){
			bw.write(arr[i]+" ");
		}
		bw.close();


	}

	private static void qSort(int start, int end){
		if(start<end){
			int pivot=partition(start,end);
			qSort(start,pivot-1);
			qSort(pivot+1,end);
		}

	}

	private static int partition( int start, int end){
		int i=start-1;
		int pivot=arr[end];
		int tmp=0;
		for(int j=start; j<=end-1; j++) {
			if(arr[j]<=pivot) {
				i++;
				tmp=arr[j];
				arr[j]=arr[i];
				arr[i]=tmp;
			}
		}
		tmp=arr[i+1];
		arr[i+1]=arr[end];
		arr[end]=tmp;
		
		return i+1;
	}

}

```

