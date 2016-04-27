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

## Display notes in the list


## Place SingleFieldSubmit at the top of the list
