# caver.klay.accounts

caver.klay.accounts contains functions to generate Klaytn accounts and sign transactions and data.

## create
caver.klay.accounts.create([entropy])
Generates an account object with private key and public key.

Parameters

Name

Type

Description

entropy

String

(optional) A random string to increase entropy. If none is given, a random string will be generated using randomHex.

Return Value

Object - The account object with the following structure:

Name

Type

Description

address

String

The account address.

privateKey

String

The accounts private key. This should never be shared or stored unencrypted in local storage! Also make sure to null the memory after usage.

signTransaction(tx [, callback])

Function

The function to sign transactions. See caver.klay.accounts.signTransaction.

sign(data)

Function

The function to sign transactions. See caver.klay.accounts.sign.

encrypt

Function

The function to encrypt private key with given password.

Example

> caver.klay.accounts.create();
{
    address: '0x79FF91738661760AC67b3E951c0B4f1F70F80478',
    privateKey: '0x{private key}',
    signTransaction: [Function: signTransaction],
    sign: [Function: sign],
    encrypt: [Function: encrypt],
    getKlaytnWalletKey: [Function: getKlaytnWalletKey] 
}
​
> caver.klay.accounts.create('entropy');
{
    address: '0x205fffB1025F4af604fEB1d3a22b46C0D2326585',
    privateKey: '0x{private key}',
    signTransaction: [Function: signTransaction],
    sign: [Function: sign],
    encrypt: [Function: encrypt],
    getKlaytnWalletKey: [Function: getKlaytnWalletKey] 
}
​
> caver.klay.accounts.create(caver.utils.randomHex(32));
{ 
    address: '0x62Ca8964610A9D447E1a64753a09fC8b3D40b405',
    privateKey: '0x{private key}',
    signTransaction: [Function: signTransaction],
    sign: [Function: sign],
    encrypt: [Function: encrypt],
    getKlaytnWalletKey: [Function: getKlaytnWalletKey] 
}
## privateKeyToAccount
caver.klay.accounts.privateKeyToAccount(privateKey)
Creates an account object from a private key.

Parameters

Name

Type

Description

privateKey

string

The private key to convert.

Return Value

Object - The account object

Example

> caver.klay.accounts.privateKeyToAccount('0x{private key}');
{ 
    address: '0x62ca8964610a9d447e1a64753a09fc8b3d40b405',
    privateKey: '0x{private key}',
    signTransaction: [Function: signTransaction],
    sign: [Function: sign],
    encrypt: [Function: encrypt],
    getKlaytnWalletKey: [Function: getKlaytnWalletKey] 
}
## privateKeyToPublicKey
caver.klay.accounts.privateKeyToPublicKey(privateKey)
Gets public key from a given private key

Parameters

Name

Type

Description

privateKey

string

The private key to convert.

Return Value

String - The public key (64 bytes)

Example

> caver.klay.accounts.privateKeyToPublicKey('0x{private key}')
'0xbb1846722a4c27e71196e1a44611ee7174276a6c51c4830fb810cac64b0725f217cb8783625a809d1303adeeec2cf036ab74098a77a6b7f1003486e173b29aa7'
## signTransaction
caver.klay.accounts.signTransaction(tx, privateKey [, callback])
Signs a Klaytn transaction with a given private key.

Parameters

Name

Type

Description

tx

Object

The transaction object.  The fields of the transaction object are different for each transaction type. For a description of each transaction, see caver.klay.sendTransaction.

privateKey

String

The private key to sign with.

callback

Function

(optional) Optional callback, returns an error object as the first parameter and the result as the second.

Return Value

Promise returning Object: The signed data RLP encoded transaction, or if returnSignature is true the signature values as follows:

Name

Type

Description

messageHash

String

The hash of the given message.

r

String

First 32 bytes of the signature.

s

String

Next 32 bytes of the signature.

v

String

Recovery value + 27.

rawTransaction

String

The RLP encoded transaction, ready to be send using caver.klay.sendSignedTransaction.

txHash

32-byte String

Hash of the transaction.

senderTxHash

32-byte String

Hash of a transaction that is signed only by the sender. See SenderTxHash​

Example

> caver.klay.accounts.signTransaction({
      type: 'VALUE_TRANSFER',
      from: '0xab0833d744a8943fe3c783f9cc70c13cbd70fcf4',
      to: '0xa9d2cc2bb853163b6eadfb6f962d72f7e00bc2e6',
      value: caver.utils.toPeb(1, 'KLAY'),
      gas: 900000,
    }, '0x{private key}').then(console.log)
{ 
     messageHash: '0xa803f112f4bb7f0514bba08004df291e4d7b964a66decc616bcca10c4843aa60',
     v: '0x4e44',
     r: '0xb895e0aed7117d289b3adcb65869ead9e548bc2d62205bdf003f35e73b00b4b2',
     s: '0x74d899225baf65c6de256c7c0f0a7b55f7ccdfbcdb9656bc402f3cb7cdfe6db3',
     rawTransaction: '0x08f887808505d21dba00830dbba094a9d2cc2bb853163b6eadfb6f962d72f7e00bc2e6880de0b6b3a764000094ab0833d744a8943fe3c783f9cc70c13cbd70fcf4f847f845824e44a0b895e0aed7117d289b3adcb65869ead9e548bc2d62205bdf003f35e73b00b4b2a074d899225baf65c6de256c7c0f0a7b55f7ccdfbcdb9656bc402f3cb7cdfe6db3',
     txHash: '0x55547ac7620ba718e911aa4db745424e8bd280f063f6c59dc4ff3769f45f501f',
     senderTxHash: '0x55547ac7620ba718e911aa4db745424e8bd280f063f6c59dc4ff3769f45f501f'
}
## recoverTransaction
caver.klay.accounts.recoverTransaction(rawTransaction)
Recovers the Klaytn address that was used to sign the given RLP encoded transaction.

Parameters

Name

Type

Description

signature

String

The RLP encoded transaction.

Return Value

Type

Description

String

The Klaytn address used to sign this transaction.

Example

> caver.klay.accounts.recoverTransaction('0xf86180808401ef364594f0109fc8df283027b6285cc889f5aa624eac1f5580801ca031573280d608f75137e33fc14655f097867d691d5c4c44ebe5ae186070ac3d5ea0524410802cdc025034daefcdfa08e7d2ee3f0b9d9ae184b2001fe0aff07603d9');
'0xF0109fC8DF283027b6285cc889F5aA624EaC1F55'
## hashMessage
caver.klay.accounts.hashMessage(message)
Hashes the given message in order for it to be passed to caver.klay.accounts.recover. The data will be UTF-8 HEX decoded and enveloped as follows:

"\x19Klaytn Signed Message:\n" + message.length + message
and hashed using keccak256.

Parameters

Name

Type

Description

message

String

A message to hash.  If it is a HEX string, it will be UTF-8 decoded first.

Return Value

Type

Description

String

The hashed message

Example

> caver.klay.accounts.hashMessage("Hello World")
'0xf334bf277b674260e85f1a3d2565d76463d63d29549ef4fa6d6833207576b5ba'
​
// the below results in the same hash
> caver.klay.accounts.hashMessage(caver.utils.utf8ToHex("Hello World"))
'0xf334bf277b674260e85f1a3d2565d76463d63d29549ef4fa6d6833207576b5ba'
## sign
caver.klay.accounts.sign(data, privateKey)
Signs arbitrary data. This data is before UTF-8 HEX decoded and enveloped as follows:

"\x19Klaytn Signed Message:\n" + message.length + message
Parameters

Name

Type

Description

data

String

The data to sign.

privateKey

String

The private key to sign with.

Return Value

String|Object: The signed data RLP encoded signature. The signature values as follows:

Name

Type

Description

message

String

The given message.

messageHash

String

The hash of the given message.

r

String

First 32 bytes of the signature.

s

String

Next 32 bytes of the signature.

v

String

Recovery value + 27

signature

String

The generated signature.

Example

> caver.klay.accounts.sign('Some data', '0x{private key}');
{
    message: 'Some data',
    messageHash: '0x8ed2036502ed7f485b81feaec1c581d236a8b711e55a24077724879c8a263c2a',
    v: '0x1b',
    r: '0x4a57bcff1637346a4323a67acd7a478514d9f00576f42942d50a5ca0e4b0342b',
    s: '0x5914e19a8ebc10ce1450b00a3b9c1bf0ce01909bca3ffdead1aa3a791a97b5ac',
    signature: '0x4a57bcff1637346a4323a67acd7a478514d9f00576f42942d50a5ca0e4b0342b5914e19a8ebc10ce1450b00a3b9c1bf0ce01909bca3ffdead1aa3a791a97b5ac1b'
}
## recover
caver.klay.accounts.recover(signatureObject)
caver.klay.accounts.recover(message, signature [, preFixed])
caver.klay.accounts.recover(message, v, r, s [, preFixed])
Recovers the Klaytn address that was used to sign the given data.

Parameters

Name

Type

Description

message | signatureObject

String | Object

Either signed message or hash. For the details of the signature object, see the table below.

messageHash

String

The hash of the given message.

signature

String

The raw RLP encoded signature, OR parameter 2-4 as v, r, s values.

preFixed

Boolean

(optional, default: false) If the last parameter is true, the given message will NOT automatically be prefixed with "\x19Klaytn Signed Message:\n" + message.length + message, and assumed to be already prefixed.

The signature object has following values:

Name

Type

Description

messageHash

String

The hash of the given message already prefixed with "\x19Klaytn Signed Message:\n" + message.length + message.

r

String

First 32 bytes of the signature.

s

String

Next 32 bytes of the signature.

v

String

Recovery value + 27

Return Value

Type

Description

String

The Klaytn address used to sign this data.

Example

> caver.klay.accounts.recover({
      messageHash: '0x8ed2036502ed7f485b81feaec1c581d236a8b711e55a24077724879c8a263c2a',
      v: '0x1b',
      r: '0x4a57bcff1637346a4323a67acd7a478514d9f00576f42942d50a5ca0e4b0342b',
      s: '0x5914e19a8ebc10ce1450b00a3b9c1bf0ce01909bca3ffdead1aa3a791a97b5ac',
  })
'0x2c7536E3605D9C16a7a3D7b1898e529396a65c23'
​
// message, signature
> caver.klay.accounts.recover('Some data', '0x4a57bcff1637346a4323a67acd7a478514d9f00576f42942d50a5ca0e4b0342b5914e19a8ebc10ce1450b00a3b9c1bf0ce01909bca3ffdead1aa3a791a97b5ac1b');
'0x2c7536E3605D9C16a7a3D7b1898e529396a65c23'
​
// message, v, r, s
> caver.klay.accounts.recover('Some data', '0x1b', '0x4a57bcff1637346a4323a67acd7a478514d9f00576f42942d50a5ca0e4b0342b', '0x5914e19a8ebc10ce1450b00a3b9c1bf0ce01909bca3ffdead1aa3a791a97b5ac');
'0x2c7536E3605D9C16a7a3D7b1898e529396a65c23'
## encrypt
caver.klay.accounts.encrypt(privateKey, password [, options])
Encrypts a private key to the Klaytn keystore v3 standard.

Parameters

Name

Type

Description

privateKey

String

A private key or a Klaytn wallet key to encrypt.

password

String

The password used for encryption.

options

Object

(optional) The options parameter allows you to specify the values to use when using encrypt. You can also use the options object to encrypt decoupled accounts. See the example below for usage of options.

NOTE: There are two ways to encrypt the private key when an account has a decoupled private key from the address. 1. Use the KlaytnWalletKey format with the privateKey parameter. 2. Use the options.address to send the address as a parameter.

Return Value

Type

Description

Object

The encrypted keystore v3 JSON.

Example

> caver.klay.accounts.encrypt('0x{private key}', 'test!');
{
    version: 3,
    id: '04e9bcbb-96fa-497b-94d1-14df4cd20af6',
    address: '2c7536e3605d9c16a7a3d7b1898e529396a65c23',
    crypto: {
        ciphertext: 'a1c25da3ecde4e6a24f3697251dd15d6208520efc84ad97397e906e6df24d251',
        cipherparams: { iv: '2885df2b63f7ef247d753c82fa20038a' },
        cipher: 'aes-128-ctr',
        kdf: 'scrypt',
        kdfparams: {
            dklen: 32,
            salt: '4531b3c174cc3ff32a6a7a85d6761b410db674807b2d216d022318ceee50be10',
            n: 262144,
            r: 8,
            p: 1
        },
        mac: 'b8b010fff37f9ae5559a352a185e86f9b9c1d7f7a9f1bd4e82a5dd35468fc7f6'
    }
}
​
// Encrypt decoupled account - 1. Use the KlaytnWalletKey format with the privateKey parameter.
> caver.klay.accounts.encrypt('0x{private key}0x{type}0x{address in hex}', 'test');
{ 
    version: 3,
    id: '432b16f6-bf4e-4a10-af79-d6ad644b9d84',
    address: '0x3bd32d55e64d6cbe54bec4f5200e678ee8d1a990',  
    crypto: { 
        ciphertext: 'a82029d303ad21218bb51d215a88cad0ed08ee5b10016b8caf8d72163bfa6ef4',
        cipherparams: { iv: '0699a7176af8def3dc5d403c4e03f1e4' },
        cipher: 'aes-128-ctr',
        kdf: 'scrypt',
        kdfparams: { 
            dklen: 32,
            salt: '4654e7e4827221bfb7d963259f5491ecc2fced50cd24378de647a7087757c3ab', 
            n: 4096,
            r: 8,
            p: 1 
        },
        mac: '6bbc9ac1f558ae769d1977f03c6c7f71e83485bd3373866122c456be1744fddf' 
    } 
}
​
// Encrypt decoupled account - 2. Use the options to send the address as a parameter.
> caver.klay.accounts.encrypt('0x{private key}', 'test', { address: '0x7d46813010aee975946d6ee9c7fb887eef6b318d' });
{ 
    version: 3,
    id: '47a3ab30-d50e-4db6-8763-d91c0bfe029b',
    address: '0x7d46813010aee975946d6ee9c7fb887eef6b318d',
    crypto: { 
        ciphertext: '92b585bfd5c50634910e83e38261445036b3262d35f1ed5128be0ece69ca9d66',
        cipherparams: { iv: 'd97d47ed3a8dd5ecf3944b254729dc5f' },
        cipher: 'aes-128-ctr',
        kdf: 'scrypt',
        kdfparams: { 
            dklen: 32,
            salt: 'f736b6a1c32e602f910717e198e7da9a3bd7e39fa6962b3c3f5ade8027ebbab4',
            n: 4096,
            r: 8,
            p: 1 
        },
        mac: '8cdca022bfd580d72d250f4e296035339faa8c4d9eaa1f29d8cd441bec3f205b' 
    } 
}
​
// Using options objects with encryption option values
> caver.klay.accounts.encrypt('0x{private key}', 'test', {
      salt: '776ad46fde47572c58ba5b9616a661a1fbc4b9ff918300faeba04bb9ff5be04c',
      iv: Buffer.from('b62ef75e39fa396de62c51c4734b69a2', 'hex'),
      kdf: 'scrypt',
      dklen: 32,
      n: 262144,
      r: 8,
      p: 1,
      cipher: 'aes-128-cbc',
      uuid: Buffer.from('f0b40ab7d69fdd9606e2a5242dddd813', 'hex'),
    })
{ 
    version: 3,
    id: 'f0b40ab7-d69f-4d96-86e2-a5242dddd813',
    address: '0xdac9f72e27f05eca08df7a2ea2d044b3ed3a6e54',
    crypto: { 
        ciphertext: 'de3199afd50051ecef60675b3cc60170670e84945a5571cb2ec414b628a28c71844f7144c02301db9b41044c1f262562',
        cipherparams: { iv: 'b62ef75e39fa396de62c51c4734b69a2' },
        cipher: 'aes-128-cbc',
        kdf: 'scrypt',
        kdfparams: { 
            dklen: 32,
            salt: '776ad46fde47572c58ba5b9616a661a1fbc4b9ff918300faeba04bb9ff5be04c',
            n: 262144,
            r: 8,
            p: 1 
        },
        mac: 'a3c3bbc90b5c8f0ae019e428a4081c39f91876adf8441d51cafbbe37ca839b8c' 
    } 
}
​
> caver.klay.accounts.encrypt('0x{private key}', 'test', {
      salt: '776ad46fde47572c58ba5b9616a661a1fbc4b9ff918300faeba04bb9ff5be04c',
      iv: Buffer.from('b62ef75e39fa396de62c51c4734b69a2', 'hex'),
      kdf: 'pbkdf2',
      dklen: 32,
      c: 262144,
      cipher: 'aes-128-cbc',
      uuid: Buffer.from('f0b40ab7d69fdd9606e2a5242dddd813', 'hex'),
    })
{ 
    version: 3,
    id: 'f0b40ab7-d69f-4d96-86e2-a5242dddd813',
    address: '0xdac9f72e27f05eca08df7a2ea2d044b3ed3a6e54',
    crypto: { 
        ciphertext: '8b4b480b003af59210ba8c8815425955274c395b27e5354f7eef870f3e8ddc0e4c97bd4a30e8b60337aea2fdbbd50009',
        cipherparams: { iv: 'b62ef75e39fa396de62c51c4734b69a2' },
        cipher: 'aes-128-cbc',
        kdf: 'pbkdf2',
        kdfparams: { 
            dklen: 32,
            salt: '776ad46fde47572c58ba5b9616a661a1fbc4b9ff918300faeba04bb9ff5be04c',
            c: 262144,
            prf: 'hmac-sha256' 
        },
        mac: 'c19e889b887812920d2453bbcb87640a6246e49fc513f2d927954edab73fefab' 
    } 
}
## decrypt
caver.klay.accounts.decrypt(keystoreJsonV3, password)
Decrypts a keystore v3 JSON and returns the decrypted account object.

Parameters

Name

Type

Description

keystoreJsonV3

String

JSON string containing the encrypted private key to decrypt.

password

String

The password used for encryption.

Return Value

Type

Description

Object

The decrypted account.

Example

> caver.klay.accounts.decrypt({
     version: 3,
     id: '04e9bcbb-96fa-497b-94d1-14df4cd20af6',
     address: '2c7536e3605d9c16a7a3d7b1898e529396a65c23',
     crypto: {
         ciphertext: 'a1c25da3ecde4e6a24f3697251dd15d6208520efc84ad97397e906e6df24d251',
         cipherparams: { iv: '2885df2b63f7ef247d753c82fa20038a' },
         cipher: 'aes-128-ctr',
         kdf: 'scrypt',
         kdfparams: {
             dklen: 32,
             salt: '4531b3c174cc3ff32a6a7a85d6761b410db674807b2d216d022318ceee50be10',
             n: 262144,
             r: 8,
             p: 1
         },
         mac: 'b8b010fff37f9ae5559a352a185e86f9b9c1d7f7a9f1bd4e82a5dd35468fc7f6'
     }
  }, 'test!');
{ 
    address: '2c7536e3605d9c16a7a3d7b1898e529396a65c23',
    privateKey: '0x{private key}',
    signTransaction: [Function: signTransaction],
    sign: [Function: sign],
    encrypt: [Function: encrypt],
    getKlaytnWalletKey: [Function: getKlaytnWalletKey]
}
## wallet
caver.klay.accounts.wallet
Contains an in-memory wallet with multiple accounts. These accounts can be used when using caver.klay.sendTransaction.

Example

> caver.klay.accounts.wallet;
Wallet {
  '0':
   { address: '0xce3bda34a14415f3bc2bcd5e61c48043857a6451',
     privateKey: '0x{private key}',
     signTransaction: [Function: signTransaction],
     sign: [Function: sign],
     encrypt: [Function: encrypt],
     getKlaytnWalletKey: [Function: getKlaytnWalletKey],
     index: 0 },
  _accounts: Accounts { ... },
  length: 1,
  defaultKeyName: 'caverjs_wallet',
  '0xce3bda34a14415f3bc2bcd5e61c48043857a6451': { ... },
  '0XCE3BDA34A14415F3BC2BCD5E61C48043857A6451': { ... },
  '0xce3bDa34A14415F3BC2bCd5E61C48043857a6451': { ... } 
}
## wallet.create
caver.klay.accounts.wallet.create([numberOfAccounts] [, entropy])
Generates one or more accounts in the wallet with randomly generated key pairs. If wallets already exist, they will not be overridden.

Parameters

Name

Type

Description

numberOfAccounts

Number

(optional) The number of accounts to create. Leave empty to create an empty wallet.

entropy

String

(optional) A random string to increase entropy. If none is given, a random string will be generated using randomHex.

Return Value

Type

Description

Object

The wallet object.

Example

> caver.klay.accounts.wallet.create(1, 'entropy');
Wallet {
  '0': { ... },
  _accounts: Accounts { ... },
  length: 1,
  defaultKeyName: 'caverjs_wallet',
  '0xc89cdd4258e17471fbaf75283b6a952451eb7f54': { ... },
  '0XC89CDD4258E17471FBAF75283B6A952451EB7F54': { ... },
  '0xC89cDD4258e17471fBaf75283b6A952451Eb7f54': { ... }
## wallet.add
caver.klay.accounts.wallet.add(account [, targetAddress])
Adds an account using a private key or account object to the wallet.

NOTE: If the same address exists inside the wallet, an error is returned. If you want to change the private key associated to an account in the wallet, please use caver.klay.accounts.wallet.updatePrivateKey.

Parameters

Name

Type

Description

account

String | Object

A private key or account object created with caver.klay.accounts.create.

targetAddress

String

A target address which will be used with a given private key.

NOTE: caver-js supports two types of private key formats. One is a raw private key format of a 32-byte string type and the other is the KlaytnWalletKey.

Return Value

Type

Description

Object

The added account.

Example

> caver.klay.accounts.wallet.add('0x{private key}');
{ 
    address: '0xdac9f72e27f05eca08df7a2ea2d044b3ed3a6e54',
    privateKey: '0x{private key}',
    signTransaction: [Function: signTransaction],
    sign: [Function: sign],
    encrypt: [Function: encrypt],
    getKlaytnWalletKey: [Function: getKlaytnWalletKey],
    index: 4 
}
​
// Use key '0x{private key}' as a private key
// for address '0xfe9157e180c8f4c229e88d0c1763a746db8b19b4'
> caver.klay.accounts.wallet.add('0x{private key}', '0xfe9157e180c8f4c229e88d0c1763a746db8b19b4');
{ 
    address: '0xfe9157e180c8f4c229e88d0c1763a746db8b19b4',
    privateKey: '0x{private key}',
    signTransaction: [Function: signTransaction],
    sign: [Function: sign],
    encrypt: [Function: encrypt],
    getKlaytnWalletKey: [Function: getKlaytnWalletKey],
    index: 5
}
​
> caver.klay.accounts.wallet.add({
      privateKey: '0x{private key}',
      address: '0xb8CE9ab6943e0eCED004cDe8e3bBed6568B2Fa01'
  });
{ 
    address: '0xb8CE9ab6943e0eCED004cDe8e3bBed6568B2Fa01',
    privateKey: '0x{private key}',
    signTransaction: [Function: signTransaction],
    sign: [Function: sign],
    encrypt: [Function: encrypt],
    getKlaytnWalletKey: [Function: getKlaytnWalletKey],
    index: 6
}
​
// Add wallet with KlaytnWalletKey format
> caver.klay.accounts.wallet.add('0x{private key}0x{type}0x{address in hex}');
{ 
    address: '0x3bd32d55e64d6cbe54bec4f5200e678ee8d1a990',
    privateKey: '0x{private key}',
    signTransaction: [Function: signTransaction],
    sign: [Function: sign],
    encrypt: [Function: encrypt],
    getKlaytnWalletKey: [Function: getKlaytnWalletKey],
    index: 1 
}
## wallet.remove
caver.klay.accounts.wallet.remove(account)
Removes an account from the wallet.

Parameters

Name

Type

Description

account

String | Number

The account address or the index in the wallet.

Return Value

Type

Description

Boolean

true if the wallet was removed. false if it could not be found.

Example

> caver.klay.accounts.wallet;
Wallet {
  '0': { ... },
  _accounts: Accounts { ... },
  length: 1,
  defaultKeyName: 'caverjs_wallet',
  '0xce3bda34a14415f3bc2bcd5e61c48043857a6451': { ... },
  '0XCE3BDA34A14415F3BC2BCD5E61C48043857A6451': { ... },
  '0xce3bDa34A14415F3BC2bCd5E61C48043857a6451': { ... } 
}
​
> caver.klay.accounts.wallet.remove('0xce3bda34a14415f3bc2bcd5e61c48043857a6451');
true
​
> caver.klay.accounts.wallet.remove(3);
false
## wallet.clear
caver.klay.accounts.wallet.clear()
Securely empties the wallet and removes all its accounts.

Parameters

None

Return Value

Type

Description

Object

The wallet object.

Example

> caver.klay.accounts.wallet.clear();
Wallet {
  _accounts: Accounts { ... },
  length: 0,
  defaultKeyName: 'caverjs_wallet' 
}
## wallet.encrypt
caver.klay.accounts.wallet.encrypt(password)
Encrypts all wallet accounts and returns an array of encrypted keystore v3 objects.

Parameters

Name

Type

Description

password

String

The password that will be used for encryption.

Return Value

Type

Description

Array

The encrypted keystore v3 objects.

Example

> caver.klay.accounts.wallet.encrypt('test');
[ 
    { 
        version: 3,
        id: '2b334f59-a0bc-446c-9f25-c934e432e832',
        address: '0x57629b4a9dc137f15400a3d96ab9e1e57b7f57c7',
        crypto: { 
            ciphertext: '9ca62a29f0f634ca63dfab40a4631f9fabb689ae60e4bfb475c58c69ad060543',
            cipherparams: { iv: '3d924a71a7b4db0f2f8456068c1c7b8e' },
            cipher: 'aes-128-ctr',
            kdf: 'scrypt',
            kdfparams: { 
                dklen: 32,
                salt: '42628f28de6aa8b988c425fa97d8f790ac26a6f89b44b0321c56101e7fb8bbcf',
                n: 4096,
                r: 8,
                p: 1 
                },
            mac: 'a35bc8f650aa1ff0d2316de7be1494927851e19b3e817cd16482a442912f133b' 
        } 
    },
    { 
        version: 3,
        id: '9b8b4e4f-e72c-4a28-af57-38b6838b5533',
        address: '0x4fb4006448106831a7c8c8e0d0139e05550f3d3e',
        crypto: { 
            ciphertext: '65b9350969efdfeadb357145c97992b67c4114bd1d24592e8c62dbddfab2a49f',
            cipherparams: { iv: 'b9d19c69a62745b3db409ff0879669a2' },
            cipher: 'aes-128-ctr',
            kdf: 'scrypt',
            kdfparams: { 
                dklen: 32,
                salt: '914a4628a991f521d547a9da593b5daa63a1a82fcafe0282c09e80967874f36c',
                n: 4096,
                r: 8,
                p: 1 
            },
            mac: 'a9de2c54c4b29807fd21d40fe79f556a7d5b771045cbbda0a943d3ced4cacafc' 
        } 
    } 
]
## wallet.decrypt
caver.klay.accounts.wallet.decrypt(keystoreArray, password)
Decrypts keystore v3 objects.

Parameters

Name

Type

Description

keystoreArray

Array

The encrypted keystore v3 objects to decrypt.

password

String

The password that was used for encryption.

Return Value

Type

Description

Object

The wallet object.

Example

> caver.klay.accounts.wallet.decrypt([ 
    { 
        version: 3,
        id: '2b334f59-a0bc-446c-9f25-c934e432e832',
        address: '0x57629b4a9dc137f15400a3d96ab9e1e57b7f57c7',
        crypto: { 
            ciphertext: '9ca62a29f0f634ca63dfab40a4631f9fabb689ae60e4bfb475c58c69ad060543',
            cipherparams: { iv: '3d924a71a7b4db0f2f8456068c1c7b8e' },
            cipher: 'aes-128-ctr',
            kdf: 'scrypt',
            kdfparams: { 
                dklen: 32,
                salt: '42628f28de6aa8b988c425fa97d8f790ac26a6f89b44b0321c56101e7fb8bbcf',
                n: 4096,
                r: 8,
                p: 1 
                },
            mac: 'a35bc8f650aa1ff0d2316de7be1494927851e19b3e817cd16482a442912f133b' 
        } 
    },
    { 
        version: 3,
        id: '9b8b4e4f-e72c-4a28-af57-38b6838b5533',
        address: '0x4fb4006448106831a7c8c8e0d0139e05550f3d3e',
        crypto: { 
            ciphertext: '65b9350969efdfeadb357145c97992b67c4114bd1d24592e8c62dbddfab2a49f',
            cipherparams: { iv: 'b9d19c69a62745b3db409ff0879669a2' },
            cipher: 'aes-128-ctr',
            kdf: 'scrypt',
            kdfparams: { 
                dklen: 32,
                salt: '914a4628a991f521d547a9da593b5daa63a1a82fcafe0282c09e80967874f36c',
                n: 4096,
                r: 8,
                p: 1 
            },
            mac: 'a9de2c54c4b29807fd21d40fe79f556a7d5b771045cbbda0a943d3ced4cacafc' 
        } 
    } 
], 'test');
Wallet {
  '0': { ... },
  '1': { ... },
  _accounts: Accounts { ... },
  length: 2,
  defaultKeyName: 'caverjs_wallet',
  '0x57629b4a9dc137f15400a3d96ab9e1e57b7f57c7': { ... } ,
  '0X57629B4A9DC137F15400A3D96AB9E1E57B7F57C7': { ... } ,
  '0x57629B4A9DC137F15400A3d96Ab9e1e57B7F57C7': { ... } ,
  '0x4fb4006448106831a7c8c8e0d0139e05550f3d3e': { ... } ,
  '0X4FB4006448106831A7C8C8E0D0139E05550F3D3E': { ... } ,
  '0x4fb4006448106831a7c8C8e0D0139E05550F3D3E': { ... } 
}
## wallet.getKlaytnWalletKey
caver.klay.accounts.wallet.getKlaytnWalletKey(index)
caver.klay.accounts.wallet.getKlaytnWalletKey(address)
Return the Klaytn wallet key for the account on the wallet of caver-js.

Parameters

Name

Type

Description

indexOrAddress

Number|String

An index in the wallet address list, an address in hexadecimal. The given value should exist in the caver-js wallet.

Return Value

Type

Description

String

KlaytnWalletKey that matches the account. This value allows you to log in to the wallet.

Example

// With non-human-readable address
> caver.klay.accounts.wallet.getKlaytnWalletKey(0)
'0x{private key}0x{type}0x{address in hex}'
​
// With index of wallet list
> caver.klay.accounts.wallet.getKlaytnWalletKey(1)
'0x{private key}0x{type}0x{address in hex}'
​
// With an address in hexadecimal
> caver.klay.accounts.wallet.getKlaytnWalletKey('0xa9d40b07a6d06e7b7af6cf9a17fb107c9fc7fe58')
'0x{private key}0x{type}0x{address in hex}'
​
// If the given account does not exist in the caver-js wallet, returns an error.
> caver.klay.accounts.wallet.getKlaytnWalletKey('0x35170d0c774b8c80e9f802a7af6d0497e621c215')
Error: Failed to find account
## wallet.updatePrivateKey
caver.klay.accounts.wallet.updatePrivateKey(privateKey, address)
Update the account's private key information stored in the wallet.

NOTE: This function only changes the information stored in the wallet of caver-js. This function has no effect on the key information stored on the Klaytn network. Keys in the Klaytn network can be changed by sending a 'ACCOUNT_UPDATE' transaction.

Parameters

Name

Type

Description

privateKey

String

New private key to be used for updates.

address

String

The account address in the wallet.

Return Value

Type

Description

Object

An object that contains information about the updated account.

Example

> caver.klay.accounts.wallet.updatePrivateKey('{private key}', '0xf2e2565629c7763dc0b595e8e531a31371a95f95');
{ 
    address: '0xf2e2565629c7763dc0b595e8e531a31371a95f95',
    privateKey: '0x{private key}',
    signTransaction: [Function: signTransaction],
    sign: [Function: sign],
    encrypt: [Function: encrypt],
    getKlaytnWalletKey: [Function: getKlaytnWalletKey],
    index: 0 
}