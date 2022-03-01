## gh-pages를 이용한 자동 배포

### gh-pages란?

-   github pages에 업로드 할 수 있게 해주는 package

### 기본 사용법

```bash
npm i gh-pages
```

-   gh-pages 설치

```json
    "scripts": {
        "build": "react-scripts build",
        "deploy": "gh-pages -d build",
        "predeploy": "npm run build"
    },
"homepage": "https://ppmyor.github.io/study-ReactJS-basic"
```

-   package.json에서 위와 같이 설정
-   npm run deploy 입력 시 predeploy와 build 가 역으로 실행되면서 build 폴더를 홈페이지 URL로 업로드
