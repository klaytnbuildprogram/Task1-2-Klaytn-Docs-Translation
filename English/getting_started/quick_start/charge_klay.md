# Attaching to the Console
Klaytn Endpoint Node comes with JavaScript console. From the console command line, you can initiate part of Klaytn API calls to your EN.  
To attach to the JavaScript console, execute the following command.
```shell
$ ken attach ~/kend_home/klay.ipc
Welcome to the Klaytn JavaScript console!

instance: Klaytn/vX.X.X/XXXX-XXXX/goX.X.X
 datadir: ~/kend_home
 modules: admin:1.0 debug:1.0 governance:1.0 istanbul:1.0 klay:1.0 miner:1.0 net:1.0 personal:1.0 rpc:1.0 txpool:1.0

>
```
**NOTE**: You must wait until it downloads all the blocks. Enter `klay.blockNumber` in a console and check whether it matches the current block number [here](https://baobab.scope.klaytn.com/)  
**NOTE**: Type `klay` or `personal` to get the list of available functions.

# Creating a New Klaytn Account
To create a new Klaytn account from the JavaScript console, execute the following command. Your private key will be encrypted with the passphrase you enter.

```shell
> personal.newAccount()
Passphrase:  # enter your passphrase
Repeat passphrase:
"0x75a59b94889a05c03c66c3c84e9d2f8308ca4abd" # created account address
```

Keystore file will be created under `keystore` folder in the EN data directory, `DATA_DIR`  set in the `kend.conf`. If you follows the quick start default guideine, it must be `~/kend_home/keystore/`.

```bash
$ ls ~/kend_home/keystore/
UTC--2019-06-24T11-20-15.590879000Z--75a59b94889a05c03c66c3c84e9d2f8308ca4abd
```



# Unlocking the Klaytn Account

To unlock the created account, execute the following command. It unlocks the account for 300 seconds.  
**Note**: If you want to manually set the unlock duration, refer to this [link](https://docs.klaytn.com/api/management/personal#personal_unlockaccount).  
**`WARNING`**: Unlocking an account could be very dangerous if not done carefully. There are chances that your tokens will be taken away by hackers if your EN is hacked by a hacker.
To use safer method, refer to this [deployment guide using private key](https://docs.klaytn.com/tutorials/countapp/6-deploy-contract#deploy-method-1-by-private-key)

```shell
> personal.unlockAccount('75a59b94889a05c03c66c3c84e9d2f8308ca4abd') # account address to unlock
Unlock account 75a59b94889a05c03c66c3c84e9d2f8308ca4abd
Passphrase: # enter your passphrase
true
```

# Getting testnet KLAY from the Baobab Faucet
- Using the Baobab faucet in KlaytnWallet.
1. Access [https://baobab.wallet.klaytn.com](https://baobab.wallet.klaytn.com).
2. You can either create a new account from the Wallet or use the keystore file you created from the EN JavaScript console above to log into the Wallet.
3. Go to "KLAY Faucet" from the left pane menu, and click the "Run Faucet" button to get 5 KLAY.
You can run the KLAY Faucet once every 24 hours.
4. If you created a new account to get KLAY, then send the KLAY to your created account on the EN.

# Checking the Balance in Your Account
To see the balance of your account, execute the following command.

The default unit is peb (1 KLAY = 10<sup>^18</sup> peb).
More information about KLAY units can be found at [Units of KLAY](https://docs.klaytn.com/klaytn/design/computation/exec_model#units-of-klay).
```shell
> klay.getBalance('75a59b94889a05c03c66c3c84e9d2f8308ca4abd') # enter your account address
1e+21  # 1000 KLAY
```

# Exiting the Console
To leave the javascript console, execute the following command.
```shell
> exit
$
```
