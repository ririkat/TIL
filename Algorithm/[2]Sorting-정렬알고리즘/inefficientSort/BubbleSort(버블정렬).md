# Bubble Sort (버블정렬)

- ### 인접한 두 수를 비교하여 정렬



### JAVA 코드

```java
import java.io.*;
class Main {
	public static void main(String[] args) throws Exception {
		//입력
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int n = Integer.parseInt(br.readLine());//배열 크기
		String[] s=br.readLine().split(" ");//배열로 만들기
		int[] arr=new int[n];//숫자로 변환해서 담을 그릇
		for(int i=0; i<n; i++) {
			arr[i]=Integer.parseInt(s[i]);
		}
		//정렬 메소드 호출
		arr=bubbleSort(arr,n);
		
		//출력
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
		for(int i=0; i<arr.length; i++){
			bw.write(arr[i]+" ");
		}
		bw.close();
	}
	static int[] bubbleSort(int[] arr, int n){
		//앞부터 두개씩 비교해가면서 정렬
		int tmp=0;
		for(int last=n; last>=2; last--){
			for(int i=0; i<last-1; i++){
				if(arr[i]>arr[i+1]){
					tmp=arr[i];
					arr[i]=arr[i+1];
					arr[i+1]=tmp;
				}
			}
		}
		return arr;
	}
}
```

