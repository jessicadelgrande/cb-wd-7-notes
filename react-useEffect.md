# React useEffect - Quickstart Guide

**What is an *effect*/a *side effect*?**

The terms *side effect* and *effect* are used interchangeably and mean the same thing in React: they refer to operations that don't affect the UI or output value. If the operation you are performing is managing any state change *other than* the final return value, then it's a side effect!

The function of a React component is to handle render and manipulate the UI. Because side effects don't impact the render phase, they don't belong in the main body of a component.

**What is `useEffect`?**

`useEffect` is a React Hook that allows you to run side effects independent of rendering.

If you have parts of your code that are not directly related to the UI or tasks that are asynchronous and execute outside of the normal control flow, you should put them inside the `useEffect` hook. This allows them to operate *outside* of the render cycle and to function behind the scenes without interfering with the UI.

`useEffect` accepts two arguments: 
- a (required) callback -- the *effect* -- that will be executed after component evaluation if specified dependencies change;
- the (optional) dependencies that are being checked by that function.

The default of `useEffect` is to run after every completed render, but you can choose to run your effects only when specific values have changed.

Examples of calculations that are independent of render and should live inside a `useEffect` hook:
- using timers;
- network requests (like `fetch`);
- reading from local storage;
- registering and deregistering event listeners;
- manually updating the DOM.

**How do we use `useEffect`?**

- `import { useEffect } from 'react'`
- Side effect logic goes inside the callback function.
- Dependencies control *when* you want the side effect to run. They are passed in as an array.

This is the basic structure of the `useEffect` hook:

`useEffect(() => { logic }, [dependencies]);`

Let's look at how `useEffect` works. In this example, we're geting user information from a database after a `loggedIn` state updates to `true`, and then we print that info to the page:
```
import { useState, useEffect } from 'react';

function App() {

  const [loggedIn, setLoggedIn] = useState(false);
  const [userName, setUserName] = useState("");

  useEffect( () => {
    if (loggedIn === true) {
      // [ retrieving user info from an imaginary database here ]
      // [ we set the returned user info in state ]
      setUserName("Lisa Simpson");
    } else {
      setUserName("");
    }
  }, [loggedIn]);

  return (
    <div>
      <h1>Hello</h1>
      <button onClick={ () => setLoggedIn(!loggedIn) } >Log in / out</button>

      {
        loggedIn === true
          ? <p>Hello, {userName}</p>
          : <p>Please log in</p>
      }
    </div>
  )
};

export default App;
```
Let's break it down:

- We have an `if` statement that checks an imaginary database to see if the user is `loggedIn`. If they are, we update the state of `userName`. (In the return we have logic to display their name on the screen if `loggedIn === true`.)
- When the button (in the return) is clicked, `loggedIn` is updated in state using the `setLoggedIn` function.
- `useEffect` runs every time the `loggedIn` state changes, because we've passed `loggedIn` as a dependency.
- `useEffect` does *not* run when the `userName` state changes, because we haven't put it in the dependency array.

**`useEffect` dependencies**

Dependencies are how we control when `useEffect` runs.

- If you want `useEffect` to run on every render, omit dependencies.
- If you want it to run only once after initial render, provide an empty array.
- If you want it to run after a specific value changes, pass that as a dependency.

What gets included in `useEffect` dependencies? Anything used in the `useEffect` function IF those things could change when a component is re-rendered. 
- If you are using `props` or `state` values, you must declare these as dependencies; when these values change, `useEffect` will run. (In the above example, it's okay to omit the `setUserName` function from the dependencies because it's not a state value -- it's a function that *updates* the state value, so it will never be out of sync with state.)

You don't need to add as dependencies:
- state updating functions;
- built-in APIs or functions;
- variables or functions that are defined outside of a component function (like a helper function that is in a separate file).

**Cleaning up an effect**

Some side effects -- like timers or subscriptions (connections to a persistent data source) -- require clean-up, because we don't want them to be floating around after the component is removed from the DOM.

To clean up we just return a function inside `useEffect` and it will clean up; these functions are appropriately referred to as `cleanup functions`. These cleanup functions run *after* the next render, but *before* the next `useEffect`.
