# Account

## defaultAccount
caver.klay.defaultAccount
This default address is used as the default from property, if no from property is specified in parameters of the following methods:

​caver.klay.sendTransaction()​

​caver.klay.call()​

​new caver.klay.Contract() -> myContract.methods.myMethod().call()​

​new caver.klay.Contract() -> myContract.methods.myMethod().send()​

Property

20-byte String - Any Klaytn address. You should have the private key for that address in your node or keystore. Default is undefined.

Example

> caver.klay.defaultAccount;
undefined
​
// set the default account
> caver.klay.defaultAccount = '0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe';
## accountCreated
caver.klay.accountCreated(address [, defaultBlock] [, callback])
Returns true if the account associated with the address is created. It returns false otherwise.

Parameters

Name

Type

Description

address

String

The address of the account you want to query to see if it has been created on the network.

defaultBlock

Number | String

(optional) If you pass this parameter, it will not use the default block set with caver.klay.defaultBlock.

callback

Function

(optional) Optional callback, returns an error object as the first parameter and the result as the second.

Return Value

Promise returns Boolean - The existence of an input address.

Example

> caver.klay.accountCreated('0x7e6ea9e6f24567cd9edb92e6e2d9b94bdae8a47f').then(console.log);
true
​
> caver.klay.accountCreated('0x6a616d696e652e6b6c6179746t00000000000000').then(console.log);
false
## getAccount
caver.klay.getAccount(address[, defaultBlock] [, callback])
Returns the account information of a given address. There are two different account types in Klaytn: Externally Owned Account (EOA) and Smart Contract Account. See Klaytn Accounts.

Parameters

Name

Type

Description

address

String

The address of the account for which you want to get account information.

defaultBlock

Number | String

(optional) If you pass this parameter, it will not use the default block set with caver.klay.defaultBlock.

callback

Function

(optional) Optional callback, returns an error object as the first parameter and the result as the second.

Return Value

Promise returns a JSON object - A JSON object that contains the account information.

Example

> caver.klay.getAccount('0x52791fcf7900a64a6bcab8b89a78ae4cc60da01c').then(console.log);
{ 
  accType: 1,
  account:
  { 
     nonce: 3,
     balance: '0x446c3b15f9926687c8e202d20c14b7ffe02e7e3000',
     humanReadable: false,
     key: { keyType: 1, key: {} } 
  } 
}
​
> caver.klay.getAccount('0x52791fcf7900a64a6bcab8b89a78ae4cc60da01c', 'latest').then(console.log);
{ 
  accType: 1,
  account:
  { 
     nonce: 3,
     balance: '0x446c3b15f9926687c8e202d20c14b7ffe02e7e3000',
     humanReadable: false,
     key: { keyType: 1, key: {} } 
  } 
}
## getAccounts
caver.klay.getAccounts([callback])
Returns a list of accounts that the node controls.

Parameters

Name

Type

Description

callback

Function

(optional) Optional callback, returns an error object as the first parameter and the result as the second.

Return Value

Promise returns Array - An array of addresses controlled by node.

Example

> caver.klay.getAccounts().then(console.log);
["0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe", "0xDCc6960376d6C6dEa93647383FfB245CfCed97Cf"]
## getAccountKey
caver.klay.getAccountKey(address [, defaultBlock] [, callback])
Returns the account key of the Externally Owned Account (EOA) at a given address. If the account has AccountKeyLegacy or the account of the given address is a Smart Contract Account, it will return an empty key value. See Account Key.

Parameters

Name

Type

Description

address

String

The address of the account for which you want to get accountKey.

defaultBlock

Number | String

(optional) If you pass this parameter, it will not use the default block set with caver.klay.defaultBlock.

callback

Function

(optional) Optional callback, returns an error object as the first parameter and the result as the second.

Return Value

Promise returns Object - The account key consist of public key(s) and a key type.

Example

// AccountKey type: AccountKeyLegacy
> caver.klay.getAccountKey('0x7e6ea9e6f24567cd9edb92e6e2d9b94bdae8a47f').then(console.log);
{ KeyType: 1, Key: {} }
​
// AccountKey type: AccountKeyPublic
> caver.klay.getAccountKey('0x6a616d696e652e6b6c6179746t00000000000000').then(console.log);
{
  KeyType: 2,
  Key:{
    X:'0xb9a4b266083c05deb3ce95055510c34c84b8bb2ad1e0a687fafaf15118511e59',
    Y:'0x7a28526d3d076d019f8856a56f1fefff33c6100e9f3a190e85d9c754aae7513d'
  }
}
## getBalance
caver.klay.getBalance(address [, defaultBlock] [, callback])
Gets the balance of an address at a given block.

Parameters

Name

Type

Description

address

String

The address to get the balance of.

defaultBlock

Number | String

(optional) If you pass this parameter, it will not use the default block set with caver.klay.defaultBlock.

callback

Function

(optional) Optional callback, returns an error object as the first parameter and the result as the second.

Return Value

Promise returns String - The current balance for the given address in peb.

Example

> caver.klay.getBalance("0x407d73d8a49eeb85d32cf465507dd71d507100c1").then(console.log);
"1000000000000"
## getCode
caver.klay.getCode(address [, defaultBlock] [, callback])
Gets the code at a specific address.

Parameters

Name

Type

Description

address

String

The address to get the code from.

defaultBlock

Number | String

(optional) If you pass this parameter, it will not use the default block set with caver.klay.defaultBlock.

callback

Function

(optional) Optional callback, returns an error object as the first parameter and the result as the second.

Return Value

Promise returns String - The data at given address address.

Example

> caver.klay.getCode("0xd5677cf67b5aa051bb40496e68ad359eb97cfbf8").then(console.log);
"0x600160008035811a818181146012578301005b601b6001356025565b8060005260206000f25b600060078202905091905056"
## getTransactionCount
caver.klay.getTransactionCount(address [, defaultBlock] [, callback])
Gets the number of transactions sent from this address.

Parameters

Name

Type

Description

address

String

The address to get the number of transactions from.

defaultBlock

Number | String

(optional) If you pass this parameter, it will not use the default block set with caver.klay.defaultBlock.

callback

Function

(optional) Optional callback, returns an error object as the first parameter and the result as the second.

Return Value

Type

Description

Number

The number of transactions sent from the given address.

Example

> caver.klay.getTransactionCount("0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe")
  .then(console.log);
1
## isContractAccount
caver.klay.isContractAccount(address [, defaultBlock] [, callback])
Returns true if an input account has a non-empty codeHash at the time of a specific block number. It returns false if the account is an EOA or a smart contract account which doesn't have codeHash.

Parameters

Name

Type

Description

address

String

The address of the account you want to check for isContractAccount.

defaultBlock

Number | String

(optional) If you pass this parameter, it will not use the default block set with caver.klay.defaultBlock.

callback

Function

(optional) Optional callback, returns an error object as the first parameter and the result as the second.

Return Value

Promise returns Boolean - true means the input parameter is an existing smart contract address.

Example

> caver.klay.isContractAccount('0x7e6ea9e6f24567cd9edb92e6e2d9b94bdae8a47f').then(console.log);
true
​
> caver.klay.isContractAccount('0x407d73d8a49eeb85d32cf465507dd71d507100c1').then(console.log);
false
