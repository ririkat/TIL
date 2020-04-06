# Recursion 대표 문제[2] - N Queen's Problem

### N Queen's Problem

##### 문제 설명

N-Queen 문제는 크기가 N × N인 체스판 위에 퀸 N개를 서로 공격할 수 없게 놓는 문제이다.

N이 주어졌을 때, 퀸을 놓는 방법의 수를 구하는 프로그램을 작성하시오.

- ##### 입력

  > 첫째 줄에 N이 주어진다. (1 ≤ N < 15)
  >

- ##### 출력

  > 첫째 줄에 퀸 N개를 서로 공격할 수 없게 놓는 경우의 수를 출력한다.



##### 풀이 코드

```java
import java.io.*;
import java.util.*;
class Main {
   public static void main(String[] args) throws Exception {
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
      
      // 체스판의 크기 입력받기
      int size = Integer.parseInt(br.readLine());
      
      // 상하좌우, 대각선으로 공격할 수 있기에 한 줄에 한개의 퀸만 존재할 수 있다.
      // 행을 중심으로 배치
      int[] board = new int[size];   // index -> 행 board[index] -> 열
      // 검사해야할 조건
      /*
         1. 행, 열, 대각선의 충돌이 있는지
         2. 마지막 줄인지 -> 성공
         3. 다음 줄에 case 추가
      */
      
      for(int i=0; i<size; i++){
         board[0] = i;
         queens(board, 0);
      }
      System.out.println(total);
   }
   public static int total = 0;
   
   public static void queens(int[] board, int level){
      if(promising(board, level)){   // 충돌이 있으면 false
          if(level == (board.length-1)){      // 충돌이 없으며 마지막 행에 도달했을 때
            //System.out.println(Arrays.toString(board));
            total++;
            
          } else {
            for(int i=0; i<board.length; i++){
               board[level+1] = i;      // 다음 행에 경우의 수 대입해보기
               queens(board, level+1);
            }
          }
      }
   }
   // 충돌 여부 확인 메소드
   public static boolean promising(int[] board, int level){
      for(int i=0; i<level; i++){
         if(board[i] == board[level]){      // 같은 열에 있는 경우 -> 충돌
            return false;
         } else if((level-i) == Math.abs(board[i]-board[level])){   // 같은 대각선상에 있는 경우 -> 충돌
            return false;
         }
      }
      // 충돌이 없다.
      return true;
   }
}
```

