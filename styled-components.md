## Styled Components

- `yarn add styled-components`

Create a `styles.js` file.

```jsx
import styled from 'styled-components';

export const Title = styled.h1`
  font-size: 24px;
  color: darkgreen;

  small {
    font-size: 11px;
    color: yellow;
  }
`;
```

Import the style and use it.

```jsx
import React from 'react';

import { Title } from './styles';

export default function Main() {
  return (
    <Title>
      MAI
      <small>Small text</small>
    </Title>
  );
}
```