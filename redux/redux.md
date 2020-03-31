## Configuration Redux && Redux Saga

A configuration guide to redux and redux saga.

- `yarn add redux react-redux redux-saga reactotron-redux reactotron-redux-saga immer`

Create a `store` folder in src.

Inside `store` folder create a `index.js` file.

Inside `store` folder create another folder `modules`

Inside `modules` you must create your module folder, in the example I'm going to use `auth`

Inside `auth` you must create the following files:

- `sagas.js`
- `reducer.js`
- `actions.js`

Inside `modules` folder you must create the following files:

- `rootReducer.ks`
- `rootSaga.js`

In your `reducer.js` you need to create the initial structure for state return.

```js
const INITIAL_STATE = {};

export default function auth(state = INITIAL_STATE, action) {
  switch (action.type) {
    default:
      return state;
  }
}
```

In your `sagas.js` you can add the initial implementation:

```js
import { all } from "redux-saga/effects";

export default all([]);
```

In your `rootReducer.js` you can add the initial implementation:

```js
import { combineReducers } from "redux";

import auth from "./auth/reducer";

export default combineReducers({
  auth
});
```

In your `rootSaga.js` you can add the initial implementation:

```js
import { all } from "redux-saga/effects";

import auth from "./auth/sagas";

export default function* rootSaga() {
  return yield all([auth]);
}
```

You must create a `createStore.js` in the `store` folder to abstract the store creation

```js
import { createStore, compose, applyMiddleware } from "redux";

export default (reducers, middlewares) => {
  const enhancer =
    process.env.NODE_ENV === "development"
      ? compose(console.tron.createEnhancer(), applyMiddleware(...middlewares))
      : applyMiddleware(...middlewares);

  return createStore(reducers, enhancer);
};
```

If you use reactotron you need to configure redux and saga.

```js
import Reactotron from "reactotron-react-js";
import { reactotronRedux } from "reactotron-redux";
import reactotronSaga from "reactotron-redux-saga";

if (process.env.NODE_ENV === "development") {
  const tron = Reactotron.configure()
    .use(reactotronRedux())
    .use(reactotronSaga())
    .connect();

  tron.clear();

  console.tron = tron;
}
```

Now we can create the implementation of the `index.js` in the `store` folder, it should look like this

```js
import createSagaMiddleware from "redux-saga";
import createStore from "./createStore";

import rootReducer from "./modules/rootReducer";
import rootSaga from "./modules/rootSaga";

const sagaMonitor =
  process.env.NODE_ENV === "development"
    ? console.tron.createSagaMonitor()
    : null;

const sagaMiddlewares = createSagaMiddleware({ sagaMonitor });

const middlewares = [sagaMiddlewares];

const store = createStore(rootReducer, middlewares);

sagaMiddlewares.run(rootSaga);

export default store;
```

Now in your `App.js` you need to serve the store

```js
import { Provider } from "react-redux";

import store from "./store";

return (
  <Provider store={store}>
    <Router history={history}>
      <Routes />
      <GlobalStyles />
    </Router>
  </Provider>
);
```

Creating actions in the `actions.js`

```js
export function signInRequest(email, password) {
  return {
    type: "@auth/SIGN_IN_REQUEST",
    payload: { email, password }
  };
}

export function signInSuccess(token, user) {
  return {
    type: "@auth/SIGN_IN_SUCCESS",
    payload: { token, user }
  };
}

export function signFailure() {
  return {
    type: "@auth/SIGN_FAILURE"
  };
}
```

Now let's define our sagas for the login request in the `sagas.js`

```js
import { takeLatest, call, put, all } from "redux-saga/effects";

import history from "~/services/history";
import api from "~/services/api";

import { signInSuccess } from "./actions";

export function* signIn({ payload }) {
  const { email, password } = payload;

  const response = yield call(api.post, "sessions", {
    email,
    password
  });

  const { user } = response.data;

  if (!user.provider) {
    console.tron.error(`usuario não é prestador`);
    return;
  }

  yield put(signInSuccess(user.token, user));

  history.push("/dashboard");
}

export default all([takeLatest("@auth/SIGN_IN_REQUEST", signIn)]);
```

Reducer.js

```js
import produce from "immer";

const INITIAL_STATE = {
  token: null,
  signed: false,
  loading: false
};

export default function auth(state = INITIAL_STATE, action) {
  switch (action.type) {
    case "@auth/SIGN_IN_SUCCESS":
      return produce(state, draft => {
        draft.token = action.payload.token;
        draft.signed = true;
      });
    default:
      return state;
  }
}
```

the recuder listen to the triggered actions

saga can intercept a action and deal with side effects

Calling a actions

```js
import { useDispatch } from "react-redux";

const dispatch = useDispatch();

import { signInRequest } from "~/store/modules/auth/actions";

function handleSubmit({ email, password }) {
  dispatch(signInRequest(email, password));
}
```
