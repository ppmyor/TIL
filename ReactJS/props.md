## props

### props란?

-   부모 컴포넌트로부터 자식 컴포넌트에 데이터를 보낼 수 있게 해주는 방법
    -   컴포넌트(component): 어떤 JSX를 반환하는 함수

### 기본 사용법

-   전달받은 property가 모두 들어가는 Object의 형태
-   어떤 props이든 컴포넌트에 보내면 해당 함수의 첫번째 argument로 들어감

```js
function Btn(props) {
    {
        {props.text}
    }
}

function App() {
    <Btn text="abc" />;
}
```

-   props는 object의 형태이기 때문에 key 값으로 선언한 property의 이름을 기재해야함

```js
function Btn({ text, fontSize }) {
    {text}
    console.log(fontSize);
}

function App() {
    <Btn text="abc" fontSize={18} />;
}
```

-   props가 object의 형태이기 때문에 함수의 argument 영역에 중괄호만 열고 key값을 기재하는 방식으로도 사용 가능
-   property가 2개 이상일 때는 , 로 구분하여 기재
-   props로 onClick이나 style을 적어도 자동적으로 return에 들어가 처리되지 않으므로, argument로 받아서 직접 컴포넌트에서 처리해줘야함을 유념

## propsType

### propsType이란?

-   어떤 type의 props를 받고 있는지를 체크함으로써 type error 를 방지할 수 있음
-   props의 type과 어떤 모양이어야 하는지를 설명

### 기본 사용법

```js
Btn.PropTypes = {
    text: PropTypes.string.isRequired,
    fontSize: PropTypes.number,
};
```

-   위의 형태와 다른 type으로 값이 넘어오게 되면 error 메세지를 줌
-   필수적으로 받아야하는 값들은 isRequired를 적게되면 값이 넘어오지 않았을 때 error 메세지를 줌
    -   기재하지 않는다면 optional

[PropTypes와 함께하는 타입 검사](https://ko.reactjs.org/docs/typechecking-with-proptypes.html)
