# Add an app title component


``` /client/content/page_title.jsx ```

```js

import React from 'react'

export const PageTitle = (props) => <h1 className="page-title">{props.pageTitle}</h1>

PageTitle.propTypes = {
	pageTitle: React.PropTypes.string
}

PageTitle.defaultProps = { 
  pageTitle: "My Notes App"
}

```

- Discuss: component naming, why page title?
- Discuss: props, propTypes, and useful defaults.

# Insert the Page Title component

Let's now add this component to the main app:

```js
...
import {PageTitle} from './content/page_title'

export const App = () => <div><PageTitle /></div>

```
You should now see your default page title in the browser window.


## Add a single field submit component
- Discuss component naming
- After creating: where will the data go?

NOTE: May be introducing styling and SASS already here.


