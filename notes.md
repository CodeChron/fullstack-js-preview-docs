# Notes
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


