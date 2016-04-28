# Delete a Note


## Add a button component for deleting a note

``` /imports/components/buttons/button.jsx ```

```js
import React from 'react'

export const Button = (props) =>
  <button onClick={props.handleClick}>
    {props.label}
  </button>

TextBtn.propTypes = {
	handleClick: React.PropTypes.func.isRequired,
	label: React.PropTypes.string.isRequired
}
```
Discuss: will likely want to have many button types, eg text button, icon button.


## Add delete as an optional list feature

## Delete notes on click


