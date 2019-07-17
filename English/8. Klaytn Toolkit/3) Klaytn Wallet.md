# Klaytn Wallet

Klaytn Wallet is a browser-based account management tool for blockchain application (BApp) developers on Klaytn. It helps developers create new accounts or view existing account information directly through a web browser without having to run a Klaytn node locally. Klaytn Wallet also lets users transfer KLAY or Klaytn tokens to other accounts for testing purposes.

Important Notice on Security
Please note: Klaytn Wallet is should be used for development and testing purposes only. Do NOT use Klaytn Wallet for commercial or personal use, including storage or transfer of KLAY or Klaytn tokens. Klaytn Wallet has NOT been tested for commercial-level security and may be vulnerable to malicious attacks. Klaytn Wallet stores user's private key in the browser's local storage, which may be susceptible to attacks that exploit the browser's security vulnerabilities.

Klaytn Wallet for the Cypress mainnet: https://wallet.klaytn.com​

Klaytn Wallet for the Baobab testnet: https://baobab.wallet.klaytn.com​


## Klaytn Wallet Functions
Klaytn Wallet provides the following list of features.

Account and key management 

Create a new account 

Load existing account using the private key or keystore file

Download a new keystore file

Asset management 

View account balance

Add tokens to the wallet

Transfer KLAY and Klaytn tokens

Baobab testnet KLAY faucet

## Create a New Account
If you already have a Klaytn ccount, you may choose to skip this process and go to Access Existing Account.

You can use Klaytn Wallet to create new Klaytn accounts. To create a new account, click the Create Account button on the menu bar on the left, and then follow the steps below.

Step 1. Set password for your new account's keystore file

Step 2. Download the keystore file to your local storage

Step 3. Save your new account's Klaytn Wallet Key

Before continuing, a few words of caution:
NEVER share your 'Wallet Key' or 'private key'  with anyone. Giving information about your 'Wallet Key' or 'private key' means giving away complete and permanent access to your account.

Do not keep this information on a device connected to the Internet. Hackers can steal your credentials from your local storage.

Choose a strong password and store critical information in multiple locations.

Klaytn is UNABLE to restore 'Wallet Key' or 'private key' in case you lose it. Take utmost care not to lose your key information.

Step 1. Set Password for your Keystore File
As the first step in creating a new account, you must create a password for your keystore file. A keystore file is a JSON file that securely stores your Klaytn account information, including the account's address and the private key associated with the account. A keystore file's password must be strong enough to meet Klaytn's security standard, as the password protects the private key stored within the file.


When you click the password input form, a tooltip will appear above and it will show you, as you type in, if the entered password satisfies the security requirements. If your password meets all the requirements, Next Step button will be activated. ! 

Step 2. Download the Keystore File
In the second step, you download the keystore file that has been encrypted with the submitted password. Click the Download & Next Step button to immediately download the keystore file and move on to the last step. (Note that if the downloaded keystore file gets lost, you can download a new keystore file in the View Account Info menu.)


Step 3. Save your Klaytn Wallet key and Private Key
In the final step, you are shown the Wallet Key and the private key corresponding to your newly created account. You are strongly encouraged to store the key in a separate, disconnected storage.

For more in-depth information about Klaytn account, please visit Klaytn Docs and review the Account section.


## Access Existing Account
To check your account's balance of KLAY or Klay tokens, or to transfer tokens to another account, you need to access your account. Klaytn Wallet offers two ways to access your account.

Using Klaytn Wallet Key or Private Key A Klaytn Wallet Key is a string of 106 hexadecimal characters associated with an account, whereas a private key is a string of 64 hexadecimal characters (the character count does not include the "0x" prefixes that indicate hexadecimal numbers; if we count them in, a Klaytn Wallet Key is 112 characters long, and a private key is 66 characters long). Using one's private key should always be a last-ditch effort of access, only to be utilized when all else fails. This should not be the main method for anyone to access their accounts. Private keys are the most sensitive information because private keys allow complete access to an account. Therefore, it is extremely important to keep this information safe, secure, and secret.

Keystore file and password A keystore file is a JSON file that stores encrypted private key and account address information. This file is encrypted using the user-provided password.

Access Existing Account Using Klaytn Wallet Key or Private Key
Step 1. Enter the Wallet Key or Private Key
To access your account, click the View Account Info button from the menu bar on the left, and go to the Private Key tab on the screen. Enter the Klaytn Wallet Key or private key for the account you wish to access in the input box.


Step 2. Check the Checkbox and Click 'Access' button
Click the Access button to go to your account page. If the key information you provided does not conform to any key format, the Access button will not be active.


Access Existing Account Using Keystore File and Password
Step 1. Go to the Keystore File Tab
Go to the Keystore File tab on the screen.


Step 2. Select the Keystore File to Use
Click the Upload button, and locate your keystore file.


Step 3. Enter Keystore File Password
Enter the password corresponding to the selected keystore file, and click the Access button to go to your account page.


View Account Info
On this page, you can check your account's address, private key, and Klaytn Wallet Key information. On the right side of the page, you can check the balance of your KLAY and other Klaytn tokens. Using Klaytn Wallet to check account balance is recommended for blockchain application developers who do not wish to unlock their accounts every time a balance check is needed, for security reasons.


## How to Add Klaytn Tokens
Klaytn Wallet supports KLAY and Klaytn tokens to be registered so that their balances can be checked. To register Klaytn tokens to Klaytn Wallet, please follow the steps below.

Step 1. Access Existing Account's Information
Go to your account page by following the steps of Access Existing Account.

Step 2. Click the Add Token Button in the Balance Section
Click the '+' button in the bottom-right of the screen in the Balance area.


Step 3. Enter Token Information
Enter the Token Symbol, Token Contract Address, and Decimals. After clicking the Save button, you will see the token listed in your account's balance section.


## How to Send KLAY and Tokens
You can send KLAY or Klaytn tokens to other accounts using Klaytn Wallet. When sending KLAY or tokens, you must have the minimum amount of KLAY in your account to pay for the transaction fee.

Step 1. Go to 'Send KLAY & Tokens' menu
Either click the Send KLAY & Token button from the menu bar on the left, or the same button on the main page.


Step 2. Access Your Account
In case you have not loaded your account into the wallet yet, do so by following the steps in Access Existing Account.

Step 3. Select the Token to Send
Select the token to transfer in Step 1. Select Tokens area.


Step 4. Select Token Transfer Information
After selecting the token to send, move on to Step 2. Enter the information section and fill in the necessary information (To Address and Amount to Send), then click the Send Transaction button.


Step 5. Confirm the Transfer
A confirmation page will appear. Double check the amount to transfer and the recipient address. If everything is correct, click Yes, I'm sure. Otherwise, you can go back to the previous page to edit the token transfer information.


Step 6. Review Transfer Details
Your transaction request is completed. You can check the status of the transaction on the Klaytnscope. Clicking the View Transaction Info will launch Klaytnscope to show the transaction details.


## How to Receive Baobab testnet KLAY
The testnet KLAY faucet runs on the Baobab network. The faucet can be accessed from the Baobab Klaytn Wallet.

To receive testnet KLAY, you should have a valid Klaytn account.

If you do not have an account, please create one by following the steps in Create a New Account.

Load your account into the wallet by following the steps in Access Existing Account. Testnet KLAY will be sent to the loaded account. 

Step 1. Go to the testnet KLAY Faucet
From the Baobab Klaytn Wallet, KLAY Faucet menu on the left bar brings you to the testnet KLAY request page.

The requested page will show your address and the current testnet KLAY balance of your account.


Step 2. Run Faucet
Clicking Run Faucet button will send you 5 testnet KLAY and your balance will be updated. Note that you can run the faucet for each account once every 24 hours.