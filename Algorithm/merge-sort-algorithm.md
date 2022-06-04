## 합병 정렬(Merge Sort)

### 분할정복법(Divide and Conguer)

#### 원리

- 분할: 해결하고자 하는 문제를 작은 크기의 **동일한** 문제들로 분할
- 정복: 각각의 작은 문제를 순환적으로 해결 === recursion으로 해결
- 합병: 작은 문제의 해를 합하여(merge) 원래 문제에 대한 해를 구함

- 본질적으로 recursion을 사용해서 해결하는 기법

#### 분할 정복법을 사용하는 대표적인 sort

- Merge Sort
- Quick Sort

### 합병정렬

#### 원리

ALGORITHMS

- divide: 데이터가 저장된 배열을 절반으로 나눔
  ALGOR ITHMS
  - 나누는 과정을 반복하면서 배열의 길이가 1이 되었을 때 까지 나눔(길이가 1인 배열은 배열 안의 데이터가 정렬되었다고 볼 수 있음)
- recursively sort: 각각을 순환적으로 정렬
  AGLOR HIMST
- merge:정렬된 두개의 배열을 합쳐 전체를 정렬
  AGHILMORST
  - 정렬된 두개의 배열을 합치기 위해서는 추가배열을 이용
  - 첫번째 배열(A)의 가장 작은 값인 배열 첫째 자리 i와 두번째 배열(B)의 가장 작은 값인 배열 첫째 자리 j를 비교해서 작은 값을 추가배열의 첫째 자리인 k에 넣음
  - k는 오른쪽으로 한칸 shift해서 두번째 자리를 가리키도록 함
  - k에 삽입된 값이 포함된 배열, 예를 들어 A 배열이라고 한다면 i의 값을 오른쪽으로 한칸 shift해준 뒤(두번째 자리) 다시 B 배열의 j와 비교
  - 삽입한 값의 배열은 오른쪽으로 한칸 shift해주면서 위의 과정을 반복(k또한 값이 추가되었다면 오른쪽으로 shift)

#### psudo code

```java
mergeSort(A[], p, r) //A[p...r]을 정렬한다. 매개변수를 p와 q로 명시화
{
    if(p < r) then {
        q <- (p+q) / 2; // p, r의 중간 지점 계산 === q
        mergeSort(A, p, q); // 전반부 정렬
        mergeSort(A, q+1, r); // 후반부 정렬
        merge(A, p, q, r); // 합병
    }
}

merge(A[], p, q, r)
{
    정렬되어 있는 두 배열 A[p...q]와 A[q+1...r]을 합하여 정렬된 하나의 배열 A[p...r]을 만든다.
}
```

#### code

```java
void merge(int data[], int p, int q, int r) {
    int i=p, j=q+1, k=p;
    int tmp[data.length()];
    while(i<=q && j<=r) { //한쪽의 데이터가 끝날 때 까지 반복
        if(data[i]<=data[j])
            tmp[k++]=data[i++];
        else
            tmp[k++]=data[j++]; //비교 후 tmp로 내려주고 오른쪽으로 한칸 shift
    }
    while(i<=q)
        tmp[k++]=data[i++]; //앞쪽 리스트에 데이터가 남아있을 때 실행
    while(j<=r)
        tmp[k++]=data[j++]; //뒤쪽 리스트에 데이터가 남아있을 때 실행
    for(int i=p; i<=r; i++)
        data[i]=tmp[i]; //새로운 추가배열 tmp에 옮겨와서 정렬되었기 때문에 원래 배열로 옮겨주는 과정
}
```

#### 실행 시간

- if n = 1
  - T(n) = 0
- otherwise
  - T(n) = T(n/2) + T(n/2) + n // n이 홀수일 경우 내림이나 올림의 과정 필요
  - T(n) = 2T(n/2) + n
  - T(n) = O(nlogn)
- 일반적으로 분할정복법을 따르는 알고리즘의 시간복잡도는 for문의 반복횟수를 따지면서 시간복잡도 분석을 하지 않고, 시간복잡도에 관한 순환식을 세운 후 순환식을 수학적으로 풀어서 계산

### 참고

- [영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C)
