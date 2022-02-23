## async와 await

-   기존의 비동기 처리 방식인 콜백 함수와 프로미스의 단점을 보완한 비동기 처리 문법

### 기본 사용법

```js
async function 함수명() {
    await 비동기_처리_메서드_명();
}
```

-   함수 키워드 앞에 async라는 예약어를 붙이고, 함수의 내부 로직 중 HTTP 통신을 하는 비동기 처리 코드 앞에 await를 붙임
-   비동기 처리 메서드가 꼭 프로미스 객체를 반환해야 await가 의도한 대로 동작함

```js
let hello = async function () {
    return "Hello";
};

let hello = async () => {
    return "Hello";
};
```

-   화살표 함수를 사용해서 조금 더 short cut으로 작성할 수 있음

```js
const getMovies = async() => {
    const response = awiat fetch(`API_URL`);
    const json = await response.json();
}

const getMovies = async() => {
    const json = await ( await fetch(`API_URL`).json());
}
```

-   response 등의 변수를 생략하고 한번에 묶어서 short cut으로 작성할 수 있음

*   [mozilla - async와 await를 사용하여 비동기 프로그래밍을 쉽게 만들기](https://developer.mozilla.org/ko/docs/Learn/JavaScript/Asynchronous/Async_await)
*   [캡틴판교 - 자바스크립트 async와 await](https://joshua1988.github.io/web-development/javascript/js-async-await/)
