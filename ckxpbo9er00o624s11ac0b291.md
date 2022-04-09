## Getting Started with Ethereum Blockchain Development with Solidity.


When a bright Russian programmer, [Vitalik Buterin](https://vitalik.ca/), was 19 years old, he came up with the idea of creating a decentralized, open-source blockchain system, which he named **Ethereum**. The aim was to embed [smart contract](https://blog.michaelasiedu.com/the-lifecycle-and-application-of-blockchain-smart-contracts) functionality into this blockchain (something Bitcoin cannot do).


Vitalik saw Bitcoin as a fantastic kind of digital money, but he saw it as having a weak programming language, making it difficult to build any type of significant application on top of it.

Working with Dr. Gavin Wood, a group of clever software engineers gained responsibility for the development effort in 2014.

Any developer who wants to create permanent and irreversible decentralized applications on the Ethereum platform, with which users can interact, is welcome to do so on the Ethereum platform.

All you need is an internet connection to utilize Ethereum, and that's it.

### Components of the Ethereum Blockchain 

Runs on the Ethereum main network on TCP port 30303 and runs a protocol called ÐΞVp2p. (P2P network).

#### Transactions 

In Ethereum, a transaction is a communication sent across the network that contains information such as the sender, recipient, value, and payload.


#### Consensus Protocol 

Ethereum currently relies on a consensus algorithm known as Proof-of-Work (PoW). In order to prevent attacks on the Ethereum network, all the nodes must agree on the current state of the Ethereum blockchain.

However, a Proof-of-Stake(PoS) voting system, dubbed Casper, is about to be implemented as the network's fundamental consensus process.


#### Currency 

The Ethereum platform's native cryptocurrency, Ether (ETH or Ξ), is a digital asset.

At present, it is the second-largest cryptocurrency by market capitalization, after Bitcoin, at the time of this writing.


#### State Machine 

The Ethereum Virtual Machine (EVM) processes Ethereum state changes (EVM).
Smart contracts are programs written to the EVM, a decentralized code that is well known.


They are written in high-level languages (such as Solidity, Vyper,...) and translated into low-level bytes that the EVM can understand and execute.


### Decentralized Applications ( DApps )

When it comes to the development of complex apps, Ethereum has quickly become a platform for developers.

It is common for individuals to mistake DApps for smart contracts. As previously said, smart contracts are included in DApps. Using a DApp, a user can access a front-end user interface and a back-end smart contract on a blockchain in one web application.

In order to bring the World Wide Web into the next evolutionary stage, the technology of decentralized applications is supposed to introduce decentralization using peer-to-peer protocols into every component of a web application. They're calling it Web3.

Centrally-managed apps are being replaced by decentralized ones that are built on protocols that spread power and control across all participants on the web. Aren't you looking forward to it?

![Untitled-design.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1640648131147/HH9G6lrhR.jpeg)

On the client side, JavaScript and other front-end programming languages are used to create DApps' user interfaces on the client side.

In this scenario, the backend is a set of smart contracts that the users interact with.

Frameworks (e.g., web3.js, ethers.js) provide methods and functions that users can utilize to make calls to the smart contract while constructing the frontend of DApps.

Smart contracts have a life cycle, which I describe in great depth in an article I wrote. For further information, click [here](https://blog.michaelasiedu.com/the-lifecycle-and-application-of-blockchain-smart-contracts).

That also means a developer familiar with JavaScript applications can dive into Ethereum and start writing code very quickly.


### Smart Contract Development with Solidity 

It is an object-oriented high-level programming language for smart contracts. Developed by Dr. Gavin Wood (Sofware Engineer & Co-Founder of Ethereum).

Programming in Solidity is heavily influenced by C++ as well as Python and JavaScript. It is designed to run on the Ethereum Virtual Machine (EVM).

For EVM bytecode encoding, `solc` is the compiler for the Solidity programming language. (advanced -> intermediate )

Compiling and deploying a specific version of the Solidity programming language is done in each stage of the Solidity compiler development process.

Compilation fails if the version of the code does not match the compiler's version number.

Semantic Versioning is a widely used versioning model for Solidity.

semantic versioning is the use of a three-part version number (major, minor, and patch) to indicate compatibility. Eg. 1.1.0, 1.1.1, and 1.1.2

According to the following, the numbers are progressively increased:


- **Changes that are both significant and backward-incompatible are referred to as "major".**

- **Minor = Between major versions, minor (backward-compatible) enhancements are made. **

- **Patches = ++ bug fixes that are backwards compatible**

Solidity's current version is 0.8.11.

Because Solidity is a language that is always changing and adding new features, programmers must be ready to change their skills on a regular basis in order to stay up to date.



#### Development Environment 

Any text editor can be used to write Solidity code, as long as the `solc` compiler is installed on the command line.

Start coding right away with a web-based IDE like [Remix](https://remix.ethereum.org/). The `.sol` extension is used to save Solidity files.

Below is a sample of Solidity code.

```
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract SimpleStorage {
    uint storedData;

    function set(uint x) public {
        storedData = x;
    }

    function get() public view returns (uint) {
        return storedData;
    }
}

``` 


#### Features and Applications  

Solidity is a curly-bracket language that is statically typed and allows for inheritance, libraries, and complex types made by the author.

In order to be more familiar to existing web developers, it is built on top of the ECMAScript syntax.

Developers can use Solidity to make things like voting, crowdsourcing, blind auctions, multi-signature wallets, and more.


#### Best Practices 

It is critical that you use the most recent version of Solidity to run your code. This is due to the fact that security fixes are only made available for the most recent version.

#### Availability on Blockchain Platforms 

-  Ethereum

- Binance Smart Chain

- Ethereum Classic

- Tron

- Avalanche 

Ethereum has an active development community and is a wonderful place to learn about blockchain technology. I hope you found this information interesting.

#### Some great resources to check out 
-  [Solidity Docs]( https://docs.soliditylang.org/en/v0.8.11/) 

-  [Mastering Ethereum: Building Smart Contracts and DApps](https://www.amazon.com/Mastering-Ethereum-Building-Smart-Contracts/dp/1491971940) 

-  [Ethereum | Wikipedia](https://en.wikipedia.org/wiki/Ethereum) 















