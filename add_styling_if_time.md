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
