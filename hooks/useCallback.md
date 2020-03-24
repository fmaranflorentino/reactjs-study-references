## React Hooks - useCallback

`useCallback` is a hook used to minimalize the javascript proccess (with useCallback your function will be 'remounted' only when the dependencies declared change), it is a good hook to be used in function that deals with state or variables of the function. With this hook you must define a dependency, similar comcept of the useMemo hook. 

```js
import React, { useState, useEffect, useMemo, useCallback } from "react";

function App() {
  const [animals, setAnimals] = useState(["Dog", "Cat"]);

  const addAnimal = useCallback(() => {
    setAnimals([...animals, "Lion"]);
  }, [newTech, tech]);

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

      <p>You added {animalsSize} animals.</p>

      <button type="button" onClick={addAnimal}>Add new animal</button>
    </>
  );
}
export default App;
```
