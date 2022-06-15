## 정렬의 lower bound

### 정렬 알고리즘들의 시간 복잡도

- bubble Sort : O(n^2)
- selection Sort: O(n^2)
- insertion Sort: O(n^2)
- quick Sort:
  - 최악의 경우: O(n^2)
  - 평균: O(nlogn)
- merge Sort: O(nlogn)
- heap Sort: O(nlogn)

-> O(nlogn)보다 더 낮은 시간복잡도는 없을까?

### 정렬 알고리즘의 유형

#### Comparison sort

- 데이터들간의 **상대적 크기관계** 만을 이용해서 정렬하는 알고리즘
- 따라서 데이터들간의 크기 관계가 정의되어 있으면 어떤 데이터에서든 적용 가능(문자열, 알파벳, 사용자 정의 객체 등)
- 버블 소트, 삽입 정렬, 합병 정렬, 퀵소트, 힙정렬 등

#### Non-comparison sort

- 정렬할 데이터에 대한 **사전지식**을 이용 - 적용에 제한
  - ex) 두자리 정수, 영문 알파벳 ..
- Bucket sort
- Radix sort

### 정렬문제의 하한

#### 하한(Lower bound)

- 입력된 데이터를 한번씩 다 보기 위해서 최소O(n)의 시간복잡도 필요
- 합병절렬과 힙정렬 알고리즘들의 시간복잡도는 O(nlog2n)
- 어떤 comparison sort 알고리즘도 O(nlog2n)보다 나을 수 없다.

### Decison Tree

<img width="408" alt="스크린샷 2022-06-15 오후 12 54 01" src="https://user-images.githubusercontent.com/52994378/173733589-c8d0985e-4f9e-4aaf-a34d-6f897b1c7da0.png">

- Decision Tree
  - 임의의 comparision sort 알고리즘이 있다고 가정
  - n개의 데이터가 입력으로 주어졌을 때 comparison sort가 정렬을 하기 위해서 값들을 비교해가는 전체 과정을 하나의 tree로 표현
- 모든 경우의 수를 가지고 decison tree를 구현
- leaf노드의 개수는 n!개. 왜냐하면 모든 순열()에 해당되기 때문
- 최악의 경우 시간복잡도는 Decision Tree의 높이에 비례
- 트리의 높이는
  - height >= log2n! = O(nlog2n)
  - full binary tree, Complete binary tree 일 때 전체 노드 개수 n개를 유지하면서 높이가 가장 낮출 수 있는 방법 -> 높이 log2n
  - 전체 노드의 개수가 n!보다 많다면 높이는 log2n!보다 낮을 수 없음
  - 따라서 O(nlog2n)
