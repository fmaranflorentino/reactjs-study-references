## Styled Components

- `yarn add styled-components`

Create a `styles.js` file.

```jsx
import styled from "styled-components";

export const Title = styled.h1`
  font-size: 24px;
  color: darkgreen;

  small {
    font-size: 11px;
    color: yellow;
  }
`;
```

Import the style and use it.

```jsx
import React from "react";

import { Title } from "./styles";

export default function Main() {
  return (
    <Title>
      MAI
      <small>Small text</small>
    </Title>
  );
}
```

Accesing components pros from styled component

```jsx
return (
  <Title error>
    MAI
    <small>Small text</small>
  </Title>
);
```

```jsx
import styled from "styled-components";

export const Title = styled.h1`
  font-size: 24px;
  color: ${props => (props.error ? "red" : "green")};

  small {
    font-size: 11px;
    color: yellow;
  }
`;
```


### Global Styles

Create a `styles` folder and create the file `global.js`

```jsx
import { createGlobalStyle } from 'styled-components';

export default createGlobalStyle`
  * {
    margin: 0;
    padding:0;

    box-sizing: border-box;
  }

  html, body, #root {
    min-height: 100%;
  }

  body {
    background: #7159c1;
    -webkit-font-smoothing: antialiased !important;
  }

  body, input , button {
    color: #222;
    font-size: 14px;
  }

  button {
    cursor: pointer;
  }
`;
```

In your `App.js`

```jsx
import GlobalStyles from './styles/global';

function App() {
  return (
    <>
      <Routes />
      <GlobalStyles />
    </>
  );
}
```