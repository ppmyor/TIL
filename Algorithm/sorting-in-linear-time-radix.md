## 선형시간 정렬 알고리즘

- 시간 복잡도: O(n)
- Comparision Sort가 아님

## Radix Sort

- n개의 d자리 정수들
- 가장 낮은 자리수부터 정렬
- 두번째로 낮은 자리수 정렬
  - 단순히, 두번째 자리로만 정렬을 하는 것이 아니라 첫번째 자리 정렬 또한 거쳐왔기 때문에 첫번째 자리와 두번째 자리를 모두 고려하여 정렬되어있음
- 자리수만큼 d번 반복
- d번째로 낮은 자리수 정렬
- stable sort
  - 동일한 데이터가 두개 이상 있다면 정렬했을 때 입력에서 들어온 순서대로 순서가 그대로 유지

### psudo code

```java
RADIX-SORT(A, d) // A: n개의 데이터가 저장된 배열, d: d자리 정수
    for i <- to d
        do use a stable sort to sort array A on digit i
```

- 시간 복잡도 O(d(n+k)) (k < n) // k: 서로 다른 값의 개수 (ex. 10진수의 경우 10)
  - O(dn) = O(n) (d가 상수인 경우)

## 정렬 알고리즘들

<img width="579" alt="스크린샷 2022-06-16 오후 2 26 40" src="https://user-images.githubusercontent.com/52994378/173997847-24b48a62-8039-4bfb-9463-37cf437053b1.png">
