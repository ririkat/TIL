# Insertion Sort (삽입정렬)

- ### 이미 정렬된 부분을 탐색하여

- ### 해당 데이터가 들어가야할 곳을 찾아

- ### 나머지를 한칸씩 옮긴뒤 빈 자리에 끼워넣는다. (삽입)



### JAVA 코드

```java
import java.io.*;
class Main {
	public static void main(String[] args) throws Exception {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int n = Integer.parseInt(br.readLine());
		String[] str=br.readLine().split(" ");
		int[] arr=new int[n];
		for(int i=0;i<n;i++){
			arr[i]=Integer.parseInt(str[i]);
		}
		int s=Integer.parseInt(br.readLine());

		
		int[] answer=insertSort(arr,n,s);
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
		for(int i=0;i<n; i++){
			bw.write(answer[i]+" ");
		}
		bw.close();

	}
	
	static int[] insertSort(int[] arr,int n,int s){
		
		for(int i=1; i<=s; i++){
			//System.out.println("====="+i+"단계=====");
			int idx=i;
			int tmp=arr[i];
			//System.out.println(i+":"+tmp);
			for(int j=i-1; j>=0; j--){
				if(j==0) idx=0;
				if(tmp>arr[j]){
					idx=j+1;
					//System.out.println(idx);
					break;
				}
				arr[j+1]=arr[j];
				//System.out.println(j+1+":"+arr[j+1]);
			}
			arr[idx]=tmp;
			//System.out.println(idx+":"+arr[idx]);
		}
		return arr;
	}
}
```

