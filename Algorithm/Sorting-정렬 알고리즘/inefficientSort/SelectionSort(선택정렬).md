# Selection Sort (선택정렬)

- ### 배열에서 가장 작은 값(또는 큰 값)을 선택해 맨 앞(또는 뒤)의 값과 교환

- ### 이미 정렬된 부분은 신경쓰지 않는다. 



### JAVA 코드

```java
import java.io.*;
class Main {
	public static void main(String[] args) throws Exception {
		//입력
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		String[] s1=br.readLine().split(" ");
		int n = Integer.parseInt(s1[0]);//수열개수
		int s = Integer.parseInt(s1[1]);//진행단계
		String[] s2=br.readLine().split(" ");
		int[] arr=new int[n];
		for(int i=0; i<n; i++) {
			arr[i]=Integer.parseInt(s2[i]);
		}
		//정렬메소드 호출
		int[] result=selectSort(arr,n,s);
		
		//출력
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
		for(int i=0; i<n; i++){
			bw.write(result[i]+" ");
		}
		bw.close();
	}
	
	private static int[] selectSort(int[] arr,int n,int s){
		for(int start=0; start<s; start++){
			int min=arr[start];
			int idx=start;
			for(int i=start; i<n; i++){
				if(min>arr[i]){min=arr[i];idx=i;}
			}
			arr[idx]=arr[start];
			arr[start]=min;
		}
		return arr;
	}
	
}
```

