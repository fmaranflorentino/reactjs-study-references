## How to persist token in http request

After retriving the token from the backend you must do the following configuration in your `auth/sagas.js`

```js
  api.defaults.headers.Authorization = `Bearer ${user.token}`;
```

To persist the configuration above after the user refresh the page and stuff you must list to the persist action `persist/HYDRATE`. 

Add a new `takeLastest` entrance in you `all` method in the `sagas.js`

```js
  takeLatest('persist/REHYDRATE', setToken),
```

The `setToken` method is going to execute after the persist action load all states

```js
export function setToken({ payload }) {
  if (!payload) return;

  const { token } = payload.auth;

  if (token) {
    api.defaults.headers.Authorization = `Bearer ${token}`;
  }
}
```

Now every request is going to container the `authorization` header when token is present