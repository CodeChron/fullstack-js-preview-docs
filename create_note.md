# Create Notes (Add Data Support)
First, we need to enable use of data in our React components.  There are many ways to do this.  I prefer the official Meteor method.


## Add support for handling Meteor Data in React

- Add the Meteor package: ```meteor add react-meteor-data```
- Add the npm package: ```npm i react-addons-pure-render-mixin --save```


## Create a Notes Collection
``` /imports/api/notes/notes.js ```

```js
import { Mongo } from 'meteor/mongo'
import { Meteor } from 'meteor/meteor'

export const Notes = new Mongo.Collection('notes')
```

## Make the collection available on the server

The Notes collection we created needs to be available on the server side for database operations to work.

``` /imports/startup/server/index.js ```

```js 
import { Notes} from '/imports/api/notes/notes'
```

``` /server/index.js ```

```js 
import '/imports/startup/server/'
```

## Add a React component that supports creating notes on submit

``` /imports/components/forms/single_field_submit.jsx ```

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

-  Why are we using React.Component in this case?
-  What's the purpose of the constructor?

## Auto-binding functions
- Why is binding necessary?
- What code would need to write if we did not auto-bind?
- See [Why and how to bind methods in your React component classes](http://reactkungfu.com/2015/07/why-and-how-to-bind-methods-in-your-react-component-classes/).

Let's make things easy and just auto-bind instead

``` npm i react-autobind --save ```

Now, add ``` autoBind(this)``` to your constructor and remove all your ``` ...bind(this) ```


## Create a data container for handling form input
We need to handle the data submitted in the form.  For this, we'll create a container, that allows us to interface between React and Meteor.

``` /imports/components/containers/notes_container.js ```

```js
import { createContainer } from 'meteor/react-meteor-data'
import { Notes } from '../../api/notes/notes'
import { SingleFieldSubmit } from '../forms/single_field_submit'

export default createContainer(() => {
	
  const handleCreateNote = (content) => {
    Notes.insert({ 
	  content:content,
	    updatedAt: new Date() 
	  })
	}

  return {
  	handleSubmit: handleCreateNote,
	placeholder: "New Note",
  }
}, SingleFieldSubmit)
```


## Add the container (wrapping the form) to our app layout

``` /imports/components/layouts/app_layout.jsx ```

```js
...
import NotesContainer from '../containers/notes_container'

export const AppLayout = () =>
  ...
    <div id="main-content" className="container">
      <NotesContainer />
    </div>
  ...
```

## Add 

## View the notes you've created
- view in the mongo console
- view using the mongol package

