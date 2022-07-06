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

#### Insert

- 보통의 BST에서처럼 노드를 INSERT한다.
- 새로운 노드 z를 red노드로 한다.
- RB-INSERT-FIXUP을 호출한다.

- psudo code

```java
RB-INSERT(T, z) //T: 레드블랙트리 z: insert 할 노드
  y <- nil[T]
  x <- root[T]
  while x != nil[T]
    do y <- x
      if key[z] < key[x]
        then x <- left[x]
        else x <- right[x]
  p[z] <- y
  if y == nil[T] // y가 null인 것은 empty tree
    then root[T] <- z // 새로운 노드가 root
    else if key[z] < key[y]
      then left[y] <- z
      else right[y] <- z
  left[z] <- nil[T]
  right[z] <- nil[T]
  color[z] <- RED // 새로 insert한 노드의 색은 red
  RB-INSERT-FIXUP(T, z) // z: insert한 새로운 노드, 레드 블랙 트리의 규칙을 위반 할 가능성이 다분하므로 다시 fix
```

##### RB-INSERT-FIXUP

- 위반될 가능성이 있는 조건들

1. 모든 노드는 red와 black 이어야 한다. -> OK.
2. 루트노드는 black 이어야 한다. -> 만약 z가 루트노드라면 위반, 아니라면 OK.
3. 모든 nil 노드는 black 이어야 한다.-> OK.
4. red가 연속해서는 안된다. -> z의 부모 p[z]가 red이면 위반.
5. 어떤 노드에서 출발하더라도 nil까지 이르는 동안 만나는 black 노드의 개수는 동일해야한다. -> OK.

- r-r 위반은 루프를 돌면서, r-r위반을 트리의 위쪽으로 올림.
- Loop Invariant:

  - z는 red노드
  - 오직 하나의 위반만이 존재한다:
    - 조건 2: z가 루트노드이면서 red 이거나, 또는
    - 조건 4: z와 그 부모 p[z]가 둘 다 red이거나
  - 종료조건:
    - 부모노드 p[z]가 black이 되면 종료한다. 조건 2가 위반일 경우 z를 black으로 바꿔주고 종료한다.

- 경우 1: z의 삼촌이 red
  <img width="536" alt="스크린샷 2022-07-06 오후 12 36 44" src="https://user-images.githubusercontent.com/52994378/177462887-3ac1c476-6523-4f64-ada5-2e69cc78741c.png">

  - 부모가 red인 경우에는 할아버지 노드가 반드시 존재(루트노드는 무조건 black)

  1. 부모가 할아버지 노드의 왼쪽 자식이면서
  2. 본인, 부모 노드, 삼촌 노드: red, 할아버지 노드: black

  - 부모 노드, 삼촌 노드의 색과 할아버지 노드의 색을 switch
  - 즉, 부모와 삼촌 노드의 색을 black으로 바꾸어주고 할아버지 노드를 red로 바꿈.
  - r-r 위반이 두레벨 위로 올라감.

- 경우 2와 3: z의 삼촌이 black
  <img width="556" alt="스크린샷 2022-07-06 오후 12 37 02" src="https://user-images.githubusercontent.com/52994378/177462916-2e72c260-14db-452c-8e94-dc0a28dc0a53.png">

  - 삼촌의 노드는 black이므로 nil노드 일 가능성도 있음

  1. 부모가 할아버지 노드의 왼쪽 자식이면서
  2. z의 삼촌이 black

  - 경우 2: z가 오른쪽 자식인 경우
    - p[z]에 대해서 left-rotation한 후 원래 p[z]를 z로 하고 경우 3으로 넘김
  - 경우 3: z가 왼쪽 자식인 경우
    - p[z]를 black, p[p[z]]를 red로 바꿈
    - p[p[z]]에 대해서 right-rotation
    - 부모였던 노드가 새로 z가 됨.
    - 할아버지를 중심으로 right-rotation을 하면, z의 부모가 위로 올라가고 할아버지가 부모의 오른쪽 자식으로 내려감.
    - 부모와 할아버지 노드의 색을 exchange

- 경우 1, 2, 3은 p[z]가 p[p[z]]의 왼쪽 자식인 경우들
- 경우 4, 5, 6은 p[z]가 p[p[z]]의 오른쪽 자식인 경우들

  - 경우 1, 2, 3과 대칭적이므로 생략

- psudo code

```java
RB-INSERT-FIXUP(T, z) // z: red
  while color[p[z]] == RED //z의 부모가 red인 동안(r-r 충돌인 경우)
    do if p[z] == left[p[p[z]]] // z의 부모가 할아버지 노드의 왼쪽자식인 동안
      then y <- right[p[p[z]]]
        if color[y] == RED //  부모와 삼촌이 red, 할아버지는 black
          then color[p[z]] <- BLACK //Case 1
                color[y] <- BLACK //Case 1
                color[p[p[z]]] <- RED //Case 1
                z <- p[p[z]] //Case 1 -> 할아버지를 새로운 문제 노드로 변경
          else if z == right[p[z]]
                then z <- p[z] //Case 2
                      LEFT-ROTATE(T,z) //Case 2
                color[p[z]] <- BLACK //Case 3
                color[p[p[z]]] <- RED //Case 3
                RIGHT-ROTATE(T, p[p[z]]) //Case 3
      else (same as then clause whit "right" and "left" exchanged) // Case 4, 5, 6
  color[root[T]] <- BLACK // Case 1이나 Case 4 인 경우로 빠져나온다면 루트가 red이므로 BLACK으로 바꾸어주는 코드 추가
```

<img width="410" alt="스크린샷 2022-07-06 오후 1 19 03" src="https://user-images.githubusercontent.com/52994378/177467406-e0c0783c-3a82-49ba-b7c8-d96bb7d49110.png">

- BST에서의 INSERT: O(log2n)
- RB-INSERT-FIXUP
  - 경우 1에 해당 할 경우 z가 2레벨 상승
  - 경우 2에 해당 할 경우 O(1)
  - 따라서 트리의 높이에 비례하는 시간
- 즉, INSERT의 시간복잡도는 O(log2n)

### 참고

- [영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C)
