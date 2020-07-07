## **React Doc**

### Creating components

We can create components using function as well as class

> Using function

```js
import React from 'react';
import ReactDOM from 'react-dom';

function Hello() {
  return (
    <div>
      <h1>Hello Everyone</h1>
      <p>How are you?</p>
    </div>
  );
}

const Hello2 = () => {
  // anonymous function
  return (
    <div>
      <h1>Hello All!</h1>
      <p>How are you?</p>
    </div>
  );
};

ReactDOM.render(<Hello />, document.getElementById('root'));
// ReactDOM.render(<Hello2 />, document.getElementById('root'));
```

> Using class

```js
```

### Understanding properties

Props or properties, is an object in react that contain properties of the component. With props we can display dynamic data within a component.

```js
import React from 'react';
import ReactDOM from 'react-dom';

function Hello(props) {
  return (
    <div>
      <h1>Welcome to {props.library}!</h1>
      <p>{props.message}</p>
      <p>Number of properties: {props.number}</p>
    </div>
  );
}

ReactDOM.render(
  <Hello library='React' message='Have fun !' number={3} />,
  document.getElementById('root')
);
```

It's also common to see values from the probs object de-structured for brevity. So what we can do instead of passing in the entire object is we can reference library, message, and number by name.

```js
import React from 'react';
import ReactDOM from 'react-dom';

function Hello({ library, message, number }) {
  return (
    <div>
      <h1>Welcome to {library}!</h1>
      <p>{message}</p>
      <p>Number of properties: {number}</p>
    </div>
  );
}

ReactDOM.render(
  <Hello library='React' message='Have fun !' number={3} />,
  document.getElementById('root')
);
```

### Composing components

```js
import React from 'react';
import ReactDOM from 'react-dom';

function Lake({ name }) {
  return <h1>{name}</h1>;
}

function App() {
  return (
    <div>
      <Lake name='Ganga' />
      <Lake name='Yamuna' />
      <Lake name='Nile' />
    </div>
  );
}

ReactDOM.render(<App />, document.getElementById('root'));
```

### Rendering list

```js
import React from 'react';
import ReactDOM from 'react-dom';

const lakeList = ['Ganga', 'Yamuna', 'Nile'];

function App({ lakes }) {
  return (
    <ul>
      {lakes.map((lake) => (
        <li>{lake}</li>
      ))}
    </ul>
  );
}

ReactDOM.render(<App lakes={lakeList} />, document.getElementById('root'));
```

### Rendering list of object

```js
import React from 'react';
import ReactDOM from 'react-dom';

const lakeList = [
  { id: 1, name: 'Gange', city: 'Uttarakhand' },
  { id: 2, name: 'Yamuna', city: 'Uttarakhand' },
  { id: 3, name: 'Nile', city: "Don't know" },
];

function App({ lakes }) {
  return (
    <div>
      {lakes.map((lake) => (
        <div key={lake.id}>
          <h2>{lake.name}</h2>
          <p>City: {lake.city}</p>
        </div>
      ))}
    </div>
  );
}

ReactDOM.render(<App lakes={lakeList} />, document.getElementById('root'));
```

### Conditional rendering

```js
import React from 'react';
import ReactDOM from 'react-dom';

function Lake({ name }) {
  return (
    <div>
      <h1>Visit {name}</h1>
    </div>
  );
}

function SkiResort({ name }) {
  return (
    <div>
      <h1>Visit {name}</h1>
    </div>
  );
}

// function App(props) {
//   if (props.season === 'summer') {
//     return <Lake name='Jenny Lake' />;
//   } else if (props.season === 'winter') {
//     return <SkiResort name='JHMR' />;
//   } else {
//     return <h1>Come back another time</h1>;
//   }
// }

// ----- or ------

function App(props) {
  return (
    <div>
      {props.season === 'summer' ? (
        <Lake name='Jenny Lake' />
      ) : props.season === 'winter' ? (
        <SkiResort name='JHMR' />
      ) : (
        <h1>Come back another time</h1>
      )}
    </div>
  );
}

ReactDOM.render(<App season='winter' />, document.getElementById('root'));
```

### React fragment

We can use `<> </>` or `<React.Fragment> </React.Fragment>`

```js
import React from 'react';
import ReactDOM from 'react-dom';

function Lake() {
  return <h1>Visit Jenny Lake</h1>;
}

function SkiResort() {
  return <h1>Visit JHMR</h1>;
}

function App() {
  return (
    <>
      <Lake name='Jenny Lake' />
      <SkiResort name='JHMR' />
    </>
  );
}

ReactDOM.render(<App />, document.getElementById('root'));
```

```js
import React from 'react';
import ReactDOM from 'react-dom';

function Lake() {
  return <h1>Visit Jenny Lake</h1>;
}

function SkiResort() {
  return <h1>Visit JHMR</h1>;
}

ReactDOM.render(
  <>
    <Lake />
    <SkiResort />
  </>,
  document.getElementById('root')
);
```

### Array destructuring

```js
const [first, second, third] = ['Apple', 'Orange', 'Mango'];

console.log(first);
console.log(second);
console.log(third);
```

If we want ony the third item then,

```js
const [, , third] = ['Apple', 'Orange', 'Mango'];

console.log(third);
```

If we want first and third item,

```js
const [first, , third] = ['Apple', 'Orange', 'Mango'];

console.log(first);
console.log(third);
```

### Using useState hook

```js
import React, { useState } from 'react';
import ReactDOM from 'react-dom';

function App() {
  const [status, setStatus] = useState('Open');
  return (
    <div>
      <h1>Status: {status}</h1>
      <button onClick={() => setStatus('Open')}>Open</button>
      <button onClick={() => setStatus('Back in 5')}>Break</button>
      <button onClick={() => setStatus('Closed')}>Closed</button>
    </div>
  );
}

ReactDOM.render(<App />, document.getElementById('root'));
```

### Using multiple state variable

```js
import React, { useState } from 'react';
import ReactDOM from 'react-dom';

function App() {
  const [year, setYear] = useState(2050);
  const [manager, setManager] = useState('Alex');
  const [status, setStatus] = useState('Open');
  return (
    <>
      <div>
        <h1>Year: {year}</h1>
        <button onClick={() => setYear(year + 1)}>New Year</button>
      </div>
      <div>
        <h1>Manager: {manager}</h1>
        <button onClick={() => setManager('Mark')}>New Manager</button>
      </div>
      <div>
        <h1>Status: {status}</h1>
        <button onClick={() => setStatus('Open')}>Open</button>
        <button onClick={() => setStatus('Back in 5')}>Break</button>
        <button onClick={() => setStatus('Closed')}>Closed</button>
      </div>
    </>
  );
}

ReactDOM.render(<App />, document.getElementById('root'));
```

### useEffect

useEffect is going to allow us to perform side effects inside of our function components. The things that we want the component to do other than return UI are called effects. So an alert, a console log, any sort of interaction with the browser or a native API is not part of the render or return. So we can use these use effect hooks to do all sorts of things in the applications to make them more interactive and to handle all sorts of bits of functionality.

```js
import React, { useState, useEffect } from 'react';
import ReactDOM from 'react-dom';

function Checkbox() {
  let [checked, setChecked] = useState(false);

  useEffect(() => {
    alert(`checked: ${checked.toString()}`);
  });

  return (
    <>
      <input
        type='checkbox'
        value={checked}
        onChange={() => setChecked((checked = !checked))}
      />
      {checked ? 'checked' : 'not checked'}
    </>
  );
}

ReactDOM.render(<Checkbox />, document.getElementById('root'));
```

### Updating with the use effect dependency array

The second argument that we pass to useEffect is called dependency array.
In that array we will use the state variable that we want to listen for changes in.

```js
import React, { useState, useEffect } from 'react';
import ReactDOM from 'react-dom';

function App() {
  const [val, setVal] = useState('');
  const [val2, setVal2] = useState('');

  useEffect(() => {
    console.log(`field 1: ${val}`);
  }, [val]);

  useEffect(() => {
    console.log(`field 2: ${val2}`);
  }, [val2]);

  return (
    <>
      <label>
        Favorite Phrase:
        <input value={val} onChange={(e) => setVal(e.target.value)} />
      </label>
      <br />
      <br />
      <label>
        Second Favorite Phrase:
        <input value={val2} onChange={(e) => setVal2(e.target.value)} />
      </label>
    </>
  );
}

ReactDOM.render(<App />, document.getElementById('root'));
```

### Fetching data with useEffect

```js
import React, { useState, useEffect } from 'react';
import ReactDOM from 'react-dom';

function GitHubUser({ login }) {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch(`https://api.github.com/users/${login}`)
      .then((res) => res.json())
      .then(setData)
      .catch(console.error);
  }, [login]);

  if (data) {
    return (
      <div>
        <h1>{data.login}</h1>
        <img src={data.avatar_url} alt={data.login} width={100} />
      </div>
    );
  }

  return null;
}

function App() {
  return <GitHubUser login='abfarhan' />;
}

ReactDOM.render(<App />, document.getElementById('root'));
```

### useReducer

```js
import React, { useReducer } from 'react';
import ReactDOM from 'react-dom';

function Checkbox() {
  let [checked, toggle] = useReducer((checked) => !checked, false);

  return (
    <>
      <input type='checkbox' value={checked} onChange={toggle} />
      {checked ? 'checked' : 'not checked'}
    </>
  );
}

ReactDOM.render(<Checkbox />, document.getElementById('root'));
```
