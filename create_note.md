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

## Add a React component that submits input when using the return key

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
      return <form  className="form-inline" onSubmit={this.handleSubmit}>
      <div className="form-group">
        <input
          type="text"
          className="form-control"
          placeholder={this.props.placeholder}
          value={this.state.inputValue}
          onChange={this.updateInputValue}
        />
        </div>
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


# Create a data container for handling form input
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

# Add the container (wrapping the form) to our app layout

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

# Try creating some notes
If you enter some text and hit return, it will appear as if nothing is happening. This is only because we haven't added support yet for viewing notes.

## View your notes in a mongo console

In your terminal, open a new window):

``` meteor mongo ``` (make sure meteor is still running)

``` 
meteor:PRIMARY> db.notes.find().pretty()

{
	"_id" : "PJr8Ykuz7yBaT5RpL",
	"content" : "a test note",
	"updatedAt" : ISODate("2016-04-28T16:28:26.298Z")
}
{
	"_id" : "bqfx2Xw9RW5MnPGua",
	"content" : "another test note",
	"updatedAt" : ISODate("2016-04-28T16:28:30.332Z")
}
```

You can also view them directly in the client using the [mongol package](https://atmospherejs.com/msavin/mongol).
