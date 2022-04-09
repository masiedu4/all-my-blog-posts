## JavaScript's scopes and closures have been explained!

Understanding JavaScript's Closures is essential to our development process. However, even the most basic of closures can prove difficult to comprehend.

An inner function can access the scope of an outer function through a closure.

Closures define whether a variable can be accessed from another function's scope, as well as whether a function can access the variable from another function's scope.

Don't worry if you don't understand what we're saying; we'll develop some simple code to help.


But first, **why closures**?  

- Closures are used to give objects data privacy.

- Closures let you associate data (the lexical environment) with a function that operates on that data.


Let’s write some basic code using variables and functions that will make sense!

JavaScript variables can belong to the local or global scope.

####  LOCAL VARIABLES.

A function can access all variables defined inside the function. 

```
function localScope() {
  const integer = 4;
  return integer * integer;
} 
``` 

The variable ```integer``` is created within the ```localScope()```

Local Scope occurs when you create a variable inside a function.

From the code above, we can confirm that the visibility and accessibility of the ```integer```  is only allowed within ```localScope()```

```
// integer cannot be assessed from here

function localScope() {
  const integer = 4;
  return integer * integer;
} 

// integer cannot be assessed from here

``` 

#### GLOBAL VARIABLES

A function can also access variables defined outside the function.

```
const integer = 4;

function localScope() {
  return integer * integer;
}  

```
From the example above,```integer``` is a global variable. In order words, global variables belong to the window object and can be assessed by any function, including ```localScope()```

Contrary to a local variable that can only be used inside the function where it is defined. 

Local variables are hidden from other functions and other scripting codes except for their parent function.

#### LEXICAL SCOPING

Let’s take a look at the code below. 

```
function lexical() {
  var carName = 'Tesla'; 
  // carName is a local variable created by init

  function displayCarName() 
 // displayCarName() is the inner function, a closure

 alert(carName); // use variable declared in the parent function
  }
  displayCarName();
}
lexical();

```

```lexical()``` creates a local variable ```carName``` and a function ,```displayCarName()```


```displayCarName()``` is an inner function that is defined inside ```lexical()``` and is available only within the body of the ```lexical()```. 

**NB: ```displayCarName()``` function has no local variables of its own.**


It must be noted, inner functions have access to the variables of outer functions, therefore ```displayCarName()``` can access the variable ```carName``` declared in the parent function, ```lexical()```.

Lexical scope means that in a nested group of functions, the inner functions have access to the variables and other resources of their parent scope.


#### Conclusion 

It's critical to grasp the ideas of scopes and closures because they have numerous applications in the world of software development.

If you're interested in more sophisticated applications, I'll be writing more articles on scopes and closures in the future.

Until we meet again, thanks!