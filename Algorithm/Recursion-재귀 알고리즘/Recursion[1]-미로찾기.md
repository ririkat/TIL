# Recursion 대표 문제[1] - 미로찾기

### 4*4 미로찾기

##### 문제 설명

4*4미로에서 출발점(1,1)에서 도착점(4,4)까지로의 경로를 출력하는 프로그램을 작성하시오.

- ##### 입력

  > 길=1, 벽=0
  >
  > 단, 출발점으로부터 도착점까지의 길은 하나밖에 없습니다.

- ##### 출력

  > 출발점부터 도착점까지 미로를 헤매지 않고 이동하는 경로를 정사각형 위에 1로 표현



##### 풀이 코드

```java
import java.io.*;
class Main {
	private static int[][] arr=new int[4][4];
	private static final int PATHWAY=1;
	private static final int WALL=0;
	private static final int VISIT_BLOCK=2;
	private static final int VISIT_PATH=3;
	public static void main(String[] args) throws Exception {
		//입력
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

		for(int i=0; i<4; i++) {
			String[] s=br.readLine().replaceAll(" ","").split("");
			arr[i][0]=Integer.parseInt(s[0]);
			arr[i][1]=Integer.parseInt(s[1]);
			arr[i][2]=Integer.parseInt(s[2]);
			arr[i][3]=Integer.parseInt(s[3]);
		}
		//출력
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
		
		findRoad(0,0);
		for(int i=0; i<4; i++){
			for(int j=0; j<4; j++){
		
				if(arr[i][j]==VISIT_PATH){
					bw.write(" "+1+" ");
				}else{
					bw.write(" "+0+" ");
				}
			}
			bw.write("\n");
		}
		bw.close();
	}
	//길=1, 벽=0
	//출발은 0,0 -> 3,3 도착
	private static boolean findRoad(int x, int y){
		//끝나는 조건 : 3,3에 도착했을 때임.
		if(x<0||y<0||x>3||y>3) {return false;}
		else if(arr[x][y]!=PATHWAY){return false;}
		else if(x==3&&y==3) {arr[x][y]=VISIT_PATH;return true;}
		else{
			arr[x][y]=VISIT_PATH;//현재의 위치
			//에서 갈 수 있는 방향은 왼쪽,오른쪽,아래,위 임(사방)
			if(findRoad(x-1,y)||findRoad(x,y-1)||findRoad(x,y+1)||findRoad(x+1,y)){
				return true;
			}
			arr[x][y]=VISIT_BLOCK;
			return false;
		}
		
	}
}
```

