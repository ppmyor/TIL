## useEffect

-   state를 변경할 때 모든 코드들을 다시 실행되기 때문에 component 내부의 특정 코드의 실행되는 시기를 조절하기 위해 사용
    -   component 안에서 딱 한번만 실행되거나,
    -   component 안에서 특정 데이터가 변화할 때 실행
-   코드의 특정한 부분만이 변화했을 때 원하는 코드를 실행

### 기본 사용법

```js
useEffect(() => {
    console.log("Hello");
}, []);
```

-   첫번째 argument에서는 실행시키고 싶은 코드를 작성
-   두번째 argument는 defendency (value를 작성)
    -   해당 value가 변화할 때 코드를 실행할 것이라고 react에게 알려줌
-   dependency가 없는 경우 지켜볼게 없기 때문에 한번만 실행
-   dependency가 하나만 존재하는 경우 해당 값의 변화가 있을 때 코드 실행
-   dependency가 여러개 존재하는 경우 여러개 중 하나라도 값의 변화가 있으면 코드 실행

### cleanup Function

-   component가 destroy될 때도 코드를 실행 가능
-   component가 destroy될 때 실행될 function을 하나 만듦

```js
useEffect(() => {
    console.log("created :)");
    return () => console.log("destroyed :(");
}, []);
```

-   return 시에 함수를 호출해 destroy될 때 실행되도록 함
