# Overview

## App setup
- create project dir with readme and tmp directory and .gitignore
- initialize git
- create Meteor app:
- Note new Meteor create: client and server dirs are created by default, package.json, and .gitignore also
- To run your Meteor app, just type ```meteor``` in your command line.
- Open a browser window and enter the URL: http://localhost:3000 
- You should see the default Meteor app.
- Leave this window open while building the app. Meteor will auto-refresh as you make changes.
- I also recommend having the console open in this window.  ([Viewing the console in Chrome](https://developer.chrome.com/devtools/docs/console).)
- run meteor and set up browser with console open, and terminals for server and shell:

![Sample Screen Setup](images/sample-screen-setup.png)

## Replace some default Meteor files and code

``` rm client/main.css client/main.js ```

Update client/main.html to be as follows:

``` /client/main.html ```


```html
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body><div id="app"></div></body>
```

- Discuss Metor Blaze rendering engine (which we removed)
- Discuss: why no html tags?




## Add React
- Discuss using npm instead of Meteor packages

[NEW SECTION]

### Install React
- Discuss: what is react-dom?

``` npm i react react-dom --save  ```

- Discuss: save option

"By default, NPM simply installs a package under node_modules. When you're trying to install dependencies for your app/module, you would need to first install them, and then add them (along with the appropriate version number) to the dependencies section of your package.json.

The --save option instructs NPM to include the package inside of the dependencies section of your package.json automatically, thus saving you an additional step."
http://stackoverflow.com/questions/19578796/what-is-the-save-option-for-npm-install

## Add a top-level "app" React Component

``` /client/components/app.jsx ```

```js
import React from 'react'

export const App = () => <div>My React App</div>

```
Discuss: 
- modules
- stateless components


## Add a "render target" to your web app

We need to create a location for where to render our (future) React components.

``` /client/index.html ```


```html
<body><div id="app"></div></body>



