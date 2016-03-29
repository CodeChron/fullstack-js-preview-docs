# Add a New Note Form

Next, let's add a form that will allow us to just type something and use the return key to submit the data to a handler.

``` /client/forms/single_field_submit.jsx ```

```js
import React from 'react'

export class SingleFieldSubmit extends React.Component {

  constructor(props){
    super(props)
    this.state = {
      inputValue: this.props.inputValue,
      autoFocus: this.props.autoFocus
    }
  }

  updateInputValue(e){
    this.setState({inputValue: e.target.value})
  }

  handleSubmit(e) {
    e.preventDefault()
    this.handleContentInput()
  }

  handleOnKeyPress(e) {
    // submit via return key, needed for some devices
    if ( e.which === 13 ) {
      e.preventDefault()
      this.handleContentInput()
    }
  }

  handleContentInput(){
    this.props.handleInput(this.state.inputValue.trim())
  }

  render() {
      return <form className="single-field-submit" onSubmit={this.handleSubmit}>
        <input
          type="text"
          name="newNote"
          placeholder={this.props.placeholder}
          value={this.state.inputValue}
          onChange={this.updateInputValue}
          autoFocus={this.state.autoFocus}
          onKeyPress={this.handleOnKeyPress}
          onBlur={this.handleOnBlur}
        />
         <input type="submit" style={{display:'none'}} />
      </form>
  }
}

SingleFieldSubmit.propTypes = {
  handleInput: React.PropTypes.func.isRequired,
  placeholder: React.PropTypes.string
}

SingleFieldSubmit.defaultProps = {
  inputValue:  ""  ,
  placeholder: "New...",
  autoFocus:  true,
  saveOnBlur: false,
  handleOnBlur: null
}
```
- Discuss: using React.Component
- Discuss need for form tag
- Discuss various handler functions
- Discuss React event model

# Insert New Note Form

Let's now add this component to the main app:

```js
...
import {PageTitle} from './content/page_title'

export const App = () => <div><PageTitle /></div>

```
You should now see your default page title in the browser window.


## Add a single field submit component
- Discuss component naming
- After creating: where will the data go?

NOTE: May be introducing styling and SASS already here.




