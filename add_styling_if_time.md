# Add Styling (if time)

We'll add some basic styling.
Why create roll our own styles rather than use something like Bootstrap?
Why did we wait to add styling?

## Install the Sass package
Why use a css pre-processor?
What are some alternatives to Sass?

``` meteor add fourseven:scss ```

## Add support for auto-prefixing

Add this to the root directory of the app:

``` /scss.json ```

```json
{
  "enableAutoprefixer": true
}
```
What is auto-prefixing?

## Add and import a main stylesheet

Create a "main" scss file at: 
```/imports/stylesheets/main.scss ```

Add the following comment blocks.  This is the general structure of the our stylesheets.

```js
// CORE
// Here we'll add base files that are not specific to any design and which support other stylesheets


// LAYOUTS
// We'll likely have multiple layouts, such as the overall app layout, a centered layout for a login view and more.

//COMPONENTS
// styles generally corresponding to our UI components

//THEME
// color palette, typography, etc.

```

Then import it on startup:

``` /imports/startup/client/index.js ```

```js
import '../../stylesheets/main'
...
```
Note that it is the first item to be imported.

What's the purpose of the main.scss file?


## Add Normalize
What is normalize?

```/imports/stylesheets/main.scss ```

Why are we adding it is as a local file and not, for example via CDN?
