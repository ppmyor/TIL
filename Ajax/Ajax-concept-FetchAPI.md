# Ajax

## Ajax의 개념

1. Asynchronous Javascript And Xml

2. web 페이지 전체를 리로딩 하지 않고 **부분적으로 정보를 받아올 때** 사용

-   페이지 전체를 리로딩 하는 것은 서버 입장에서 모든 페이지를 다시 전송하기 때문에 손실이 큼
-   부분적으로 웹페이지를 갱신할 시 서버뿐만 아니라 사용자의 입장에서도 네트워크의 자원, 시간 등을 절약할 수 있음
-   ex) 추천검색어 등

3. Single Page Application

## Fetch API

### 기본 사용법

```js
fetch("http://example.com/movies.json").then(function (response) {
    return response.json();
});
```

[fetch 개념](https://developer.mozilla.org/ko/docs/Web/API/Fetch_API/Using_Fetch)

### 요청과 응답

-   fetch의 첫번째 인자로 받은 데이터를 서버로부터 요청

-   fetch API의 응답이 끝나면 then 내부에 있는 함수를 실행
    -   이 때 해당 함수의 첫번째 인자 값으로 response 객체를 입력값으로 넘겨주는 것이 원칙

### Response 객체

-   fetch를 통해 요청했을 때 웹서버가 응답한 결과들을 담고 있음
-   예시로 response 객체에서 status 값을 활용하여 예외처리 가능(404)
