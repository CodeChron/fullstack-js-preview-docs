# Step 7: Making List Features Optional

Let's make the add item form and the delete button optional in the list.  This will make the component more versatile and easier to re-use.

Discuss: this is getting advanced...don't freak out :-}

## Move optional features into a collection

``` /imports/components/lists/list.jsx ```

```js
...
 const listFeatures = {
  	addItem: () => <li><SingleFieldSubmit {...props} /></li>,
  	deleteItem: (args) => <Btn label={"x"}  handleClick={()=> handleDelete(args)} />
	}
...
}
```

Discuss use of objects and key/value pairs.

## Create a function for accessing a feature and passing in arguments

```js
...
const displayFeature = (shouldDisplay, feature, args ) => {
	  return shouldDisplay? feature(args) : null
	}
...
}
```


Discuss optional arguments


## Use the function to dynamically display a feature

```js
	return <ul>
	    {displayFeature(props.addItem, listFeatures.addItem)}
	    { 
	    	props.collection.map((item) => {
	 	      return <li key={item._id}>{item.content} {displayFeature(props.deleteItem, listFeatures.deleteItem, item)}
	 	      </li>

	      })
	    }
  </ul>
}

```

## Add propTypes and defaultProps to hide features by default

```js
List.propTypes = {
	collection: React.PropTypes.array.isRequired,
	addItem: React.PropTypes.bool,
	deleteItem:  React.PropTypes.bool,
}
List.defaultProps = {
	addItem: false,
	deleteItem: false
}
```


## "Turn on" the features via props

``` /imports/containers/note_container.jsx ```


```js
  return {
     ...
	  addItem: true,
	  deleteItem: true
  }
```

Discuss: we can now easily scale this set of features.