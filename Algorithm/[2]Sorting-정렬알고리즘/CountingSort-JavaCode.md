# Counting Sort - Java Code

**1~5사이의 수 30개를 정렬하는 코드를 작성해라**

```java
public class CountingSort {
	public static void main(String[] args) {
		//1~5까지의 수 
		int[] count=new int[5];
		int[] array= {
				1,3,2,4,3,2,5,3,1,2,
				3,4,4,3,5,1,2,3,5,2,
				3,1,4,3,5,1,2,1,1,1
		};
		
		//countingSort
		for(int i=0; i<array.length; i++) {
			count[array[i]-1]++;
		}
		
		System.out.print("[");
		for(int i=0; i<5; i++) {
			if(count[i]!=0) {
				for(int j=0; j<count[i]; j++) {
					System.out.print((i+1)+" ");
				}
			}
		}
		System.out.print("]");
	}	

}
```

