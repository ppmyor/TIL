## DOM(Document Object Model)

### DOM이란?

-   HTML, XML문서의 프로그래밍 interface
    -   문서의 구조화된 표현을 제공
    -   프로그래밍 언어가 DOM 구조에 접근할 수 있는 방법을 제공
    -   웹페이지를 스크립트 또는 프로그래밍 언어들에서 사용될 수 있게 연결시켜줌
-   DOM의 개체 구조는 노드 트리로 표현됨

### 그래서?

```html
<!DOCTYPE html>
<html>
    Hello, world!
</html>
```

-   DOM은 유효하지 않은 HTML 코드를 교정
    -   위의 코드는 <head>와 <body> 요소가 빠져있지만 DOM의 노드 트리에서는 교정되어 나타남

```js
const addTitle = document.createElement("h1");
const titleContext = document.createTextNode("Title");
addTitle.appendChild(titleContext);
document.body.appendChild(addTitle);
```

-   자바스크립트를 이용해 DOM에 새로운 노드를 추가할 수 있음
    -   위의 코드는 DOM을 업데이트 하여 h1 태그를 추가하지만 HTML 문서의 내용을 변경하지는 않음

```html
<!DOCTYPE html>
<html>
    <head></head>
    <body>
        <h1 style="display: none;">hiding!</h1>
    </body>
</html>
```

-   DOM 은 display: none 속성을 가지고 있는 h1 태그를 포함

    -   최종적으로 랜더 트리에 해당하는 뷰 포트에는 h1 태그를 포함시키지 않음

-   가상 요소(::before, ::after)는 DOM의 일부가 아니기 때문에 자바스크립트에 의해 수정할 수 없음

*   [DOM 소개](https://developer.mozilla.org/ko/docs/Web/API/Document_Object_Model/Introduction)
*   [(번역) DOM은 정확히 무엇일까?](https://wit.nts-corp.com/2019/02/14/5522)
