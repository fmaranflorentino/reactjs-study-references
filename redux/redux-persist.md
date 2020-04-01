## React Redux Persist - Persist data

- `yarn add redux-persist`

In your `store`folder create a new file `persistReducers.js`

```js
import storage from 'redux-persist/lib/storage';
import { persistReducer } from 'redux-persist';

export default (reducers) => {
  const persistedReducers = persistReducer(
    {
      key: 'gobaber',
      storage,
      whitelist: ['auth', 'user'],
    },
    reducers
  );

  return persistedReducers;
};
```

Now you need to change your `index.js` in the `store` folder

```js
import { persistStore } from 'redux-persist';
import createSagaMiddleware from 'redux-saga';

import createStore from './createStore';
import persistReducers from './persistReducers';

import rootReducer from './modules/rootReducer';
import rootSaga from './modules/rootSaga';

const sagaMonitor =
  process.env.NODE_ENV === 'development'
    ? console.tron.createSagaMonitor()
    : null;

const sagaMiddlewares = createSagaMiddleware({ sagaMonitor });

const middlewares = [sagaMiddlewares];

const store = createStore(persistReducers(rootReducer), middlewares);
const persistor = persistStore(store);
sagaMiddlewares.run(rootSaga);

export { store, persistor };
```

In your `App.js` and `Route.js` you need to change the way of importing store

```js
import { store } from './store';
```

Now in your `App.js` you need to add PersistGate feature that will only render the application after load the persistor

```js
import React from 'react';
import { PersistGate } from 'redux-persist/integration/react';
import { Provider } from 'react-redux';
import { Router } from 'react-router-dom';

import './config/ReactotronConfig';

import Routes from './routes';
import history from './services/history';

import { store, persistor } from './store';

import GlobalStyles from './styles/globals';

function App() {
  return (
    <Provider store={store}>
      <PersistGate persistor={persistor}>
        <Router history={history}>
          <Routes />
          <GlobalStyles />
        </Router>
      </PersistGate>
    </Provider>
  );
}

export default App;
```