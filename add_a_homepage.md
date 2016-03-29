# Add a Homepage (Routing)
While we could start adding content directly to the default app container we've created, this is not a good idea, since we know that this app will have multiple pages (Homepage, Note Details, Login, and more.)

Therefore, let's add an actual homepage.  This means that we're going to want to add routing, even though we only have one page.

## Add Routing

``` meteor add kadira:flow-router ```

Install layout support for react:
``` npm i react-mounter --save ```


Discuss the state of routing and community packages.

After installing this we should see message that we don't have a homepage.

## Add a homepage (root) route

``` /client/routes.jsx ```



