# Getting Started

## API Reference
If you need more information about caver-java API reference, please refer to our Javadoc.

## Prerequisites
Dependency
maven

<dependency>
  <groupId>com.klaytn.caver</groupId>
  <artifactId>core</artifactId>
  <version>1.0.1</version>
</dependency>
gradle

implementation 'com.klaytn.caver:core:1.0.1'
If you want to use Android dependency, just append -android at the end of the version string. (e.g. 1.0.1-android)

If you want to see details of the JSON-RPC requests and responses, please include LOGBack dependency in your project. Below is a Gradle build file example. You can add the dependency to Maven as well. Since caver-java uses the SLF4J logging facade, you can switch to your preferred logging framework instead of LOGBack.

implementation "ch.qos.logback:logback-classic:1.2.3"
Installation
If you want to generate transactions related with a smart contract, you need to install a Solidity compiler and caver-java commmand-line tool first.

Solidity Compiler
You can install the Solidity compiler locally, following the instructions as per the project documentation. Klaytn recommends you to install Solidity version either 0.4.24 or 0.5.6. If you are a macOS user, you can install the versions via Homebrew:

$ brew install klaytn/klaytn/solidity@0.4.24  # version 0.4.24
$ brew install klaytn/klaytn/solidity@0.5.6   # version 0.5.6
Command-line Tool
The command-line tool allows you to generate Solidity smart contract function wrappers from the command line.

Installation (Homebrew)

Java 1.8+ is required to install this.

$ brew tap klaytn/klaytn
$ brew install caver-java
After installation you can run command 'caver-java' like below:

$ caver-java solidity generate -b <smart-contract>.bin -a <smart-contract>.abi -o <outputPath> -p <packagePath>
Installation (Other)

Currently, we do not support other package managers. As another solution, we provide a method to build the CLI below.

Download or fork caver-java.

Do task 'shadowDistZip' in the console module using Gradle. As a result, console/build/distributions/console-shadow-{version}.zip is generated.

$ ./gradlew :console:shadowDistZip
Unzip the zip file in the build directory

$ unzip ./console/build/distributions/console-shadow-{version}.zip
Execute the binary file to run the command-line tool like below. You can find a shell script file for macOS users and a batch file for Window users.

$ ./console/build/distributions/console-shadow-{version}/bin/caver-java
## Managing Accounts
Creating an Account
In order to sign transactions, you need to have either an EC (Elliptic Curve) key pair or a Klaytn keystore file.

Using an EC Key Pair
You can create a Klaytn account using an EC key pair like below:

KlayCredentials credentials = KlayCredentials.create(Keys.createEcKeyPair());
String privateKey = Numeric.toHexStringWithPrefix(credentials.getEcKeyPair().getPrivateKey()); 
String address = credentials.getAddress();
Using a Keystore File
If you want to create a new account with a keystore file (you can also create a new keystore file in Klaytn Wallet):

KlayWalletUtils.generateNewWalletFile(
        <yourPassword>,
        new File(<walletFilePath>)
);
To load an account using a keystore file like below:

KlayCredentials credentials = KlayWalletUtils.loadCredentials(<password>, <walletFilePath>);
## Sending a Transaction
Getting KLAY via Baobab Faucet
After creating an account, you can receive some Baobab testnet KLAYs for the Baobab testnet via Baobab Faucet, available at https://baobab.wallet.klaytn.com/. The received testnet KLAY will be used for transaction fee later.

Connecting to Baobab
You can use a Klaytn public EN (https://api.baobab.klaytn.net:8651) to connect to the Baobab testnet.

Caver caver  = Caver.build(Caver.BAOBAB_URL);  // Caver.BAOBAB_URL = https://api.baobab.klaytn.net:8651
Sending a Value Transfer Transaction
After you get a Caver instance and create an account which has some KLAY, you can send 1 peb to a certain address(0xe97f27e9a5765ce36a7b919b1cb6004c7209217e) with a gas limit BigInteger.valueOf(100_000) like below:

TransactionManager is introduced to hide the complexity of transaction types. For example, a FeeDelegatedValueTransferTransaction object can be transformed from a ValueTransferTransaction object. For more details, see Fee Delegation. In addition to Fee Delegation, TransactionManager can be used with GetNonceProcessor, ErrorHandler, and TransactionReceiptProcessor.

TransactionManager transactionManager = new TransactionManager.Builder(caver, credentials)
        .setChaindId(ChainId.BAOBAB_TESTNET).build();
​
ValueTransferTransaction valueTransferTransaction = ValueTransferTransaction.create(
        credentials.getAddress(),  // fromAddress
        "0xe97f27e9a5765ce36a7b919b1cb6004c7209217e",  // toAddress
        BigInteger.ONE,  // value
        BigInteger.valueOf(100_000)  // gasLimit
);
​
KlayRawTransaction klayRawTransaction = transactionManager.sign(valueTransferTransaction);
String transactionHash = transactionManager.send(klayRawTransaction);
​
TransactionReceiptProcessor transactionReceiptProcessor = new PollingTransactionReceiptProcessor(caver, 1000, 15);  // pollingSleepDuration = 1000, pollingAttempts = 15
KlayTransactionReceipt.TransactionReceipt transactionReceipt = transactionReceiptProcessor.waitForTransactionReceipt(transactionHash);
If you use ValueTransfer class, you can more easily compose and send a transaction. This is because ValueTransfer class makes the processes above simple like below:

KlayTransactionReceipt.TransactionReceipt transactionReceipt
        = ValueTransfer.create(caver, credentials, ChainId.BAOBAB_TESTNET).sendFunds(
                redentials.getAddress(),  // fromAddress
                "0xe97f27e9a5765ce36a7b919b1cb6004c7209217e",  // toAddress
                BigDecimal.ONE,  // value 
                Convert.Unit.PEB,  // unit 
                BigInteger.valueOf(100_000)  // gasLimit
            ).send();
Checking Receipts
If you send a transaction via sendFunds, caver-java tries to get a transaction receipt by default. After you get a receipt, you can see the following log in the console.

{
   "jsonrpc":"2.0",
   "id":4,
   "result":{
      "blockHash":"0x45542cc3e3bce952f368c5da9d40f972c134fed2b2b6815231b5caf33c79dacd",
      "blockNumber":"0x39a57b",
      "contractAddress":null,
      "from":"0xe97f27e9a5765ce36a7b919b1cb6004c7209217e",
      "gas":"0x186a0",
      "gasPrice":"0x5d21dba00",
      "gasUsed":"0x5208",
      "logs":[],
      "logsBloom":"0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
      "nonce":"0x114e",
      "senderTxHash":"0x3d50b9fa9fec58443f5618ed7e0f5aec5e9a6f7269d9ff606ff87156ca5b4afd",
      "signatures":[
         {
            ...
         }
      ],
      "status":"0x1",
      "to":"0xe97f27e9a5765ce36a7b919b1cb6004c7209217e",
      "transactionHash":"0x3d50b9fa9fec58443f5618ed7e0f5aec5e9a6f7269d9ff606ff87156ca5b4afd",
      "transactionIndex":"0x1",
      "type":"TxTypeValueTransfer",
      "typeInt":8,
      "value":"0x1"
   }
}
In this receipt, you can check the status of the transaction execution. If the 'status' field in the receipt is "0x1", it means the transaction is processed successfully. If not, the transaction failed. The detailed error message is presented in the txError field. For more detail, see txError.

## Sending Other Transaction Types
Account Update
If you want to update the key of the given account to a new AccountKeyPublic key:

AccountUpdateTransaction accountUpdateTransaction = AccountUpdateTransaction.create(
        credentials.getAddress(),  // fromAddress
        AccountKeyPublic.create(
                "0xbf8154a3c1580b5478ceec0aac319055185280ce22406c6dc227f4de85316da1",  // publicKeyX
                "0x0dc8e4b9546adcc6d1f11796e43e478bd7ffbe302917667837179f4da77591d8"  // publicKeyY
        ),  // newAccountKey
        BigInteger.valueOf(100_000)  // gasLimit
);
Account.create(caver, credentials, ChainId.BAOBAB_TESTNET).sendUpdateTransaction(accountUpdateTransaction).send();
An account key represents the key structure associated with an account. To get more details and types about the Klaytn account key, please read Account Key.

Smart Contract
caver-java supports auto-generation of smart contract wrapper code. Using the wrapper, you can easily deploy and execute a smart contract. Before generating a wrapper code, you need to compile the smart contract first (Note: This will only work if a Solidity compiler is installed in your computer. See Solidity Compiler.

$ solc <contract>.sol --bin --abi --optimize -o <output-dir>/
Then, generate the wrapper code using caver-java’s command-line tool.

$ caver-java solidity generate -b <smart-contract>.bin -a <smart-contract>.abi -o <outputPath> -p <packagePath>
Above command will output <smartContract>.java. After generating the wrapper code, you can deploy your smart contract like below:

<smartContract> contract = <smartContract>.deploy(
        caver, credentials, <chainId>, <gasProvider>,
        <param1>, ..., <paramN>).send();
After the smart contract has been deployed, you can create a smart contract instance like below:

<smartContract> contract = <smartContract>.load(
        <deployedContractAddress>, caver, credentials, <chainId>, <gasProvider>
);
To transact with a smart contract:

KlayTransactionReceipt.TransactionReceipt transactionReceipt = contract.<someMethod>(
        <param1>,
        ...).send();
To call a smart contract:

<type> result = contract.<someMethod>(<param1>, ...).send();
Example
This section describes how to deploy and execute a smart contract on the Baobab testnet. In this example, we use a smart contract ERC20Mock. If contract deployment fails and an empty contract address is returned, it will throw RuntimeException.

ERC20Mock erc20Mock = ERC20Mock.deploy(
        caver, credentials, 
        ChainId.BAOBAB_TESTNET,  // chainId
        new DefaultGasProvider(),  // gasProvider
        credentials.getAddress(),  // param1(initialAccount)
        BigInteger.valueOf(100)  // param2(initialBalance)
).send();
String deployedContractAddress = erc20Mock.getContractAddress();
To create an instance of the deployed ERC20Mock contract:

ERC20Mock erc20Mock = ERC20Mock.load(
        deployedContractAddress, 
        caver, credentials, 
        ChainId.BAOBAB_TESTNET,  // chainId 
        new DefaultGasProvider()  // gasProvider
);
If you transfer 10 tokens to a specified address (e.g., 0x2c8ad0ea2e0781db8b8c9242e07de3a5beabb71a), use the following code:

KlayTransactionReceipt.TransactionReceipt transactionReceipt = erc20Mock.transfer(
        "0x2c8ad0ea2e0781db8b8c9242e07de3a5beabb71a",  // toAddress
        BigInteger.valueOf(10)  // value
).send();
To check the balance of the recipient (e.g., 0x2c8ad0ea2e0781db8b8c9242e07de3a5beabb71a), use the code below:

BigInteger balance = erc20Mock.balanceOf(
        "0x2c8ad0ea2e0781db8b8c9242e07de3a5beabb71a"  // owner
).send();
Fee Delegation
Klaytn provides Fee Delegation feature which allows service providers to pay transaction fees instead of the users.

Value Transfer
On the client side, client who initiates the transaction will generate a fee-delegated value transfer transaction as follows: A sender creates a default ValueTransferTransaction object, then transactionManager.sign() returns a signed FeeDelegatedValueTransferTransaction object if the second parameter is set to true.

TransactionManager transactionManager = new TransactionManager.Builder(caver, credentials)
        .setChaindId(ChainId.BAOBAB_TESTNET).build();  // BAOBAB_TESTNET = 1001
ValueTransferTransaction valueTransferTransaction = ValueTransferTransaction.create(
        credentials.getAddress(),  // fromAddress
        "0xe97f27e9a5765ce36a7b919b1cb6004c7209217e",  // toAddress
        BigInteger.ONE,  // value
        BigInteger.valueOf(100_000)  // gasLimit
);
String senderRawTransaction = transactionManager.sign(valueTransferTransaction, true).getValueAsString();  // isFeeDelegated : true
A signed transaction, senderRawTransaction, is generated. Now the sender delivers the transaction to the fee payer who will pay for the transaction fee instead. Transferring transactions between the sender and the fee payer is not performed on the Klaytn network. The protocol should be defined by themselves.

After the fee payer gets the transaction from the sender, the fee payer can send the transaction using the FeePayerManager class as follows. FeePayerManager.executeTransaction() will sign the received transaction with the fee payer's private key and send the transaction to the Klaytn network.

KlayCredentials feePayer = KlayWalletUtils.loadCredentials(<password>, <walletfilePath>);
FeePayerManager feePayerManager = new FeePayerManager.Builder(caver, feePayer).build();
feePayerManager.executeTransaction(senderRawTransaction);
Smart Contract Execution
The difference between fee-delegated smart contract execution and fee-delegated value transfer above is that this needs input data to call a function of a smart contract. A sender can generate a fee-delegated smart contract execution transaction as shown below. Note that transactionManager.sign() returns a TxTypeFeeDelegatedSmartContractExecution object if you pass true to the second parameter. The example below invokes the transfer method of ERC20Mock contract which is described in Smart Contract.

String recipient = "0x34f773c84fcf4a0a9e2ef07c4615601d60c3442f";
BigInteger transferValue = BigInteger.valueOf(20);
Function function = new Function(
        ERC20Mock.FUNC_TRANSFER,  // FUNC_TRANSFER = "transfer"
        Arrays.asList(new Address(recipient), new Uint256(transferValue)),  // inputParameters
        Collections.emptyList()  // outputParameters
);
String data = FunctionEncoder.encode(function);
​
TransactionManager transactionManager = new TransactionManager.Builder(caver, credentials)
        .setChaindId(ChainId.BAOBAB_TESTNET).build();  // BAOBAB_TESTNET = 1001
SmartContractExecutionTransaction smartContractExecution = 
        SmartContractExecutionTransaction.create(
                credentials.getAddress(),  // fromAddress
                erc20Mock.getContractAddress(),  // contractAddress
                BigInteger.ZERO,  // value
                Numeric.hexStringToByteArray(data),  // data
                BigInteger.valueOf(100_000)  // gasLimit
        );
String senderRawTransaction = transactionManager.sign(smartContractExecution, true).getValueAsString();
After you get senderRawTransaction, the rest of the process using FeePayerManager is the same way as you saw in fee-delegated value transfer above:

KlayCredentials feePayer = KlayWalletUtils.loadCredentials(<password>, <walletfilePath>);
FeePayerManager feePayerManager = new FeePayerManager.Builder(caver, feePayer).build();
feePayerManager.executeTransaction(senderRawTransaction);
## Porting from web3j
We made caver-java as similar as possible to web3j for portability. The below code snippets show how to port an application written in web3j to caver-java.

/* start a client */
Web3j web3 = Web3j.build(new HttpService(<endpoint>)); // Web3j
Caver caver = Caver.build(new HttpService(<endpoint>)); // caver-java
​
/* get nonce */
BigInteger nonce = web3j.ethGetTransactionCount(<address>, <blockParam>).send().getTransactionCount(); // Web3j
Quantity nonce = caver.klay().getTransactionCount(<address>, <blockParam>).send().getValue(); // caver-java
​
/* convert unit */
Convert.toWei("1.0", Convert.Unit.ETHER).toBigInteger(); // Web3j
Convert.toPeb("1.0", Convert.Unit.KLAY).toBigInteger(); // caver-java
​
/* generate wallet file */
WalletUtils.generateNewWalletFile(<password>, <filepath>); // Web3j
KlayWalletUtils.generateNewWalletFile(<address>, <password>, <filepath>); // caver-java
​
/* load credentials */
Credentials credentials = WalletUtils.loadCrendetials(<password>, <filepath>"); // Web3j
KlayCredentials credentials = KlayWalletUtils.loadCredentials(<password>, <filepath>); // caver-java
​
/* Value Transfer */
TransactionReceipt transactionReceipt = Transfer.sendFunds(...),send(); // Web3j
KlayTransactionReceipt.TransactionReceipt transactionReceipt = ValueTransfer.sendFunds().send(); // caver-java
## Related projects
​caver-js for JavaScript

## Thanks to
The web3j project for the inspiration. 🙂
