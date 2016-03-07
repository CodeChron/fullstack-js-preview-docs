# App Setup
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


TODO: Roll our own CSS.  Instead of just using TWBS, we're going use a custom CSS framework.
- Download and add this folder to your clients directory
- Add this package: ```meteor add fourseven:scss```
- Discuss sass and framework organization.

## References
- https://forums.meteor.com/t/meteor-1-3-beta-modules-mobile-and-testing-now-available/18186
- https://www.eventedmind.com/classes/getting-started-with-meteor/meteor-getting-set-up
