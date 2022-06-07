## 빠른 정렬(Quick Sort)

### 분할정복법(Divide and Conguer)

- 분할: 배열을 다음과 같은 조건이 만족되도록 두 부분으로 나눈다.
  - 예시에서는 정렬 데이터 중 마지막 값을 pivot(기준값)으로 사용
  - pivot을 가운데에 두고 pivot보다 작은 값과 큰 값으로 나눔
    - merge sort에서는 2/n개씩 쪼개지지만 quick sort에서는 보장할 수 없음
    - elements in lower parts <= elements in upper parts
- 정복: 각 부분을 순환적으로 정렬한다.
  - 양쪽을 다시 quick sort로 순환적으로 정렬
- 합병: nothing to do

### 원리

1. 정렬할 배열이 주어짐. 마지막 수를 기준(pivot)으로 삼는다.
   31 8 48 93 11 3 20 29 65 15(pivot)
2. 기준보다 작은 수는 기준의 왼쪽에 나머지는 기준의 오른쪽에 오도록 재배치(분할)한다.
   - 어떻게 pivot을 기준으로 분할을 하는지가 중요
     8 11 3 15(pivot) 31 48 20 29 65 73
3. 기준의 왼쪽과 오른쪽을 각각 순환적으로 정렬한다(정렬 완료)
   3 8 11 15(pivot) 20 29 31 48 65 73

### psudo code

```java
quicoSort(A[], p, r) -> A[p...r]을 크기순으로 정렬한다
{
    if(p<r) then {
        q = partition(A, p, r); -> 분할, q는 pivot
        quickSort(A, p, q-1); -> 왼쪽 부분배열 정렬
        quickSort(A, q+1, r); -> 오른쪽 부분배열 정렬
    }
}

partition(A[], p, r)    {
    배열 A[p...r]의 원소들을 A[r]을 기준으로 양쪽으로 재배치하고 A[r]이 자리한 위치를 return 한다;
}
```

### partition

<img width="494" alt="스크린샷 2022-06-07 오후 5 25 44" src="https://user-images.githubusercontent.com/52994378/172334496-a18e86e8-e468-48ea-89fa-2e41118edcee.png">
<img width="472" alt="스크린샷 2022-06-07 오후 5 29 28" src="https://user-images.githubusercontent.com/52994378/172334569-c3f388f4-c12c-4874-8efe-9235333c6a3f.png">

```java
if A[j] >= x
    j<-j+1;
else
    i<-i+1;
    exchange A[i] and A[j];
    j<-j+1;
```

```java
Partition(A, p, r)
{
    x<-A[r];
    i<-p-1;
    for j<-p to r-1
        if(A[j] <= x) then
           i<-i+1;
         exchangeA[i] and A[j];
    exchange A[i+1] and A[r];
    return i+1;
}
```

- pivot은 그자리에 가만히 두고 나머지 데이터들을 pivot보다 작은 것과 큰 것들로 먼저 분할
- 마지막 step에서 pivot보다 큰 것 중 첫번째 값과 exchange
- i: pivot보다 작은 값들 중 마지막 값
- j: 지금 검사하려는 값
  - j가 pivot보다 크다면 그냥 j를 +1(오른쪽에 pivot보다 큰값이 위치하기 때문)
  - j가 pivot보다 작다면 i+1번째와 exchange 후 i를 +1

### 실행 시간

- n개의 data를 partition하는데 걸린 시간 O(n)
- 최악의 경우
  - 항상 한 쪽은 0개, 다른 쪽은 n-1개로 분할되는 경우
    - T(n) = T(0) + T(n-1) + n - 1 = T(n-2) + T(n-1) + n - 1 + n - 2 ... = n(n-1)/2 = O(n^2)
  - 이미 정렬된 입력 데이터(마지막 원소를 피봇을 선택하는 경우)
- 최선의 경우
  - 항상 절반으로 분할되는 경우(merge sort와 동일)
    - T(n) = 2T(n/2) + n = O(nlogn)
- 항상 한쪽이 적어도 1/9 이상이 되도록 분할한다면?
  <img width="497" alt="스크린샷 2022-06-07 오후 5 49 15" src="https://user-images.githubusercontent.com/52994378/172338380-23010dd9-0052-41d6-a19e-3e74d9b055e2.png">
  - k층이라고 한다면 (9/10)^kn = 1이라고 할 때 k = log(10/9)^n
  - 시간복잡도는 O(nlogn)
  - quick sort는 partition이 얼마나 balance있게 나누어지냐에 따라 성능이 나뉨
- 평균 시간복잡도
  <img width="585" alt="스크린샷 2022-06-07 오후 6 00 34" src="https://user-images.githubusercontent.com/52994378/172342063-2097f9a7-23a9-4c8d-87bc-ea70a2663df9.png">

### pivot의 선택

- 첫번째 값이나 마지막 값을 pivot으로 선택
  - 이미 정렬된 데이터 혹은 거꾸로 정렬된 데이터가 최악의 경우
  - 현실의 데이터는 랜덤하지 않으므로(거꾸로) 정렬된 데이터가 입력으로 들어 올 가능성은 매우 높음
  - 따라서 좋은 방법이라고 할 수 없음
- "Median of Three"
  - 첫번째 값과 마지막 값, 그리고 가운데 값 중에서 중간값(median)을 피봇으로 선택
  - 최악의 경우 시간복잡도가 달라지지는 않음
- Randomized Quicksort
  - 피봇을 랜덤하게 선택
  - no worst case instance, but worst case execution
    - 어떤 데이터가 들어오든 pivot에 따라 달라지기 때문
  - 평균 시간복잡도 O(nlogn)

### js 구현

- basic quick sort

```js
function quickSort(array) {
  if (array.length < 2) {
    return array;
  }
  const pivot = [array[0]];
  const left = [];
  const right = [];
  for (let i = 1; i < array.length; i++) {
    if (array[i] < pivot) {
      left.push(array[i]);
    } else if (array[i] > pivot) {
      right.push(array[i]);
    } else {
      pivot.push(array[i]);
    }
  }
  console.log(`left: ${left}, pivot: ${pivot}, right: ${right}`);
  return quickSort(left).concat(pivot, quickSort(right));
}
const sorted = quickSort([5, 3, 7, 1, 9]);
console.log(sorted);
```

- in place quick sort

```js
function quickSort(array, left = 0, right = array.length - 1) {
  if (left >= right) {
    return;
  }
  const mid = Math.floor((left + right) / 2);
  const pivot = array[mid];
  const partition = divide(array, left, right, pivot);

  quickSort(array, left, partition - 1);
  quickSort(array, partition, right);

  function divide(array, left, right, pivot) {
    console.log(`array: ${array}, left: ${array[left]}, pivot: ${pivot}, right: ${array[right]}`);
    while (left <= right) {
      while (array[left] < pivot) {
        left++;
      }
      while (array[right] > pivot) {
        right--;
      }
      if (left <= right) {
        let swap = array[left];
        array[left] = array[right];
        array[right] = swap;
        left++;
        right--;
      }
    }
    return left;
  }
  return array;
}
```

### 참고

- [영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C)
- [JS/Sorting 퀵 정렬, 자바스크립트로 구현하기(Quick Sort in JavaScript](https://im-developer.tistory.com/135)
