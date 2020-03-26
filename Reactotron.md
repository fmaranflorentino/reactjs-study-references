## Configuring Reactotron

- `yarn add reactotron-react-js`

Create a folder `config` inside it create the file `ReactotronConfig.js`

```js
import Reactotron from 'reactotron-react-js';

if (process.env.NODE_ENV === 'development') {
  const tron = Reactotron.configure().connect();

  tron.clear();

  console.tron = tron;
}
```

In your `App.js` import the reactotron configuration.

```js
import './config/ReactotronConfig';
```