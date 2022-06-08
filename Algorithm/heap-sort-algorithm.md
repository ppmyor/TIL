## 힙 정렬(heap Sort)

- 최악의 경우 시간복잡도 O(nlog2n)
- Sorts in place - 추가 배열 불필요
  - merge sort 같은 경우는 추가 배열 필요
- 이진 힙(binary heap) 자료구조를 사용

### heap

#### 정의

1. complete binary tree이면서

   - binary tree: 트리의 각 노드가 최대 두개의 자식을 가지는 트리
     - 자식이 하나이더라도 부모의 왼쪽 자식인지 오른쪽 자식인지 정해져있음
   - complete binary tree: 마지막 레벨을 제외하면 완전히 꽉 차있고, 마지막 레벨에는 가장 오른쪽부터 연속된 몇 개의 노드가 비어있을 수 있음
   - full binary tree: 모든 레벨에 노드들이 꽉 차있는 형태
     - full binary tree는 그 자체로 complete binary tree임

2. heap property를 만족해야함
   - max heap property: 부모는 자식보다 크거나 같다
   - min heap property: 부모는 자식보다 작거나 같다
3. 동일한 데이터를 가진 여러가지 모양의 heap이 있을 수 있다.

#### 표현

- 힙은 논리적으로는 binary tree이지만 일차원 배열로 표현 가능: A[1...n](n은 노드 개수)
  - 레벨 순서대로(같은 레벨상에서는 오른쪽에서 왼쪽으로) 해서 일차원배열로 정렬
- 루트 노드 A[1]
- A[i]의 부모 = A[i/2]
- A[i]의 왼쪽 자식 = A[2i]
- A[i]의 오른쪽 자식 = A[2i+1]

#### 기본 연산: MAX-HEAPIFY

- 전체를 힙으로 만들어라
  <img width="499" alt="스크린샷 2022-06-08 오후 5 45 40" src="https://user-images.githubusercontent.com/52994378/172573633-51226024-96c4-49bb-8af3-9098eacdfe7c.png">

1. 트리의 전체 모양은 complete binary tree여야하고,
2. 왼쪽 서브트리는 그 자체로 heap이고
3. 오른쪽 서브트리도 그 자체로 heap일 때
4. 유일하게 루트만이 heap property를 만족하지 않은 상황에서
5. 트리 전체를 heap으로 만들어주는 연산 -> heapify

##### 원리

- 두 자식들 중 더 큰 쪽이 나보다 크면 exchange한다.
- recursive

##### psudo code

- recursive version

```java
MAX-HEAPIFY(A, i)
{
    if there is no child of A[i]
        return;
    k <- index of the biggest child of i;
    if A[i] >= A[k]
        return;
    exchange A[i] and A[k];
    MAX-HEAPIFY(A, k);
}
```

- 노드 i를 루트로 하는 서브트리를 heapify한다.
- A는 1차원 배열
- i는 heapify의 대상이 되는 노드
- root노드에 대한 heapify는 MAX-HEAPIFY(1)을 호출하면 됨

- iterative version

```java
MAX-HEAPIFY(A, i)
{
    while A[i] has a child do
        k <- index of the biggest child of i;
        if A[i] >= A[k]
            return;
        exchange A[i] and A[k];
        i=k; // 자식 노드를 루트로 하는 새로운 heapify 수행
    end
}
```

- 트리의 높이를 h라고 한다면 max-heapify 연산의 시간복잡도는 O(h)
  - complete binary tree에서 노드 수를 n이라고 한다면 h=logn
  - 따라서 시간복잡도는 O(logn)

### 참고

- [영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C)
