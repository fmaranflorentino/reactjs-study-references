## Validate props with prop-types

<p>First install the following dependencie:</p>

- `yarn add prop-types`

<p>To validate the props of a component follow the examples below:</p>

<p>In a functional component:</p>

```js
import PropTypes from 'prop-types';

function Component({ name, click }) {
  return (
    <li>
      {name}
      <button type="button" onClick={click}>
        Remover
      </button>
    </li>
  );
}

Component.propTypes = {
  name: PropTypes.string.isRequired,
  click: PropTypes.func.isRequired,
};
```

<p>In a class component:</p>

```js
import PropTypes from 'prop-types';

class Component extends Component {
  static propTypes = {
    name: PropTypes.string.isRequired,
    click: PropTypes.func.isRequired,
  }
}

```