## Styled Components - Global Styles

You need to add the dependency

- `yarn add styled-components`

In your `src` folder create a new one `styles``

Inside the `styles` folder create a file `globals.js`

```js
import { createGlobalStyle } from 'styled-components';

export default createGlobalStyle
  * {
    box-sizing: border-box;
    outline: 0;

    margin: 0;
    padding: 0;
  }

  *:focus {
    outline: 0;
  }

  html,
  body, 
  #root {
    height: 100%;
  }

  body {
    -webkit-font-smoothing: antialiased;
  }

  body, input, button {
    font-family: 'Roboto', sans-serif;
  }

  ul {
    list-style: none;
  }

  button {
    cursor: pointer;
  }
;
```

In your `App.js` you must serve the global styles

```js
  import GlobalStyles from './styles/globals';
  
  return (
    <Router>
      <Routes />
      <GlobalStyles />
    </Router>
  )
```