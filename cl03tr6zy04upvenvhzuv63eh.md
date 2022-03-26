## Advanced Solidity for Developers Who Are Also Busy and Lazy.

Solidity is a challenging programming language to learn.

On the plus side, it's based on the ECMAScript syntax, so existing web developers will feel right at home.

When it comes to features, Solidity is a curly-bracket language that is statically typed and allows for inheritance, libraries, and sophisticated user-defined types.

### Introduction  

For developers who are already familiar with Solidity but don't have the time or patience to sit through extended tutorial videos, I created this Solidity series.

Using the simplest English possible, I'll explain the following Solidity ideas to you. ↓



**- Structs**

**- View and Pure Functions **

**- Constructor**

**- Conditional Statements** 

**- Abstract Contracts **

**- Interface **

**- Libraries **

**- Function Overloading**




### Structs

Variable types are known at compile-time in Solidity, a statically typed language.

In a nutshell, a value type in Solidity stores a data value in its own dedicated memory region. The term **"value type" ** refers to a type of variable that stores data in the form of values.

Solidity's value types include
 

Value types in Solidity include - 

- Booleans 

- Signed and Unsigned integers 

- Address

- Enums 

- Fixed-size and dynamically-size byte arrays 

**What do Structs have to do with this?**

Keeping a record is what a struct is used for.

Structs in Solidity allow you to store a variety of different sorts of data as a single unit.

An example of this would be a young boy who is applying for a visa. It is important that we add and alter his personal information in order to store it in a struct.

#### Defining a Struct

A struct is defined with the keyword ```struct```, a name for the struct, and an open parenthesis that houses the struct statements.

The format of the statements follows the same syntax as defining a value type.

``` 
struct structName {
 type_a typeAName;
 type_b typeBName;
 type_c typeCName;
}
```
Now, let's define a real struct. We want it to contain the name, age, and marital status of the boy.

```
struct Forms {
   string name;
   uint age;
   bool married;
}
```


Our struct is defined, with their default values!

Let's create a contract that contains a function. The function will take the details of the boy and populate the struct. 

#### Updating a struct

From here I will entreat you to head over to [Remix IDE](https://remix.ethereum.org/),** switch to the JavaScript VM, copy the code, compile and deploy**. 
Time to get our hands dirty! 


With 3 defined types in our struct, our function responsible for updating the struct will contain 3 parameters.

```
  // SPDX-License-Identifier: MIT
pragma solidity ^0.8.10;

contract VisaApplication {

struct Forms {
   string name;
   uint age
   bool married;
}


 function addDetails (string memory _name, unit _age, bool _married) public {

}

}
```

We need to write a simple logic in our function that updates the struct.

```
 function addDetails (string memory _name, unit _age, bool _married) public {
    Forms storage form = Forms(_name,_age , _married);
}
```

The ```storage``` keyword lets us get a reference to the struct in storage. 

** In updating a struct, we start by stating the name of the struct, the keyword(memory, storage, calldata), the name of our new struct tenant, on the left-hand side.**

On the right-hand side of the logic, we will take our function parameters and pass them to the struct in the order with which we defined the struct statements.

To rid ourselves of the order, we can explicitly define the keys and their values.

```
 function addDetails (string memory _name, unit _age, bool _married) public {
    Forms storage form = Forms({name : _name , married : _married , age  : _age});
}
```

Let us get our hands dirtier by creating an array of structs and pushing our new struct data to the array.


 ```
  // SPDX-License-Identifier: MIT
pragma solidity ^0.8.10;

contract VisaApplication {

struct Forms {
   string name;
   uint age
   bool married;
}

// new array of structs which is named "allForms"
// allForms will be called when we want details from the array.
Forms [] public allForms;


 function addDetails (string memory _name, unit _age, bool _married) public {

}

}
```

Array methods in Solidity are very similar to JavaScript. Our method to add data to the last member of the array is ``` push()```.


```
 function addDetails (string memory _name, unit _age, bool _married) public {
        Forms storage form = Forms(_name,_age , _married);
        allForms.push(form);
}
```

Head over to Remix and make sure your code is compiled successfully. 

Deploy and let's test it out!


![Screenshot 2022-02-26 00.27.19.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645835256252/VJcbQ-Weo.png)

Type in ```0``` to retrieve the first member of ```allForms``` and see if it all worked out.



![Screenshot 2022-02-26 00.29.09.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645835364457/yISO2Mubl.png)


### View and Pure Functions

The use of the **View** and **Pure** keyword in Solidity is also known as **State Mutability of Functions.**

#### View Functions

Functions can be declared ```view``` in which case they promise not to modify the state. In other words, a view function is only viewing data from the state but not modifying it.

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.10;

contract StateMutability {

 uint age = 9;

 function whatAge () public view returns(uint) {
    return age + 10;
 }

}
```
**The following statements are considered "modifying" the state.**

- creating other contracts

- writing to state variables

- using ```selfdestruct()```

- emitting events 

- calling any function not marked view or pure



#### Pure Functions

Pure functions do not read or modify. To elaborate, you are not even accessing any data in the contract.

Pure functions do not read from the state of the contract - their value is dependent on the function parameters. 



```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.10;

contract StateMutability {

 function whatAge (uint x , uint y) public pure returns(uint) {
   return x + y ;
 }

}

``` 


**The following statements are considered "reading" the state.**

- reading from state variables

- accessing any member of ```block```, ```tx```, ```msg``` (except ```msg.data``` and ```msg.sig```)

- accessing ```address(this).balance``` or ```<address>.balance```


NB: Pure function can use **revert()** and **require()** since they are not considered **"state modification"**

One good thing is, the Remix compiler automatically points us to what we need to mark our functions with. Don't stress on them. Remix IDE is here to help.

### Constructor

It's a function that is called when the contract is deployed, which can also accept arguments.

The constructor is used in the same way as regular functions, but just once, during the deployment of the contract.

It is not necessary to include a constructor in your code. Overloading isn't possible because contracts can only include one constructor.

Setting a contract's owner to the account that deployed the contract is the most common use of the constructor.


```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.10;

contract SetOwner {
   address owner;

   constructor() {
      owner = msg.sender;
   }
}

``` 


### Conditional Statements

In Solidity, you can use conditional statements if you wish to validate a scenario before specific actions are taken.

For example, an if-else statement is a nice place to start if you want to add two numbers, but you want to make sure that one of them is greater than 1.

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.10;

contract Conditionals {

 function evenFirst (uint x , uint y) public pure returns(uint) {
    if ( x > 1 ) {
       return x * y;
    } else if(x < y){
       return (x + y) * 2;
    } else {
       return x;
    } 
}

}
```

The use of the if-else statement in Solidity is much like how it is implemented in JavaScript.

### Abstract Contracts 

Contracts are marked ```abstract``` when **at least one** of the functions are not implemented.

Also, if a contract inherits from an abstract contract and does not implement all non-implemented functions by overriding, it needs to be marked ```abstract``` too.

 

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.10;

abstract contract Abstract1 {
    function absFuncOne() public virtual returns (bytes32);
}

abstract contract Abstract2 is Abstract1 {
    function absFuncTwo() public  pure returns (bytes32) {
    return "2 abstract contracts"; 
  }
}

``` 


### Interfaces 

Interfaces allow us to communicate with other contracts on the blockchain that we do not own.

The `interface` keyword and a `random name` are used to declare the interface.


```
interface someRandomContract {
  // the function we want to call will be here
}
``` 

Let's consider an example where we want to call another a function from a contract on the blockchain.

 ```
  interface someRandomContract {
    // Only the interested functions will be in the interface
    function balanceOf(address account) external view returns (uint256);
}

```

We can initialize this external contract in our own contract with the ``` constructor``` function and create another function to call the ```balanceOf``` function from the interface.


```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.10;

interface someRandomContract {
   // Only the interested functions will be in the interface
    function balanceOf(address account) external view returns (uint256);
}

contract MyContract {
    someRandomContract externalContract;
    
    constructor(address _externalContract) {
        // Initialize a someRandomContract contract instance
        // We will expliciity inlcude the external contract address as a constructor parameter 
        externalContract = someRandomContract(_externalContract);
    }
    
    function getBalance() public view returns(uint){
       // checking the balance of anyone that calls(msg.sender) this function
       // calling the balanceOf func from thee interface
        return externalContract.balanceOf(msg.sender);
    }
}
``` 

#### Some takeaways on working with interfaces

- Interfaces do not need to necessarily contain all the functions that exist in the external contract

- Only needed contracts should be included 

- Functions of an interface can be of type ``` external```

- Interfaces cannot have state variables and constructors, but they can have enum, structs which can be accessed using the interface name dot notation. 


### Libraries

Libraries are similar to contracts. Libraries are used as support functions to a contract.

They are defined with the ```library``` keyword and a random name.

``` 
library AddFunc {
 
} 
```

#### Using a library in a contract ↓


```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.10;

library AddNumber {
   
    function add(uint x, uint y) internal pure returns (uint) {
        uint z = x + y;
        return z;
    }
}

contract UseLibrary {
    function addition(uint x, uint y) public pure returns (uint) {
        return AddNumber.add(x, y);
    }
}
``` 
#### Some takeaways on working with libraries

- A library cannot use the fallback function, payable keyword, or a non-constant state variable

- A library can modify storage variables

- Libraries do not have an Event log but events can be emitted by a library.






### Bonus: Function Overloading

Function overloading is when a contract can have multiple functions of the same name but with different parameter types. 


```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.10;

contract Test {
   function addNumbers(uint a, uint b) public pure returns(uint){      
      return a + b;
   }
   function addNumbers(uint a, uint b, uint c) public pure returns(uint){      
      return a + b + c;
   }
}
``` 


### Conclusion

Every industry-standard smart contract has the application of these Solidity concepts. 

Feel free to reach out to me on [Twitter](https://twitter.com/asiedu_dev) and let us have a chat!

I'm glad you enjoyed this. See you soon.