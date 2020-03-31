## React routing with private routes example

- `yarn add react-router-dom`

Create a `routes` folder insite it create tow new files `index.js` and `route.js`

Your `routes.js` must contain the following code

```js
import React from 'react'
import PropTypes from 'prop-types';
import { Route, Redirect } from 'react-router-dom';

export default function RouteWrapper({
  component: Component,
  isPrivate,
  ...rest
}) {
  const signed = true;

  if (!signed && isPrivate) {
    return <Redirect to="/" />;
  }

  if (signed && !isPrivate) {
    return <Redirect to="/dashboard" />;
  }

  return <Route {...rest} component={Component} />;
}

RouteWrapper.propTypes = {
  isPrivate: PropTypes.bool,
  component: PropTypes.oneOfType([PropTypes.element, PropTypes.func])
    .isRequired,
};

RouteWrapper.defaultProps = {
  isPrivate: false,
};
```

Your `index.js` must have the following code

```js
import React from 'react';
import { Switch } from 'react-router-dom';
import Route from './Route';

import Component from '../pages/Component';


export default function Routes() {
  return (
    <Switch>
      <Route path="/" exact component={Component} />

      <Route path="/dashboard" component={Component} isPrivate />
    </Switch>
  );
}
```

Your `App.js` needs to import and serve the routes

```js
import React from 'react';
import { Router } from 'react-router-dom';

import Routes from './routes/';

function App() {
  return (
    <Router>
      <Routes />
    </Router>
  );
}

export default App;
```