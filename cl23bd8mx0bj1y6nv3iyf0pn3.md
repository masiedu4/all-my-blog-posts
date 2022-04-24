## Build and deploy an NFT Whitelist App with React and Solidity | Step-by-Step Tutorial.

Working on the technical components of [NFTs](https://www.michaelasiedu.com/nfts-greater-physical-art-why-digital-art-will-completely-disrupt-physical-art) might result in a plethora of features that must be implemented, and these capabilities are coded into the smart contract and the project's minting/roadmap website.

Consider starting an NFT and granting exclusive access to specific art or incentives through a limited whitelist. You can create your whitelist using the smart contract. The website then allows users to connect with and join the **Whitelist Smart Contract.**

Essentially, a DApp in which users can communicate with the smart contract via the frontend.

This project demonstrates a basic whitelisting use case. 

## Introduction.

In this post, we will create a full-fledged DApp that will be deployed on Ethereum.

Solidity is our smart contract's tech stack, Alchemy is our RPC, and Hardhat is our local development environment.

To handle all of our blockchain interaction functionality, we will use React.js and ethers.js on the front end.


## Pre-requisites.

All that is necessary is a basic knowledge of the Solidity programming language and an intermediate grasp of React.js.

## Let's build something.

The plan is to construct and deploy the smart contract first, and then the frontend subsequently.

In the following lines, we will set up our [Hardhat](https://hardhat.org/getting-started/) environment and then write some Solidity code.

Finally, we will fund our wallet with test tokens and launch our contract on the testnet!

We'll go ahead and receive our contract address and contract abi. It will act as a route of communication with the blockchain contract.

Let's get our hands a little muddy.

## Setting up our environment

We will **construct** and **deploy **our smart contract locally using the Hardhat environment.

- Make a folder for your smart contract in the root or anywhere you want it.

- To configure the environment, `cd` into the root folder and run the following commands.


```
// in this order, run these commands

npm init --yes
npm install --save-dev hardhat
npx hardhat

``` 

Once you run `npx hardhat`, you will be given a few configurations to set up.

- **Select** Create a basic sample project

- **Press enter** for the already specified Hardhat Project root

- **Press enter** for the question if you want to add a `.gitignore`

Complete the hardhat installation by installing these packages. 

Copy and paste this into your terminal

```
npm install --save-dev @nomiclabs/hardhat-waffle ethereum-waffle chai @nomiclabs/hardhat-ethers ethers

``` 

That's it! We can start writing some code.


## The Whitelist Smart Contract

After installing Hardhat and the other required dependencies, we can see that the `contracts`, `scripts`, and `test` folders include the `Greeting.sol` sample smart contract, as well as its deploy and test scripts.

Make sure all of these folders are empty because we will be creating a fresh smart contract from start!


**Create a new file in the `contracts` folder and name it `Whitelist.sol`**


- The contract will include a `uint public maxWhitelistedAddresses` that represents the maximum number of accounts that can be on our whitelist. 
No one can join the whitelist if this number is achieved. We will set the value for this entity with a **constructor** function when we are deploying.


-  The contract will include a `uint public numAddressesWhitelisted` that represents the current number of accounts we already have on our whitelist. Upon deployment, the value for this value will be **zero** and it will be increased until the maximum is reached. 

- The contract will include a `mapping(address => bool) public whitelistedAddresses`. This logic sets a particular address to `true` immediately it joins the whitelist. It will also be used to ensure that, no account can join the whitelist twice! 


- Moreover, we will have a `constructor` function which will be used to set the value of the maximum accounts that can join the whitelist i.e `maxWhitelistedAddress`.
The value will be set upon deployment. 







```
//SPDX-License-Identifier: Unlicense
pragma solidity ^0.8.0;

contract Whitelist {

    // Represents the total number of accounts we want to have in our whitelist.
    // Value of this will be set with the constructor when we deploy.
    uint  public maxWhitelistedAddresses;

    // This logic creates a mapping of address to boolean
    // default value is false. It will be set to true when an address joins.
    mapping(address => bool) public whitelistedAddresses;

    // This variable will keep track of the number of whitelisted addresses. 
    // It will increase until the maximum number is reached.
    uint public numAddressesWhitelisted;

    // Takes an input that will set the value of maxWhitelistAddress
    // Owner will put the value at the time of deployment
    constructor(uint _maxWhitelistedAddresses) {
        maxWhitelistedAddresses =  _maxWhitelistedAddresses;
    }

 
}
``` 

Now that we have all **our types**, **a mapping**, and **a constructor**, we need to complete this contract by adding the most important function `addAddressToWhitelist()`.

This function will be called when the user wants to join the whitelist.


```
function addAddressToWhitelist() public {
  // ensures that the caller of the function is not already part of the whitelist. 
  require(!whitelistedAddresses[msg.sender], "Sender has already been whitelisted");

   // check if the maximum number of whitelisted addresses is not reached, if not then throw an error.
   require(numAddressesWhitelisted < maxWhitelistedAddresses, "You cannot join now. Limit has been reached");

   // Sets the callers address to true.
   // This makes it a legible whitelisted addres
   whitelistedAddresses[msg.sender] = true;

    // This will increase the number of whitelisted addresses
    numAddressesWhitelisted += 1;
}

``` 

### Putting our entire contract together


```
//SPDX-License-Identifier: Unlicense
pragma solidity ^0.8.0;

contract Whitelist {

    // Represents the total number of accounts we want to have in our whitelist.
    // Value of this will be set with the constructor when we deploy.
    uint  public maxWhitelistedAddresses;

    // This logic creates a mapping of address to boolean
    // default value is false. It will be set to true when an address joins.
    mapping(address => bool) public whitelistedAddresses;

    // This variable will keep track of the number of whitelisted addresses. 
    // It will increase until the maximum number is reached.
    uint public numAddressesWhitelisted;

    // Takes an input that will set the value of maxWhitelistAddress
    // Owner will put the value at the time of deployment
    constructor(uint _maxWhitelistedAddresses) {
        maxWhitelistedAddresses =  _maxWhitelistedAddresses;
    } 

    function addAddressToWhitelist() public {
  // ensures that the caller of the function is not already part of the whitelist. 

  require(!whitelistedAddresses[msg.sender], "Sender has already been whitelisted");

   // check if the maximum number of whitelisted addresses is not reached, if not then throw an error.
   require(numAddressesWhitelisted < maxWhitelistedAddresses, "You cannot join now. Limit has been reached");

   // Sets the callers address to true.
   // This makes it a legible whitelisted addres
   whitelistedAddresses[msg.sender] = true;

    // This will increase the number of whitelisted addresses
    numAddressesWhitelisted += 1;
  }

 }
``` 

## Configuring the deploy script

In the `scripts` folder, create a `deploy.js` file. It is within this file that we will have all our deployment logic and set values constructors.



```
const { ethers } = require("hardhat");

async function main() {
  /*
  A ContractFactory in ethers.js is an abstraction used to deploy new smart contracts,
  so `ourContract` here is a factory for instances of our Whitelist contract.
  */
  const ourContract = await ethers.getContractFactory("Whitelist");

  // here we deploy the contract
  const deployedContract = await ourContract.deploy(10);
  // 10 is the Maximum number of whitelisted addresses allowed ie our constructor
  
  // Wait for it to finish deploying
  await deployedContract.deployed();

  // prints and logs the address of the deployed contract in the console
  console.log(
    "Contract Address:",
    deployedContract.address
  );
}

// Call the main function and catch if there is any error
main()
  .then(() => process.exit(0))
  .catch((error) => {
    console.error(error);
    process.exit(1);
  });

``` 


## Funding our wallet and getting our RPC.

#### Funding our wallet

To launch our smart contract, we will fund our [Metamask wallet](https://metamask.io/) with some testnet (fake) coins for development reasons.


- Visit [this link](https://faucets.chain.link/rinkeby) to fund your wallet with some fake ETH


![Rinkeby Testnet Faucets](https://cdn.hashnode.com/res/hashnode/image/upload/v1650130062498/KUDzClQEF.png)

- Before making the request, launch Metamask and switch to **the Rinkeby test network.**


![Metamask funded succesfully](https://cdn.hashnode.com/res/hashnode/image/upload/v1650130147381/QsYc5kCxO.png)


#### Getting our RPC

[Alchemy](https://auth.alchemyapi.io/) is a blockchain API service that will allow us to easily deploy our smart contract!


![Alchemy Authentication](https://cdn.hashnode.com/res/hashnode/image/upload/v1650130740200/8a8exKiOy.png)

[Sign up](https://auth.alchemyapi.io/), and then let's go over to create our app and acquire our API keys.



- After successful signup, **create an app** from the dashboard.

![Alchemy Create App Dashboard](https://cdn.hashnode.com/res/hashnode/image/upload/v1650131015820/Yw3DKGQjx.png)


- Fill in some pertinent data to finish your app setup. Select **Ethereum** and the **RInkeby Test Network**.


![Alchemy project setup](https://cdn.hashnode.com/res/hashnode/image/upload/v1650131222002/P5WesMcIm.png)



- **View details** of your app and **copy your HTTP endpoint**. We will use this endpoint for the deployment of the contract soon.


![Deployment Endpoint](https://cdn.hashnode.com/res/hashnode/image/upload/v1650131412850/iD5OztcBo.png)

### Let's finish the deployment


- Create a **`.env`** file in the root of your smart contract folder. This file will contain your Alchemy HTTP endpoint as well as your Rinkeby Private Key.

Switch to the Rinkeby test network in Metamask and copy the private key.


![Metamask Private Key](https://cdn.hashnode.com/res/hashnode/image/upload/v1650131961123/S46JtQOqg.png)



- **In your .env file:**

```
API_KEY="add-your-alchemy-endpoint-url-here"

PRIVATE_KEY="add-your-rinkeby-private-key-here"

``` 


- To be able to import our keys into our final config file, we need an npm package called **dotenv** .


```
npm install dotenv

``` 


### Final config before deployment


- Navigate to the **hardhat.config.js** file. This file will be used to configure our networks and API keys for the deployment process.

Copy and paste the following lines of code into the file for convenience.


```
require("@nomiclabs/hardhat-waffle");
require("dotenv").config({ path: ".env" });

const API_KEY = process.env.API_KEY;

const PRIVATE_KEY = process.env.PRIVATE_KEY;

module.exports = {
  solidity: "0.8.0",
  networks: {
    rinkeby: {
      url: API_KEY,
      accounts: [PRIVATE_KEY],
    },
  },
};

``` 

#### Compile the contract


```
 npx hardhat compile

``` 

#### Deploy the contract


```
npx hardhat run scripts/deploy.js --network rinkeby

``` 

- Voilla! Our contract is successfully deployed on the Ethereum RInkeby Test Network!

- Take note of the contract address that was entered into the console. It will be required on the frontend in order to communicate with the smart contract.


-A new `artifacts` folder is created after a successful deployment. This folder contains a **.json** file with our contract's ABI. Copy it and save it because we'll need it along with the contract address.


## The Whitelist Frontend Development

Now that we've completed the difficult aspect, let's build our front.
Communicating directly with a smart contract is difficult for the typical person.

It is our responsibility as developers to create an interactive interface from which users may send requests to the smart contract.

In the second and last part of this tutorial, we will create a React app, connect it to Metamask, and use ethers.js to call functions.

Essentially, our app will leverage basic React principles such as managing and updating states and calling transactions through functions. Nothing too complicated. I've got you covered.

#### Installing React.js and ethers.js

-  Visit the [official docs](https://reactjs.org/docs/create-a-new-react-app.html) to install and set up React.js on your computer. 


- After successfully installing React, install **ethers.js** as a dependency by running this code.

```
npm install ethers

``` 


- For the sake of simplicity and convenience, I'm going to do all of my reasoning in the `src` file's root. You can arrange the folder structure as you see fit.


![Folder Structure](https://cdn.hashnode.com/res/hashnode/image/upload/v1650156597416/7qNEhACf-.png)


#### Building the frontend

In the `Whitelist.js` file:


```
import { useState } from "react";


export default function Whitelist() {

// this manages the state of the number of people on the whitelist
// initial value is set at `null`
 const [numofWhitelisted, setNumofWhitelisted] = useState(null);

// this manages the text shown in the button when connected or not.
// initial value is set at `Connect Wallet`
const [connectButtonText, setConnetButtonText] = useState("Connect Wallet");

// this manages the state of the connected account / address
//intial value is set at `null`
const [connectedAddress, setConnectedAddress] = useState(null);

  return (
    <div>
      <div>
        <div>
          <h1>Welcome to the Whitelist Tutorial!</h1>
          <div>


// when this button is clicked , Metamask should pop up for the user to connect
// upon successful connecting , the text state should change. 
            <button>
              {connectButtonText}
            </button>

// upon successful connecting, the text state should change
// the address of the connected account should show up
            <p> Connected Address : {connectedAddress} </p>
          </div>


          <div>

// when this button is clicked, state should update and the whitelisted number should show
            <button>
              Get the number of whitelisted addresses
            </button>
            {numofWhitelisted} have already joined the Whitelist
          </div>


          <div>
// when this button is clicked, Metamask should pop up for a transaction to be signed
// when signed , the user will be added to the whitelist
            <button>
              {joinWhiteListText}
            </button>
          </div>
        </div>
      </div>

      <footer>Made by Michael Asiedu</footer>
    </div>
  );



}

``` 


Now that you have the unfiltered app, let us implement all of the blockchain functions and update the states.



```
import { useState } from "react";
import { ethers } from "ethers";

// save your ABI in a json file and import it here
import contract_abi from "./contract_abi.json";

export default function Whitelist() {

// address of the smart contract
const contractAddress = `0x90b989349A58a20415Cb3ff440b6244cF3737e12`;

// this manages the state of the number of people on the whitelist
// initial value is set at `null`
 const [numofWhitelisted, setNumofWhitelisted] = useState(null);

// this manages the text shown in the button when connected or not.
// initial value is set at `Connect Wallet`
const [connectButtonText, setConnetButtonText] = useState("Connect Wallet");

// this manages the state of the connected account / address
//intial value is set at `null`
const [connectedAddress, setConnectedAddress] = useState(null);

 // state management of provider , signer and contract
  const [provider, setProvider] = useState(null);
  const [signer, setSigner] = useState(null);
  const [contract, setContract] = useState(null);


  return (
    <div>
      <div>
        <div>
          <h1>Welcome to the Whitelist Tutorial!</h1>
          <div>
            <button onClick={connectWalletHandler}>
              {connectButtonText}
            </button>

            <p> Connected Address : {connectedAddress} </p>
          </div>


          <div>
            <button onClick={getNumWhitelistHandler}>
              Get the number of whitelisted addresses
            </button>
            {numofWhitelisted} have already joined the Whitelist
          </div>


          <div>
            <button onClick={joinWhitelistHandler}>
              {joinWhiteListText}
            </button>
          </div>
        </div>
      </div>

      <footer>Made by Michael Asiedu</footer>
    </div>
  );



}

``` 
#### What are Providers and Signers?

- A Provider is an abstraction of an Ethereum network connection that provides a clear, **consistent interface to regular Ethereum node functions.**


- A Signer in ethers is an abstraction of an Ethereum Account that may be used** to sign messages and transactions and submit signed transactions to the Ethereum Network** to perform state changes.


```
// the if-else statement checks if the browser has Metamasks installed
// if installed, it will connect to the first account/address

  const connectWalletHandler = () => {
    if (window.ethereum) {
      window.ethereum
        .request({ method: "eth_requestAccounts" })
        .then((result) => {

    // after connection, state of connectedAddress and connectButtonText  will update
         setConnectedAddress(result[0]);
          setConnetButtonText("Wallet Connected!");
    // updateEthers will initiate the provider, signer and the contract instnace
          updateEthers();
        });
    } else {
      setConnectedAddress("Please Install Metamask Extension!");
    }
  };


    const updateEthers = async () => {

    // initiate a provider with ethers.js
    const provider = new ethers.providers.Web3Provider(window.ethereum);
    setProvider(provider);
   
   // initiate a signer with ethers.js
    const signer = provider.getSigner();
    setSigner(signer);

   // initiating a new contract instance with ethers.js
    const contract = new ethers.Contract(contractAddress, contract_abi, signer);

    setContract(contract);

    // will log the provider, signer, and contract in the console when successful.
    console.log({provider, signer , contract})
  };


``` 

#### Getting the number of whitelisted accounts and joining the whitelist.


```
  const getNumWhitelistHandler = async () => {
   // calls the numAddressesWhitelisted public uint from our contract directly
    let number = await contract.numAddressesWhitelisted.length;
    setNumofWhitelisted(number);
  };

  const joinWhitelistHandler = async () => {
  // calls the addAddressToWhitelist function in our smart contract directly 
    const tx = await contract.addAddressToWhitelist();
    await tx.wait();

    setJoinWhiteListText("Succesfully Joined!");
    await getNumWhitelistHandler();
  };

``` 


### Putting the frontend together


```
import { useState } from "react";
import { ethers } from "ethers";
import "./styles.css";
import contract_abi from "./contract_abi.json";

export default function Whitelist() {
  const contractAddress = `0x90b989349A58a20415Cb3ff440b6244cF3737e12`;

  const [numofWhitelisted, setNumofWhitelisted] = useState(null);
  const [connectButtonText, setConnetButtonText] = useState("Connect Wallet");

  const [connectedAddress, setConnectedAddress] = useState(null);

  // state management of provider , signer and contract
  const [provider, setProvider] = useState(null);
  const [signer, setSigner] = useState(null);
  const [contract, setContract] = useState(null);

  const connectWalletHandler = () => {
    if (window.ethereum) {
      window.ethereum
        .request({ method: "eth_requestAccounts" })
        .then((result) => {
          setConnectedAddress(result[0]);
          setConnetButtonText("Wallet Connected!");
          updateEthers();
        });
    } else {
      setConnectedAddress("Please Install Metamask Extension!");
    }
  };

  const updateEthers = async () => {
    const provider = new ethers.providers.Web3Provider(window.ethereum);
    setProvider(provider);
    console.log(provider.getCode(contractAddress));

    const signer = provider.getSigner();
    setSigner(signer);

    const contract = new ethers.Contract(contractAddress, contract_abi, signer);

    setContract(contract);
  };

  const getNumWhitelistHandler = async () => {
    let number = await contract.numAddressesWhitelisted.length;
    setNumofWhitelisted(number);
  };

  const joinWhitelistHandler = async () => {
    const tx = await contract.addAddressToWhitelist();
    await tx.wait();

    setJoinWhiteListText("Succesfully Joined!");
    await getNumWhitelistHandler();
  };

  return (
    <div>
      <div className="main">
        <div>
          <h1 className="title">Welcome to the Whitelist Tutorial!</h1>
          <div>
            <button onClick={connectWalletHandler}>

              {connectButtonText}
            </button>
            <p> Connected Address : {connectedAddress} </p>
          </div>
          <div className="description">
            <button onClick={getNumWhitelistHandler}>
      
              Get the number of whitelisted addresses
            </button>
            {numofWhitelisted} have already joined the Whitelist
          </div>
          <div>
            <button onClick={joinWhitelistHandler}>
        
              {joinWhiteListText}
            </button>
          </div>
        </div>
      </div>

      <footer className="footer">Made by Michael Asiedu</footer>
    </div>
  );
}


``` 

### Before connecting to Metamask...

![Before connecting to Metamask](https://cdn.hashnode.com/res/hashnode/image/upload/v1650160437199/kYL9BR5CJ.png)


### After connecting to Metamask...


![After connecting to Metamask](https://cdn.hashnode.com/res/hashnode/image/upload/v1650160485378/zCfII2zfc.png)


### Before you leave

If your React.js is good, you'll notice that there are several best practices, such as the ContextAPI and the [useReducer hook](https://www.michaelasiedu.com/using-reacts-usereducer-hook-to-manage-complex-states), that may be used to make our code more clean and efficient.

What are some of the features that you can implement on your own?

I've created [a repository for this lesson](https://github.com/masiedu4/whitelist-smart-contract-solidity-), with separate branches for the smart contract and the frontend. You can look into it.

Check out more of my articles [here.](https://www.michaelasiedu.com/)