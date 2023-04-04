# Table of Contents

# Javascript
```javascript
//////////// VARIABLES ////////////

let x = 5; // variable will change -> let
const a = 17; // variable will not change -> const

// deconstruction
let a, b, rest;
[a, b] = [10, 20];
[a, b, ...rest] = [10, 20, 30, 40, 50]; // rest is array

// template literals
// use backtick `
let a = `he is ${5+1} years old`


//////////// OPERATORS ////////////
let a = isMember ? 10 : 15


//////////// CONTROL ////////////

// for loop
for (let i = 0; i < arr.length; i++) { }


//////////// FUNCTIONS ////////////

// normal basic function
function square(number) {
  return number * number;
}

// anonymous function
const square = function (number) {
  return number * number;
};
const x = square(4); // x gets the value 16

// arrow anonymous function with block body
const func2 = (x, y) => {
  return x + y;
};

// arrow anonymous function in use
const a3 = a.map((s) => s.length); // ["hi", "b"] -> [2,1]


//////////// DATA STRUCTURES ////////////

// object
let person1 = {
  name: "john",
  age: 2,
}

// array
const a = [1,"hi"];
a.push(2.34);
a.length


//////////// IMPORTING/EXPORTING ////////////

// exporting/importing library/multiple
// exporting in say.js
function sayHi(user) {
  alert(`Hello, ${user}!`);
}
let months = ['Jan', 'Feb', 'Mar']
export {sayHi, months}; // a list of exported variables

// importing in main.js
import {sayHi, months} from './say.js';
import * as say from './say.js';
say.sayHi('john');

// exporting one class
// exporting in user.js
export default class User { // just add "default"
  constructor(name) {
    this.name = name;
  }
}

// importing in main.js
import User from './user.js'; // not {User}, just User
new User('John');

```

# JSX
- lets you write HTML like code in javascript
- you can convert HTML to jsx using a [converter tool like this](https://transform.tools/html-to-jsx)
- 3 Rules:
  1. Multiple elements together must be in one tag
``` jsx
<>
  <h1>Hedy</h1>
  <h2>hi<\h2>
</>
```
  2. All tags need to be closed, even single ones
``` jsx
<img 
  src="https://i.imgur.com/yXOvdOSs.jpg"
/>
```
  3. CamelCase most things
``` jsx
<img 
  src="https://i.imgur.com/yXOvdOSs.jpg"
  className="photo" // originally class-name
/>
```

# Importing
- Import React (core library) and ReactDOM (to interact with DOM) and babel (javascript compiler to convert jsx to javascript)
``` HTML
<!-- index.html -->
<html>
  <body>
    <div id="app"></div>

    <script src="https://unpkg.com/react@17/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>

    <script type="text/jsx">
      const app = document.getElementById('app');
      ReactDOM.render(<h1>Develop. Preview. Ship. 🚀</h1>, app);
    </script>

  </body>
</html>
```

# Components
- functions that group html into a component
- must be capitalized and calced as an html tag
``` jsx
function Header() {
  return <h1>hello there</h1>;
}

function HomePage() {
  return (
    <div>
      <Header />
    </div>
  );
}

ReactDOM.render(<HomePage />, app);
```

# Props
- arguments that go into a component
``` jsx
// pass in props as object
function Header(props) {
  return <h1>{props.title}</h1>;
}

// pass in props use object destructuring
// use javascript in the html using { } inside the <></>
function Header({ title }) {
  return <h1>{title ? title : 'Default title'}</h1>;
}

// call component with props
function HomePage() {
  return (
    <div>
      <Header title="First title" />
      <Header title="Second title" />
    </div>
  );
}

// output of js in html can be arrays of html
// each array element must have key prop to uniquely identify each so react knows which to update in dom 
function HomePage() {
  const names = ['Ada Lovelace', 'Grace Hopper', 'Margaret Hamilton'];

  return (
    <div>
      <Header title="Names List" />
      <ul>
        {names.map((name) => (
          <li key={name}>{name}</li>
        ))}
      </ul>
    </div>
  );
}
```

# states
- states are stored for each instance of the component in useState
``` jsx
// handle events like onClick, onSubmit, onChange
function HomePage() {
  function handleClick() {
    console.log('increment like count');
  }

  return (
    <div>
      <button onClick={handleClick}>Like</button>
    </div>
  );
}

// handle state and updating states
function HomePage() {
  // [state value, function to update value]
  // 0 is initial value of state value
  const [likes, setLikes] = React.useState(0);

  function handleClick() {
    setLikes(likes + 1);
  }

  return (
    <div>
      <button onClick={handleClick}>Likes ({likes})</button>
    </div>
  );
}
```

# package management

### nvm
- install nvm to control the version of npm [here](https://github.com/nvm-sh/nvm#installing-and-updating)
- download nodejs (which include npm) from online
- include nodejs version in .nvmrc file for nvm to know what npm to use. then run `nvm install` and `nvm use`
```
16.13.0
```

### npm
- create empty package.json
```
{
}
```
- install using npm
```
npm install react react-dom next
```
- now there is a `node_modules` folder which is the actual dependencies. never code or change this
- `package.json` has dependencies outlined while `package-lock.json` locks in specific version for everything
- now when people use `npm install`, the project knows exactly what to install

- add dev mode to `package.json`
``` json
// package.json
{
"scripts": {
    "dev": "next dev"
  },
  // "dependencies": {
  //   "next": "^11.1.0",
  //   "react": "^17.0.2",
  //   "react-dom": "^17.0.2"
  // }
}
```
- run dev mode with `npm run dev` and see at [localhost:3000](http://localhost:3000/)
- import what is needed and export function that is run first

### next.js file system
- make a `pages` folder with file `index.jsx` in it
```jsx
import { useState } from 'react';

function Header({ title }) {
  return <h1>{title ? title : 'Default title'}</h1>;
}

export default function HomePage() {
  const names = ['Ada Lovelace', 'Grace Hopper', 'Margaret Hamilton'];
  const [likes, setLikes] = useState(0);

  function handleClick() {
    setLikes(likes + 1);
  }

  return (
    <div>
      <Header title="Develop. Preview. Ship. 🚀" />
      <ul>
        {names.map((name) => (
          <li key={name}>{name}</li>
        ))}
      </ul>

      <button onClick={handleClick}>Like ({likes})</button>
    </div>
  );
}
```

# link
- client side navigation
- fast and preloaded
- make new folders under pages -> url-folder -> name.js which makes the url /url-folder/name
- include link method
```
import Link from 'next/link';
```
- link within pages
``` jsx
<Link href="/">Back to home</Link>
```
