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

``` /both/routes.jsx ```
- Discuss jsx file type

```js
import React from 'react';
import {mount} from 'react-mounter';

FlowRouter.route("/", {
  action() {
    mount(MainLayout, {
        content: (<Homepage />)
    });
  }
});
```

- Discuss module system and imports vs Meteor's Magic Globals

Follow the errors: "MainLayout is not defined"

Add /components/layouts/MainLayout.jsx, /components/pages/HomePage.jsx





