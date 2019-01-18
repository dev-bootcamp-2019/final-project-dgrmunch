# About this dApp

* Ethereum dApp built on Solidity + React.
* Project developed by Diego Gonzalez (@ Enxendra/Docuten) for ConsenSys Bootcamp 2019 (Twitter: @dgrmunch | Web: xmunch.com)
* To be used for distributed proof-of-existence and proof-of-life experiments (using document hashes + ipfs hashes).


# Video tutorials 

## To run your own

* Check this video to see how to run your own instance of the dApp:

[![How to run the dApp](http://img.youtube.com/vi/U5QU9qvx7fA/0.jpg)](https://www.youtube.com/watch?v=U5QU9qvx7fA "How to run the dApp")

* I have published also some instructions below, just in case you want to go deeper or if something in the video is not clear enough.

## To use an online version

* Check this video to see how the dApp works and how to use it:

[![How to use it](http://img.youtube.com/vi/p14buBTG1kY/0.jpg)](https://www.youtube.com/watch?v=p14buBTG1kY "How to use it")


# Course requirements and extra characteristics:


## User Interface:

○      dApp runs on server (locally for testing/grading) and has an online deployed version **[DONE]**
○      There is an URL to interact with the dApp  **[DONE]**
  ■      App recognizes current account  **[DONE]**
  ■      Sign transactions using MetaMask **[DONE]**
  ■      Contract state is updated  **[DONE]**
  ■      Update reflected in UI  **[DONE]**

## Solidity Tests:

○       11 tests for both deployed contracts  **[DONE]**
○       Why did I write those tests? Because I wanted to verify security issues in both the delegate and the proxy.  **[DONE]**
○  Tests run with *truffle develop > test*  **[DONE]**

##  Design Pattern Requirements:

○      Implement a circuit breaker (emergency stop) pattern  **[DONE]**
○      More info about used design patterns: Especified in *design_pattern_decisions.md*  **[DONE]**

## Security Tools / Common Attacks:

○      These contracts are not susceptible to common attacks. More info in *avoiding_common_attacks.md*  **[DONE]**


##   Use a library or extend a contract

**I decided to extend my deployed contracts** with inheritance (and several layers of aux contracts). I also decided to deploy a delegate and a proxy. This way I avoided the use of specific libraries deployed in one specific network. So this dApp is network-neutral and all the required code is written by myself.  *design_pattern_decisions.md*  **[DONE]**

  
##  Other requirements

●      Deploy your application onto one of the test networks. Include a document called deployed_addresses.txt that describes where your contracts live (which testnet and address).  **[DONE]**

●      Stretch requirements (for bonus points, not required): Implement an upgradable design pattern  **[DONE]**


# How to use a currently deployed instance

## Use directly the dApp:
* Access https://dgrmunch.github.io/docuten-blockchain-proof-dapp
* Connect Metamask to Ropsten

## Use etherscan and interact directly with the proxy contract
* More info about the addresses + ABIs for deployed smart contracts in the file deployed_addresses.txt

# To run it in your own server

## Installation

```
npm install
npm install truffle-hdwallet-provider
npm install --save gh-pages

```

## Running the dApp

### On one shell

Run:

`truffle migrate --network ropsten`

or

`truffle migrate --reset` (for local test)


This will deploy the smart contracts.

* Remember that in order to open the use of your deployed instance to other users (and not only the contract owner who deployed the contract) you should call to the openToEveryUser() function in the proxy. This will make all the functions with the modifier onlyAuthorizedUsers (in the delegated contract, ProofOfLife, or its parent contracts) to be enabled to "other users" and not only to the authorized ones.

### On another shell


```
cd client
npm run start

```
This will run a node dApp. Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

You will need Metamask in your browser to make it work<br>


## Deploying the dApp in Github pages

```
truffle migrate --reset --network ropsten
npm run deploy

```

By default, it will be deployed here: https://dgrmunch.github.io/docuten-blockchain-proof-dapp/
Update the configuration in truffle-config.js in order to adapt it to your needs.

## Test the smart contracts

`truffle test`

## How to get the ABI of the contract to use in MyEtherWallet?

* In deployed_address.txt (updated)
* In the truffle develop shell, typing:

```
const fs = require('fs');
const contract = JSON.parse(fs.readFileSync('client/src/contracts/ProofOfLife.json', 'utf8'));
console.log(JSON.stringify(contract.abi));

```
