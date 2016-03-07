# Add an App Homepage
- Try going to /afsdfdsdfsf you'll see the same view is displayed.
- Create a new branch for this feature
- Add tasks in our feature card
- Add react via npm
- ```npm init -f```
- ```npm i react react-dom --save```
- look at package.json file
- discuss module system in Meteor 1.3: https://github.com/meteor/meteor/blob/release-1.3/packages/modules/README.md
- Add routing
- Discuss Meteor packages
- ``` meteor add kadira:flow-router ```
- ``` npm i react-mounter --save ```
- Discuss following the errors, eg "there is no route for '/'"

Add routes file:

``` /client/routes.jsx ```
- Discuss jsx file type

```js
import React from 'react'
import {mount} from 'react-mounter'

FlowRouter.route("/", {
  action() {
    mount(MainLayout, {
        content: (<Homepage />)
    });
  }
})
```



- Discuss module system and imports vs Meteor's Magic Globals
- Discuss stateless functions: /*
 * This is a stateless function or stateless component. It's a type of React
 * component (though technically just a function) whose only job is to render
 * output. It isn't aware of any state, it doesn't perform any logic.
 * See https://facebook.github.io/react/docs/reusable-components.html#stateless-functions
 *
 * Technically the name MainLayout isn't needed here since it's an export
 * default, but I include it so WebStorm can trace back to it when I cmd-click
 * on any references to MainLayout. Plus, code clarity.
 */
 

Follow the errors: "MainLayout is not defined"

Add /client/layouts/MainLayout.jsx, /client/pages/HomePage.jsx

```
import React from 'react'

export const MainLayout = ({content}) => <div>
	  <h1>My App</h1>
	  {content}
	</div>
  ```
  
  ```js 
  import React from 'react'

export const Homepage = () => <div>This is the homepage</div>
```






