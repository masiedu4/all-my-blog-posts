## A Step-by-Step Guide to Understanding React Router for Complete Beginners

## Introduction

**Routing** is used in software development to navigate between paths and pages.

Routing is the process of choosing a path for data to go from source to destination.

React Router is a client-server routing library.

React Router can be used on the web, the server (via node.js), and React Native.

This post will teach you all you need to know about React Router v6 to build dynamic web apps.

It is assumed that you know JavaScript and React.

Let's start now.

## Installation and Configuration.

This tutorial will be on using ```create-react-app ``` to implement the latest version of React Router(v6).

Follow the link  [here](https://reactjs.org/docs/create-a-new-react-app.html#create-react-app)  to set up a new ``` create-react-app```  project.


**Installing React-Router  **

Before we start using React Router,  we need to install it as a dependency in our project.

 

```
// installing via npm 
npm install react-router-dom@6

// installing via yarn 
yarn add react-router-dom@6

//installing via pnpm
pnpm add react-router-dom@6
``` 



Once the project is set up and React Router is installed, open the ```src/index.js```  file and import ``` BrowserRouter```  from  ```react-router-dom```  on the top of your file and wrap your app in a ```<BrowserRouter>```


```
import ReactDOM from "react-dom";
import { BrowserRouter } from "react-router-dom";
import App from "./App";

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById("root")
);

``` 

With this simple step completed, we can use the React Router anywhere in our project! 


## Creating routes in our app


`ROUTES`: The `Routes` component was missing in previous versions.

With v6, it determines where routes will be placed in your router system.

This component is imported from react-router-dom and contains all of our routes.



`ROUTE`: The <Route /> component is used to define a route, its path, and the destination element/component of the path. 


![Screenshot 2021-12-10 13.22.43.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1639142610114/r3c8wE63c.png)

Within our ```src``` folder, there is a sub-folder called ```pages``` which contains 4 ```.js```  files and these 4 files will be the pages we will use for this tutorial.


Let's write our first route in the ```App.js```. 

```
// don't forget to import the pages you want to route to  as well

import {  Routes, Route  } from "react-router-dom"

import Home from "./pages/Profile"
import Contact from "./pages/Contact"
import About from "./pages/About"

export default function App() {
  return (
    <>
      <Routes>

        <Route path="/home" element={<Profile />} />
        <Route path="/contact" element={<Contact />} />
        <Route path="/about" element={<About />} />

      </Routes>
    <>
  )
}


``` 

``` <Route /> ``` take two properties ie ``` path```, which contains the route name as value, and the ```element```, which contains the destination component as value. 

 On local hosting, when we visit ```localhost:3000/profile```, it will be directed to the ```<Profile/>``` component. The same happens for all our other routes. 



> Now we can write routes, what happens when a user visits a route we have not defined in our code?

 
We can create a custom component(page) where we can redirect all invalid route requests to.
```
import {  Routes, Route  } from "react-router-dom"

import Home from "./pages/Profile"
import Contact from "./pages/Contact"
import About from "./pages/About"
import Error from "./pages/Error"

export default function App() {
  return (
    <>
      <Routes>

        <Route path="/home" element={<Profile />} />
        <Route path="/contact" element={<Contact />} />
        <Route path="/about" element={<About />} />
        <Route path="*" element={<Error />} />

      </Routes>
    <>
  )
}


``` 

 NB: 
> 1. "Error" routings always have to be the last route at the bottom before the closing tag ```</Routes>```.**

 > 2. The ``` path``` value is given as an ```*``` with the ``` element``` value set to the corresponding error page.  ** 

> 3. The user will be redirected to the Error page whenever they visit a wrong route.**

** Refer to code above.**



``` LINK ```:  We can successfully create a route but how can we link JSX elements to pages? 

Let's say we have an item on the Navigation bar and upon click, we want the user to be directed to its corresponding page, how do we implement that? 

That's where the ```<Link>``` from our ```react-router-dom``` comes in. 


```
import {  Link } from "react-router-dom";


export default function Navbar() {
  return (
     
    <nav>
        <Link to="/profile"> Profile </Link>
        <Link to="/about"> About </Link>
        <Link to="/contact"> Contact </Link>
      </nav>
     
  );
}

``` 

** NB: ```<Link>``` takes ```to``` instead of ```path```.**



## Handling Redirects in React Router 

Handling redirects is a key element of the "routing" process. When you want to keep an existing link but redirect all of the traffic that comes from that link to a different URL, you use redirects.

We'll start with the most straightforward method of dealing with redirects (client-side) using the React router.

We will use the component `<Navigate/>` to handle redirection.



```
import { Routes, Route, Navigate } from "react-router-dom";

export default  function App() {
  return (
    <Routes>
      <Route path="/profile" element={<Home />} />
      <Route path="/products" element={<Navigate replace to="/home" />} />
    </Routes>
  );
}
``` 

From the code above, we used the ```<Navigate replace to = "/home"/>``` to handle a redirect from when a user visits ```products``` page. 

In this case, all routing requests to ```/products``` will be redirected to ```/home```



### The useParams() Hook 

 React Router comes with a ```useParams()``` hook that allows us to access the current URL params wherever you need them, especially when making API requests to a server.

```
import { Routes, Route, useParams } from "react-router-dom";

function App() {
  let {id} = useParams();
  return (
    <Routes>
      <Route path="users/:id" element={<UserProfile />} />
    </Routes>
  );
}
  
```


## Conclusion 

React Router is really straightforward to utilize in our applications, and [the documentation](https://reactrouter.com/docs/en/v6) provides an in-depth explanation of the framework.

I have a strong belief that you will be able to easily construct and use React Router in your projects after reading this article.

## Learn More

This blog is dedicated to educating curious individuals who want to learn about technology and improve their skills.

Check out [the blog](https://www.michaelasiedu.com/) to show your support. Thank you very much.

