# 이진검색트리(Binary Search Tree)

> #### 이진트리 기반의 탐색을 위한 자료구조
>
> - 모든 노드의 키는 유일하다 (각 노드에 하나의 키 저장)
> - (왼쪽 자식) < (부모)
> - (오른쪽 자식) > (부모)
> - 왼쪽과 오른쪽 서브 트리도 이진 탐색 트리이다.



![^img](https://t1.daumcdn.net/cfile/tistory/99ACAF335989659B19)[^img1]

[^img1]: https://t1.daumcdn.net/cfile/tistory/99ACAF335989659B19



### SEARCH

------

#### # 일반 검색

키 12를 검색 : 18 ▷ 7 ▷ 12

- **pseudocode**

  x : 루트노드,  k : 찾는 값, key[x] : 노드 x에 저장된 값

  ```pseudocode
  TREE-SEARCH(x,k)
  	if x = NIL or k = key[x]
  		then return x
  	if k < key[x]
  		then return TREE-SEARCH(left[x],k)
  		else return TREE-SEARCH(right[x],k)
  ```

- **시간복잡도 : O(h)**   //h : 트리의 높이



#### # 최소값 찾기

최소값을 항상 가장 왼쪽 노드에 존재

- **pseudocode**

  x : 루트노드

  ```pseudocode
  TREE-MINIMUM(x)
  	while left[x]≠NIL
  		do x <- left[x]
  	return x
  ```

- **시간복잡도 : O(h)**   //h : 트리의 높이



#### # Successor 찾기

노드 x의 successor란 key[x]보다 크면서 가장 작은 키를 가진 노드

18의 successor = 27, 7의 successor = 12

- **3가지 경우**
  - 노드 x의 **오른쪽 서브트리가 존재**할 경우 ▷ 오른쪽 서브트리의 최소값=successor
  - 노드 x의 **오른쪽 서브트리가 없는** 경우
    - 노드 x가 부모노드의 왼쪽서브트리인 경우 ▷ 부모노드값=successor
    - otherwise ▷ 부모를 따라 올라가면서 처음으로 누군가의 왼쪽 자식이 되는 노드값=successor
  - otherwise ▷ successor 존재하지 않음 (x가 최대값)

- **pseudocode**

  p[x] : x의 부모노드

  ```pseudocode
  TREE-SUCCESSOR(x)
  1	if right[x] ≠ NIL						//1. 오른쪽 서브트리가 존재하면
  2		then return TREE-MINIMUM(right[x])	//1-1. 오른쪽 서브트리의 최소값을 찾아서 리턴
  3	y <- p[x]								//2. 오른쪽 서브트리 없으면, 부모를 y에 넣음
  4	while y ≠ NIL and x = right[y]			//2-1. 왼쪽자식이될 때까지 while문 반복
  5		do x <- y							//2-1-1. 부모로 한칸씩 올라감
  6		   y<- p[y]
  7	return y								//2-2. 최종 y값을 리턴
  ```

- **시간복잡도 : O(h)**   //h : 트리의 높이



#### # Predecessor 찾기

노드 x의 Predecessor 란 key[x]보다 작으면서 가장 큰 키를 가진 노드

successor와 반대

- **Case**
  1. 노드 x의 **왼쪽서브트리가 존재**할 경우 ▷ 왼쪽 서브트리의 최대값=Predecessor 
  2. 노드 x의 **왼쪽 서브트리가 없는** 경우
     - 노드 x가 부모노드의 오른쪽서브트리인 경우 ▷ 부모노드값=Predecessor 
     - otherwise ▷ 부모를 따라 올라가면서 처음으로 누군가의 오른쪽 자식이 되는 노드값=Predecessor 
  3. otherwise ▷ Predecessor 존재하지 않음 (x가 최소값)

- **pseudocode**

  p[x] : x의 부모노드

  ```pseudocode
  TREE-SUCCESSOR(x)
  1	if left[x] ≠ NIL						//1. 왼쪽 서브트리가 존재하면
  2		then return left[x]					//1-1. 왼쪽 서브트리의 최대값 찾아서 리턴
  3	y <- p[x]								//2. 왼쪽 서브트리 없으면, 부모를 y에 넣음
  4	while y ≠ NIL and x = left[y]			//2-1. 오른쪽자식이될 때까지 while문 반복
  5		do x <- y							//2-1-1. 부모로 한칸씩 올라감
  6		   y<- p[y]
  7	return y								//2-2. 최종 y값을 리턴
  ```

- **시간복잡도 : O(h)**   //h : 트리의 높이



### INSERT

------

키 14를 추가 > 12의 오른쪽 노드에 삽입

- 2개의 포인터 x,y를 사용
- 기존의 노드들은 변경하지 않음.

- **pseudocode**

  T : 트리, z : insert할 노드, x : 탐색하는 노드, y : x의 부모노드

  ```pseudocode
  TREE-INSERT(T,z)
  	y <- NIL
  	x <- root[T]					//시작은 y=null, x는 루트에서 출발
  	while x ≠ NIL					//1. x가 null이될때까지 반복
  		do y <- x					
  			if key[z] < key[x]			//1-1.z와 현재 노드=x의 값을 비교
  				then x <- left[x]			//1-1-1.z가 작으면 왼쪽으로
  				else x <- right[x]			//1-1-2.z가 크면 오른쪽으로 한칸씩 전진
  	p[z] <- y						//2. 결과 세팅 : z의부모노드주소=y로 세팅
  	if y = NIL							//2-1. y=null인 경우 : T가 empty Tree인 경우
  		then root[T] <- z				//2-1. empty Tree의 루트노드로 z를 추가
  		else if key[z] < key[y]			//2-2. 빈 트리가 아닌 경우
  				then left[y] <- z			//2-2-1. 부모보다 작으면 왼쪽노드에 추가
  				else right[y] <- z			//2-2-2. 부모보다 크면 오른쪽노드에 추가.
  ```

- **시간복잡도 : O(h)**   //h : 트리의 높이



### DELETE

------

키 14를 추가 > 12의 오른쪽 노드에 삽입

- **Case**
  1. **자식**노드가 **없는** 경우 ▷ 그냥 삭제
  2. **자식**노드가 **1개**인 경우 ▷ 자식노드를 원래 자신의 위치로
  3. **자식**노드가 **2개**인 경우 ▷ 삭제하려는 노드의 successor(또는 Predecessor)를 자신의 위치로 가져오고 해당 노드는 삭제(case1 or 2에 해당).

- **pseudocode**

  T : 트리, z : DELETE할 노드, x , y  : 실제 삭제할 노드

  ```pseudocode
  TREE-DELETE(T,z)
  1	if left[z] = NIL or right[z] = NIL//1. case 판별
  2		then y <- z						//1-1. y에 z를 넣고
  3		else y <- TREE-SUCCESSOR(z)		//1-2. case 3인 경우 > y에 z의 successor를 넣음
  4	if left[y] ≠ NIL				//2. 노드y를 삭제(y의 자식은 0 or 1개임)
  5		then x <- left[y]				//2-1. y의 자식 여부에 따라 x값 처리
  6		else x <- right[y]				
  7	if x ≠ NIL							//2-2. y의 자식이 없는 경우 처리
  8		then p[x] <- p[y]
  9	if p[y] = NIL						//2-3. y의 부모 여부에 따라 처리
  10		then root[T] <- x					//2-3-1. y=루트노드면, x를 루트값으로 넣음.
  11		else if y = left[p[y]]				//2-3-2. 부모 있는 경우,왼쪽,오른쪽 여부로 처리
  12				then left[p[y]] <- x			
  13              else right[p[y]] <- x             
  14  if y ≠ z						//3. case3인 경우만 실행      
  15		then key[z] <- key[y]    			//3-1.successor=y를 z자리로 옮기고 
  16			copy y's satellite data into z	//3-2.y값을 z로 바꿈
  17	return y						//4. 삭제값 리턴
  ```

- **시간복잡도 : O(h)**

  최악의 경우 O(n)



### Balanced Tree

------

키의 삽입이나 삭제시 추가로 트리의 균형을 잡아줌으로써 높이를 O(log2n)으로 유지시켜주는 이진검색트리

이진검색트리를 개선. (최악의 경우에도 O(log2n)을 넘지 않도록 하기 위함.)

- 코드는 복잡하지만 효율 면에서 더 좋음

- 레드-블랙 트리 등..