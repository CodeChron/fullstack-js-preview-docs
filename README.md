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

## Add React
- Discuss using npm instead of Meteor packages


### Install React
- Discuss: what is react-dom?

``` npm i react react-dom --save  ```

- Discuss: save option

"By default, NPM simply installs a package under node_modules. When you're trying to install dependencies for your app/module, you would need to first install them, and then add them (along with the appropriate version number) to the dependencies section of your package.json.

The --save option instructs NPM to include the package inside of the dependencies section of your package.json automatically, thus saving you an additional step."
http://stackoverflow.com/questions/19578796/what-is-the-save-option-for-npm-install



