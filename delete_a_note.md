# Delete a Note


## Add a button component for deleting a note

``` /imports/components/buttons/button.jsx ```

```js
import React from 'react'

export const Btn = (props) =>
  <button onClick={props.handleClick}>
    {props.label}
  </button>

TextBtn.propTypes = {
	handleClick: React.PropTypes.func.isRequired,
	label: React.PropTypes.string.isRequired
}
```
Discuss: Why not "Button"?, will likely want to have many button types, eg text button, icon button.


``` ```

## Add the component as a delete button to the list

``` /imports/components/lists/list.jsx ```

```js

```

Discuss need for {() => callFunction()} See http://stackoverflow.com/questions/33846682/react-onclick-fuction-fires-on-render (TL;DR "Because you are calling that function instead of passing function to onClick"

## Make delete an optional list feature

## Add delete as an optional list feature

## Delete notes on click


