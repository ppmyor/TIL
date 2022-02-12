## create react app

-   react의 툴체인
-   Node 14.0.0 혹은 상위 버전 및 npm 5.6 혹은 상위 버전이 필요(22.02.12 기준)

### 설치방법

```bash
npx create-react-app my-app
cd my-app
npm start
```

### CSS module

-   create react app은 CSS 코드를 js 오브젝트로 변환시켜줌
    -   따라서 styles도 modular가 될 수 있음
-   CSS module의 이름은 name.module.css 의 형태

```js
import PropTypes from "prop-types";
import styles from "./Button.module.css";

function Button({ text }) {
    return <button className={styles.btn}>{text}</button>;
}

Button.propTypes = {
    text: PropTypes.string.isRequired,
};

export default Button;
```

```css
.btn {
    color: white;
    background-color: goldenrod;
}
```

-   import한 이름에 css의 class이름을 붙이면 스타일을 지정할 수 있음
-   해당 className은 React에서 랜덤하게 부여하기 때문에(ex)class="Button_btn\_\_F4YlC" ) 다른 css module 파일에서 같은 클래스의 이름을 사용하는것이 가능
    -   각각 다른 module.css에서 title이라는 이름을 사용하더라도 함께 import하더라도 사용하는것은 문제 없음

-   컴포넌트를 분리해서 만들고, 그 컴포넌트를 위한 css를 만드는 독립적인 형태를 띄는 것이 react의 힘

[새로운 React App 만들기](https://ko.reactjs.org/docs/create-a-new-react-app.html)
