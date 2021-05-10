# React useRef - Quickstart Guide

**What's a *ref*?**

*Ref* stands for *reference*, and it's an attribute that allows us to store a reference to DOM nodes/React elements.

**What is `useRef`?**

`useRef` is a React Hook that attaches to a DOM node and allows us to access that node's properties. `ref` is a property that is available on React elements.

`useRef` takes an initial value as its optional argument and returns a JavaScript object that has a `.current` property, which will start out being set to the initial value that you give it. The object provides **persistent mutable values** that are available across renders.  

If you think it sounds a little bit like `useState`, you're right! Both store DOM values - but `useRef` is **used when we have a value that we need to store and access *without* triggering a re-render**. Use `useRef` to remember any non-state data that needs to persist between renders.

Because `useRef` does not affect render, that means that it's a side effect and belongs inside the `useEffect` hook.

**How do we use `useRef`?**

- `import { useRef } from 'react'`
- declare a variable and set its value to the function `useRef()`.
- add `ref` as a prop on the element that is being referenced and set its value to the variable name.

This is what `useRef` looks like in action:

```js
import { useRef, useEffect } from 'react';

const Timer = () => {

  const [elapsedSeconds, setElapsedSeconds] = useState(0);
  const timerRef = useRef();

  useEffect(() => {
    timerRef.current = setInterval(() => {
      setElapsedSeconds((secs) => secs + 1);
    }, 1000);
    // return the cleanup component
    return () => {
      clearInterval(timerRef.current);
    };
  }, []);

  return (
    <>
      //...
    </>
  );
};

export default App;
```

Here's what's happening:

- We have a `Timer` component where we store `elapsedSeconds` in state and declare a `timerRef` variable.
- In the `useEffect` hook we set the `current` property of the `timerRef` object to a `setInterval` function that every 1000ms increments the number of seconds by 1. 
- `timerRef` retains a memory of the current timer value, and it doesn't trigger a re-render when that value changes.
- A cleanup function holds `clearInterval`, where we clear the timer.
