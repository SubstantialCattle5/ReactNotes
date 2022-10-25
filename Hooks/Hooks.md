# [Hooks](https://reactjs.org/docs/hooks-reference.html)

## Table of Contents

1. Basic Hooks
   1. [useState](#useState)
   2. [useEffect](#useEffect)
   3. [useContext](#useContext)
2. Additional Hooks
   1. useReducer
   2. useCallback
   3. useMemo
   4. useRef
   5. useImperativeHandle
   6. useLayoutEffect
   7. useDebugValue
   8. useDeferredValue
   9. useTransition
   10. useId
3. Library Hooks
   1. useSyncExternalStore
   2. useInsertionEffect

## BasicHooks

### useState

```js
const [state, setState] = useState(initialState);
```

Returns a stateful value, and a function to update it.

During the initial render, the returned state (`state`) is the same as the value passed as the first argument (`initialState`).

The `setState` function is used to update the `state`. It accepts a new state value and enqueues a re-render of the component.

```js
setState(newState);
```

During subsequent re-renders, the first value returned by useState will always be the most recent state after applying updates.

#### Functional updates

```js
function Counter({ initialCount }) {
  const [count, setCount] = useState(initialCount);
  return (
    <>
      Count: {count}
      <button onClick={() => setCount(initialCount)}>Reset</button>
      <button onClick={() => setCount((prevCount) => prevCount - 1)}>-</button>
      <button onClick={() => setCount((prevCount) => prevCount + 1)}>+</button>
    </>
  );
}
```

#### Lazy Inital State

The initialState argument is the state used during the initial render. In subsequent renders, it is disregarded. If the initial state is the result of an expensive computation, you may provide a function instead, which will be executed only on the initial render:

```js
const [state, setState] = useState(() => {
  const initialState = someExpensiveComputation(props);
  return initialState;
});
```

#### Bailing out of a state update

If you update a State Hook to the same value as the current state, React will bail out without rendering the children or firing effects.

Note that React may still need to render that specific component again before bailing out. That shouldn’t be a concern because React won’t unnecessarily go “deeper” into the tree. If you’re doing expensive calculations while rendering, you can optimize them with `useMemo`.

### useEffect

The Effect Hook, useEffect, adds the ability to perform side effects from a function component. It serves the same purpose as componentDidMount, componentDidUpdate, and componentWillUnmount in React classes, but unified into a single API

```js
import React, { useState, useEffect } from "react";
function Example() {
  const [count, setCount] = useState(0);

  // Similar to componentDidMount and componentDidUpdate:
  useEffect(() => {
    // Update the document title using the browser API
    document.title = `You clicked ${count} times`;
  }, []);
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

#### Cleaning up an effect

```js
useEffect(() => {
  const subscription = props.source.subscribe();
  return () => {
    // Clean up the subscription
    subscription.unsubscribe();
  }; , [props.source]
});
```

The clean-up function runs before the component is removed from the UI to prevent memory leaks. Additionally, if a component renders multiple times (as they typically do), the previous effect is cleaned up before executing the next effect.
The subscription will only be recreated when props.source changes.

### useContext

Accepts a context object (the value returned from `React.createContext`) and returns the current context value for that context. The current context value is determined by the `value` prop of the nearest `<MyContext.Provider>`above the calling component in the tree.

When the nearest `<MyContext.Provider>` above the component updates, this Hook will trigger a rerender with the latest context value passed to that MyContext provider. Even if an ancestor uses`React.memo` or `shouldComponentUpdate`, a rerender will still happen starting at the component itself using useContext.

A component calling `useContext` will always re-render when the context value changes. If re-rendering the component is expensive, you can optimize it by using `memoization`.

```js
const themes = {
  light: {
    foreground: "#000000",
    background: "#eeeeee",
  },
  dark: {
    foreground: "#ffffff",
    background: "#222222",
  },
};

const ThemeContext = React.createContext(themes.light);

function App() {
  return (
    <ThemeContext.Provider value={themes.dark}>
      <Toolbar />
    </ThemeContext.Provider>
  );
}

function Toolbar(props) {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

function ThemedButton() {
  const theme = useContext(ThemeContext);
  return (
    <button style={{ background: theme.background, color: theme.foreground }}>
      I am styled by theme context
    </button>
  );
}
```

## Additional Hooks

### useReducer

```js
const [state, dispatch] = useReducer(reducer, initialArg, init);
```

An alternative to `useState`. Accepts a reducer of type `(state, action) => newState`, and returns the current state paired with a dispatch method
