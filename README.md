# My First Smart Contract

We need Ganache on local environment

### Getting started

Create a project with Truffle

``` shell
truffle init
```

Create the Hello World Contract:

``` solidity
// Specifies the version of Solidity, using semantic versioning.
// Learn more: https://solidity.readthedocs.io/en/v0.5.10/layout-of-source-files.html#pragma
pragma solidity ^0.5.10;

// Defines a contract named `HelloWorld`.
// A contract is a collection of functions and data (its state).
// Once deployed, a contract resides at a specific address on the Ethereum blockchain.
// Learn more: https://solidity.readthedocs.io/en/v0.5.10/structure-of-a-contract.html
contract HelloWorld {

    // Declares a state variable `message` of type `string`.
    // State variables are variables whose values are permanently stored in contract storage.
    // The keyword `public` makes variables accessible from outside a contract
    // and creates a function that other contracts or clients can call to access the value.
    string public message;

    // Similar to many class-based object-oriented languages, a constructor is
    // a special function that is only executed upon contract creation.
    // Constructors are used to initialize the contract's data.
    // Learn more: https://solidity.readthedocs.io/en/v0.5.10/contracts.html#constructors
    constructor(string memory initMessage) public {
        // Accepts a string argument `initMessage` and sets the value
        // into the contract's `message` storage variable).
        message = initMessage;
    }

    // A public function that accepts a string argument
    // and updates the `message` storage variable.
    function update(string memory newMessage) public {
        message = newMessage;
    }
}
```

Create Migration to Hello World Contract:

``` solidity
const HelloWorld = artifacts.require("HelloWorld");

module.exports = function (deployer) {
  deployer.deploy(HelloWorld, "Hello World");
};

```

Compile the code:

``` shell
truffle compile
```

Configure the Ganache on `truffle-config.js` adding the development network

``` json
 development: {
     host: "127.0.0.1",     // Localhost (default: none)
     port: 7545,            // Standard Ethereum port (default: none)
     network_id: "*",       // Any network (default: none)
    },
```

Apply the migration, sending contract to Ganache Network

``` shell
truffle migrate
```


### Interact with contract through Truffle

Call Truffle console

``` shell
truffle console
```

Get the contract from network

``` js
contract = await HelloWorld.deployed()
```

Getting the initial contract message

``` js
await contract.message.call()
```

Update the contract message

````js
await contract.update("Alou mundão veio sem fronteira");
```