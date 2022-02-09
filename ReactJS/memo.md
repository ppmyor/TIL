## memo

### memo란?

-   Memorize
-   props가 변경되지 않는 한에서 re-redner를 하지 않게 방지해주는 기능

```js
const MemorizeComponent = React.memo(Component);
```

### 사용하는 이유

```js
const MemorizedBtn = React.memo(Btn);
<MemorizedBtn text={value} onClick={changeValue} />
<MemorizedBtn text="Continue" />
```

-   memo 기능이 없으면
    -   첫번째 MemorizedBtn에서 클릭 이벤트가 일어나 re-render가 될 때, props가 변경되지 않는 두번째 MemorizedBtn 또한 re-render가 일어남
-   memo 기능이 있으면
    -   props가 변경된것만 re-render가 일어남
-   props가 변경되지 않은 컴포넌트들도 다 re-render가 일어나면 어플리케이션의 성능 저하가 일어날 수 있으므로 memo기능을 사용
