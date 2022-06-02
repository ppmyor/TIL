## 에라토스테네스의 체

### 소개

- 소수를 더 빠르게 찾을 수 있는 방법

### 알고리즘

<p align="center">
    <img src="https://upload.wikimedia.org/wikipedia/commons/b/b9/Sieve_of_Eratosthenes_animation.gif">
</p>

1. 2부터 소수를 구하고자 하는 구간의 모든 수를 나열한다. 그림에서 회색 사각형으로 두른 수들이 여기에 해당한다.
2. 2는 소수이므로 오른쪽에 2를 쓴다. (빨간색)
3. 자기 자신을 제외한 2의 배수를 모두 지운다.
4. 남아있는 수 가운데 3은 소수이므로 오른쪽에 3을 쓴다. (초록색)
5. 자기 자신을 제외한 3의 배수를 모두 지운다.
6. 남아있는 수 가운데 5는 소수이므로 오른쪽에 5를 쓴다. (파란색)
7. 자기 자신을 제외한 5의 배수를 모두 지운다.
8. 남아있는 수 가운데 7은 소수이므로 오른쪽에 7을 쓴다. (노란색)
9. 자기 자신을 제외한 7의 배수를 모두 지운다.
10. 위의 과정을 반복하면 구하는 구간의 모든 소수가 남는다.

- 그림의 경우, 11^2 > 120이므로 11보다 작은 수의 배수들만 지워도 충분하다.
- 즉, 120보다 작거나 같은 수 가운데 2, 3, 5, 7의 배수를 지우고 남는 수는 모두 소수이다.

### 에라스토테네스의 체를 활용한 소수 찾기 알고리즘

- start부터 finish 값 사이에 있는 소수를 찾는 알고리즘

```js
const [start, finish] = input[0];

const isPrime = new Array(finish + 1).fill(true);
isPrime[0] = false;
isPrime[1] = false;

let result = [];

for (let i = 2; i <= Math.ceil(Math.sqrt(finish)); i++) {
  if (isPrime[i]) {
    for (let j = 2; j <= finish / i; j++) {
      isPrime[j * i] = false;
    }
  }
}

for (let m = start; m <= finish; m++) {
  if (isPrime[m]) {
    result.push(m);
  }
}

console.log(result.join("\n").trim());
```

- isPrime Array에 finish 개수 만큼 true를 채움
- 0과 1은 소수가 아님으로 false로 변경해줌
- finish의 제곱근까지만 비교해주어도 소수를 구할 수 있기 때문에 2부터 finish의 제곱근까지 반복
  - i의 배수를 찾기 위해 j값을 증가시키면서 j \* i의 값들을 모두 false로 변경
  - i의 배수를 변경시키는 것이므로 finish / i 만큼만 반복
- isPrime Array에 true로 남은 값들은 모두 소수이기 때문에 start부터 finish까지 반복하면서 true인 값들을 모두 result에 push해줌

### 참고

- [에라토스테네스의 체](https://ko.wikipedia.org/wiki/%EC%97%90%EB%9D%BC%ED%86%A0%EC%8A%A4%ED%85%8C%EB%84%A4%EC%8A%A4%EC%9D%98_%EC%B2%B4)
