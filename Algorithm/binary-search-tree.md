## 이진검색트리(Binary Search Tree)

- 트리
  - 데이터 자체가 계층적인 형태를 가지고 있을 때 트리 자료구조를 사용
- 검색트리
  - 데이터 자체가 계층적인 형태를 가지고 있는 것이 아니라 일종의 컨테이너(집합)
    - 배열, 연결리스트 사용

### Dynamic Set

- 일종의 집합
- 여러개의 데이터를 저장하고 있는데 데이터들이 고정되어있지 않고 새로운 데이터가 추가되거나 삭제 등의 내용이 변함
- 여러 개의 키(key)를 저장
- 다음과 같은 연산들을 지원하는 자료구조
  - INSERT - 새로운 키의 삽입
  - SEARCH - 키 탐색
  - DELETE - 키의 삭제
- ex) 심볼 테이블
- Dynamic Set === Dictionalry === Search Structure

### 다양한 방법들

- 정렬된 혹은 정렬되지 않은 배열 혹은 연결 리스트를 사용할 경우
  - INSERT, SEARCH, DELETE 중 적어도 하나는 O(n)
- 이진탐색트리(Binary Search Tree, 레드-블랙 트리, AVL-트리등의 트리에 기반한 구조들
- Direct Address Table, 해쉬 테이블 등

### 검색트리

- Dynamic set을 트리의 형태로 구현
- 일반적으로 SEARCH, INSERT, DELETE 연산이 트리의 높이(height)에 비례하는 시간복잡도를 가짐
- 이진검색트리(Binary Search Tree), 레드-블랙 트리(red-black tree), B-트리 등

### 이진검색트리(BST)

![스크린샷 2022-06-24 오후 5 56 27](https://user-images.githubusercontent.com/52994378/175501169-27a6bd87-b064-495a-a3d5-7f687167c706.png)

- 이진 트리이면서
- 각 노드에 하나의 키를 저장
- 각 노드 v에 대해서 그 노드의 왼쪽 부트리(subtree)에 있는 키들은 key[v](v에 저장된 key)보다 작거나 같고, 오른쪽 부트리에 있는 값은 크거나 같다.

#### heap과 BST의 차이

- heap
  - 형태: Complete Binary Tree
  - max heap의 경우 max heap property를 만족해야함
    - 트리에서 부모는 자식보다 크거나 같다
- BST
  - 형태: 제약이 없으며, Binary Tree이기만 하면 됨
  - 왼쪽 subtree는 부모보다 작거나 같고, 오른쪽 subtree는 부모보다 크거나 같다

### BST 연산

#### SEARCH

- 특정한 값이 있는지 없는지, 있다면 어디에 있는지 찾는 연산

![스크린샷 2022-06-24 오후 6 01 16](https://user-images.githubusercontent.com/52994378/175501913-53cacae9-090a-4855-8a45-7d5c4e9ed38c.png)

- root노드에 접근해서 찾는 데이터인지 비교
- root노드의 데이터가 찾는 데이터가 아니고, 찾는 데이터가 root노드의 데이터보다 작을시에 찾는 데이터가 존재한다면 필시 왼쪽 subtree에 위치해 있을 것이므로 왼쪽 subtree 탐색
- root의 자식노드를 접근해서 찾는 데이터인지 비교
- root의 자식노드의 데이터가 찾는 데이터가 아니고, 찾는 데이터가 root의 자식노드의 데이터보다 클시에 찾는 데이터가 존재한다면 필시 오른쪽 subtree에 위치해 있을 것이므로 오른쪽 subtree 탐색
- 위의 법칙을 이용하여 반복하여 데이터를 search

##### psudo code

- recursion version

```java
TREE-SEARCH(x, k) // x: 트리의 노드(처음 호출 시 x는 root 노드), k: 찾는 값
    if x == NIL or k == key[x] // key[x]: 노드 x 에 저장된 값
        then return x
    if k < key[x]
        then return TREE-SEARCH(left[x], k)
        else return TREE-SEARCH(right[x], k)
```

- iterative version

```java
ITERATIVE-TREE-SEARCH(x, k)  // x: 트리의 노드(처음 호출 시 x는 root 노드), k: 찾는 값
    while x != NIL and k != key[x]
        do if k < key[x]
            then x <- left[x]
            else x <- right[x]
    return x
```

- 시간복잡도: O(h), h는 높이

### 참고

- [영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C)
