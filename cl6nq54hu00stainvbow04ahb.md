## Blockchain Oracles: Connecting the Outside World to Decentralization.

A [smart contract](https://www.michaelasiedu.com/the-lifecycle-and-application-of-blockchain-smart-contracts) is a code that contains a set of rules that govern how parties interact with one another. If and when the predefined rules are met, the agreement is automatically enforced.

By principle, blockchain networks and smart contracts are deterministic and cannot access data from the outside world.

**Oracles** solve this seemingly major issue.

In the context of blockchain networks, "oracles" are services or data feeds that bring relevant data from the off-chain world into the smart contract and vice versa.


## What are Oracles?

In our culture, an oracle is defined as a being who offers wise and insightful advice or makes transcendent forecasts.

When it comes to blockchain networks, they are not so dissimilar. 

**Oracles** are third-party services that enable smart contracts to communicate with and exchange data with the outside world. They are not part of the blockchain consensus mechanism.

For example, in your code, you could include a function that ensures that people can only send to the smart contract amounts greater than the current Ether price.

**When the function is called, two executions will occur.**

> 1. Because our contract does not have that information, the smart contract will use an oracle to retrieve the current ETH price from an external off-chain source.

> 2. The smart contract will perform a check to ensure that only amounts greater than the current Ether price are deposited or accepted.

**The pseudocode below demonstrates how the execution occurs.**


```solidity


    function fund() public payable {
        if (amountDeposited > currentETHPriceFromOracle) {
            "Transfer is successful"
            }     else {
            "You are not sending enough Ether
            }   
        
    }

``` 

## Major Classes of Oracles

The good thing about oracles is that they come in various forms, so regardless of the blockchain system and its requirements, you can find what works and integrate it. Let's take a look at them.

### Inbound Oracles

This is now by far the most common type of oracle.

**Inbound oracles**, as the name implies, have the function of injecting data into smart contracts.

This incoming data comes from an outside source, and once the transaction is completed, the contract proceeds with the subsequent execution based on the received data. 

An inbound oracle is a data feed that provides updates like the current stock price or the current temperature to a contract. Some of the most popular inbound oracles are [Chainlink(LINK)](https://chain.link/) and [WINlink(WIN).](https://winklink.org/)

### Outbound Oracles

**Outbound oracles**, in contrast to inbound oracles, send smart contract data to sources outside the contract.

Consider a smart contract use case in which the execution of certain functions results in the release of certain properties in the real world.

An outbound oracle works similarly to making API calls from your contract to trigger an event in an external source.

### Software Oracles

The vast majority of inbound and outbound oracles are **software oracles**.

Software metrics appear to be a real-time and up-to-date source of data to and from the real world.

They can be easily accessed with a few lines of code from public databases and platforms due to their mode of execution.

They provide trustworthy data on anything quantifiable, such as stock and cryptocurrency prices and weather updates. At the moment, software oracles are the most powerful and user-friendly oracles.


### Hardware Oracles

What about smart contracts that require information directly from the physical world, one might ask? That is where **hardware oracles** come into play!

They provide a channel for data exchange between blockchain networks and the Internet of Things (IoT).

A vehicle, for example, crossing a specific barrier equipped with motion sensors can detect the vehicle's movement and send data to a smart contract.

Data can be sent from the smart contract to the physical world in an outbound-hardware oracle.


### Consensus-based Oracles

Consensus-based oracles use multiple oracles and a consensus algorithm to obtain factual data for smart contracts, just as consensus-based decisions build trust and produce the best possible outcome.

More is better because manipulation is reduced or eliminated.

The caveat comes into play when only one source is used. This makes the data untrustworthy.

A combination of multiple oracles (4-6) may improve the reliability of the data we receive.


## Advantages and Possible Use Cases of Blockchain Oracles

Oracles are critical to blockchain networks because they improve on smart contract promises.

Smart contracts would only have access to data within their crypto networks if decentralized oracles were not present, limiting their potential applications and robustness.

**Reliability** is a key factor in the success of blockchain oracles.

The underlying concept of how data is obtained is that systems aggregate and thoroughly analyze data from multiple sources. Only accurate and scrutinized data from a diverse set of resources can reach smart contracts this way.

### Use Case 1: Decentralized Betting

The betting industry is one area where smart contract and oracle technology has the potential to revolutionize.

Betting companies/bookmarkers are entities that allow players to stake money on game predictions.

Players are credited a certain amount for correct predictions, which is always an increase over the initial staked amount.

Behind the scenes, betting companies retrieve game information from a centralized API and run checks to ensure that current selections are consistent with the players' predictions.

Wrong predictions by players cause the bet to be settled, resulting in a loss of funds.

**Here are some of the issues with Web2 betting companies.**

> 1. Deposits with unreported funds (with which players have to contact customer care)

> 2. Uncredited wins

> 3. Wins that are credited late

> 4. Suspension of wins ( reasons known to bookmakers )

**What benefits will a Web3 betting company provide?**

A betting company with infrastructure built on a distributed ledger can help reduce transaction friction and centralization.

Because smart contracts are deterministic in nature, automating fund transfers and deposits appears to be simple.

The caveat is the concept of transaction fees, which should not be an issue with scalable blockchain platforms!

A smart contract can communicate with an oracle, which will be in charge of injecting real-time data from the outside world.

Additional checks will be performed to ensure that winners receive their dues. The major drawbacks of Web2 betting, such as late crediting of gains and uncredited wins, will be addressed.

Finally, automation can save businesses a significant amount of time (improved user response rate) and money. Both parties benefit from this arrangement.

### Use Case 2: Buying a property 

The current model for purchasing properties such as houses and cars involves the use of trusted intermediaries who are required for transaction clearing and settlement.

When purchasing a car, additional third parties such as banks and insurance companies are involved.

Customers do not have to worry about the cost of insurance for the vehicle, but they must deal with a lengthy process.

Consider a scenario in which all parties involved used distributed ledger technology. None of the traditional steps will be skipped, but we can use oracles and smart contracts to create a safe, cheap, and secure process.

>**How will this play out?**

A buyer with a unique blockchain identity will initiate a "buy" transaction, depositing a certain amount of funds into the seller's wallet. A side smart contract transaction for an insurance policy plan will be included in a more sophisticated deal.

A further check will be performed to ensure that only a certain amount of money is required for the transfer to be successful.
 
When the point of a successful transfer is reached, **hardware outbound oracles** enter the picture. This oracle's job is to send smart contract data to the outside world (a smart garage and a car) with an integrated smart lock, such as the new owner's identity and access code. This entire procedure will be carried out only if the payment for the property in question is successful.

The new owner's blockchain identity will then be linked to the property, and he will be granted exclusive access to the property in the form of a security code.


> **Upsides and the bigger picture**

This technology eliminates the need for vehicles and insurance companies to interact manually. A computer running a blockchain node can potentially determine whether or not someone is the rightful owner of a car.

As previously illustrated, process automation will require the use of smart contracts and outbound oracles to exchange data.

One significant advantage is that owners can use smart contract access controls to authorize others to access their properties by registering the blockchain identity (temporarily or permanently) to their properties.


Owners do not need to be concerned about theft because cars are equipped with digital keys for access control.

## Cons of Using Blockchain Oracles

After firmly establishing that oracles are an essential component of the bridge between smart contracts and our regular external world, it would be unjustifiable not to discuss some of the major drawbacks stakeholders will face when working with oracles.

### 1. Security 

The concept of security is one issue that stakeholders must be prepared to deal with.

Given the history of blockchain networks, it is especially difficult to ensure that data originating off-chain can be trusted.

Even though we can boast that data is aggregated multiple times before it reaches the smart contract, it should be noted that a single unreliable data point has the potential to change the state of the final data.
As a result of attackers manipulating oracle data, Warp Finance 7.7 million USD. Synthetix, Harvest Finance, and other DeFi firms all lost a couple of million dollars due to poor oracle execution and data manipulation.


### 2. Cost

When working with the blockchain, it is common knowledge that signed transactions incur fees, and because fetching data from oracles requires a significant amount of computing power, there will be a corresponding high payment of funds just to cover fees.

Extensive computing remains inconvenient in the current state of blockchain networks. Oracles in smart contracts will most likely see widespread adoption as scalability improves.


### 3. Time of execution 

The time required to aggregate data from multiple sources and reach a consensus on the outcome is longer when compared to centralized data. Furthermore, popular smart contract networks such as Ethereum, which hosts a large portion of all decentralized apps, are slow. Again, we will be able to boast of faster processes as the scalability of various blockchain networks improves.


##  Chainlink: An Overview of the Most Popular Blockchain Oracle

[Chainlink](https://chain.link/), which was launched on the Ethereum blockchain in 2017, is an open source and decentralized service that powers smart contract use cases in Defi, Enterprise, Insurance, NFTs, and Gaming.

The decentralized oracle network provided by Chainlink is an open-source technology infrastructure that allows any blockchain to securely connect to off-chain data and computation resources.


![Chainlink Blockchain Service](https://cdn.hashnode.com/res/hashnode/image/upload/v1658851814674/9Nn9ioWQ8.png align="left")

**LINK **, the network's native cryptocurrency, serves as data payloads, delivering required data from off-chain sources to smart contracts.
The trade value derived from these tokens is used to pay node operators for retrieving data.

**Chainlink Data Feeds** is a secure, dependable, and decentralized source of off-chain data that can be used to power unique smart contract use cases.

Chainlink can be used for a variety of off-chain computation functions, including verifiable random function (VRF), which is boosting the decentralized gaming industry.


## Learn More

This blog is dedicated to educating curious individuals who want to learn about technology and improve their skills.

Check out [the blog](https://www.michaelasiedu.com/) to show your support. Thank you very much.