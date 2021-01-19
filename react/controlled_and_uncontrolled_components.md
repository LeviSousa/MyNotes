# On Controlled and Uncontrolled Components

[Controlled](https://reactjs.org/docs/forms.html#controlled-components) and [Uncontrolled](https://reactjs.org/docs/uncontrolled-components.html) components have their main difference in one thing: who handles the changes of a form's input.

In a Controlled components, React state drives the input's value. The DOM, on the other hand, handles the form changes in Uncontrolled components. The former uses the `value` prop to set the input form element's value, while the latter uses `defaultValue`.

Controlled components allow a finer control of form input changes and to feed other components, elements and handlers with the new values. But they also require more code.

## Some important differences in behavior

A Controlled component will be managing the value itself. That means that, given the example below:

```javascript
<input type='text' value={this.state.value} onChange={this.handleChange} />
```

The `onChange` prop is responsible for updating `value` of `this.state`. If that handler is not present, or does not correctly update `value`, then user interaction may not be reflected in the input.

On the other hand, an Uncontrolled component will accept an initial value from React - passed through `defaultValue` - but will then defer to the DOM the responsibility of handling form input changes.

## Pitfalls

Passing an `undefined` or `null` value as a component's `value` prop will result in an Uncontrolled component - even though what may be wanted is a Controlled component. This may cause the scenario where the input may be changed without consent.

## Getting the current value from an Uncontrolled component

A `ref` can be used to get form values [from the DOM](https://reactjs.org/docs/refs-and-the-dom.html). The value will live under `current.value`.

## Examples

### Controlled component

```javascript
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = { value: '' };
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({ value: event.target.value });
  }
  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input
            type='text'
            value={this.state.value}
            onChange={this.handleChange}
          />
        </label>
        <input type='submit' value='Submit' />
      </form>
    );
  }
}
```

### Uncontrolled component

```javascript
class NameForm extends React.Component {
  constructor(props) {
    super(props);

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input
            defaultValue="Bob"
            type="text"
            ref={this.input} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

### Uncontrolled component with ref

```javascript
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
    this.input = React.createRef();
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.input.current.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type='text' ref={this.input} />{' '}
        </label>
        <input type='submit' value='Submit' />
      </form>
    );
  }
}
```
