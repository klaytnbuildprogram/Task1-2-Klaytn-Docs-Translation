# Download and Initialize an EN

Unzip the provided [KEN binary package](https://docs.klaytn.com/node/download) and copy the files into the klaytn folder.   
**Note**: Please download appropriate package starting with `ken`.

For Mac users, unzip the downloaded file with the following command.
```shell
$ tar zxf ken-baobab-vX.X.X-X-darwin-amd64.tar.gz
$ export PATH=$PATH:$PWD/ken-darwin-amd64/bin
```

For Linux users, unzip the downloaded file with the following command.
```shell
$ tar zxf ken-baobab-vX.X.X-X-linux-amd64.tar.gz
$ export PATH=$PATH:$PWD/ken-linux-amd64/bin
```

You should create a data directory to store the blockchain data. In this tutorial, we will create a `kend_home` folder in the home directory.
```shell
$ mkdir -p ~/kend_home
```

# Configuring an EN
The configuration file, `kend.conf`,  is located under `ken-xxxxx-amd64/conf/`. For the detilas of configurable parameters, you can refer to the [EN Configuration Guide](https://docs.klaytn.com/node/en/installation/config).
To launch an EN of Baobab testnet, please update the `kend.conf` file accordingly as follows.

```
# cypress, baobab is only available if you don't specify NETWORK_ID.
NETWORK="baobab"
# if you specify NETWORK_ID, a private network is created.
NETWORK_ID=
...
RPC_API="klay,net" # net module should be opened for truffle later on.
...
DATA_DIR=~/kend_home
```

# Launching an EN
To launch the EN, execute the following command.
```shell
$ kend start
 Starting kend: OK
```

# Checking the EN
To check if the EN is running, execute the following command.
```shell
$ kend status
kend is running
```

# Checking the log of the EN
To check the log of the EN, execute the following command.
```shell
$ tail -f ~/kend_home/logs/kend.out
...
INFO[03/26,15:37:49 +09] [5] Imported new chain segment                blocks=1    txs=0  mgas=0.000  elapsed=2.135ms   mgasps=0.000    number=71340 hash=f15511…c571da cache=155.56kB
...
```

# Troubleshooting

Please refer to the [Troubleshooting](https://docs.klaytn.com/node/troubleshooting) if you have trouble in launching the Klaytn Endpoint Node.
