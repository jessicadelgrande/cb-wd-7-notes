# React useReducer - Quickstart Guide
**What is `useReducer`?**

`useReducer` is a React hook that allows us to create and manage state in situations that are too complex for the `useState` hook.

Just like with the JavaScript `.reducer` array method, the `useReducer` hook takes in two arguments and returns a new value - but in the case of `useReducer`, the values that it takes in are the current `state` and an `action` that can be used to update state, and the value that it returns is an array with the new `state` and a `dispatch` function that can update the state..

**How do I know when I should use `useReducer`?**

If you're managing pieces of state that need to be coordinated, then `useReducer` will keep them all in sync.

From the official React docs:

"*`useReducer` is usually preferable to `useState` when you have complex state logic that involves multiple sub-values or when the next state depends on the previous one.*"

And from Refactoring Guru (https://refactoring.guru/design-patterns/command):

"*A state variable should be responsible for one concern. If the state has a complicated update logic, extract this logic out of the component into a custom hook. Same way, if the state requires multiple operations, use a reducer to incorporate these operations.*"

**How do we use `useReducer`?**

First, let's recall what the `useState` hook looks like:
```js
const [state, setState] = useState(0);
```

`useReducer` is just taking the pattern of the `useState` hook and adding in the reducer as a middleman! 

The basic pattern of `useReducer` is:
```js
const [state, dispatch] = useReducer(reducerFunction, initialState);
```

Here's what all the parts are doing:
- *[state, dispatch]* is the array of two elements that `useReducer` returns. `state` is the current state, and `dispatch` is a *function* that can be used to *dispatch* an action that can trigger an update of state. When we want to update state, we call `dispatch` and it will call the *reducerFunction*. (Note that this uses ES6 array destructuring syntax.)
- *reducerFunction* is the first argument passed to `useReducer`, and it gets triggered automatically when an action is *dispatched*. As a best practice, the function should be declared outside the reducer (and outside the component) and passed in as a variable. As you might guess, this is the function that does the reducing!
- *initialState* is exactly what it sounds like - you're setting the initial state.
- *optionalInit* is an optional third argument (not shown). It's a function that can be run to set the initial state.

Here is a bare-bones example of a reducer. Note that you could call the reducer function anything you want -- pizza, kitten, luxuryCruise -- but it makes sense to just call it reducer:

```js
// the reducer is written above the component
const reducer = (state, action) => {
 return state + action;
}
// the hook is written inside the component
const [sum, dispatch] = useReducer(reducer, 0);
```
You can see that the reducer function has a return, and that the second argument in the hook sets the initial value at 0.

Here's what a basic `useReducer` looks like in the wild:

```js
import React, { useReducer } from "react";

const reducer = (state, action) => {
 return state + action;
}

const App = () => {
  const [sum, dispatch] = useReducer(reducer, 0);
  return (
    <>
      {sum}
      <button onClick={() => dispatch(1)}>Add 1</button>
    </>
  );
};

export default App;
```
And here's a `useReducer` that has a little bit more going on:
```js
const reducer = (state, action) => {
  switch (action) {
    case "add":
      return state + 1;
    case "subtract":
      return state - 1;
    default:
      return state;
  }
};

const App = () => {
  const [count, dispatch] = useReducer(reducer, 0);
  return (
    <>
      <p>{count}</p>
      <button onClick={() => dispatch("add")}>Add 1</button>
      <button onClick={() => dispatch("subtract")}>Subtract 1</button>
    </>
  );
};
```
What's happening here?
1. `state` is created on first render and the initial state is set to 0 in the `useReducer` hook.
2. When either button is clicked, the `dispatch` function is called.
3. The `dispatch` function calls the `reducer` function.
4. Notice that the `reducer` function has a parameter of `action` - so this `action` runs when `dispatch` is called.
5. The `reducer` function checks the `switch` statement for the appropriate `action` and returns it.
6. Behold - the number changes when the buttons are clicked! Try this for yourself in a sandbox: https://codesandbox.io/s/busy-chaplygin-c6eti?file=/src/App.js:531-1073




