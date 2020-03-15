## React routing example

- `yarn add react-router-dom`

<p>Create the files route.js</p>

```jsx
import React from 'react';
import { BrowserRouter, Switch, Route } from 'react-router-dom';

import Main from './pages/Main';
import Repository from './pages/Repository';

export default function Routes() {
  return (
    <BrowserRouter>
      <Switch>
        <Route path="/" exact component={Main} />
        <Route path="/repository" component={Repository} />
      </Switch>
    </BrowserRouter>
  );
}
```

Return routes as component in `App.js`

```jsx
import React from 'react';

import Routes from './routes';

function App() {
  return <Routes />;
}

export default App;
```