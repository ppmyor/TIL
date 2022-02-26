## react router dom

-   페이지의 로딩없이 필요한 컴포넌트를 불러와 렌더링하여 보여줌(사용자의 입장에서는 빠른 페이지 전환처럼 느껴짐)
-   라우터별로 컴포넌트를 나누듯이 나누어 사용

### 종류

-   Browser Router
    -   보통의 웹사이트 URL
-   Hash Router
    -   /#/가 덧붙어 보임

### 기본 사용법

```bash
npm i react-router-dom
```

```js
import React from "react";
import { BrowserRouter as Router, Switch, Route, Link, useParams } from "react-router-dom";
import Home from "./routes/Home";
import Movie from "./routes/Movie";

function App() {
    return (
        <Router>
            <Switch>
                <Route path="/">
                    // <Home /> 등과 같이 사용 할 component 선언
                </Route>
                <Route path="/movie/:id">
                    // <Movie /> 등과 같이 사용 할 component 선언
                </Route>
            </Switch>
        </Router>
    );
}

export default App;
```

-   `<Switch>`
    -   route를 찾는 역할
    -   route를 찾으면 컴포넌트를 렌더링
-   `<Route>`
    -   path를 선언해줌
    -   유저가 해당 경로에 있으면 해당 Route를 렌더링
    -   path에 변수를 사용해야하는 경우에는 /movie/:id와 같이 ":" 를 사용
        -   여기에 오는 id의 값이 무엇인지 알고싶다고 React Router에 요청
        -   이후 컴포넌트에서 useParams를 이용해서 해당 key/value의 짝을 맞춤

```js
function Movie() {
    const { id } = useParams();
}

export default Movie;
```

-   useParams
    -   URL 인자들의 key/value(키/값) 짝들의 객체를 반환함
    -   해당 라우트에 선언된 컴포넌트에서 useParams를 이용하여 path의 변수 부분에 들어 갈 변수를 선언해줌

```js
<Link to={`/movie/${id}`}>{title}</Link>
```

-   Link
    -   react router dom의 Link 컴포넌트를 사용해서 브라우저의 새로고침 없이도 유저를 다른 페이지로 이동시켜줌
    -   화면 간 이동할 때 a 태그를 사용하지 않는 이유는 전체 페이지가 재실행되기 때문

### 참고

-   [react router Quick Start](https://v5.reactrouter.com/web/guides/quick-start)
-   [Hooks](https://v5.reactrouter.com/web/api/Hooks)
