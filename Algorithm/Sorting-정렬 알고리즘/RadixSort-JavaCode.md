# Radix Sort - Java Code

```java
import java.util.LinkedList;

public class RadixSort {
	public static void main(String[] args) {
		//1~5까지의 수 
		int[] array= {
				50,20,319,218,3,99,192,172,342,999,1,0,344
		};
		maxLen=3;
		radixsort(array);
	}
	
	private static int maxLen=0;
	
	//0~9bucket들을 담을 배열 생성
	 private static LinkedList<Integer>[] counter = new LinkedList[] {
            new LinkedList<Integer>(), new LinkedList<Integer>(),
            new LinkedList<Integer>(), new LinkedList<Integer>(),
            new LinkedList<Integer>(), new LinkedList<Integer>(),
            new LinkedList<Integer>(), new LinkedList<Integer>(),
            new LinkedList<Integer>(), new LinkedList<Integer>() }; 
	 

	
	private static void bucketSort(int[] arr,int mod, int exp){
		
		for(int i=0; i<arr.length; i++) {
			int bucket=(arr[i]%mod)/exp;
			counter[bucket].add(arr[i]);
			
		}
		
		int idx=0;
		for(int i=0; i<10; i++) {
			while(!counter[i].isEmpty()) {
				arr[idx++]=counter[i].poll();
			}
		}
		
		for(int i=0; i<arr.length; i++) {
			System.out.print(arr[i]+", ");
		}
		System.out.println();
	}
	
	private static void radixsort(int[] data) {
		// 자리수 만큼 반복
		int mod=10;
		int exp=1;
		for(int i=0; i<maxLen; i++, mod*=10,exp*=10) {
			System.out.println(exp+"자리 기수정렬");
			bucketSort(data, mod, exp);
		}
	}

}
```

