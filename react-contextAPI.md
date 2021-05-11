# React Context API - Quickstart Guide

**What is *context*?**

In React, *context* refers to a global level of state that can be used in your app and throughout components. The React Context API is a way to maintain consistent state by transporting that state to multiple components.

The React Context API isn't a state management tool -- we still need to manage state using hooks like `useState`; it simply allows us to pass and share state as needed.

**Why do we need the Context API?**

Rather than passing state as props down through the component tree (a practice known as *forwarding props* or *prop drilling*), the Context API allows us to declare state in one place and use it wherever it's needed.

**How do I manage context?**

There are three parts to managing context in React:
- `createContext()`
- `.Provider`
- `useContext()`

Here's how to use them:
- Declare a variable and call `createContext()` to create a context object instance.
- Render the `.Provider` (in the same file where you created the instance) to assign a value to the context. Re-render happens in dependent components when the value of the `.Provider` changes.
- Call `useContext()` in any component that is nested in that provider in order to use the context value. The argument passed to the `useContext` hook must be the context object itself.

Here's what that looks like:

```js
// App.js
import { createContext } from "react";

// declare a variable and create a context object instance
export const DeliveryContext = createContext();

const App = () => {
  const [driver, setDriver] = useState("Mario");
  const driverValue = { driver, setDriver };
  return (
    <>
      // render the provider to assign value to the context
      <DeliveryContext.Provider value={driverValue}>
        <Specials />
      </DeliveryContext>
    </>
  )
}

export default App;
```

```js
// Orders.js - not a direct descendant of App.js!
import { useContext } from "react";
import { DeliveryContext } from "./App";

const Orders = () => {
  const { driver, setDriver } = useContext(DeliveryContext);
  return (
    <>
      <div>Your pizza will be delivered by {driver}!</div>
    </>
  )
}

export default Orders;
```

Here's what's happening:
- We are creating a context object instance in the `App.js` component by declaring a variable and calling `createContext()`.
- We are assigning a value to the context using `.Provider`.
- In a separate component -- that is not a direct descendant of `App.js` --  we are calling `useContext` so we can use `DeliveryContext` in that component. 

**How does this all work?**

Think of this like a context pipeline: whatever you put in the pipeline at `DeliveryContext.Provider` comes out the other end at `useContext(DeliveryContext)`. 

**Cool, I'm going to put everything in context now!**

Please no. It's okay to pass data between a few levels of components, even if it's not very pretty. The Context API is designed to be used when your data needs to be accessible by many components at many different nesting levels.
