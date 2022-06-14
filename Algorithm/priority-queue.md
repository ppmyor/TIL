## 힙의 응용: 우선순위 큐

- 자료구조 상의 queue: FIFO(first in first out)
  - 순서를 우선순위라고 본다면 우선순위 큐의 일종
- 최대 우선순위 큐(maximum priority queue)는 다음의 두가지 연산을 지원하는 자료구조
  - INSERT(x): 새로운 원소 x를 삽입
  - EXTRACT_MAX(): 최대값을 삭제하고 반환
- 최소 우선순위 큐(minimum priority queue)는 EXTRACT_MAX 대신 EXTRACT_MIN을 지원하는 자료구조
- MAX HEAP을 이용하여 최대 우선순위 큐를 구현

### INSERT 연산 원리

- 기본적으로 heap이 되려면 complete binary tree, max heap의 조건을 만족해야 함

1. 새로운 노드를 추가해야하므로 heap 의 맨 마지막 자리에 새로운 값 추가
2. 문제 노드와 부모 노드를 비교해서 크다면 자리를 exchange 하는 과정을 문제 노드가 부모 노드보다 작을 때까지 혹은 root까지 올라가는 과정까지 반복

### INSERT 연산 psudo code

```java
MAX-HEAP-INSERT(A, key) { //A: heap, key: insert node
    heap_size = heap_size + 1; // 새로 추가 되는 노드를 위해 length를 1 증가
    A[heap_size] = key; // 새로 추가 되는 노드를 배열의 끝자리에 추가
    i = heap_size; //문제 노드의 index
    while(i>1 and A[PARENT(i)] <A[i])   { //A가 root가 아님, A[PARENT(i)]: 부모 노드의 값, A[i]: 문제 노드의 값
        exchange A[i] and A[PARENT(i)];
        i = PARENT(i); //문제 노드의 부모 노드가 새로운 문제 노드
    }
}
```

시간복잡도: O(log2n)

### EXTRACT_MAX() 연산 원리

- heap으로부터 최대값을 삭제하고 반환하는 연산
- heap에서 최대값은 항상 root에 존재

1. root 에 있는 값을 삭제하고 노드의 개수를 하나 줄임
   - 노드의 개수가 하나 줄어야 하는데, complete binary tree 모양을 유지해야하므로 root노드의 데이터가 삭제되고 빈 노드만 남김
   - complete binary tree모양을 유지하기 위해 삭제해도 되는 노드는 마지막 노드 밖에 없기 때문에 마지막 노드 자체가 삭제되고, 마지막 노드에 있는 데이터를 root노드로 옮김
2. root 만이 heap property를 만족하지 못하는 상황이니 MAX-HEAPIFY 연산을 진행

### EXTRACT_MAX() 연산 psudo code

```java
HEAP-EXTRACT-MAX(A)
    if heap-size[A] < 1
        then error "heap underflow" // heap이 빈 것에 대한 예외 처리
    max <- A[1] // root 노드의 데이터를 max에 저장 후 return
    A[1] <- A[heap-size[A]] // 맨 마지막 노드에 있는 값을 root로 옮김
    heap-size[A] <- heap-size[A] - 1 // 맨 마지막 노드 삭제
    MAX-HEAPIFY(A, 1) // heap조건을 만족시키기 위해 MAX-HEAPIFY 연산 진행
    return max
```

시간 복잡도 : O(log2n)

### 참고

- [영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C)
