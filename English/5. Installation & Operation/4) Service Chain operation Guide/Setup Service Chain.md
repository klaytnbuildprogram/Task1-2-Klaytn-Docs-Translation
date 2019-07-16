# Setup Service Chain

Basically, Service Chain uses Clique PoA (Proof-of-authority) consensus. To setup your service chain, you need to determine the scsigner (service chain signer) address. This page shows how to create scsigner keystore/password and generate the genesis file. Currently, service chain supports only a single consensus node.

## Creation of SCSigner Keystore / Password Files
When you run a service chain node, you need a keystore file and the associated password file for the scsigner. You can generate the files like the following. Also you can refer to Accounts for more details.

### Create Your Password File
First you can generate the password file simply like below. This password file will be used to generate a keystore file and run the service chain node.

$ echo passwordString >> passwd
### Create Your Keystore File
You can create the keystore file with your password file like below.

$ ken account new --datadir "./" --password ./passwd
Address: {c04ae62e6a8e084e8f00030d637380792db3dc26}
You should note the address and use it for the scsigner in the genesis file.

Now, you can have the keystore file and password file like below.

$ tree
.
├── keystore
│   └── UTC--2019-03-28T06-10-39.102092000Z--c04ae62e6a8e084e8f00030d637380792db3dc26
└── passwd
After Initialization of a Genesis Block, you will copy these files to the data directory.

## Creation of a Genesis File
First, you should create new genesis file for your own service chain and initialize all service chain nodes with the same genesis file. The genesis file of the service chain is different with main chain. To create new genesis file, you should write the scsigner address of your service chain in governingnode, extraData and alloc field. The unitPrice is set to 0 in the example below, but you can change it to the value you want.

The genesis.json examples follow. You can find more details in Genesis JSON.

geneis.json example for a consensus node.

The consensus node's scsigner is c04ae62e6a8e084e8f00030d637380792db3dc26.

{
     "config": {
         "chainId": 3000,
         "clique": {
             "period": 1,
             "epoch": 604800
         },
         "unitPrice": 0
     },
     "extraData": "0x0000000000000000000000000000000000000000000000000000000000000000c04ae62e6a8e084e8f00030d637380792db3dc260000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
     "alloc": {
         "c04ae62e6a8e084e8f00030d637380792db3dc26": {
             "balance": "0x446c3b15f9926687d2c40534fdb564000000000000"
         }
     },
     "number": "0x0",
     "gasUsed": "0x0",
     "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000"
}
## SCN (Service Chain Node) Configuration
The SCN configuration is to create a data directory and to set up the several values on the configuration file kscnd.conf.

Create the SCN data directory.

Configure the SCN with kscnd.conf.

### SCN Data Directory Creation
Considering the fact that the size of Klaytn blockchain data is always increased, it is recommended to use a big enough storage. You may need to create the directory on your specific path.

$ mkdir -p ~/kscnd_home
Service Chain Node Setup
Setting up the node will go through the following steps.

Copy the initial files to the SCN data directory.

Configure the kscnd.conf file.

Initialization of a Genesis Block

Before starting an service chain node, it is necessary to initialize the genesis block of the service chain network using kscn and genesis.json.

$ kscn init --datadir ~/kscnd_home genesis.json
...
All required steps are done for launching an SCN.

Copy SCSigner Key / Password File

To set scsigner for the service chain node, we need the right pair of scsigner keystore and password file. Copy the files like below. Keystore file needs a password file to unlock the account.

$ cp ./keystore/UTC--2019-...--ef28e51ef33fe0f487289c1c6e1ccdf5e571366b ~/kscnd_home/keystore
$ cp ./passwd ~/kscnd_home/
Configuration of the Initial File

The kscnd.conf contains the following properties.

Name

Description

SCSIGNER

SCSigner Address 
 e.g.) "c04ae62e6a8e084e8f00030d637380792db3dc26"

SCSIGNER_PASSWD_FILE

SCSigner Keystore password file path
 e.g.) "~/kscnd_home/passwd"

NETWORK_ID

Klaytn Network ID 
 e.g.) 8217 : Cypress (Main network), 1000 : Aspen test network, 1001 : Baobab test network

PORT

P2P port 
 e.g.) default: 32323

SERVER_TYPE

Json rpc server type 
 e.g.) "http", "fasthttp" (default: "fasthttp")

SYNCMODE

Blockchain sync mode 
 e.g.) "fast", "full" (default: "full")

VERBOSITY

Logging verbosity 
 e.g.) 0=silent, 1=error, 2=warn, 3=info, 4=debug, 5=detail (default: 3)

TXPOOL_EXEC_SLOTS_ALL

Maximum number of executable transaction slots for all accounts 
 e.g.) default: 4096

TXPOOL_NONEXEC_SLOTS_ALL

Maximum number of non-executable transaction slots for all accounts 
 e.g.) default: 1024

TXPOOL_EXEC_SLOTS_ACCOUNT

Number of executable transaction slots guaranteed per account 
 e.g.) default: 16

TXPOOL_NONEXEC_SLOTS_ACCOUNT

Maximum number of non-executable transaction slots permitted per account 
 e.g.) default: 64

RPC_ENABLE

Enable the HTTP-RPC server 
 e.g.) 1 to be enabled

RPC_API

API's offered over the HTTP-RPC interface 
 e.g.) admin,debug,klay,miner,net,personal,rpc,txpool,web3

RPC_PORT

RPC port, Klaytn RPC clients (ex. klaytn console) 
 e.g.) port default: 8551

RPC_ADDR

HTTP-RPC server listening interface 
 e.g.) default: "localhost"

RPC_CORSDOMAIN

Comma separated list of domains from which to accept cross origin requests (browser enforced) 
 e.g.) default: ""

RPC_VHOSTS

Comma separated list of virtual hostnames from which to accept requests (server enforced). Accepts '*' wildcard. 
 e.g.) default: "localhost"

WS_ENABLE

Enable the WS-RPC server 
 e.g.) 1 to be enabled

WS_API

API's offered over the WS-RPC interface 
 e.g.) admin,debug,klay,miner,net,personal,rpc,txpool,web3

WS_ADDR

WS-RPC server listening interface 
 e.g.) default: "localhost"

WS_PORT

WS port, Klaytn WebSocket port 
 e.g.) default: 8552

WS_ORIGINS

Origins from which to accept websockets requests 
 e.g.) default: ""

MAIN_BRIDGE

Enable main bridge service for service chain 
 e.g.) 1 to be enabled 
 e.g.) 1 to be enabled

MAIN_BRIDGE_PORT

main bridge listen port 
 e.g.) default: 50505

MAIN_BRIDGE_INDEXING

Enable storing transaction hash of service chain transaction for fast access to service chain data

SC_SUB_BRIDGE

Enable sub-bridge service as main bridge for service chain 
 1 to be enabled

SC_SUB_BRIDGE_PORT

bridge listen port 
 e.g.) default: 50506

SC_TX_PERIOD

The period to make and send a chain transaction to main chain 
 e.g.) default: 1

SC_TX_LIMIT

Number of service chain transactions stored for resending 
 e.g.) default: 1000

SC_MAIN_CHAIN_WS

main chain ws url 
 e.g.) default: "ws://0.0.0.0:8546"

METRICS

Enable metrics collection and reporting 
 e.g.) 1 to be enabled

PROMETHEUS

Enable prometheus exporter 
 e.g.) 1 to be enabled

DB_NO_PARALLEL_WRITE

Disables parallel writes of block data to persistent database 
 e.g.) 1 to be enabled

MULTICHANNEL

Create a dedicated channel for block propagation 
 e.g.) default: 1

SUBPORT

P2P subport 
 e.g.) default: 32324

ADDITIONAL

Fields for additional raw options 
 e.g.) --txpool.nolocals

DATA_DIR

Klaytn blockchain data directory (for recording) 
 e.g.) ~/kscnd_home

LOG_DIR

Klaytn node log directory (for recording) 
 e.g.) $DATA_DIR/logs

Assume that the participated SCN in Cypress (Network ID: 8217) uses the default port and mounts a large-scale partition onto ~/kscnd_home. The following configuration is an example.

# Configuration file for the kscnd
​
SCSIGNER="c04ae62e6a8e084e8f00030d637380792db3dc26"
SCSIGNER_PASSWD_FILE=~/kscnd_home/passwd   # Need to right password file path for the keystore file of the scsigner address
​
NETWORK_ID=3000 # Set your own unique network ID which is different with known network(Klaytn Mainnet(1), Baobab(1000))
​
PORT=22323 # if EN (main-bridge) and SCN (sub-bridge) on same instance, use different port with EN.(EN: 32323, SCN:22323)
​
SERVER_TYPE="fasthttp"
SYNCMODE="full"
VERBOSITY=3
​
# txpool options setting
TXPOOL_EXEC_SLOTS_ALL=16384
TXPOOL_NONEXEC_SLOTS_ALL=16384
TXPOOL_EXEC_SLOTS_ACCOUNT=16384
TXPOOL_NONEXEC_SLOTS_ACCOUNT=16384
​
# rpc options setting
RPC_ENABLE=1 # if this is set, the following options will be used
RPC_API="klay,subbridge" # available apis: admin,debug,klay,miner,net,personal,rpc,txpool,web3,mainbridge,subbridge
RPC_PORT=7551         # if main-bridge and sub-bridge on same instance, us different port with main-bridge.(main: 8551, sub:7551)
RPC_ADDR="0.0.0.0"
RPC_CORSDOMAIN="*"
RPC_VHOSTS="*"
​
# ws options setting
WS_ENABLE=1 # if this is set, the following options will be used
WS_API="klay"
WS_ADDR="0.0.0.0"
WS_PORT=7552    # if main-bridge and sub-bridge on same instance, us different port with main-bridge.(main: 8552, sub:7552)
WS_ORIGINS="*"
​
# service chain options setting
MAIN_BRIDGE=0 # if this is set, the following options will be used.
MAIN_BRIDGE_PORT=50505
MAIN_INDEXING=1
​
SC_SUB_BRIDGE=1
SC_SUB_BRIDGE_PORT=50506    # if main-bridge and sub-bridge on same instance, us different port with main-bridge.(main: 50505, sub:50506)
SC_TX_PERIOD=1
SC_TX_LIMIT=1000
SC_PARENT_CHAIN_WS="ws://0.0.0.0:8552"  # This url is the noted RPC web socket of main-bridge.
​
# Setting 1 is to enable options, otherwise disabled.
METRICS=1
PROMETHEUS=1
NO_DISCOVER=1
DB_NO_PARALLEL_WRITE=0
MULTICHANNEL=1
SUBPORT=$((PORT + 1)) # used for multi channel option
​
# Raw options e.g.) "--txpool.nolocals"
ADDITIONAL=""
​
DATA_DIR=~/kscnd_home
LOG_DIR=$DATA_DIR/logs
The recommended txpool sizes based on SCN type is as follows:

TXPOOL_EXEC_SLOTS_ALL=16384
TXPOOL_NONEXEC_SLOTS_ALL=16384
TXPOOL_EXEC_SLOTS_ACCOUNT=16384
TXPOOL_NONEXEC_SLOTS_ACCOUNT=16384
### Start
Depending your installation type, you can operate kscn like below different ways.

### Package
You can start/stop the Klaytn service with the following systemctl command.

start

$ systemctl start kscnd.service
termination

$ systemctl stop kscnd.service
status

$ systemctl status kscnd.service
### RPM
The kscnd command can control the SCN's lifecycle.

start

$ kscnd start
termination

$ kscnd stop
status

$ kscnd status
## Account Creation
Account creation is currently blocked by default in the service chain. You can enable the account creation by using the option --scnewaccount.

WARNING: currently when the option is set as true, generated accounts are not synced with the main chain.
