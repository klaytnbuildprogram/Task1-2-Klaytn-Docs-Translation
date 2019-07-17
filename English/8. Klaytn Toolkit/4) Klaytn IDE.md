# Klaytn IDE


Klaytn IDE is a browser-based compiler and IDE that helps developers build Klaytn smart contracts with Solidity language. Klaytn IDE also supports test and deployment of smart contracts. Klaytn IDE is forked from Remix 0.7.7.

You can access to the Klaytn IDE at https://ide.klaytn.com. This document is an overview of the Klaytn IDE, it explains the major features and the usage guideline. You can find more detailed information in Remix docs.

## What's different from Remix?
Sign-in with Klaytn accounts

Supports 2 Solidity versions (v0.4.24 and v0.5.6)

Does not support Plugin, Gist add-on, and Swarm.

## Overview

The layout of the Klaytn IDE is as shown above. There are 4 areas - file explorer, code editor, console, and modules.

## 1. File Explorer

The file explorer on the left side of the workspace shows the list of smart contract files stored in your browser. Please be aware that clearing the browser storage will permanently delete all smart contract files you wrote. You can add, rename, and delete files from the file explorer.

Create a new file  

You can create Untitled1.sol file by clicking  icon on the title bar.

Add a local file  

You can select files from the local file system and import them to the browser storage. Clicking  icon will display a select-file dialog.

Rename and delete a file  

Right-click on a file will show up a context menu from which you can rename or delete the file.

## 2. Code Editor

At the center of the workspace, you can edit files.

File tabs
You can open multiple files, and the editor displays the opened files as tabs. When you create or add a file to the file explorer, the file appears on the file tabs. Clicking  icon on the tab will close the file.

Note: Closing a file (by clicking  icon) does not remove the file from the file explorer.

Auto-completion for Solidity reserved keywords
There are frequently-used statements in Solidity, for example, bytes32, public, and modifier. You don't need to type the whole characters since Klaytn IDE suggests the word you are intending to type. The auto-completion works for all reserved keywords in Solidity and the functions, variables, and classes you define.


Error detection
A red marker is displayed next to the line number where a compilation error occurred.


## 3. Modules
There are six tabs in Modules. Compile, Run, Analysis, Testing, Debugger, and Settings.


Compile: To select the compiler version and to enable/disable several compilation options. A list of compiled projects is displayed in this tab as well. 

Run: In this tab, you can deploy a contract to the network and invoke the contract functions. This tab has options to manage the parameters for transactions, such as network, account, gas limit, and input params.

Analysis: You can run static and runtime code analysis with the selected checklist. 

Testing: Create and run unit tests.

Debugger: Allows you to debug the transaction. 

Settings: General settings and Help & Support links.

Compile
Compiling is triggered when you click the Start to compile button. If you want the file to be compiled each time the file is saved or when another file is selected - check the Auto compile checkbox.

For now, we support two compiler versions, Solidity v0.4.24 and v0.5.6. So you always need to add pragma solidity 0.4.24; or pragma solidity 0.5.6 on top of the document. You can manually click "Compile" button (Cmd+s for MacOS, Ctrl+s for Windows) every time you need, or you can activate the auto-compile function.


Note:

Your codes are automatically saved every 15 seconds. Auto-save is also triggered when you compile a file, close the file tab, or leave the Klaytn IDE.  

If activated, "Auto-compile" starts to compile when you stop typing.

Run
Environment (Network Selector)

You can choose which network to use from the "Environment" dropdown. By default, Klaytn IDE provides following network options:

Baobab network (Klaytn testnet)

Cypress network (Klaytn mainnet)

If you want to connect to another custom node, click the dropdown list, select "Caver provider", and fill the URL of the network you want to connect to. If the protocol of network you want to connect to is HTTP, not HTTPS, please use http\://ide.klaytn.com.

To deploy a contract, you need KLAY to pay the transaction fee. For the Baobab network (Klaytn testnet), you can get some testnet KLAY from the faucet [https://baobab.wallet.klaytn.com/faucet]. After receiving testnet KLAY from the faucet, import the account to the Klaytn IDE in the "Account" selector.

Account (Account Selector)

With Account Selector, you can change your current account to another one.
To import an account, click  button and choose the import method either by private key or keystore.


After Import, your account balance will appear in theAccount selector in a few seconds.

Value

On the Value (Tx Value Controller), you can fill the amount of value for the next created transaction.

Gas Limit Controller

In the Gas Limit controller, you can fill the maximum amount of gas which will be used for calling a smart contract function.

Deploy

Once you compile the code, you will find the contract listed in the dropdown selector. Among the compiled list, you can select a contract and deploy it by clicking the Deploy button.


If the contract is deployed successfully, the contract address is shown and you can see the list of functions that the contract exposes in the below. There are only two types of functions in the smart contract, functions that write data to the blockchain (transaction) and functions that read data from the blockchain.

Analysis

This section shows the output from the last compilation. By default, a new analysis is run at each compilation.

The analysis tab gives detailed information about the contract code. It can help you avoid code mistakes and to enforce best practices.

If you need more information, please visit Remix docs > Analysis ​

Testing

In this section, you can create a new solidity test file in the current folder and execute the tests. The execution result is displayed below. If you need more information, please visit Remix docs > Unit Testing​

Debugger

This module allows you to debug the transaction. It can be used to deploy transactions created from IDE and already mined transactions.

Debugging works only if the current environment provides the necessary features. For debugging, the personal API must be enabled in the EN node. Please see the RPC_API option in the EN configuration file.

If you need more information, please visit Remix docs > Debugger​

Settings

This tab contains general settings and support channels.

Important settings:

Text Wrap: controls if the text in the editor should be wrapped.

Enable Personal Mode : use in private network

## 4. Terminal

At the bottom of the code editor, compiled outputs, compiler errors, deployment results, and transaction information are shown in the terminal.

If you click on the transaction output, detailed information will be shown. If debugging is supported, debugging the transaction will work on the Debug tab.

## Develop with OpenZepplin
OpenZeppelin is a library for secure smart contract development. It provides implementations of standards like ERC20 and ERC721 which you can deploy as-is or extend to suit your needs, as well as Solidity components to build custom contracts and more complex decentralized systems.

The OpenZepplin library is available after connecting to localhost via remixd. This requires the installation of remixd.

Install Remixd
Remixd is a tool that is intended to be used with Remix IDE (aka. Browser-Solidity). It allows a websocket connection between Remix IDE (web application) and the local computer. Get more details at: remixd document.

remixd can be globally installed using the following command: After installation, start remixd. -s option gives the IDE access to the given folder. In the given folder, you will install OpenZepplin and place your contract source code.

```bash $ remixd -s  --remix-ide http://ide.klaytn.com​

For example, remixd -s ~/temp/openzepplin --remix-ide http://ide.klaytn.com

Then, you will see the following messages in your terminal.


Install OpenZepplin
Go to the shared folder, and install OpenZepplin.

```bash $ cd  $ npm install openzeppelin-solidity

Connect Remixd
Click remix connect button as shown below.


Click connect.


localhost directory will appear in the file browser.


In your contract source file, import the required solidity contract from the OpenZepplin.


## Need more information?
The klaytn IDE is based on the Remix v0.7.7. Many features are compatible, so please refer to the official Remix documentation.

## Send us feedback!
If you have any feedback or suggestions about Klaytn IDE, please send an email to developer@klaytn.com.