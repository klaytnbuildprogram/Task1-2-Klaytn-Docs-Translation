# Prerequisites

​CC Operation Guide and EN Operation Guide describe how to install Klaytn binaries and configure each node depending on your operating system. We assumed that you installed the Klaytn binaries as well as homi tool already. After installing these programs, you are ready to build your own Klaytn network! Let's get started.

## Configuration
After installing the klaytn binaries properly, you need to configure each node to run locally. In order to build your own network, the following files are needed in common.

genesis.json describes the genesis block configuration.

static-nodes.json contains nodes to which the running node tries to dial.

These files are generated using homi tool. For example,

$ homi setup --governance --gov-mode single --ist-proposer-policy 2 --ist-subgroup 13 --ist-epoch 604800 --reward-mint-amount 9600000000000000000 --reward-staking-interval 86400 --reward-proposer-interval 3600 --reward-ratio 34/54/12 --reward-deferred-tx --unitPrice 25000000000 --deriveShaImpl 2 --reward-minimum-stake 5000000 --ist-epoch 604800 --ist-proposer-policy 2 --ist-subgroup 13 --num 1 --pn-num 1 --en-num 1 local
Under the directory homi-output by default, there are keys, keys_pn, scripts, scripts_pn sub-directories. The keys directory contains validators information as well as private keys of CNs and keys_pn of PNs. The scripts directory has the genesis.json for the network and all CNs' kni address. The scirpts_pn has PNs addresses. Please check out Genesis JSON for more details.

You must update the configuration files, kcnd.conf, kpnd.conf, and kend.conf. The below configuration should be applied to all nodes, CP, PN, and EN.

Setup NeworkID

Disablr Multichannel Option

Enable Nodiscover Option

### Setup NetworkID
We are building a private network, so the NETWORK_ID must be specified. You can pick any integer value for your network ID, and the network ID should be the same across all nodes.

...
NETWORK_ID=4321
...
### Disable Multichannel Option
Since we are not using multichannel option, please update the configuration file properly.

...
MULTICHANNEL=0
...
### Enable Nodiscover Option
We are going to use static-nodes.json which means the nodes do not need to use the discovery feature. Please update the configuration file as follows.

...
NO_DISCOVER=1
...
