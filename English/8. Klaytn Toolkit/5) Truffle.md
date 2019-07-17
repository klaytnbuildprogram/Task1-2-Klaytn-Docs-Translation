# Truffle

## Compatibility with Truffle
In Klaytn, a smart contract written in Solidity can be compiled and deployed via Truffle. At the moment, Klaytn supports up to Truffle v5.0.26, the latest version at the time of writing. Please find details about Truffle on the websites below.

​Truffle overview​

​Truffle repository​

You can install Truffle as the following:

$ sudo npm install -g truffle
If you have a local EN running, you can deploy contracts directly with truffle framework. For more details, refer to this link.

If you want to deploy with a remote EN node, you should use truffle-hdwallet-provider-klaytn.

## Configuring truffle-hdwallet-provider-klaytn
truffle-hdwallet-provider-klaytn is a JavaScript HD wallet provider forked from truffle-hdwallet-provider.

Install as the following

$ npm install truffle-hdwallet-provider-klaytn
Set truffle-config.js as below.

Using a mnemonic
const HDWalletProvider = require("truffle-hdwallet-provider-klaytn");
​
const mnemonic = "mountains supernatural bird ...";
​
module.exports = {
  networks: {
    development: {
      host: "localhost",
      port: 8545,
      network_id: "*" // Match any network id
    },
    testnet: {
      provider: () => new HDWalletProvider(mnemonic, "https://api.baobab.klaytn.net:8651"),
      network_id: '1001', //Klaytn baobab testnet's network id
      gas: '8500000',
      gasPrice: null
    },
    mainnet: {
      provider: () => new HDWalletProvider(mnemonic, "https://api.cypress.klaytn.net:8651"),
      network_id: '8217', //Klaytn mainnet's network id
      gas: '8500000',
      gasPrice: null
    }
  }
};
Using a private key
const HDWalletProvider = require("truffle-hdwallet-provider-klaytn");
​
const privateKey = "0x123 ...";
​
module.exports = {
  networks: {
    development: {
      host: "localhost",
      port: 8545,
      network_id: "*" // Match any network id
    },
    testnet: {
      provider: () => new HDWalletProvider(privateKey, "https://api.baobab.klaytn.net:8651"),
      network_id: '1001', //Klaytn baobab testnet's network id
      gas: '8500000',
      gasPrice: null
    },
    mainnet: {
      provider: () => new HDWalletProvider(privateKey, "https://api.cypress.klaytn.net:8651"),
      network_id: '8217', //Klaytn mainnet's network id
      gas: '8500000',
      gasPrice: null
    }
  }
};
WARNING: Be very careful not to expose your mneomonic or private key.

Deploying on Klaytn testnet

$ truffle deploy --network testnet
Deploying on Klaytn mainnet

$ truffle deploy --network mainnet
For more information, refer to tutorials.
