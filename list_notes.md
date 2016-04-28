# List Notes

## Add a List Component

``` /imports/components/lists/list.jsx ```

```js
import React from 'react'

export const List = (props) =>{

	return <ul>
	    { 
	    	props.collection.map((item) => {
	 	      return <li key={item._id}>{item.content}</li>
	      })
	    }
  </ul>
}

List.propTypes = {
	collection: React.PropTypes.array.isRequired
}
```

Discuss: required propTypes

## Place SingleFieldSubmit at the top of the list
 - Discuss copy props.
 - Discuss: making add Item an optional "feature" of a list. We'll do that later.


## Display notes in the list

### Update NotesContainer

```js
import { createContainer } from 'meteor/react-meteor-data'
import { Notes } from '../../api/notes/notes'
import { List } from '../lists/list'
// import { SingleFieldSubmit } from '../forms/single_field_submit'


export default createContainer(() => {

	const notes = Notes.find({}, { sort: { updatedAt: -1 }}).fetch()
	
	const handleCreateNote = (content) => {
		Notes.insert({ 
			content:content,
			updatedAt: new Date() 
		})
	}

  return {
  	handleSubmit: handleCreateNote,
	  placeholder: "New Note",
      collection: notes
  }

}, List)

```

The browser should now update to display your notes as you add them

_insert screen shot_

- Discuss: reactively updating data. 


