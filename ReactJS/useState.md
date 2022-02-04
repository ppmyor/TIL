## state

### state란?

-   data가 저장되는 곳

### 리렌더링 문제

-   값을 갱신하고 싶은 부분이 있을 때 변수에 값을 갱신해주더라도, 하단에 ReactDOM.render을 한번 호출하기 때문에 브라우저 상에는 초기의 상태만 노출됨
-   값을 갱신하는 함수에 ReactDOM.render를 삽입해주면 해결되지만 해당 방법은 좋은 해결방법은 아님
-   따라서 리렌더링 문제를 해결하기 위해 React에서 제공하는 useState 함수를 사용

### useState

```js
const data = React.useState();
```

-   위와 같이 사용
-   React.useState()는 배열로 두개의 값을 받음
    -   첫번째 값은 초기 값을 나타냄
    -   두번째 값은 그 값을 바꾸는 함수를 나타냄

```js
const [counter, setCounter] = React.useState(0);
const countUp = () => {
    setCounter(counter + 1);
};
```

-   배열의 값들을 조금 더 용이하게 사용하기 위해 위와 같이 선언해주면 편리함
-   배열의 두번째 값에는 보통 첫번째 값의 이름 앞에 set을 붙여주는 방식으로 사용
-   배열의 두번째 값(modifier 함수)는 그 값으로 업데이트하고 리렌더링을 해줌
    -   데이터의 값을 바꿀 함수
