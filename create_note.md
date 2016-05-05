_Get caught up to this step: Check out branch 03-app-header - see Introduction for info on how to get caught up using branches._
<hr>
# Step 4: Create Notes (Add Data)
First, we need to enable use of data in our React components.  There are [many ways](https://www.discovermeteor.com/blog/data-loading-react/) to do this.  I prefer the [official](http://guide.meteor.com/react.html) Meteor method.

## Add support for handling Meteor Data in React

- Add the Meteor package: ```meteor add react-meteor-data```
- Add the npm package: ```npm i react-addons-pure-render-mixin --save```


## Create a Mongo dB Notes Collection
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

export class SingleFieldSubmit extends React.Component {

  constructor(props){
    super(props)
    this.state = {
      inputValue: this.props.inputValue
    }
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
      return <form  className="form-inline" onSubmit={this.handleSubmit.bind(this)}>
        <input
          type="text"
          className="form-control"
          placeholder={this.props.placeholder}
          value={this.state.inputValue}
          onChange={this.updateInputValue.bind(this)}
        />
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
-  Why are we naming our component in this way?


## Create a data container for handling form input
We need to handle the data submitted in the form.  For this, we'll create a container, that allows us to interface between React and Meteor.

``` /imports/components/containers/notes_container.js ```

```js
import { createContainer } from 'meteor/react-meteor-data'
import { Notes } from '../../api/notes/notes'
import { SingleFieldSubmit } from '../forms/single_field_submit'

export default createContainer(() => {
	
  const handleCreate = (content) => {
    Notes.insert({ 
	  content:content,
	    updatedAt: new Date() 
	  })
	}

  return {
  	handleSubmit: handleCreate,
	placeholder: "New Note",
  }
}, SingleFieldSubmit)
```

- What's going on with ```export default```?
- Where does the stuff we return go to?

# Add the Notes container to our app

Note: we are replacing the "React placeholder" text with this component.

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
- Why is there no need for brackets when importing ```NotesContainer```?

## Try creating some notes
If you enter some text and hit return, it will appear as if nothing is happening. This is only because we haven't added support yet for viewing notes.

## View your notes in a mongo console

In your terminal, open a new window or tab:

``` meteor mongo ```

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

## Auto-binding functions

Why is binding necessary? See [Why and how to bind methods in your React component classes](http://reactkungfu.com/2015/07/why-and-how-to-bind-methods-in-your-react-component-classes/).

Let's make things easy and just auto-bind instead.

- Install the autobind package: ``` npm i react-autobind --save ```

- Update the one component where we've used binding so far. Add ``` autoBind(this)``` to your constructor and remove all your bind calls.

``` /imports/components/forms/single_field_submit.jsx ```

```js
...
import autoBind from 'react-autobind'

export class SingleFieldSubmit extends React.Component {

  constructor(props){
   ...
    autoBind(this)
  }

 ...

  render() {
      return <form  className="form-inline" onSubmit={this.handleSubmit.bind(this)}>
         ...
          onChange={this.updateInputValue}
        />
      </form>
  }
}
 ...
```

