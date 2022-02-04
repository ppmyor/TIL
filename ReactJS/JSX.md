## JSX

### JSX란?

-   JavaScript를 확장한 문법
-   React element를 생성
-   HTML과 유사하기에 조금 더 직관적으로 코드 파악 가능

### 사용법

```js
const element = <h1>Hello, {name}</h1>;
```

-   element를 선언할 때 사용 할 태그로 감싸 선언할 수 있음

```js
const name = "Josh Perez";
const element = <h1>Hello, {name}</h1>;

ReactDOM.render(element, document.getElementById("root"));
```

-   JSX 중괄호 내에는 유효한 JavaScript 표현식을 모두 넣을 수 있음

```js
function getGreeting(user) {
    if (user) {
        return <h1>Hello, {formatName(user)}!</h1>;
    }
    return <h1>Hello, Stranger.</h1>;
}
```

-   JSX 표현식이 정규 JavaScript로 호출 되고, JavaScript 객체로 인식
-   따라서, 반복문이나 조건문 변수 할당, 인자로 사용, 함수로 반환 등을 수행할 수 있음

```js
const element = <img src={user.avatarUrl} />;

const element = (
    <div>
        <h1>Hello!</h1>
        <h2>Good to see you here.</h2>
    </div>
);
```

-   tag가 비어있다면 />을 사용하여 태그를 닫아주어야
-   또한, JSX 태그는 자식을 포함할 수 있음

*   [JSX 소개](https://ko.reactjs.org/docs/introducing-jsx.html)
