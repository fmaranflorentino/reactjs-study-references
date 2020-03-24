## useEffect

`useEffect` is a hook that overcames lifecycles functions (componentDidUpdate and go on...).

Bellow you can see a simple example of the use of useEffect hook.

```js
import React, { useState, useEffect } from "react";

function App() {
  const [animals, setAnimals] = useState(["Dog", "Cat"]);

  function addAnimal() {
    setAnimals([...animals, "Lion"]);
  }

  useEffect(() => {
    localStorage.setItem('animals', JSON.stringify(animals));
  }), [animals]);

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

`useEffect` is going to be triggered everytime animals chages.

To execute an `useEffect` hook one time only you can follow the example bellow.

```js
useEffect(() => {
  const animals = localStorage.getItem("animals");

  if (animals) {
    setAnimals(JSON.parse(animals));
  }
}, []);
```

To execute an `useEffect` hook when component willUnmount, you must return a funciont inside the hook. You can follow the example bellow.

```js
useEffect(() => {
  const animals = localStorage.getItem("animals");

  if (animals) {
    setAnimals(JSON.parse(animals));
  }

  return () => {
    document.removeEventlistener();
  };
}, []);
```
