# Step 2: Add App Header
Normally, I would not focus on this component until later, but creating the app header component will allow us to create a relatively simple component before getting into more advanced components.

## Create a AppHeaderLayout Component
This component should only be responsible for layout and nothing else.

``` /imports/components/layouts/app_header_layout.jsx ```

```js
import React from 'react'

export const AppHeaderLayout = (props) =>
  <div id="app-header">
  	<div className="header-left">
	   {props.headerLeft}
	  </div>
	  <div className="header-center">
	    {props.headerCenter}
	  </div>
	  <div className="header-right">
      {props.headerRight}
    </div>
  </div>

AppHeaderLayout.propTypes = {
  headerLeft:   React.PropTypes.object,
  headerCenter: React.PropTypes.object,
  headerRight:  React.PropTypes.object
}

AppHeaderLayout.defaultProps = { 
  headerCenter: <h1 className="page-title">My Notes App</h1>
}
```

- Discuss: using props, propTypes, and defaultProps

## Add App Header to the main App Layout

``` /imports/components/layouts/app_layout.jsx ```

```js
...
import { AppHeaderLayout } from './app_header_layout'

export const AppLayout = () =>
  <div id="app-container">
    <AppHeaderLayout />
  ...
  </div>
```

You should now see an unstyled version of the app header

## Add some basic styling
_skip this?_
