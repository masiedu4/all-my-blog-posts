## Using React’s useEffect() Hook to Interact with APIs.

APIs are vital for web developers to understand because they are the backbone of every fully-fledged web application, thus we must be comfortable with them.

APIs are the means by which data is retrieved from servers, contact is launched and established with other systems, and, eventually, the means by which we can write to databases and servers.

This article will teach you how to collect data from an API, and more specifically, how to do it while utilizing the useEffect hook to accomplish your goal.


## Pre-requisites

-  It is necessary to have some prior knowledge of JavaScript and React.js in order to properly comprehend this tutorial.

-  Visit the [official docs](https://reactjs.org/docs/create-a-new-react-app.html) to install and set up React.js on your computer. 

Let's get into it.

 ### File Structure 


![File Structure for our project](https://cdn.hashnode.com/res/hashnode/image/upload/v1645982515819/fyVIdaUfs.png)

The App.js file will include all of the code involved in retrieving API data and applying useEffect. This is done for the purpose of simplicity and readability. You have complete control over how yours is structured.

This is the [link to the source code](https://codesandbox.io/s/working-with-api-and-useeffect-hook-ct0enl?file=/src/App.js) of this tutorial. Follow along and let's go.


```
import "./styles.css";

export default function App() {
  return (
    <div className="App">
      <h1> Hello buddy 👋 </h1>
      <h2> Welcome to my API and useEffect() Tutorial!</h2>
    </div>
  );
}

``` 
API keys or other forms of authentication and permission are often needed to get into most APIs, but this is not always the case.

We will make use of a free public API that does not require the use of a key;  ``` https://catfact.ninja/fact ``` 

```
export default function App() {
  const getData = async () => {
    const response = await fetch(`https://catfact.ninja/fact`);
    try {
      console.log(response);
    } catch (error) {
      console.log(error);
    }
  };
  return (
    <div className="App">
      <h1> Hello buddy 👋 </h1>
      <h2> Welcome to my API and useEffect() Tutorial!</h2>
      <button onClick={getData}> Click To Get Data </button>
    </div>
  );
}
```
The code shown above has been broken down into steps.


-  ```const``` declares a constant called ```getData```. ```getData``` is a function that returns a promise.

- The function is declared as an async function, which means it will return a promise.

- The `async` keyword is a way of indicating that the function is asynchronous

-  The promise is in the form of an object that is created using the `fetch` function

- The `await` keyword is used to wait for the fetching to be complete before the try-catch statement is executed.

- The Promise is resolved with the `response` object from the `fetch` function

The `console.log(response)` statements are only executed if the Promise is resolved successfully. Otherwise, the `console.log(error) ` is executed.


In returning the component, we added an `onClick` event listener to the `<button>`.

This means that the only way `getData()` will be called is when there's a click on the button.


![Completed API call image](https://cdn.hashnode.com/res/hashnode/image/upload/v1646598919677/wP7sEGaFZ.png)

Greetings, you've successfully completed an API call and have logged the results in your console!

## The React Hooks Code of Conduct

It's the useEffect hook that tells the system what it should do **when it renders**. With a better understanding of how React.js hooks function, the `useEffect()` hook will have greater meaning for us.

React hooks follow a set of rules that can be summarized as:


### 1. Use hooks only at the very top of your program. 

Keep hooks out of loops, nested functions, and conditions.  Hooks can't function properly without the correct call order. 

We require a consistent call sequence in React. Using loops and conditions to render hooks breaks that!
 
**The useEffect hook can have a conditional inside of it, but not the other way around; this is okay.
The useEffect can be used to run a function.**


### 2. Don't call hooks from regular JavaScript functions
Call hooks from functional components


## Introduction to the useEffect hook

In React.js, the useEffect hook serves as a lifecycle hook that can be used at any time.

When useEffect is invoked, it means that the page has been rendered or that there has been a change in the state of the application.


```
import { useEffect } from "react";

const PageTitle = () => {
 useEffect (() => {
   window.title = "This is Michael's Tutorial";
 } , [])

 return (
 <h1> Hello Friend</h1>
)
}
``` 

The useEffect hook uses a callback function as the **first input argument** to define the effect.

When the **component is mounted**, the effect changes the title of the window to **"This is Michael's Tutorial"**.

The **second parameter** in the useEffect argument list is a dependency array called **`deps`**. 
`Deps` is optional, therefore the effect is only used once during each update if it is provided.
When `deps` is specified, the effect is only activated when the `deps` array is modified.

The useEffect is rendered for the first time when the empty array(deps) is added.
When interacting with APIs, this is critical.

**If we don't add the empty array to our useEffect after a state change, we'll be stuck in an infinite cycle.
APIs with quotas should be used with caution. **

You can create multiple useEffect hooks.

### Using the useEffect hook to make an API request

We used an event listener to retrieve data from the API in our first `fetch API` example.

In this example, we'll use the effect to accomplish our goal.

We want to be able to access the information we need without having to do anything but render our page.


```
import { useEffect } from "react";

export default function App() {
  useEffect(() => {
    getData();
  }, []);

  const getData = async () => {
    const response = await fetch(`https://catfact.ninja/fact`);
    try {
      console.log(response);
    } catch (error) {
      console.log(error);
    }
  };
  return (
    <div className="App">
      <h1> Hello buddy 👋 </h1>
      <h2> Welcome to my API and useEffect() Tutorial!</h2>
      {/* <button onClick={getData}> Click To Get Data </button> */}
    </div>
  );
}

``` 
the useEffect calls the `getData` and the Dependency list array(deps) is left empty because we have nothing to rely on at the moment.

Let us move to the console and see if our status code == 200.


![Completed API call image](https://cdn.hashnode.com/res/hashnode/image/upload/v1646615458047/eCiX9-zdZ.png)


Voila! It worked!

You can inform React that your component needs to perform something after rendering by using this Hook. We'll refer to this as our "effect," and it will be called after the DOM adjustments have been made. 

That's the beauty of the useEffect hook!

## Conclusion

This is the [link to the source code](https://codesandbox.io/s/working-with-api-and-useeffect-hook-ct0enl?file=/src/App.js) of this whole tutorial. 

## Learn More

This blog is dedicated to educating curious individuals who want to learn about technology and improve their skills.

Check out [the blog](https://www.michaelasiedu.com/) to show your support. 
