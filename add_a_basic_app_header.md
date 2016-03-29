# Add a basic app header

Here, we have a static app header and a component that submits that was input to a handler.

## Add an app header and a page title component

``` /client/layout/app_header.jsx ```

```js
import React from 'react'

export const AppHeader = (props) => 
	<header className="app-header">
	  <div className="header-left">
	   {props.headerLeft}
	  </div>
	  <div className="header-center">
	    {props.headerCenter}
	  </div>
	  <div className="header-right">
      {props.headerRight}
    </div>
	</header>

AppHeader.propTypes = {
  headerLeft: React.PropTypes.object,
  headerCenter: React.PropTypes.object,
  headerRight: React.PropTypes.object
}
```

- Discuss: adding useful default values to components.
- Discuss: why not just include a page title in the app header?

## Add a single field submit component
- Discuss component naming
- After creating: where will the data go?

NOTE: May be introducing styling and SASS already here.


