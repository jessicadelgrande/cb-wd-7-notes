# React useParams - Quickstart Guide
**What is `useParams`?**

`useParams` is a React Router Hook that allows you to access dynamic parameters in the URL.

`useParams` returns an object of key:value pairs of URL parameters. The `key` is the name you've assigned in the URL; the `value` is what is being passed in.

**How do we use `useParams`?**

* Import `useParams` from `react-router-dom`.
* Replace the part of the `path` that you would like to access as a parameter with a colon and an identifier of your choice. If you had a path that showed you the `specials` and the `specials` changed every day, your path would look something like this: `/specials/:currentDay`, where `currentDay` is dynamic based on the day.
* Declare that same variable name in the component where you will be managing the params, using the syntax `let { currentDay } = useParams();`.
* You can access multiple params in one url, e.g. `/specials/:currentDay/:birthdaySpecial`, and you can use destructuring syntax to declare them, like this: `let { currentDay, birthdaySpecial } = useParams();`. 
* Parameters are mandatory by default. If you would like your parameter to be optional, simply add a `?` after it in the `path`, like this: `/specials/:currentDay/:birthdaySpecial?`. (Remember that you'll have to handle this condition in your component!)
```js 
import { BrowserRouter, Route, Switch, useParams } from "react-router-dom";

const App = () => {
  return (
    <BrowserRouter>
      <div>
        <h1>All About Pizza</h1>
        <Switch>
          <Route path="/" exact>
            <Home />
          </Route>
          <Route path="/toppings">
            <Toppings />
          </Route>
          <Route path="/specials/:currentDay">
            <Specials />
          </Route>
        </Switch>
      </div>
    </BrowserRouter>
  )
}

export default App; 
```
