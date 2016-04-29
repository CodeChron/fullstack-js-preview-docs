# Add React

Branch: 02-add-react

- rm all blaze templates
- install react via npm - be sure you are in the app directory

```meteor npm install react react-dom --save```

- Why are we using npm instead of a Meteor package?
- What is the purpose of the ```--save``` option? 


> "By default, NPM simply installs a package under node_modules. When you're trying to install dependencies for your app/module, you would need to first install them, and then add them (along with the appropriate version number) to the dependencies section of your package.json.

> The --save option instructs NPM to include the package inside of the dependencies section of your package.json automatically, thus saving you an additional step."
http://stackoverflow.com/questions/19578796/what-is-the-save-option-for-npm-install




## Add an app layout component

``` /imports/compononents/layouts/app_layout.jsx ```
```js 
import React from 'react'

export const AppLayout = () =>
  <div id="app-container" className="container">
    <div id="main-content">
      React placeholder
    </div>
  </div>
```

- What is the '=>' thing?
- Isn't this just a plain JS function? Why are we not using React.createClass or React.Component?
- Why are we using 'className' rather than class?


 
## add a render target
```html
<body>
  <div id="app"></div>
</body>
```

## render it
```js
import React from 'react'
import ReactDOM from 'react-dom'
import { AppLayout } from '/imports/components/layouts/app_layout'

Meteor.startup(() =>
	ReactDOM.render(<AppLayout />, document.getElementById("app"))
)
```

## import on startup

```js
import './main.html'
import './main.js'

```

You should now see this in your browser:

![Dflt view with React added](images/react-added-dflt.png)
