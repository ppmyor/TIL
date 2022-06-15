## 선형시간 정렬 알고리즘

- 시간 복잡도: O(n)
- Comparision Sort가 아님

### Counting Sort

- n개의 정수를 정렬
- 단, 모든 정수는 0에서 k사이의 정수(사전 지식)
- ex) n명의 학생들의 시험점수를 정렬하라. 단 모든 점수는 100 이하의 양의 정수이다.

- k=5인 경우의 예
- 길이 k인 배열에 각 정수의 개수를 count
- 개수 만큼 늘려주면 원래 데이터를 정렬한 결과

#### code

```java
int A[n]; //정렬 할 데이터 (0~k사이의 정수)
int C[k] = {0, };
for(int i=1; i<=n; i++)
    C[A[i]]++;
for(int s=1, i=0; i<=k i++) {
    for(int j=0; j<C[i]; j++)   {
        A[s++] = i; //s: 출력할 배열의 index
    }
}
```

- 대부분의 경우 정렬할 key값들은 레코드의 일부분이기 때문
- 카운터들의 누적합을 계산
- 해당 데이터의 계산된 누적합의 값을 index로 하여 자리 배치
- 배치한 데이터의 누적합 1감소
- 반복하여 정렬

#### psudo code

```java
COUNTING-SORT(A, B, k)
    for i <- 0 to k
        do C[i] <- 0
    for j<- to length[A]
        do C[A[j]] <- C[A[j]] + 1 // 각각의 데이터마다 1 증가 시켜 카운팅
    for i <- 1 to k
        do C[i] <- C[i] + C[i - 1] //누적합 구하기, C[i-1] : 이미 전 단계의 누적합
    for j <- length[A] downto 1
        do B[C[A[j]]] <- A[j]
            C[A[j]] <- C[A[j]] - 1
```

#### 시간 복잡도

- n>k O(n+k), 또는 O(n) if k=O(n)
- k가 클 경우 비실용적
- Stable 정렬 알고리즘
  - "입력에 동일한 값이 있을 때 입력에 먼저 나오는 값이 출력에서도 먼저 나온다"
  - **Counting 정렬은 stable하다**
