# Comparison sort의 하한(lower bound)

- **Comparison sort**
  - 데이터들간의 **상대적 크기 관계**만을 이용해서 정렬하는 알고리즘
  - 따라서 데이터들간의 크기 관계가 정의되어 있으면 어떤 데이터에든 적용 가능(문자열, 알파벳, 사용자 정의 객체 등)
  - 버블정렬, 삽입정렬, 합병정렬, 퀵정렬, 힙정렬 등
- **Non-Comparison sort**
  - 정렬할 데이터에 대한 **사전지식**을 이용 - 적용에 제한
  - Bucket sort
  - Radix sort



#### Comparison sort의 하한

- **하한(Lower bound)**
  - 입력된 데이터를 한번씩 다 보기 위해서 최소 O(n)의 시간복잡도 필요
  - 합병 정렬과 힙정렬 알고리즘들의 시간복잡도는 O(nlog2n)
  - 어떤 comparison sort 알고리즘도 O(nlog2n)보다 나을 수 없다.

