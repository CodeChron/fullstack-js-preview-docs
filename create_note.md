# Create Notes (Add Data Support)
First, we need to enable use of data in our React components.  There are many ways to do this.  I prefer the official Meteor method.

## Add support for handling Meteor Data in React

- Add the Meteor package: ```meteor add meteor-react-data```
- Add the npm package: ```npm i react-addons-pure-render-mixin --save```


## Add Notes Collection
``` ADD PATH ```

```js
import { Mongo } from 'meteor/mongo'
import { Meteor } from 'meteor/meteor'

export const Notes = new Mongo.Collection('notes')
```

## Add a React component that supports creating notes on submit (return key)

``` /imports/components/forms/single_field_submit.jsx ```

_TODO: do this without binding, then add auto-bind_

```js
import React from 'react'
import autoBind from 'react-autobind'

export class SingleFieldSubmit extends React.Component {

  constructor(props){
    super(props)
    this.state = {
      inputValue: this.props.inputValue
    }
    autoBind(this)
  }

  updateInputValue(e){
    this.setState({inputValue: e.target.value})
  }

  handleSubmit(e) {
    e.preventDefault()
    this.props.handleSubmit(this.state.inputValue)
    this.setState({inputValue: ""})
  }

  render() {
      return <form onSubmit={this.handleSubmit} className="full-width invisible-field">
        <input
          type="text"
          className="full-width text-input"
          placeholder={this.props.placeholder}
          value={this.state.inputValue}
          onChange={this.updateInputValue}
        />
         <input type="submit" style={{display:'none'}} />
      </form>
  }
}

SingleFieldSubmit.propTypes = {
  handleSubmit: React.PropTypes.func.isRequired,
  placeholder: React.PropTypes.string
}

SingleFieldSubmit.defaultProps = {
  inputValue:  ""  ,
  placeholder: "New..."
}
```

- Discuss: Stateful React components, use of the constructor, passing props, binding, propTypes, and default props.

## Auto-binding functions
Why is binding necessary? See [Why and how to bind methods in your React component classes](http://reactkungfu.com/2015/07/why-and-how-to-bind-methods-in-your-react-component-classes/).

Let's make things easy and just auto-bind instead

``` npm i react-autobind --save ```

Now, add ``` autoBind(this)``` to your constructor and remove all your ``` ...bind(this) ```



## Create a Notes (Data) Container
_TODO: create a version of this with just the single field submit_


```js
code
```
