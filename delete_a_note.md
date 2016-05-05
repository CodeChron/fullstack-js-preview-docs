_Get caught up to this step: Check out branch 05-list-notes - see Introduction for info on how to get caught up using branches._
<hr>
# Step 6: Delete a Note


## Add an Icon Button component
We're going to need a button with a delete icon that accepts a click event. Let's create a reusable component.

``` /imports/components/buttons/icon_btn.jsx ```

```js
export const IconBtn = (props) =>
  <button
    onClick={props.handleClick}
    className="btn btn-default btn-xs"
    title={props.title}
     alt={props.title}
  >
    <span className={props.icon} aria-hidden="true"></span>
  </button>

IconBtn.propTypes = {
	handleClick: React.PropTypes.func.isRequired,
	icon: React.PropTypes.string.isRequired,
	title: React.PropTypes.string
	
}
```

## Add the component as a delete button to the list

``` /imports/components/lists/list.jsx ```

```js
...
import { IconBtn } from '../buttons/icon_btn'
...
	const handleDelete = (item) => {
		const confirmDelete = confirm("Really delete this?")

 	  if (confirmDelete) {
 	  	props.handleDelete(item)
 	  }
	}
    ...
    return <li key={item._id}>{item.content} <span className="pull-right"><IconBtn title={"Delete"} icon={"glyphicon glyphicon-remove"}  handleClick={()=> handleDelete(item)} /></span></li>
    ...
```

- Why the need for ```{() => callFunction()}```? See http://stackoverflow.com/questions/33846682/react-onclick-fuction-fires-on-render (TL;DR "Because you are calling that function instead of passing function to onClick")
- Could we refactor this to have a DeleteBtn? (Or, should the List component really be responsible for handling deletion?)

## Handle deletion of a note


``` /imports/containers/notes_container.jsx ```

```js
...

export default createContainer(() => {
 ...

	const handleDelete = (note) => {
		Notes.remove({_id: note._id})
	}

  return {
    ...
	  handleDelete: handleDelete
  }

}, List)

```
