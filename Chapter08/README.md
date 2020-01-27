# Chapter 8: Using Community Hooks

## Example code

1. Check out the following video to see the code in  action:
https://www.youtube.com/watch?v=ZAq-WHcXwHA&list=PLeLcvrwLe187GQf0pQTtWTpppdjSAOI5u&index=8



## for windows running

```json
{
  "name": "chapter7_3",
  "version": "1.0.0",
  "private": true,
  "dependencies": {
    "@use-hooks/axios": "^1.3.1",
    "axios": "^0.19.2",
    "concurrently": "^5.0.2",
    "http-proxy-middleware": "^0.20.0",
    "json-server": "^0.15.1",
    "navi": "^0.14.0",
    "react": "^16.12.0",
    "react-busy-indicator": "^1.0.0",
    "react-dom": "^16.12.0",
    "react-navi": "^0.14.3",
    "react-request-hook": "^2.1.1",
    "react-scripts": "^3.3.0"
  },
  "scripts": {
    "start": "npx concurrently \"npm:start-server\" \"npm:start-client\"",
    "start-server": "npx json-server --watch server/db.json --port 4000 --routes server/routes.json",
    "start-client": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "test-nowatch": "npx concurrently --kill-others --success \"first\" \"npm:start-server\" \"npm:test-client -- --watchAll=false\"",
    "test-client": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "eslintConfig": {
    "extends": "react-app"
  },
  "browserslist": [
    ">0.2%",
    "not dead",
    "not ie <= 11",
    "not op_mini all"
  ]
}
```

## Chapter 8-2 ~ 8-3

Step 1  Creating a React skeleton .

```bash
npx create-react-app chapter8_2
```

Step 2 create sample folder and its index.js

```bash
mkdir -p src/examples
vi examples/index.js
```

And the content of examples/index.js as seen below:

```js
import UsePrevious from './UsePrevious'
import UseInterval from './UseInterval'
import IntervalWithEffect from './IntervalWithEffect'
import UseTimeout from './UseTimeout'
import TimeoutWithEffect from './TimeoutWithEffect'
import UseOnlineStatus from './UseOnlineStatus'
import OnlineSync from './OnlineSync'
import UseBoolean from './UseBoolean'
import UseArray from './UseArray'
import UseCounter from './UseCounter'
import UseFocus from './UseFocus'
import UseHover from './UseHover'

export default {
  UsePrevious,
  UseInterval, IntervalWithEffect,
  UseTimeout, TimeoutWithEffect,
  UseOnlineStatus, OnlineSync,
  UseBoolean, UseArray, UseCounter,
  UseFocus, UseHover
}
```

And then the src/App.js needs to be modified as below :

```js
import React, { useState } from 'react'

import examples from './examples'

const Example = ({ name, component }) => {
  const [ active, setActive ] = useState(true)

  function toggleActive () {
    setActive(!active)
  }

  return (
    <div>
      <hr />
      <h2>
        {name}{' '}
        <button onClick={toggleActive}>
          {active ? 'unmount' : 'mount'}
        </button>
      </h2>
      {active && React.createElement(component)}
      <br />
    </div>
  )
}

export default function App () {
  return (
    <div>
      <h1>React Hooks Examples</h1>
      {Object.entries(examples).map(([ name, component ]) =>
        <Example key={name} name={name} component={component} />
      )}
    </div>
  )
}
```