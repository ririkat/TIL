# 이진트리(Binary Tree)

> **모든 노드가 자식을 최대 2개만 가지는 트리**
>
> 자식노드는 왼쪽 자식과 오른쪽 자식으로 구분된다.



### Full and Complete Binary Trees

------

높이가 h인 full bianry tree는 2^h-1개의 노드를 가진다.

노드가 N개인 full 혹은 complete 이진 트리의 높이는 O(logN)이다.



### 이진트리의 표현

------

#### 연결구조(Linked Structure) 표현

- 각 노드에 하나의 데이터 필드와 왼쪽자식(left), 오른쪽 자식(right), 그리고 부모노드(p)의 주소를 저장

  (부모노드의 주소는 반드시 필요한 경우가 아니면 보통 생략 함)

- 루트노드의 주소는 따로 보관.



### 이진트리의 순회

------

> 순회 = 이진트리의 모든 노드를 방문하는 일
>
> 루트를 언제 도느냐에 따라 중,선,후순위로 나뉜다. (자식은 왼->오 순서)



#### 중순위(inorder) 순회

- **왼쪽 ▷ 루트 ▷ 오른쪽** 순으로 순회

- **pseudocode**

  ```pseudocode
  INORDER-TREE-WALK(x)
  1	if x≠NIL
  2		then INORDER-TREE-WALK(left[x])
  3			print key[x]
  4			INORDER-TREE-WALK(right[x])
  ```

  x를 루트로 하는 트리를 inorder 순회

- **시간복잡도 O(n)**



#### 선순위(preorder) 순회

- **루트 ▷ 왼쪽 ▷ 오른쪽** 순으로 순회

- Expression트리 출력시 사용

- **pseudocode**

  ```pseudocode
  PREORDER-TREE-WALK(x)
  1	if x≠NIL
  2		then print key[x]
  3			PREORDER-TREE-WALK(left[x])
  4			PREORDER-TREE-WALK(right[x])
  ```

  x를 루트로 하는 트리를 preorder순회

- **시간복잡도 O(n)**

  

#### 후순위(postorder) 순회

- **왼쪽 ▷ 오른쪽 ▷ 루트** 순으로 순회

- **pseudocode**

  ```pseudocode
  POSTORDER-TREE-WALK(x)
  1	if x≠NIL
  2		then POSTORDER-TREE-WALK(left[x])
  3			POSTORDER-TREE-WALK(right[x])
  4			print key[x]
  ```

  x를 루트로 하는 트리를 postorder순회

- **시간복잡도 O(n)**



#### 레벨오더(level-order) 순회

- **레벨** 순으로 순회, 동일 레벨에서는 왼쪽 ▷ 오른쪽 순서

- **큐(queue)**를 이용하여 구현

- **pseudocode**

  ```pseudocode
  LEVEL-ORDER-TREE-TRAVERSAL()
  1	visit the root;
  2	Q <- root;		//Q is a queue
  3	while Q is not empty do
  4		v <- dequeue(Q);
  5		visit children of v;
  6		enqueue children of v into Q;
  7	end.
  ```