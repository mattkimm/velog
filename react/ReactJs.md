1. install package
   react router
   styled-components
   prop-types

```javascript
$ npm i history react-router-dom@next
$ npm i styled-components
$ npm i prop-types
```

# create .env file

! name them with REACT first ALL CAPITAL LETTERS

this is not safe, it will be visible in the client.

```javascript
.env file
REACT_APP_API_KEY= '5abf511111113311e';

// used in config.js

const API_URL = 'https://api.themoviedb.org/3/';
const API_KEY = process.env.REACT_APP_API_KEY;
```

# React.CreatElement without JSX

```javascript
import React from "react";

const Star = () => React.createElement("div", null, "This is a little Star");

const App = () => {
  return Star();
};

export default App;
```

JSX란?
React에서는 본질적으로 렌더링 로직이 UI 로직(이벤트가 처리되는 방식, 시간에 따라 state가 변하는 방식, 화면에 표시하기 위해 데이터가 준비되는 방식 등)과 연결된다는 사실을 받아들입니다.

React는 별도의 파일에 마크업과 로직을 넣어 기술을 인위적으로 분리하는 대신, 둘 다 포함하는 “컴포넌트”라고 부르는 느슨하게 연결된 유닛으로 관심사를 분리합니다. 이후 섹션에서 다시 컴포넌트로 돌아오겠지만, JS에 마크업을 넣는 게 익숙해지지 않는다면 이 이야기가 확신을 줄 것입니다.

React는 JSX 사용이 필수가 아니지만, 대부분의 사람은 JavaScript 코드 안에서 UI 관련 작업을 할 때 시각적으로 더 도움이 된다고 생각합니다. 또한 React가 더욱 도움이 되는 에러 및 경고 메시지를 표시할 수 있게 해줍니다.

일단 한번 시작해보겠습니다!

![](https://images.velog.io/images/matt85kim53/post/6f4502eb-c685-4081-87a9-1d8ccafa94fd/image.png)

![](https://images.velog.io/images/matt85kim53/post/212aa390-b559-4e22-a17a-c171c09620e4/image.png)

![](https://images.velog.io/images/matt85kim53/post/9a89f0d7-a4b1-4c5c-8ea5-94492450b1c7/image.png)

Props are passed into the components. You should never ever change the props in the component that gets the props. the Props values are changed from the parent that is sending in the props to the component. So If the props change in the parent, it's also going to rerender this component.

With the state Setter you can change the state in the component and will trigger a rerender.

# Styled Components

Benefits

1. you get scoped CSS. that means that you can have the same class names for
   different components, it doesn't matter because it's scoped to that component.

2. syntax, kind of like sass you can nest stuff , and you don't need to have polyfills, and stuff like that , it will create all that automatically.

3. You can have props inside of it. Can modify the CSS by sending in different props to your
   styles.

```javascript
import styled from "styled-components";

const Button = styled.button``;
```

Styled is an object that holds different properties.
In this case , this property corresponds to HTML

# Create Global Style using Styled-COMPONENTS

```javascript
import { createGlobalStyle } from "styled-components";

export const GlobalStyle = createGlobalStyle`
    :root {
        --maxWidth : 1280px;
        --white : #fff;
        --lightGrey : #eee;
        --medGrey : #353535;
        --darkGrey : #1c1c1c;
        --fontSuperBig: 2.5rem;
        --fontBig : 1.5rem;
        --fontMed : 1.2rem;
        --fontSmall : 1rem;
    }

    * {
        box-sizing : border-box;
        font-family : 'Abel', sans-serif;
    }

    body {
        margin : 0;
        padding : 0;

        h1 {
            font-size : 2rem;
            font-weight : 600;
            color : var(--white);
        }
        h3 {
            font-size : 1.1.rem;
            font-weight : 600;
        }
        p {
            font-size : 1rem;
            color : var(--white);
        }
    }
`;
```

# import Globla Styles in App.js

```javascript
import React from "react";

//Styles
import { GlobalStyle } from "./GlobalStyle";

const App = () => {
  return (
    <div className="App">
      Start here.
      <GlobalStyle />
    </div>
  );
};

export default App;
```
