## React Hooks - useMemo

`useMemo` is a hook used to prevent the render method to render unecessary states.

So, you need to define the value to be rendered after the dependency execution and
the dependency itself.

```js
import React, { useState, useEffect, useMemo } from "react";

function App() {
  const [animals, setAnimals] = useState(["Dog", "Cat"]);

  function addAnimal() {
    setAnimals([...animals, "Lion"]);
  }

  useEffect(() => {
    localStorage.setItem('animals', JSON.stringify(animals));
  }), [animals]);

  const animalsSize = useMemo(() => tech.length, [tech]);

  return (
    <>
      <ul>
        {animals.map(a => (
          <li key={a}>{a}</li>
        ))}
      </ul>

      <br />

      <p>You added {animals.length} animals.</p>

      <button type="button" onClick={addAnimal}>Add new animal</button>
    </>
  );
}
export default App;
```