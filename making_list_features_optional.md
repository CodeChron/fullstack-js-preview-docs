# Making List Features Optional

Let's make the add item form and the delete button optional in the list.  This will make the component more versatile and easier to re-use.


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

List.propTypes = {
	collection: React.PropTypes.array.isRequired
}
```

Discuss: required propTypes



