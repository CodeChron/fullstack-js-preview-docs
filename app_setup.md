
# App Setup
_keep these instructions brief and reference codechron blog posts_

_Branch name: 01-setup_ - see Introduction for info on how to get caught using branches.

## Project and App setup
Create your project directory

```mkdir my_notes_app  && cd my_notes_app```

```echo "# My Notes App" >> README.md```

(Optional, initialize a git repo.)

Reference: http://coderchronicles.org/2016/04/08/getting-started-with-meteor-1-3-react-and-flowrouter/#Create_a_project_directory_set_up_version_control_and_install_Meteor


## Create the Meteor app

```meteor create app``

``` cd app```

Start up your Meteor app and view both server and console.
See CodeChron article.

## Move app files into "imports"
- create imports dir
- move files into ```/imports/startup``` 
- import files to the client and server.

You should now see the same welcome info you see by default.  If so, you know your imports are set up properly.

## Add mobile meta tags

```html
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
```


## Install Bootstrap (optional)
This step is completely optional but it will make our app look a little nicer :-)

Make sure you are in your app directory:
``` meteor add twbs:bootstrap ```

After you install this, you should see the default welcome screen with Bootstrap styling applied.
![Default welcome screen with Bootstrap installed](images/bootstrap-dflt.png)




