# Making List Features Optional

Let's make the add item form and the delete button optional in the list.  This will make the component more versatile and easier to re-use.


## Move optional features into a collection

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



