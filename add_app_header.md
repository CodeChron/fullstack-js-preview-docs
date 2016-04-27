# Step 2: Add App Header
Normally, I would not focus on this component until later, but creating the app header component will allow us to create a relatively simple component before getting into more advanced components.

## Create a AppHeaderLayout Component
This component should only be responsible for layout and nothing else.

``` /imports/components/layouts/app_header_layout.jsx ```

```js
import React from 'react'

export const AppHeaderLayout = (props) =>
  <div id="app-header">
	<div className="header-center">
      <h1 className="page-title">{props.pageTitle}</h1>
	</div>
  </div>

AppHeaderLayout.propTypes = {
  pageTitle: React.PropTypes.string
}

AppHeaderLayout.defaultProps = { 
  pageTitle: "My Notes App"
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

You should now see an unstyled version of the app header.

Try adding your own ``` pageTitle ``, eg  to `` <AppHeaderLayout pageTitle="My Custom Title" /> ``` and you'll see the page title update.