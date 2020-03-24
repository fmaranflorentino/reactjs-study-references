## useState

Below you can see a simple example a useState Hook implementation.

```js
import React, { useState } from "react";

function App() {
  const [animals, setAnimals] = useState(["Dog", "Cat"]);

  function addAnimal() {
    setAnimals([...animals, "Lion"]);
  }

  return (
    <>
      <ul>
        {animals.map(a => (
          <li key={a}>{a}</li>
        ))}
      </ul>

      <button type="button" onClick={addAnimal}>Add new animal</button>
    </>
  );
}

export default App;
```
