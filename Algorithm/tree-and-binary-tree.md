## 트리와 이진트리(tree and binary tree)

### 트리(Tree)

- 계층적인 구조를 표현
  - 조직도
  - 디렉토리와 서브디렉토리 구조
  - 가계도
- 트리는 노드(node)들과 노드들을 연결하는 링크(link)들로 구성됨
  - 맨 위의 노드를 "root"라고 부름
  - 노드들을 연결하는 선을 "link", "edge", "branch"등으로 부름
- 부모-자식 관계
  - 두 노드의 입장에서 위에 있는 노드를 부모(parent)노드
  - 아래에 있는 노드를 자식(child)노드
- 형제 관계
  - 부모가 동일한 노드들을 형제(sibling)관계라고 부름
  - 루트노드를 제외한 트리의 모든 노드들응ㄴ 유일한 부모 노드를 가짐
- 리프(leaf) 노드
  - 자식이 없는 노드들을 leaf노드라고 부름
  - 리프노트가 아닌 노드들을 내부(internal)노드라고 부름
- 조상-자손 관계
  - 부모-자식 관계를 확장한 것이 조상-자손(ancestor-descendant)관계이다
  - 부모의 부모: 조상(ancestor)노드
  - 자식의 자식: 자손(descendant)노드
- 서브트리(부트리)
  - 전체 트리의 일부분인 또 다른 트리
  - 트리에서 어떤 한 노드와 그 노드의 자손들로 이루어진 트리를 부트리(subtree)라고 부른다.
- level
  - 트리에서 높이별로 level을 나눔
  - 루트: level 1
- 높이
  - 서로 다른 레벨의 개수

#### 트리의 기본적인 성질

- 노드가 n개인 트리는 항상 n-1개의 링크(link)를 가진다.
- 트리의 루트에서 어떤 노드로 가는 경로는 유일하다. 또한, 임의의 두 노드간의 경로도 유일하다.(같은 노드를 두 번 이상 방문하지 않는다는 조건하에)

### 이진 트리(binary tree)

- 이진 트리에서 각 노드는 최대 2개의 자식을 가진다.
- 각각의 자식 노드는 자신이 부모의 왼쪽 자식인지 오른쪽 자식인지가 지정된다.(자식이 한명인 경우에도)

#### 이진 트리 응용의 예

##### Expression Tree

<img width="336" alt="스크린샷 2022-06-16 오후 2 55 05" src="https://user-images.githubusercontent.com/52994378/174001301-a3146d7e-5220-4f6e-a240-955132397c2d.png">

- 컴파일러가 수식을 해석: 파싱
- 수식을 위의 트리 모양으로 해석하는 경우가 많음
- 수식을 어떤 순서로 계산해야하는지를 표현하고 있는 트리

##### Hffman Code

  <img width="626" alt="스크린샷 2022-06-16 오후 2 56 51" src="https://user-images.githubusercontent.com/52994378/174001603-9d7de948-e816-4cbb-bed5-83e37afa7caf.png">

- 어떤 데이터를 압축하는 혹은 인코딩하는 가장 기본적인 알고리즘
- 가변 length일 때 최소의 length로 압축
- 각각의 알파벳에 부여된 이진코드들을 하나의 트리의 형태로 표현

#### Full and Complete Binary Trees

- Full Binary Tree
  - 모든 레벨에서 노드가 다 꽉꽉 들어차있는 형태
  - 높이가 h인 full binary tree는 2^h - 1 개의 노드를 가진다.
  -
- Complete Binary Tree

  - heap
  - 맨 마지막 레벨을 제외한 나머지 레벨에는 모두 노드가 차있어야하고, 맨 마지막 레벨은 노드가 빌 수 있으나 오른쪽에서부터 빌 수 있음

- 노드가 n개인 full 혹은 complete 이진 트리의 높이는 O(logN)이다.(노드가 n개인 이진트리의 높이는 최악의 경우 n이 될수도 있다.)

#### 이진트리의 표현

##### 연결구조(Linked Structure) 표현

<img width="570" alt="스크린샷 2022-06-16 오후 3 07 50" src="https://user-images.githubusercontent.com/52994378/174002946-37fe685c-204c-4620-acc7-359fe22ba8c2.png">

<img width="631" alt="스크린샷 2022-06-16 오후 3 08 45" src="https://user-images.githubusercontent.com/52994378/174003044-c2f5d8c7-e17b-41fb-9ce8-9feeffccaf2c.png">

- 각 노드에 하나의 데이터 필드와 왼쪽자식(left), 오른쪽 자식(right), 그리고 부모 노드(p)의 주소를 저장 (부모노드의 주소는 반드시 필요한 경우가 아니면 보통 생략함)

#### 이진트리의 순회(travelsal)

- 순회: 이진 트리의 모든 노드를 방문하는 일
- 중순위(inorder) 순회
- 선순위(preorder) 순회
- 후순위(postorder) 순회
- 레벨오더(level-order) 순회

##### 이진트리의 Inorder-순회

<img width="576" alt="스크린샷 2022-06-16 오후 3 13 28" src="https://user-images.githubusercontent.com/52994378/174003709-12a1d1bc-a28c-455e-8795-0ea16012d921.png">
1. 먼저 TL을 inorder로 순회하고,
2. r을 순회하고,
3. TR을 inorder로 순회.

<img width="640" alt="스크린샷 2022-06-16 오후 3 16 31" src="https://user-images.githubusercontent.com/52994378/174004127-3ed446b1-3494-4c4e-8dea-dcca7e3e5d76.png">

```java
INORDER-TREE-WALK(x)
    if x != null
        then INORDER-TREE-WALK(left[x])
            print key[x]
            INORDER-TREE-WALK(right[x])
```

- x 를 루트로 하는 트리를 inorder 순회
- 시간복잡도: O(n)

##### Postorder와 Preorder 순회

- inorder와 동일하게 왼쪽 트리, 루트, 오른쪽 트리로 나누고 방문하는 순서만 다름

- preorder
  1. 먼저 루트를 방문
  2. 루트의 왼쪽 서브트리를 preorder로 방문
  3. 루트의 오른쪽 서브트리를 preorder로 방문

```java
PREORDER-TREE-WALK(x)
    if x != null
    then print key[x]
        PRE-ORDER-TREE-WALK(left[x])
        PRE-ORDER-TREE-WALK(right[x])
```

- postorder
  1. 루트의 왼쪽 서브트리를 postorder로 방문
  2. 루트의 오른쪽 서브트리를 preorder로 방문
  3. 루트를 마지막에 방문

```java
POSTORDER-TREE-WALK(x)
    if x != null
    then POST-ORDER-TREE-WALK(left[x])
        POST-ORDER-TREE-WALK(right[x])
        print key[x]
```

<img width="274" alt="스크린샷 2022-06-16 오후 3 31 55" src="https://user-images.githubusercontent.com/52994378/174006381-f8805fb5-a7c5-44ae-a977-89c2a01acafc.png">

- inorder 순회: x + y \* a + b / 2
- 각 부트리를 순회할 때 시작과 종료시에 괄호를 추가하면 다음과 같이 올바른 수식이 출력됨
  - (x + y) \* ((a + b) / c)
- postorder 순회하면 후위표기식이 출력됨: x y + a b + c / \*

##### Level-Order 순회

<img width="380" alt="스크린샷 2022-06-16 오후 3 35 34" src="https://user-images.githubusercontent.com/52994378/174006925-0e152de2-d426-409e-8a25-9b8bdfc0979d.png">

- 레벨 순으로 방문, 동일 레벨에서는 왼쪽에서 오른쪽 순서로
- 큐(queue)를 이용하여 구현

```java
LEVEL-ORDER-TREE-TRAVERSAL()
    visit the root;
    Q <- root; //Q is a queue
    while Q is not empty do
        v <- dequeue(Q);
        visit children of v;
        enqueue children of v into Q;
    end.
end.
```

### 참고

- [영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C)
