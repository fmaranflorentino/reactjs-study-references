## Configuration

A configurartion guide to redux.

- `yarn add redux react-redux`

Create a `store/index.js` folder in src.

```js
import { createStore } from 'redux';

const store = createStore();

export default store;
```

In your `App.js` you need to add the redux provider and store

```js
import { Provider } from 'react-redux';
import store from './store';

function App() {
  return (
    <Provider store={store}>
      <BrowserRouter>
        <Header />
        <Routes />
        <GlobalStyles />
      </BrowserRouter>
    </Provider>
  );
}
```

## Adding a reducer to the store

```js
function cart() {
  return [];
}

const store = createStore(cart);
```

## Creating a rootReducer

In your `store` folder you need to create a folder named `modules`.
In the `modules` folder add the following file `rootReducer`

```js
import { combineReducers } from 'redux';

import cart from './cart/reducer';

export default combineReducers({
  cart,
});
```

Your `index.js` inside the store folder show look like this.

```js
import { createStore } from 'redux';

import rootReducer from './modules/rootReducer';

const store = createStore(rootReducer);

export default store;
```