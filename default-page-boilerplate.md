## React default page boilerplate

In your `pages` folder you must create a `_layouts` folder

Now create a `default` folder with `index.js` and `styles.js`

In your `index.js` you need to create a functional component

```js
import React from 'react';
import PropTypes from 'prop-types';

import { Wrapper } from './styles';

export default function DefaultLayout({ children }) {
  return <Wrapper>{children}</Wrapper>;
}

DefaultLayout.propTypes = {
  children: PropTypes.element.isRequired,
};
```

Install styled components

- `yarn add styled-components`

In your `styles.js` you must create you style for the default page, below you can see a simple example

```js
import styled from 'styled-components';

export const Wrapper = styled.div`
  background: #ccc;
  height: 100%;
`;
```

Now in your routes you can provide de default style as below

```js
import DefaultLayout from '../pages/_layout/default';

const Layout = DefaultLayout;

return (
  <Switch>
    <Route 
      path="/"
      exact
      render={(props) => (
        <Layout>
          <Home />
        </Layout>
      )}
    />
  </Switch>
)
```