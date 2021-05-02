# React useState - Quickstart Guide
**What is *state*?**

State stores the current status of components and allows us to track changes. State is created and updated in React by the `useState` function, and is fully controlled by the component.

**What is `useState`?**

`useState` is a React Hook, which is another way of saying that it's a React function that allows us to *hook into* React features and easily manipulate a functional component.

`useState` receives an initial state as an argument, and returns an array of 2 items:
* a variable that represents current state;
* a function that we can use to update that specific piece of state by providing a new state.

Unlike other variables that no longer exist when the function exits, state variables are preserved by React.

`useState` triggers a re-render of the component -- in React, updating a variable or using a click handler doesn't do this. If you need to re-render anything in your component you will want to update state!

**How do we use `useState`?**

* `import { useState } from 'react'`
* To *create a state variable*, use array destructuring to assign variable names to the state's array elements, like this:
`const [pizza, setPizza] = useState(currentPizza)`
Remember that the first array item in the return is current state, and the second array item is a function which will be used to update/set the state -- this is why we typically name these variables with a pattern of `value` and `setValue`.
* To *set the initial state* of a component, pass the initial value that you want into your `useState` function as an argument. In the above example, we are setting the initial state of `pizza` to equal `currentPizza`. This is the same as saying `const pizza = currentPizza`. (If you have `const pizza = currentPizza` elsewhere you can remove it.)
* To *update the state* of a component, call the function of the `useState` variable and pass it the updated state. 
* Because `useState` is managing the state of individual components, your `useState` variable declaration needs to live inside of the component that it affects.

**DO NOT EVER directly update the value of `useState`!**

**DO**: use the *function form* of `useState` when updating state. If you wanted to update the state of `pizza` to be a pizza with a variable name of `deluxe`, you would call the `setPizza` function and pass it the new pizza name, like this:

`setPizza(deluxe)`

**DO NOT**: update the initial state of `pizza` by reassigning it, for example `pizza = deluxe`

