# React Basics

Collection of Basic topics in React.

## Table of Contents

1. [Components](#components)
2. State
3. Events
4. Rendering List
5. Conditional Content
6. Debugging React Apps
7. Practise Project
8. Fragments
9. Portals
10. Using 'refs'

## [Components](https://reactjs.org/docs/components-and-props.html)

Components let you split the UI into independent, reusable pieces, and think about each piece in isolation.

### Function and Class Components

JavaScript function:

```js
// method 1
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
// method 2
const Welcome = (props) => {
  return <h1>Hello , {props.name}</h1>;
};
```

ES6 class to define a component:

```js
// not preferred
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

### Project Usage

- [SpendorTracker](../Projects/P1_BudgetApp/src/components/Expenses/Expenses.js)
