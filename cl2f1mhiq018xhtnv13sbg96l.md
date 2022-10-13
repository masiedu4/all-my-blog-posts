# 7 Gas Optimization Techniques to Reduce the Cost of Your Smart Contracts.

Blockchain technology may be the best and most significant thing to happen to humanity since the internet's inception.

This wave is being led by a group of individuals whose responsibility is to **build scalable** blockchain applications that have the potential to change every aspect of our lives.

The finance and software industries are gradually catching up with blockchain technology. Healthcare, governments, and other industries are expected to follow suit.

However, it is not as gleaming and golden as it appears. Working with the blockchain is a great epiphany experience, but decentralized applications are expensive to deploy, manage, and even interact with.


This stumbling block makes it difficult for developers to create scalable applications.

On the bright side, blockchain technology adheres to the "Garbage In, Garbage Out" tenet.

The net cost of your application is determined by what you write in your code.

In this regard, when developing smart contracts, experts can use a variety of loopholes and techniques to reduce gas costs for their team and customers.

A better smart contract developer is one who can optimize their code to use less gas and money.

Solidity is the most popular blockchain programming language, and it is undeniably driving the transition from centralized to decentralized applications, and it has advantages.

> It is always preferable to take advantage of its benefits and workaround its limitations in order to deploy a gas-optimized application to the chain.


## Prerequisites

> To understand the concepts presented in this article, only a basic understanding of the EVM and Solidity is required.

## What exactly is gas, and why is it so important?

On the Ethereum blockchain, **"gas" ** refers to the data required to complete a transaction on the network, and **"gas fees"** are processed through "gas." The price is determined by **supply and demand for the network's computational power**, which is required to process smart contracts and other transactions.

Contract deployment, function calls, setting values, changing values, sending NFTs, withdrawing money, and transferring money are all gas-efficient processes that occur during the DApp and smart contract life cycle.


In the following paragraphs, we'll get technical and look at the techniques and metrics we can use in our Solidity code to ensure that these processes are less expensive for the team and, more importantly, for their users.

## Gas Optimization Techniques

### 1. Minimize on-chain data

One common misconception about building blockchain apps is that every detail should be on the chain.

The blockchain should be viewed as a platform that aims to improve upon the shortcomings of the current centralized model (Web2) rather than as a complete replacement.

Blockchain will only take over, or at the very least "solve problems," if it is used in conjunction with centralized systems.

As a result, developers and project managers must be familiar with their products and what they entail. This is a vital step in determining the overall software architecture of the product.

Some problems are better solved with a centralized system, while others are better solved with a decentralized one.

More data with your code means more space and, consequently, more gas.

When it comes to building on the blockchain, the first rule is to keep the important stuff on-chain and the rest off-chain.

Create a mutually beneficial relationship between the use of decentralized and centralized systems.

Simply doing so will save you a lot of money.


### 2. Use Deployed Libraries

When it comes to developing a smart contract application, less is more.

Contracts and libraries are similar. Libraries are used as contract support functions.

One method for developers to save gas is to extract common and repetitive functions and place them in libraries.

This allows multiple smart contracts to communicate with the functions without having to define them all the time.

Libraries can be **embedded** or **deployed**.

> Embedded libraries exist in our building code, while deployed libraries are already on the chain. To use deployed libraries, simply create a contract instance and invoke the function in the library!

Use deployed libraries to reduce on-chain data and redundancy, thereby lowering gas consumption.

### 3. Improve the order of variable declarations.

When it comes to data handling, the EVM has a one-of-a-kind approach.

**Storage** is a persistent storage space that can be read, written, and modified, as well as a location where each contract persistently stores data.

Storage has a total of 2^256 slots, with each slot containing **32 bytes**. The contract's "state variables" will be stored in these slots based on their specific type.

State variables with a size of fewer than 32 bytes are stored as index values in the order of their definition, i.e. 0 for position 1, 1 for position 2, and so on.

Small values, such as `uint64`, will be placed in the same slot if they are declared one after the other.


```
pragma solidity ^0.8.0;

contract C {
     uint8 a = 10;
     uint8 c = 10;
     uint8 b = 10;
     uint8 d = 10;

     function m() view public returns(uint8,uint8,uint8,uint8){
        return (a,b,c,d);
   }
}

``` 


```
contract Optimize {

    // takes up low space
    // consumes less gas
    uint8 a;
    uint8 b;

    //takes large space
    // consumes more gas
    uint8 c;
    uint256 d;

    // takes larger space
    // not feasible
    // consumes plenty gas
    uint128 e;
    string name;
    bool status; 

}
``` 



### 4. Avoid iterating over a dynamic range of data

Do not iterate over a set of figures that is supposed to change (increase) over time. In other words, avoid using loops for non-fixed data ranges that are set to grow over time.

Loops could be used if the range will remain constant after deployment.

While writing a contract, you may come across a situation in which you must repeat an action. In such cases, you would need to write loop statements to reduce the number of lines, but doing so incorrectly can harm your code.


```
uint public count
function nameLoop(uint n) public {
         for(uint i = 0; i < n; i++ ) {
	           Count +=1; // Increment the counter by 1 every time the for loop runs
          }
``` 
> The code above shows a case of an endless loop that will be run as long as the `nameLoop()` function is called. This consumes more gas. 



```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.10;

contract Looping {

    uint8[4] public numbersArray = [1,2,3,4];
    uint8 public num;


  function forLoop() public {

    for (uint i = 0 ; i < 5 ; i++) {
        // do something
        if(i = 1 ){
          num = numbers[i];
        }
    }  
  }

}
``` 
> The preceding scenario depicts looping through a fixed-size array whose size is not expected to change. This consumes less gas.

Work your way through your code, looking for places where you can reduce looping through dynamic data.


### 5. Use literal values over computed values.

Solidity includes built-in cryptographic functions for computing hashes.

Here are a few examples:

> keccak256(bytes memory) returns (bytes32), computes the input's Keccak-256 hash.

> ripemd160(bytes memory) returns (bytes20), computes the RIPEMD-160 hash of the input.

> sha256(bytes memory) returns (bytes32) ,computes the input's SHA-256 hash.



![Computed Hash using Keecak](https://cdn.hashnode.com/res/hashnode/image/upload/v1650909265057/Pq3XykE3k.png)

In terms of gas, these hashes are prohibitively expensive.

One workaround is to compute hashes outside of your contract and include them directly in your contract.

Reduce or eliminate hash computations in the build/deploy code.

### 6. Use ERC 1167 / EIP 1167

This standard is not simple, but it is an excellent way to save money on gas.

This standard specifies a minimal bytecode implementation that delegates all calls to a known, fixed address in order to easily and cheaply clone contract functionality in an immutable manner.

If you need to deploy the same contract multiple times, the [ERC-1167](https://eips.ethereum.org/EIPS/eip-1167) comes in handy. It employs a proxy contract system in which you only need to deploy the code of your smart contract once and all subsequent contracts can point to the previously deployed with a new data instance for each.

Redundancy is reduced, which saves gas.

More information about ERC 1167 can be found [here](https://blog.openzeppelin.com/deep-dive-into-the-minimal-proxy-contract/).

### 7. Use the `eth-gas-reporter` package

This is an Ethereum test suite Mocha reporter.

It has many features, the most notable of which is **a gas reporter**. It displays the gas consumption of your code, among other things, every time you run the test for your contract.


![gasreporter.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650909771870/fxdl6L22o.png)


Get it [here](https://www.npmjs.com/package/eth-gas-reporter).


## Conclusion

The best blockchain engineer is one who can create low-cost applications. Go save some gas.