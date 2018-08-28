## Considered topics for presentation

- note that it's React16
- pass by value
- pass by reference
  - when to append () to a function being passed
  - arrow syntax to pass in args in the midst of passing so that it won't be executed
- two-way binding
  - (use this when you're inside a method) https://www.safaribooksonline.com/videos/react-16/9781789132229/9781789132229-video8_11
  - this inside a class refers to the class at all times
    - stateless components use `props.<props_name>`, stateful use `this.props.<props_name>`
- component vs containers (including propTypes)
  - https://www.safaribooksonline.com/videos/react-16/9781789132229/9781789132229-video8_9
- new way of declaring state
  - https://www.safaribooksonline.com/videos/react-16/9781789132229/9781789132229-video8_11
  - https://www.safaribooksonline.com/videos/react-16/9781789132229/9781789132229-video8_12
- state should be updated in immutable way
  - https://www.safaribooksonline.com/videos/react-16/9781789132229/9781789132229-video8_15
  - spread operator (1:40)
- when to use wrapping div vs hoc
- when to use arrow functions vs normal functions (see `BurgerBuilder.js`)
  - https://www.safaribooksonline.com/videos/react-16/9781789132229/9781789132229-video8_20 (5:50)
- how React handles image
  - https://www.safaribooksonline.com/videos/react-16/9781789132229/9781789132229-video8_26 (~2:00)
- boolean props can be defined as just the props name
- SideDrawer.css is interesting
  - https://www.safaribooksonline.com/videos/react-16/9781789132229/9781789132229-video8_31 (7.20)
- set a new state based on a previous state
  - toggleHandler `this.setState({ showSideDrawer: !this.state.showSideDrawer})` is unstable
    - https://www.safaribooksonline.com/videos/react-16/9781789132229/9781789132229-video8_32 (4.50)
- performance: re-render vs life cycle methods (can only be done in class)

  - https://www.safaribooksonline.com/videos/react-16/9781789132229/9781789132229-video8_36 (from the start)
  - wrapping element controls the update of the wrapped element
  - to use life cycle hooks, preferrable to use class instead of PureComponent, because the latter will perform more checks than needed like other props you're not really interested in

each node has two things in them in addition to their information to display the view: properties and state. properties are immutable data that are passed to it by its parent while state is mutable data that will change over time. a common pattern is a state in one parent will become properties in its children elements.

setState will update the states and trigger a re-render

## React 16 Complete Guide

by Max S

### Setup

`package.json` lists all the dependencies (like Gemfile)
`rc` means release candidate
`react-scripts` package offering all the build workflow, the development server, the next gen js feature for support and all the things we'll be using for the project

`scripts` are scripts that can be run with `npm run <script_name>`

- `start` starts the server, compiles our code, optimizes the code
- `build` when you're ready for deploying your app which optimises it even more, not launch a development server but instead get your optimised code stored in a folder. because now you won't see your compiled code anywhere, it all happens in memory

`node-modules` dir holds all the dependencies and sub-dependencies of our project

`public` dir is the root folder that gets served by the server in the end

- holds the html file that's the SPA
- you don't need to add more html, all you need is a workflow

script files are in the `source` folder

`manifest.json` because create-react-app gives us a progressive web app out of the box, where we can define some metadata out of our application

### Details

Component

- need to still import React because the component has to be transformed to a React.createElement
- is a function returning some jsx
- if a function, you don't need to import { Component }, just `import React from 'react'`

Children

- refers to any elements (including plain text) between opening and closing tags

Property

- a class has properties (which can be a variable of a class)

State

- is a property that can be changed which will trigger react to re-render the DOM
- only works in components which `extends Component`
- `this` inside a class (eg, `this.state`) refers to the class itself

Event Handling

- `*handler()` is a function name to indicate it's not a method you're actively calling, but you're assigning as an event handler
- eg, `switchEventHandler = () => {}` is a property which holds a function which can be executed then in onClick, `this.switchEventHandler` without () because we only want to pass a reference (to the property which holds the function), we don't want to execute it immediately once react renders it to the DOM

Functional (STATELESS) Component
Class (STATEFUL) Component aka Container

Passing method references between components

- can pass methods also as props so you can call a method which might change the state in another component which doesn't/shouldn't have direct access to the state
- eg, you can pass down `clickHandler`s which allow you to change data in the parent component

<input>
  - react/js passes the event object, like <button>
  - `event.target.value` where target is the input in which we type, value is the value the user entered

Two-way binding (eg for <input>)

1. when we change it, we want to propagate that change so that we can update the state
2. we also want to see the current state right from the start

render()

- everything inside, not just `return` gets executed during render/re-render

`click = {() => this.deletePersonHandler(index)}` or
`click = {this.deletePersonHandler.bind(this, index)}`

`#splice(index, numberOfElements)`

```
const persons = this.state.persons
persons.splice(personIndex, 1)
this.setState({persons: persons})
```

persons was a constant then spliced but arrays & objects are referenced types so it's only holding a pointer, the element it was pointing to can be changed

Spread operator

- `const persons = this.state.persons.slice()`
  - #slice without args, simply copies the persons array or better yet:
- `const persons = [...this.state.persons]`
  - spread operator simply makes a new array out of the array you're spreading

Pseudoselector

- in CSS, means a selector based on another selector as indicated by the :

`npm install --save`

- also saves an entry in `package.json` so we also fix the version number and easily share our project

CSS Loader

- transforms CSS code in the css file to an object we can use in the js file

Higher-order Component

- any component that wraps other component, eg, with the goal of handling any errors

Key

- always has to be in the outer element in a map method, because that's the element we actually replicate

React16

- `componentWillUpdate`, `componentWillMount`, `componentWillReceiveProps` are discouraged because of frequent incorrect use. eg, you could call `setState` there and possibly defer the first render
- offers new ones
  - `getDerivedStateFromProps(nextProps, prevState)` and `getSnapshotBeforeUpdate()`

CSS Modules

```css
modules: true,
localIdentName: '[name]__[local]__[hash:base64:5]',
```

`localIdentName` generates unique CSS class names and assign automatically once imported to the object from the css file; takes the original name then the local name of the component and a randomly generated hash with base64

index.css

- used for global styling

```js
// use {} to run some logic before returning the jsx
const burgerIngredient = () = {

}
```

`npm install --save`

- also saves an entry in package.json

`font-size: 1.2rem;`

- rem depends on the font size the user selected

```js
constructor (props) {
  super (props)
  this.state = state  // this because you're inside a method
}
```

```js
.reduce((prev, current) => {
  return prev.concat(current) // will flatten the input array
}, [])
```

- reduce transforms an array; takes a function as input and this function receives 2 arguments - passed in automatically by JS - the previous value and the current value
- reduce does not only accepts the callback preceding it (eg, map statement), it also accepts an initial value, here an empty array
