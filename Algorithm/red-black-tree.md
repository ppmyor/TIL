## 레드블랙트리(Red Black Tree)

- 이진탐색트리의 일종
- 균형잡힌 트리: 높이가 O(log2n)
- SEARCH, INSERT, DELETE 연산을 최악의 경우에도 O(log2n) 시간에 지원

![스크린샷 2022-06-30 오후 10 06 09](https://user-images.githubusercontent.com/52994378/176684684-147ae7c1-ed79-44f9-bf2f-26738b2d3177.png)

- 각 노드는 하나의 키(key), 왼쪽자식(left), 오른쪽 자식(right), 그리고 부모노드(p)의 주소를 저장
- 자식노드가 존재하지 않을 경우 NIL 노드라고 부르는 특수한 노드가 있다고 가정
- 따라서 모든 리프노드는 NIL노드
- 루트의 부모도 NIL노드라고 가정
- 노드들은 내부노드와 NIL노드로 분류

### 정의

- 다음의 조건을 만족하는 이진탐색트리:
  1. 각 노드는 red 혹은 black이고,
  2. 루트노드는 black이고,
  3. 모든 리프노드(즉, NIL노드)는 black이고,
  4. red노드의 자식노드들은 전부 black이고(즉, red노드는 연속되어 등장하지 않고),
  5. 모든 노드에 대해서 그 노드로부터 자손인 리프노드에 이르는 모든 경로에 동일한 개수의 black노드가 존재한다.

### 레드-블랙 트리의 높이

![스크린샷 2022-06-30 오후 10 19 17](https://user-images.githubusercontent.com/52994378/176687415-00048ffc-6fc7-4d95-bdc6-e30aa55cf5f2.png)

- 노드 x의 높이 h(x)는 자신으로부터 리프노드까지의 가장 긴 경로에 포함된 edge의 개수이다.
- 노드 x의 블랙-높이 bh(x)는 x로부터 리프노드까지의 경로상의 블랙노드의 개수이다(노드 x 자신은 불포함)

- 높이가 h인 노드의 블랙-높이는 bh >= 2 이다.
  - 조건 4에 의해 레드노드는 연속될 수 없으므로 당연
- 노드 x를 루트로 하는 임의의 부트리는 적어도 2^(bh(x)) - 1개의 내부노드를 포함한다(수학적 귀납법)
- n개의 내부노드를 가지는 레드블랙트리의 높이는 2log2(n+1) 이하이다.
  - n >= 2^(bh) - 1 >= 2^(h/2) - 1 이므로, 여기서 bh와 h는 각각 루트 노드의 블랙-높이와 높이가 같다

### 레드-블랙 트리 연산

#### Search

- 이진검색트리의 일종이기 때문에 Search는 크게 신경 쓸 필요 없음

#### Left and Right Rotation

![스크린샷 2022-06-30 오후 10 54 48](https://user-images.githubusercontent.com/52994378/176695467-b5e815dd-7759-404a-b3d2-be5574af5867.png)

- 이진검색트리에서 한 노드를 중심으로 부분적으로 노드의 모양에 변형을 가함
- 시간복잡도 O(1)
- 이진탐색트리의 특성을 유지

##### Left Rotataion

![스크린샷 2022-06-30 오후 11 18 20](https://user-images.githubusercontent.com/52994378/176700908-fd7095c3-8e61-4667-936a-df8a720b47b5.png)

- y = right[x] != NIL이라고 가정
- 루트노드의 부모도 NIL이라고 가정

- psudo code

```java
LEFT-ROTATE(T, x) // T:레드블랙트리 x: left rorate를 실행 할 노드
    y <- right[x] // y의 왼쪽 자식을 x의 오른쪽 자식으로
    right[x] <- left[y] // y의 왼족 자식의 부모를 x
    p[left[y]] <- x
    p[y] <- p[x] //x의 부모를 y의 부모로
    if p[x] == nil[T] // x가 root
        then root[T] <- y //y가 새로운 트리의 root
        else if x == left[p[x]] //x의 부모노드가 존재한다면 y의 부모가 x의 부모가 되면서 그 노드의 자식이 x가 아니라 y
            then left[p[x]] <- y // x가 부모의 왼쪽 자식이라면 y가 x 부모의 왼쪽 자식
            else right[p[x]] <- y // x가 부모의 오른쪽 자식이라면 y가 x 부모의 오른쪽 자식
    left[y] <- x // x가 y의 왼쪽 자식
    p[x] <- y // x의 부모가 y
```

- 시간복잡도: O(1)

### 참고

- [영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C)
