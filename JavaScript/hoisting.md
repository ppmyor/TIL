## 호이스팅(hoisting)

### 호이스팅이란?

-   인터프리터가 변수와 함수의 메모리 공간을 선언 전에 미리 할당하는 것을 의미
-   변수를 정의하는 코드보다 사용하는 코드를 먼저 사용 할 수 있음

-   var로 선언한 변수의 경우 호이스팅 시 undefined로 변수를 초기화
-   let과 const로 선언한 변수의 경우 호이스팅 시 변수를 초기화 하지 않음

### 함수 호이스팅

```js
catName("클로이");

function catName(name) {
    console.log("제 고양이의 이름은 " + name + "입니다");
}
```

-   함수의 코드를 실행하기 전에 함수 선언에 대한 메모리부터 할당
    -   따라서, 함수를 호출하는 코드를 함수 선언보다 앞서 배치 가능

### 선언만 호이스팅 대상

-   초기화를 제외한 선언만 호이스팅 대상

```js
console.log(num); // 호이스팅한 var 선언으로 인해 undefined 출력
var num; // 선언
num = 6; // 초기화
```

-   아래에 초기화를 했지만 선언만 호이스팅 대상이기 때문에 undefined가 출력(var의 경우)

```js
console.log(num); // ReferenceError
num = 6; // 초기화
```

-   선언 없이 초기화만 있는 경우는 호이스팅이 일어나지 않기 때문에 ReferenceError 예외 발생

### let과 const 호이스팅

-   let과 const로 선언한 변수도 호이스팅이 일어나지만, var와 달리 변수를 undefined로 초기화하지 않기 때문에 예외 발생

### 참고

-   [호이스팅](https://developer.mozilla.org/ko/docs/Glossary/Hoisting)
