## Create the root component

<p>Here we are going to create the component that bootstraps a react application.</p>

<p>To create the root component you must create the App.js file on the src folder with the following content:</p>

```js
import React from "react";

function App() {
  return <h1>React Root Component</h1>;
}

export default App;
```

<p>Your index.js file shoulkd look like this:</p>

```js
import React from 'react';
import { render } from 'react-dom';

import App from './App';

render(<App />, document.getElementById('app'));
```

<p>In your inde.html in the public folder you must add the following entry:</p>

```html
<div id="app"></div>
```
