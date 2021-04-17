# React Router - Quickstart Guide
**What is React Router?**

React Router is a routing library for React. It provides us with a way to move between the different views (or "pages") of a single-page application without refreshing the page. 

Router shows and hides components based on the criteria that we give it, and changes the URL in the menu bar to give the user the experience of standard navigation in a multi-page site.

**How do we use React Router?**

* Import the ```BrowserRouter``` and ```Route``` components at the top of your ```App``` component.
* Wrap the HTML in your ```App``` component in the ```Router``` component - that means that ```Router``` is wrapping EVERYTHING inside of your return. (Alternatively, you could ```import { BrowserRouter } from "react-router-dom"``` in your ```index.js``` file and wrap ```BrowserRouter``` around the ```<App />``` in that file instead -- whichever you choose, you only need to do it IN ONE SPOT to enable the router magic in your application.)
* Inside the ```Router``` component, we use ```Route``` components to provide paths to display specific content. When the user visits the URL that matches the ```path``` attribute of a ```Route```, the application will render the matched component.
* ```Route``` has an attribute called ```exact``` that checks for an exact match to the path provided. The default behaviour is partial matching, so ```/``` and ```/toppings``` will both render if we don't use this ```exact``` attribute.
``` 
import { BrowserRouter, Route } from "react-router-dom";

const App = () => {
  return (
    <BrowserRouter>
      <div>
        <h1>All About Pizza</h1>
        <Route path="/" exact>
          <Home />
        </Route>
        <Route path="/toppings">
          <Toppings />
        </Route>
      </div>
    </BrowserRouter>
  )
}

export default App; 
```

# Switch
**What is Switch in React Router?**

The ```Switch``` component ensures that only the FIRST matched route child will render. This is useful when you're using nested routes, i.e. cases where you have multiple routes listed but only want to display one at a time.

**Using Switch**

Adding ```Switch``` to the above example would look like this:
``` 
import { BrowserRouter, Route } from "react-router-dom";

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
        </Switch>
      </div>
    </BrowserRouter>
  )
}

export default App; 
```
Notice that ```Switch``` wraps ALL the routes that we will toggle between. It's the same idea as HTML radio buttons: only one nested ```Route``` will be active at a time. 

