# App Setup
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