# Create Notes

## Add Notes Collection

```js
import { Mongo } from 'meteor/mongo'
import { Meteor } from 'meteor/meteor'

export const Notes = new Mongo.Collection('notes')
```


## Add support for handling Meteor Data in React

- Add the Meteor package: ```meteor add meteor-react-data```
- Add the npm package: ```npm i react-addons-pure-render-mixin --save```


## Section

```js
code
```
- Reference the desired create note flow, with a redirect after create and a note details view. Also requires private notes which means authentications. It would also require adding routing. This is too advanced and too much to try to do all at once.
- Discus a the Tracer Bullet concept - do the bare minimum work needed to complete a flow.
- Discuss breaking larger problems into smaller ones.
- Let's therefore first implement a very basic Notes CRUD, then add the more advanced stuff.
- As before, we want to think visually when using React.  Here is our simplified app component hierarchy:




Here, we have a static app header and a component that submits that was input to a handler.


## Section

```js
code
```
