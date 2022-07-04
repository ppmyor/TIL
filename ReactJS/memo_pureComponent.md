## re-render
-   Component는 다음과 같은 경우에 리랜더링
1.   state가 바뀌는 경우
2.   props가 바뀌는 경우
3.   부모 Component가 바뀌는 경우

### PureComponent
-   state가 달라진 경우, props가 달라진 경우에만 리랜더링 되게 사용
-   class에만 사용 가능

### memo

#### memo란?

-   Memorize
-   props가 변경되지 않는 한에서 re-redner를 하지 않게 방지해주는 기능
-   함수 컴포넌트에 사용 가능
-   부모 컴포넌트가 리랜더링 되었을 때 자식 컴포넌트가 리랜더링 되는 것만 막아줌
    -   state, props가 바뀐 경우에는 리랜더링

```js
const MemorizeComponent = React.memo(Component);
```

#### 사용하는 이유

```js
const MemorizedBtn = React.memo(Btn);
<MemorizedBtn text={value} onClick={changeValue} />
<MemorizedBtn text="Continue" />
```

-   memo 기능이 없으면
    -   첫번째 MemorizedBtn에서 클릭 이벤트가 일어나 re-render가 될 때, props가 변경되지 않는 두번째 MemorizedBtn 또한 re-render가 일어남
-   memo 기능이 있으면
    -   props가 변경된것만 re-render가 일어남
-   props가 변경되지 않은 컴포넌트들도 다 re-render가 일어나면 어플리케이션의 성능 저하가 일어날 수 있으므로 memo기능을 사용

#### Component 이름 변경
```js
MemorizedBtn.displayName = "MemorizedBtn";
```
-   memo를 사용한 경우 개발자도구에서 Component의 이름이 이상하게 변경되는데 이름을 지정해줘서 원상태로 되돌려줌

