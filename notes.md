# Notes
# App Install and Setup

## Create a Meteor App

```meteor create ClickToEdit```

## Upgrade to Meteor 1.3 (if needed)

_Encourage attendees to do this step before class, since downloading the new version of Meteor might take some time._

Open your terminal and navigate to a location where you want to store your app files.  I recommend having a top-level "dev" directory used for this purpose.

Create the meteor app.

_Note: Once this version of Meteor has been released, this additional step won't be necessary.

Confirm that you have the newest version of meteor typing ```meteor --version``` in your command line. (Be sure you are in the Meteor app directory.) You should see the following:

```
$ Meteor 1.3
```

_Moving forward whenever you see the following, it means you should type it or look for it in your command line terminal:

```
$ your terminal command line
```
client
## Run Meteor
To run your Meteor app, just type ```meteor``` in your command line.
- Open a browser window and enter the URL: http://localhost:3000 
- You should see the default Meteor app.
- Leave this window open while building the app. Meteor will auto-refresh as you make changes.
- I also recommend having the console open in this window.  ([Viewing the console in Chrome](https://developer.chrome.com/devtools/docs/console).)

Your browser window should look something like this:
_screen cap of default Meteor app_

## Remove default app files
We will not be using the default files created by Meteor.  Let's remove them:

```rm app_name*```

(replace app_name with whatever you named your app)

Your screen should now be blank in your browser.


## Initialize Npm

We will be using npm for managing certain packages, such as React, so let's add that now.

```npm init -f```

(Normally, I would not recommend using the "force" option, but in this case I think it makes sense.)



# Adding React
Discuss: adding React via NPM rather than as a Meteor package
 
## Add React packages using NPM
```
npm i react react-dom --save
```

"By default, NPM simply installs a package under node_modules. When you're trying to install dependencies for your app/module, you would need to first install them, and then add them (along with the appropriate version number) to the dependencies section of your package.json.

The --save option instructs NPM to include the package inside of the dependencies section of your package.json automatically, thus saving you an additional step."
http://stackoverflow.com/questions/19578796/what-is-the-save-option-for-npm-install


## Add a top-level "app" React Component

``` /client/app.jsx ```

```js
import React from 'react'

export const App = () => <div>My React App</div>

```
Discuss: 
- modules
- stateless components


## Add a "render target" to your web app (and remove some default Meteor code)

We need to create a location for where to render our (future) React components. Let's also at the same time remove some code we don't need.


## Tell Meteor to render to our target location on startup. 
Note the '.jsx' file name extension:

``` /client/startup.js ```

```js
import React from 'react'
import ReactDOM from 'react-dom'
import {App} from './app'

Meteor.startup(function(){
  ReactDOM.render(<App />, document.getElementById("app"))
})

```

# Add a text block component

```js
import React from 'react'

export class ClickToEdit extends React.Component {

  render(){
    return <div className="editable">My editable content</div>
  }
}

ClickToEdit.propTypes = { 
  editMode: React.PropTypes.bool
}

ClickToEdit.defaultProps = {
  editMode: false
}

```

- Discuss: stateful components, defining propTypes, setting default props

## Display the component

```js
import React from 'react'
import {ClickToEdit} from './content/click_to_edit'

export const App = () => <div><ClickToEdit /></div>
```

You should now see the placeholder content in your app.


# Add some style

Next, we want to add some styling to our app, not just so that it will look good (or at least ok), but also to support some key functionality, such as providing a nice big surface to click on.

Rather than just use a CSS framework like Boostrap, we'll create something from scratch.

There are several reasons why you want to do that if you are learning to code. 
You'll never really learn CSS by using something already created for you.
If you use something like Bootstrap or Foundation, you will found yourself writing CSS specific to these frameworks when customizing.

Don't get me wrong - there is nothing wrong with these frameworks, and they can be great for building web apps, but when your goal is to learn, then you should write your own from scratch.


# Add meta tags for mobile
This little meta tag is essential in allowing us to display info properly on mobile devices.

```html
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body><div id="app"></div></body>
```

# Add Support for SCSS (Sass)
Here, we are going to use a CSS pre-processor called SASS, which gives us a lot of benefits over just writing plain CSS.

We'll add a Meteor package to allow us to do that:

```
$ meteor add fourseven:scss
```

This package will allow us to create files in the SCSS format and then have them be automatically be converted to css.

Also, we want to add the following configuration file in our root directory:

``` /scss.json ```

```
{
  "enableAutoprefixer": true
}
```

This will automatically add vendor-specific prefixes to non-standard css attributes.

# Add SCSS Files
- add a stylesheets directory
- add a main.scss file



# Add Normalize
- we will just add normalize manually.  There are many reasons why I recommend doing it this way.
- You really just want to use it as is and not customize it.
- You don't want use something like npm where it might get updated and you didn't know.
- You don't want to get it via cdn or the like because that will require another connection to load your page.
- By doing it this way, the css will be minimified and added to the single css file generated by Meteor.

```scss
@import "core/_normalize";
```

After adding this, you should notice that your app display updates slightly (eg the font changes and there are no margins.



-  https://discuss.reactjs.org/t/should-we-include-the-props-parameter-to-class-constructors-when-declaring-components-using-es6-classes/2781


# (old) App Setup
- Create the app directory
- Add ReadMe with default content:

```sh
  echo "#Test Test" >> README.md

```
- Initialize Git

Gitignore:
```sh
node_modules
app/modules
npm-debug.log
tmp
.DS_Store
```

Initial Commit
- Create default meteor app
- Update to Meteor 1.3: ```meteor update --release 1.3-beta.12 ``` (TODO: in description, recommend people install this in advance once or it will take a long time.)
- Run app locally and open console - leave this tab open.
- Add deploy step here: ```meteor deploy m13-react-workshop``` (use your initials or the like to personalize)
- Why deploy first?
- Remove default files:  ```rm * ```
- Any other recommendations?
- ``` echo "node_modules" >> .gitignore ```

- Add screen cap with app with more files, like tests, build, etc.

- Add a simple deploy script:

```json
  "scripts": {
    "deploy": "meteor deploy m13-react-workshop"
  }
```

TODO: Add Head block:
```html
<head>
  <meta charset="utf-8">
  <meta name="description" content="A simple note-taking app">
  <meta name="keywords" content="Notes, ideas, scrapbook">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
```


**TODO: Roll our own CSS**

Instead of just using TWBS, we're going use a custom CSS framework.
- Download and add this folder to your clients directory
- Add this package: ```meteor add fourseven:scss```
- Add this config file: 

``` /scss.json ```

```json
{
  "enableAutoprefixer": true
}
```


- Discuss sass and framework organization.
- Discuss React use of styles: https://facebook.github.io/react/tips/inline-styles.html
- https://css-tricks.com/the-debate-around-do-we-even-need-css-anymore/
- 

## References
- https://forums.meteor.com/t/meteor-1-3-beta-modules-mobile-and-testing-now-available/18186
- https://www.eventedmind.com/classes/getting-started-with-meteor/meteor-getting-set-up


# OLD Create Note - Simplified
- Discuss: Tracer Bullet model - getting to a complete flow as quickly as possible


Next, we are going to work on adding a note.
Let's review this functionality and the components that are needed.

This version of the UI that we'll use for creating a note will be kept as simple as possible, to allow for moving forward and implementing a complete user flow.  After that is completed, we can go back and make things more user-friendly.

This means that there might be some trade-offs initially.


![Create Note - Simplified Version](images/create-note-simplified.png


Here, the user clicks on new note icon on the homepage.  This triggers the creation of a new note, followed by a redirect to the details view for that note.

## Add a "New Note" Button
The first step in our user flow is that of a user clicking on a "New" button to create a note.

# Add an ActionBtn Component

``` /client/forms/ActionBtn.jsx ```

```js
import React from 'react'

export default class ActionBtn extends React.Component {
	render() {
      return  <button 
        onClick={this.props.handleClick.bind(this)}
        className="icon-btn"
        title={this.props.title}
        alt={this.props.title}>
        <i className="material-icons">{this.props.icon}</i>
       </button>
	}
}

ActionBtn.propTypes = {
  icon: React.PropTypes.string.isRequired,
  title:  React.PropTypes.string,
  handleClick: React.PropTypes.func.isRequired
}
```

# Adding Publications and Subcriptions

## Managing subscriptions
- Remove autopublish
- Requires publishing and subscribine
- requires adding loading component and managing subscriptions

- 

# Add Icons

``` /client/head.html ```

```html
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons"
      rel="stylesheet">
```


# Use Action Btn Component in AppHeader/Homepage

``` /client/layouts/AppHeader.jsx ```

```js
...
import ActionBtn from '../forms/ActionBtn.jsx'

...
        <div className="header-left">
          <ActionBtn icon="add" title="New Note" handleClick={this.props.handleCreateNote} />
        </div>
...
```

```js
...

	handleCreateNote(){
		// create note
		// redirect to note detail view
		console.log("clicked")
	}

	render(){
		const newNoteBtn = {
			icon: "new",
			title: "New Note"
		}
		const cancelNewNoteBtn = {
			icon: "cancel",
			title: "Cancel New Note"
		}
		
		return (
			<div className="app-container">
			  <AppHeader
			   	handleCreateNote={this.handleCreateNote}
			   	
			    headerCenter={this.handleHeaderCenter()}
			  />
			  <main>
			   Homepage Content
			  </main>
      </div>
		) 
	}
...
```

- Add a handler for creating a note in our "controller" component.
- Connect to the component in the AppHeader via props.

- Discuss: Naming and organization of components
- Discuss: propTypes as API (what is an API)

## Add a Notes Collection
Now that, we ready to start creating Notes, we need somewhere to store them.

``` /both/collection/Notes.js ```
```js
import {Mongo} from 'meteor/mongo'

export const Notes = new Mongo.Collection('notes')
```

With these two lines, we've created and made a Notes collection available to our app.
Let's add some more structure, or a schema to our collection.  There are many ways we could do that, here, we'll use the Astronomy package.
- Discuss; why have a schema?
- We want to explicit model our data, to clearly define what it can contain, and what rules relate to that content. 
- Fields: Title, Content, createdAt


``` meteor add jagi:astronomy ```

``` /both/collection/Notes.js ```

```js
import {Mongo} from 'meteor/mongo'
import {Astro} from 'meteor/jagi:astronomy'

export const Notes = new Mongo.Collection('notes')

export const Note = Astro.Class({
	name: 'Note',
	collection: Notes,
	fields: {
    title: {
      type: 'string'
    },
    content: {
      type: 'string'
    },
    createdAt: {
      type: 'date'
    }
  },
  events: {
    beforeInsert() {
      this.createdAt = new Date()
    }
  }
})

```
## Publish Notes

``` /server/publications.js ```

```js
import {Notes} from '../both/collections/Notes'

Meteor.publish('allNotes', function () {
  return Notes.find();
});
```
Discuss: being explicit in your publication names

## Getting Data Using React
- There is a lot of debate and many different techniques: 
- See https://www.discovermeteor.com/blog/data-loading-react/
- https://forums.meteor.com/t/article-data-loading-in-react-four-techniques-compared/18814
- Here, we'll use [TrackerReact](https://github.com/ultimatejs/tracker-react)

``` meteor add ultimatejs:tracker-react  ```



## Access Data using a "Controller" Component


- remove autopublish
- Add Notes Collection
- Publish Notes collection


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



