## webpack

- 컴포넌트가 늘어날수록 유지보수가 힘듦
- src로 js들을 가져오면 파일간의 중복이 발생할 수 있음
- webpack은 여러개의 자바스크립트 파일을 하나로 합쳐서 하나의 자바스크립트 파일로 만들어줌
  - 하나로 합치면서 babel 적용이나 쓸데없는 코드들 삭제 가능

### 설치하기

1. npm init

```bash
npm init
```

- package.json 파일이 생성됨

2. 리액트 설치

```bash
npm i react react-dom
```

3. webpack 설치

- D옵션: development 옵션, 개발에서만 사용한다는 옵션

```bash
npm i -D webpack webpack-cli
```

- package.json 파일에서
  - 실제 서비스에서 사용되는 것들은 dependencies에 기록
  - 개발에만 사용되는 것들은 devDependencies에 기록

4. babel 설치

```bash
npm i -D @babel/core @babel/preset-env @babel/preset-react babel-loader
```

- @babel/core: 기본적인 바벨
- @babel/preset-env: 브라우저에 맞게 알아서 최신문법을 옛날 문법으로 바꾸어줌
- @babel/preset-react: jsx로 바꾸어줌
- babel-loader: babel과 webpack 연결

### 파일 생성

#### webpack.config.js

- 세팅을 진행하고 있는 폴더에 **webpack.config.js** 파일 생성

#### client.jsx

- 세팅을 진행하고 있는 폴더에 **client.jsx** 파일 생성

### 세팅

#### index.html

```html
<body>
  <div id="root"></div>
  <script src="./dist/app.js"></script>
</body>
```

- src에는 파일 하나만 삽입 가능

#### wepack.config.js

```js
const path = require("path");

module.exports = {
  name: "anna-setting",
  mode: "development",
  devtool: "eval",
  resolve: {
    extensions: [".js", ".jsx"],
  },
  entry: {
    app: ["./client"],
  },

  module: {
      rules: [{
          test: /\.jsx?/,
          loader: 'babel-loader',
          options: {
              presets: ['@babel/preset-env', '@babel/preset-react'],
          }
      }]
  },

  output: {
    path: path.join(__dirname, "dist"),
    filename: "app,js",
  },
};
```

- path: node에서 경로를 쉽게 조작 할 수 있도록 하는 기본 기능
- name: 웹팩 설정에 대한 이름
- mode: 개발용(development)인지 배포용(production)인지
- devtool: eval -> 빠르게 하겠다
- resolve:
  - extensions: app에서 해당 확장자를 가진 파일이 있는지 찾음
- entry: 입력
  - app: 합쳐줄 파일들을 배열로 정렬하여 삽입
    - client가 이미 불러온 파일이 있는 경우 넣을 필요 없음: 다른 파일이 불러온 파일은 적어 줄 필요 없이 하나만 넣으면 됨
    - 확장자 생략 후 extensions 에 기입해도 됨
- module:
  - rules: 여러개의 규칙 적용 가능(배열)
  - test: js or jsx 파일에
  - loader: babel-loader 룰을 적용
  - -> babel을 적용해서 최신이나 실험적인 문법에 호환되는 문법으로 바꾸어줌
  - options: babel에 옵션 적용
    - preset 옵션 적용
- output: 출력
  - path.join: 경로를 합쳐서 만들어줌
    - \_\_dirname: 현재 폴더 + dist
  - filename: 만들어 줄 파일 이름
- -> entry의 파일을 읽어서 module을 적용한 후 output으로 뺌

#### client.jsx

```js
const React = require("react");
const ReactDom = require("react-dom");

const Anna = require("./Anna");

ReactDom.render(<Anna />, document.querySelector("#root"));
```

- jsx로 확장자를 쓰면, react 전용(jsx문법이 담긴) 파일이라는 것을 명시적으로 표현할 수 있음
- react와 react-dom을 불러옴
- 필요한 컴포넌트만 불러와서 사용 가능

#### Anna.jsx

```js
const React = require("react");
const { Component } = React;

class Anna extends Component {
  state = {};
  render() {}
}

module.exports = Anna;
```

- Component 별로 파일을 분리
- 분리할 때 마다 npm에서 react를 불러와주어야함
- 분리할 때 마다 쪼갠 파일에서 쓰는 컴포넌트를 바깥에서도 사용할 수 있게 exports 해야함

#### package.json 파일 수정

```json
{
  "scripts": {
    "dev": "webpack"
  }
}
```

```bash
npm run dev
```

- 위와 같이 수정하면 위의 명령어로 webpack 실행 가능

```bash
npx webpack
```

- 해당 명령어로도 webpack 실행 가능
