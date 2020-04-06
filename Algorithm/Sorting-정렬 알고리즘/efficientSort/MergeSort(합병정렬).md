# Merge Sort (합병정렬)

- ### 데이터가 저장된 배열을 절반으로 나눔 (분할)

- ### 각각을 순환적으로 정렬 (정복)

- ### 정렬된 두 개의 배열을 합쳐 전체를 정렬 (합병)



### pseudocode

```pseudocode
mergeSort(A[], p, r) ▷ A[p....r]을 정렬한다
{
	if(p<r) then {
		q <- (p+q)/2; 		// 1. p,q의 중간 지점 계산
		mergeSort(A,p,q);	// 2. 전반부 정렬
		mergeSort(A,q+1,r);	// 3. 후반부 정렬
		merge(A,p,q,r);		// 4. 합병
	}
}
merge(A[],p,q,r)
{
	//정렬된 두 배열 A[p...q],A[q+1....r]을 합하여 정렬된 하나의 배열 A[q...r]을 만든다.
}
```



### JAVA 코드

```java
import java.io.*;
class Main {

	public static void main(String[] args) throws Exception {
		//입력
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int n = Integer.parseInt(br.readLine());//배열 크기
		String[] s=br.readLine().split(" ");
		int[] arr=new int[n];//정렬할 배열
		for(int i=0; i<n; i++) {
			arr[i]=Integer.parseInt(s[i]);
		}
		
		mergeSort(arr,0,n-1);
		
		//출력
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
		for(int i=0; i<n; i++){
			bw.write(arr[i]+" ");
		}
		bw.close();
		
	
	}
	
	private static void mergeSort(int[] arr,int start, int end){
		if(start<end){
			int middle=(start+end)/2;
			mergeSort(arr,start,middle);
			mergeSort(arr,middle+1,end);
			merge(arr,start,middle,end);
		}
		
	}
	
	private static void merge(int[] arr, int start, int middle, int end){
		int i=start, j=middle+1, k=start;
		int[] tmp=new int[arr.length];
		
		while(i<=middle&&j<=end){
			if(arr[i]<arr[j]){
				tmp[k++]=arr[i++];
			}else{
				tmp[k++]=arr[j++];
			}
		}
		
		if(i>middle){
			while(j<=end){
				tmp[k++]=arr[j++];
			}
		}else{
			while(i<=middle){
				tmp[k++]=arr[i++];
			}
		}
		
		for(int idx=start; idx<=end; idx++){
			arr[idx]=tmp[idx];
		}
		
	}
}
```

