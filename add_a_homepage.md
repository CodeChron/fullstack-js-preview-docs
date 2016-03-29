# Add a Homepage (Routing)
While we could start adding content directly to the default app container we've created, this is not a good idea, since we know that this app will have multiple pages (Homepage, Note Details, Login, and more.)

Therefore, let's add an actual homepage.  This means that we're going to want to add routing, even though we only have one page.

## Add Routing

``` meteor add kadira:flow-router ```

Install layout support for react:
``` npm i react-mounter --save ```

Discuss the state of routing and community packages and needing to use both meteor and npm package systems.

## Add a base layout
I prefer to just think of this as the app container. Everything we place here will be global to the entire app.
If you have multiple layouts, you can choose to name this "main_layout' or the like.

```
import React from 'react'

export const App = ({content}) => <div>{content()}<Alert /></div>
```
Discuss the {content} prop.



After installing this we should see message that we don't have a homepage.

## Add a homepage (root) route

``` /client/routes.jsx ```

```js
import React from 'react'
import {mount} from 'react-mounter'

import {App} from './app'
import {AppHeader} from './layouts/app_header'
import {NotesList} from './containers/notes_list'


FlowRouter.route('/', {
  name: 'homepage',
  action() {
    mount(App, {
      header: () =>  <AppHeader />,
      content: () => <NotesList />
    })
  }
})

```


