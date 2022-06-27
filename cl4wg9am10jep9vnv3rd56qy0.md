## Advanced Solidity: Using a smart contract to send and receive ETH.

There are **two types of accounts** in the Ethereum Virtual Machine that can be used to trigger an action and sign a transaction.

> **Externally Owned Accounts(EOAs)**: These are managed by private keys and can be used to send and receive tokens and other messages.

> **Contract Accounts**: These accounts contain code, and the functions of the code can be called to perform a specific task. Contract accounts are not controlled by private keys, but owners can explicitly include code that allows them to have exceptional control.

This is a technical article that focuses on how to use Solidity to receive and send Ether to and from a contract account.


### How to receive ETH with a smart contract

Contracts, like EOAs, have the ability to receive and hold assets sent from another account.

This functionality is not available in an empty contract. Developers can explicitly configure a contract to receive Ether from other EOAs and contracts in a variety of ways.

#### Let us set up our contract to receive Ether.

We can create a function and mark it as payable, which when called will ensure that all of the code in the body's function is executed and Ether can be received.

NB: Any Solidity function with the modifier `payable` ensures that it can send and receive Ether.

For example, if we're building a smart contract bank and want to allow a specific group of people to deposit money, we can use the payable regular function.

This method of receiving Ether can be used when we want to perform some checks or ensure that certain things are done before and after the Ether is received.


```solidity

// SPDX-License-Identifier: GPL-3.0

pragma solidity ^0.8.0;


contract UsePayable {
      bool public myBool;

      function pay() public payable {
          require(!myBool , "Your bool is set to true");
          // rest of function body here
      }     
}

``` 



Users must manually call the transaction and sign the transaction for it to occur.

### Receiving ETH with receive() and fallback()

#### The receive() function

A contract can only have one receive() function, which cannot take arguments, cannot return anything, and must have mutable `payable` state and `external` visibility (because it will be strictly called from the outside )


```solidity
 receive () external payable {}

``` 


This is the gold standard function that is called on plain Ether transfers and is executed when `calldata` is empty.

If the **receive() function** does not exist but there is a **fallback function**, **the fallback function** will be called whenever Ether is sent to the contract.

#### The fallback() function

A fallback function is syntactically similar to receive() in that it must be externally visible.

A fallback function always receives data, but it must also be marked `payable` in order to receive Ether ().

> If no receive() function is defined, **a payable fallback function** is executed for plain Ether transfers; however, Solidity recommends that developers always define a receive function for plain Ether transfers.


```solidity
  fallback() external payable{}
``` 


> Contracts that receive Ether without specifying a receive or fallback method throw an exception and send back the Ether.


```solidity

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.13;

contract ReceiveEther {
    /*
    Which function is called, fallback() or receive()?

           send Ether
               |
         msg.data is empty?
              / \
            yes  no
            /     \
receive() exists?  fallback()
         /   \
        yes   no
        /      \
    receive()   fallback()
    */

    // Function to receive Ether. msg.data must be empty
    receive() external payable {}

    // Fallback function is called when msg.data is not empty
    fallback() external payable {}

}
``` 


#### Sending ETH from a contract

Solidity, like receiving, provides three different syntactical approaches for sending ETH from a contract to another account.

- transfer
- send
- call

#### 1. transfer()

When using the `transfer()` to send ETH from a contract, there is an allotted gas limit of 2300 and the transaction fails with an error.

If a recipient is a contract and it lacks a receive or a fallback function, the Ether is rejected and an error is thrown.


```solidity
  function sendWithTransfer () public {
          payable(msg.sender).transfer(address(this).balance);
      }
``` 


#### 2. send()

The send() function works similarly to the transfer function and has a gas limit of 2300. However, it returns the transaction's status as a boolean.


```solidity
 function sendWithSend () public {
          bool success = payable(msg.sender).send(address(this).balance);
          require(success , "Send failed");
      }
``` 

#### 3. call()

The call is a low-level function that is the preferred way to send Ether.

It forwards all gas and then returns the transaction status as a boolean and some data.


```solidity
 function sendWithCall () public returns(bytes memory) {
          (bool success , bytes memory data) = payable(msg.sender).call{value:address(this).balance}("");
          require(success , "Call failed");

          return data;
     
      }
``` 


> When a contract attempts to receive Ether via send() or transfer() but does not define a receive function or a payable fallback function, an exception (error) is thrown.


### Learn More

Thank you for taking the time to read this!

I write about JavaScript, Solidity, and Blockchain technology.

More of my articles can be found [here](https://www.michaelasiedu.com/).
