## Class components

<p>Class components are generally used for component witch needs to handle the state.</p>

<p>
To handle variables in a simpler way (example below), we need to add more configuration to webpack.
</p>

```jsx
import React, { Component } from 'react';

class TechList extends Component {
  state = {
    techList: [],
  };

  render() {
    return (
      <ul>
        <li>React</li>
        <li>React Native</li>
        <li>Nodejs</li>
      </ul>
    );
  }
}

export default TechList;
```
- `yarn add @babel/plugin-proposal-class-properties  -D` 

<p>In the babel.config.js add the following config</p>

```js

```
