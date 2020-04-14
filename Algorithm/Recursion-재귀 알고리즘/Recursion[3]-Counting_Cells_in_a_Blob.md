# Recursion 대표 문제[3] - Counting Cells in a Blob

### Counting Cells in a Blob

이미지 구간과 배경 구간을 구분하여 표시된 2차원 배열이 있을 때 이미지 구간을 세는 문제

### Counting Cells in a Blob 응용 - 카카오 컬러링북

##### 문제 설명

출판사의 편집자인 어피치는 네오에게 컬러링북에 들어갈 원화를 그려달라고 부탁하여 여러 장의 그림을 받았다. 여러 장의 그림을 난이도 순으로 컬러링북에 넣고 싶었던 어피치는 영역이 많으면 색칠하기가 까다로워 어려워진다는 사실을 발견하고 그림의 난이도를 영역의 수로 정의하였다. (영역이란 상하좌우로 연결된 같은 색상의 공간을 의미한다.)

그림에 몇 개의 영역이 있는지와 가장 큰 영역의 넓이는 얼마인지 계산하는 프로그램을 작성해보자.

![alt text](http://t1.kakaocdn.net/codefestival/apeach.png)

위의 그림은 총 12개 영역으로 이루어져 있으며, 가장 넓은 영역은 어피치의 얼굴면으로 넓이는 120이다.

##### 입력 형식

입력은 그림의 크기를 나타내는 `m`과 `n`, 그리고 그림을 나타내는 `m × n` 크기의 2차원 배열 `picture`로 주어진다. 제한조건은 아래와 같다.

- `1 <= m, n <= 100`
- `picture`의 원소는 `0` 이상 `2^31 - 1` 이하의 임의의 값이다.
- `picture`의 원소 중 값이 `0`인 경우는 색칠하지 않는 영역을 뜻한다.

##### 출력 형식

리턴 타입은 원소가 두 개인 정수 배열이다. 그림에 몇 개의 영역이 있는지와 가장 큰 영역은 몇 칸으로 이루어져 있는지를 리턴한다.

##### 예제 입출력

| m    | n    | picture                                                      | answer |
| ---- | ---- | ------------------------------------------------------------ | ------ |
| 6    | 4    | [[1, 1, 1, 0], [1, 2, 2, 0], [1, 0, 0, 1], [0, 0, 0, 1], [0, 0, 0, 3], [0, 0, 0, 3]] | [4, 5] |

##### 예제에 대한 설명

예제로 주어진 그림은 총 4개의 영역으로 구성되어 있으며, 왼쪽 위의 영역과 오른쪽의 영역은 모두 `1`로 구성되어 있지만 상하좌우로 이어져있지 않으므로 다른 영역이다. 가장 넓은 영역은 왼쪽 위 `1`이 차지하는 영역으로 총 5칸이다.



##### 풀이 코드

```java
class Solution {
    private static int[][] pic;
    private static int M=0;
    private static int N=0;
    private static boolean[][] check;
  public int[] solution(int m, int n, int[][] picture) {
      int[] answer = new int[2];
      pic=picture;
      check=new boolean[m][n];
      M=m;
      N=n;
      int numberOfArea=0;
      int maxOneArea=0;
      int oneArea=0;
      for(int i=0;i<M; i++){
          for(int j=0; j<N;j++){
              if(pic[i][j]==0||check[i][j]) continue;
              numberOfArea+=1;
              oneArea=countCell(i,j,pic[i][j]);
              if(maxOneArea<oneArea){maxOneArea=oneArea;}
              oneArea=0;
          }
      }
      answer[0]=numberOfArea;
      answer[1]=maxOneArea;
      return answer;
  }
    
    private static int countCell(int x, int y,int prev){// 한 영역을 세는 데 필요한 메소드
        if(x<0||y<0||x>=M||y>=N||check[x][y]||pic[x][y]!=prev){
            return 0;
        }else{
            check[x][y]=true;
            return 1+countCell(x-1,y,prev)+countCell(x,y+1,prev)+countCell(x+1,y,prev)+countCell(x,y-1,prev);       
        }
        
    }
}
```

