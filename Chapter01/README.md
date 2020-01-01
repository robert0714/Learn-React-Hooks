# Introducing React and React Hooks

## Example code

1. traditional class component: chapter1_1 
1. using Hooks instead ( function component ): chapter1_2
1. Check out the following video to see the code in  action:
http://bit.ly/2Mm9yoC
1. Comparison

Class component

```js
import React from 'react'

class MyName extends React.Component {
    constructor (props) {
        super(props)
        this.state = { name: '' }
        this.handleChange = this.handleChange.bind(this)
    }

    handleChange (evt) {
        this.setState({ name: evt.target.value })
    }

    render () {
        const { name } = this.state
        return (
            <div>
                <h1>My name is: {name}</h1>
                <input type="text" value={name} onChange={this.handleChange} />
            </div>
        )
    }
}

export default MyName
```

Function component with Hook

```js
import React, { useState } from 'react'

function MyName () {
    const [ name, setName ] = useState('')

    function handleChange (evt) {
        setName(evt.target.value)
    }
    
    return (
        <div>
            <h1>My name is: {name}</h1>
            <input type="text" value={name} onChange={handleChange} />
        </div>
    )
}

export default MyName
```

