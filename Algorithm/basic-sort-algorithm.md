## 기본적인 정렬 알고리즘

### Selection Sort

#### 원리

1. 가장 큰 값을 찾음
   29 10 14 37 13
2. 가장 큰 값을 맨 끝자리와 exchange & fix
   29 10 14 13 37
3. 남아있는 데이터 중 가장 큰 값을 찾음
   13 10 14 29 37
4. 가장 큰 값을 마지막 - 1 자리와 exchange & fix
   13 10 14 29 37
5. 마지막 두개의 데이터가 남을 때 까지 반복.
   10 13 14 29 37

#### psudo code

```java
selection(A[], n) // 배열 A[1...n]을 정렬한다
{
    for last <- n downto 2 {
        A[1...last] 중 가장 큰 수 A[k]를 찾는다;
        A[k] <-> A[last]; //A[k]와 A[last]의 값을 교환
    }
}
```

#### 실행 시간

1. for루프는 n-1번 반복
2. 가장 큰 수를 찾기 위한 비교횟수: last-1 번의 비교 필요(n-1, n-2, ..., 2, 1)
3. 교환은 상수시간 작업

- 시간 복잡도: T(n) = (n-1) + (n-2) + ... + 2 + 1 = n(n-1)/2 = O(n\*\*2)
- 시간 복잡도는 최악, 최선, 평균의 경우 모두 동일

#### js 구현

```js
function selectionSort(array) {
  for (let i = 0; i < array.length; i++) {
    let minIndex = i;
    for (let j = i + 1; j < array.length; j++) {
      if (array[minIndex] > array[j]) {
        minIndex = j;
      }
    }
    if (minIndex !== i) {
      let swap = array[minIndex];
      array[minIndex] = array[i];
      array[i] = swap;
    }
    console.log(`${i}회전: ${array}`);
  }
  return array;
}
console.log(selectionSort([5, 4, 3, 2, 1]));
```

### Bubble Sort

#### 원리

- Selection Sort와 유사하나 가장 큰 값을 찾는 세부적인 과정이 다름

1. 첫번째 값과 다음 값을 비교
   29 10 14 37 13
2. 클 시에는 다음 값과 자리 exchange, 작을 시에는 유지
   10 29 14 37 13
3. 두번째 값과 다음 값을 비교
4. 클 시에는 다음 값과 자리 exchange, 작을 시에는 유지
   10 14 29 37 13
5. 맨 마지막 값 바로 앞까지 반복
   10 14 29 13 37
6. 맨 마지막 값을 제외하고 해당 과정을 반복
   10 14 13 29 37
7. 맨 마지막과 마지막 -1 값을 제외하고 해당 과정 반복
8. 마지막 두개의 데이터가 남을 때 까지 해당 전체 과정 반복
   10 13 14 29 37

#### psudo code

```java
bubbleSort(A[], n)  // 배열 A[1...n]을 정렬한다.
{
    for last <- n downto 2 {
        for i <- 1 to last -1   {
            if(A[i] > A[i+1]) then A[i] <-> A[i+1]; //교환
        }
    }
}
```

#### 실행 시간

1. for루프는 n-1번 반복
2. 내부 루프는 각각 n-1, n-2, ..., 2, 1번 반복

   - last의 값이 줄어들수록 내부 루프가 도는 횟수는 줄어듬

3. 교환은 상수시간 작업

- 시간 복잡도: T(n) = (n-1) + (n-2) + ... + 2 + 1 = n(n-1)/2 = O(n\*\*2)
- 시간 복잡도는 최악, 최선, 평균의 경우 모두 동일

#### js 구현

```js
function bubbleSort(array) {
  for (let i = 0; i < array.length; i++) {
    let swap;
    for (let j = 0; j < array.length - 1 - i; j++) {
      if (array[j] > array[j + 1]) {
        swap = array[j];
        array[j] = array[j + 1];
        array[j + 1] = swap;
      }
    }
    console.log(`${i}회전: ${array}`);
    if (!swap) {
      break;
    }
  }
  return array;
}
console.log(bubbleSort([5, 4, 3, 2, 1]));
```

### 삽입정렬(Insertion Sort)

#### 원리

1. 첫번째 데이터는 데이터가 하나이기 때문에 정렬되어있다고 봄
   15 12 13 10 14 11
2. 두번째 데이터를 추가해서 두개의 데이터가 정렬된 상태가 되도록 만들어 줌
   - 작은 수 앞으로 끼워 넣음
     12 15 13 10 14 11
3. 세번째 데이터를 추가해서 세개의 데이터가 정렬된 상태가 되도록 만들어 줌
   - 작은 수 앞으로 끼워 넣음
     12 13 15 10 14 11
4. 해당 과정을 n-1 번 반복
   10 11 12 13 14 15

- k-1개의 데이터들이 정렬되어있다고 가정할 때 k번째 데이터를 끼워넣음
  - insert할 해당 값을 tmp에 저장하고 해당 값의 한자리 앞의 값과 비교해 감
  - 비교한 값이 크다면 한칸 뒤로 shift시키고(오름차순 기준)
  - 비교한 자리의 한자리 앞의 값과 비교
  - 해당 과정 반복
  - 비교한 값보다 해당 값이 크다면 해당 자리에 tmp 값을 넣음
  - 앞에서 비교하는 것보다 뒤에서 비교하는게 효율적인 방법

#### psudo code

```java
insertionSort(A[], n)   //배열 A[1...n]을 정렬한다.
{
    for i <- 2 to n {
        A[1...i]의 적당한 자리에 A[i]를 삽입한다.
    }
}
```

#### 실행 시간

1. for루프는 n-1번 반복
2. 삽인은 최악의 경우 i-1번 비교

- 최악의 경우 시간 복잡도: T(n) = (n-1) + (n-2) + ... + 2 + 1 = n(n-1)/2 = O(n\*\*2)
- 최선의 경우(모두 정렬되어있는 경우) : n - 1
- 평균으로는 대략 최선의 경우와 최악의 경우의 절반 정도

#### js 구현

```js
function insertionSort(array) {
  for (let i = 1; i < array.length; i++) {
    let cur = array[i];
    let left = i - 1;
    while (left >= 0 && array[left] > cur) {
      array[left + 1] = array[left];
      left--;
    }
    array[left + 1] = cur;
    console.log(`${i}회전: ${array}`);
  }
  return array;
}
console.log(insertionSort([5, 4, 3, 2, 1]));
```

### 참고

- [영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C)
- [JS/Sorting 버블 정렬, 삽입 정렬, 선택 정렬 자바스크립트로 구현하기 (Bubble Sort, Insertion Sort, Selection Sort in JavaScript)](https://im-developer.tistory.com/133)
