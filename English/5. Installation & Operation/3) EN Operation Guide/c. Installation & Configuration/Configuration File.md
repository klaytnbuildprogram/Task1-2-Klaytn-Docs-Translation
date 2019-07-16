# Configuration File
The kend.conf contains the following properties.

Name

Description

NETWORK

Preconfigured Network. It is used when NETWORK_ID is not defined. Only "cypress" or "baobab" is valid for now.

NETWORK_ID

Klaytn Network ID 
 e.g) 8217 : Cypress (Main network), 1000 : Aspen test network, 1001 : Baobab test network

PORT

P2P port 
 e.g) default : 32323

SERVER_TYPE

Json rpc server type 
 e.g) "http", "fasthttp" (default: "fasthttp")

SYNCMODE

Blockchain sync mode 
 e.g) "fast", "full" (default: "full")

VERBOSITY

Logging verbosity 
 e.g) 0=silent, 1=error, 2=warn, 3=info, 4=debug, 5=detail (default: 3)

MAXCONNECTIONS

Maximum number of physical connections. All single channel peers can have up to  MAXCONNECTIONS peers. All multi-channel peers can have up to MAXCONNECTIONS/2 peers. (Network connection is disabled if set to 0.) 
 e.g) default: 25

TXPOOL_EXEC_SLOTS_ALL

Maximum number of executable transaction slots for all accounts 
 e.g) default: 4096

TXPOOL_NONEXEC_SLOTS_ALL

Maximum number of non-executable transaction slots for all accounts 
 e.g) default: 1024

TXPOOL_EXEC_SLOTS_ACCOUNT

Number of executable transaction slots guaranteed per account 
 e.g) default: 16

TXPOOL_NONEXEC_SLOTS_ACCOUNT

Maximum number of non-executable transaction slots permitted per account 
 e.g) default: 64

RPC_ENABLE

Enable the HTTP-RPC server 
 e.g) 1 to be enabled

RPC_API

API's offered over the HTTP-RPC interface 
 e.g) admin,debug,klay,miner,net,personal,rpc,txpool,web3

RPC_PORT

RPC port, Klaytn RPC clients (ex. klaytn console) 
 e.g) port default : 8551

RPC_ADDR

HTTP-RPC server listening interface 
 e.g) default: "localhost"

RPC_CORSDOMAIN

Comma separated list of domains from which to accept cross origin requests (browser enforced) 
 e.g) default: ""

RPC_VHOSTS

Comma separated list of virtual hostnames from which to accept requests (server enforced). Accepts '*' wildcard. 
 e.g) default: "localhost"

WS_ENABLE

Enable the WS-RPC server 
 e.g) 1 to be enabled

WS_API

API's offered over the WS-RPC interface 
 e.g) admin,debug,klay,miner,net,personal,rpc,txpool,web3

WS_ADDR

WS-RPC server listening interface 
 e.g) default: "localhost"

WS_PORT

WS port, Klaytn WebSocket port 
 e.g) default : 8552

WS_ORIGINS

Origins from which to accept websockets requests 
 e.g) default: ""

SC_MAIN_BRIDGE

Enable bridge service as main bridge for service chain 
 1 to be enabled

SC_MAIN_BRIDGE_PORT

Main bridge listens on this port. 
 e.g) default: 50505

SC_MAIN_BRIDGE_INDEXING

Enables storing transaction hash of child chain transaction for fast access to child chain data 
 e.g) 1 to enabled

METRICS

Enable metrics collection and reporting 
 e.g) 1 to be enabled

PROMETHEUS

Enable prometheus exporter 
 e.g) 1 to be enabled

DB_NO_PARALLEL_WRITE

Disables parallel writes of block data to persistent database 
 e.g) 1 to be enabled

MULTICHANNEL

Create a dedicated channel for block propagation 
 e.g) default: 1

SUBPORT

Listening sub port number if multichannel option is enabled e.g) default: $((PORT + 1)), 32324

NO_DISCOVER

Turn off the discovery option if it is set to 1. 
 e.g) 1 to be enabled

BOOTNODES

Comma separated kni address of bootstrap nodes 
 e.g) "kni://3f5541794b65fcd0d28dd2b0cd22fac2bdc86b458f0c1f619308f522050de07196bac80f4ab82571499ffcc1b817aff67659c3bd8f049af396af8a80b4c87e84@0.0.0.0:32323?discport=0"

ADDITIONAL

Fields for additional raw options 
 e.g) --txpool.nolocals

DATA_DIR

Klaytn blockchain data directory (for recording) 
 e.g) ~/kend_home (with Linux binaries), /var/kend/data (with RPM)

LOG_DIR

Klaytn node log directory (for recording) 
 e.g) ~/kend_home (with Linux binaries), /var/log/kend/ (with RPM)

Assume that the participated EN in Cypress (Network ID: 8217) uses the default port and mounts a large-scale partition onto ~/.kend. The following configuration is an example.

# Configuration file for the kend
​
# cypress, baobab is only available if you don't specify NETWORK_ID.
NETWORK="cypress"
# if you specify NETWORK_ID, a private network is created.
NETWORK_ID=
​
PORT=32323
​
SERVER_TYPE="fasthttp"
SYNCMODE="full"
VERBOSITY=3
MAXCONNECTIONS=10
​
# txpool options setting
TXPOOL_EXEC_SLOTS_ALL=4096
TXPOOL_NONEXEC_SLOTS_ALL=4096
TXPOOL_EXEC_SLOTS_ACCOUNT=4096
TXPOOL_NONEXEC_SLOTS_ACCOUNT=4096
TXPOOL_LIFE_TIME="30m"
​
# rpc options setting
RPC_ENABLE=1 # if this is set, the following options will be used
RPC_API="klay" # available apis: admin,debug,klay,miner,net,personal,rpc,txpool,web3
RPC_PORT=8551
RPC_ADDR="0.0.0.0"
RPC_CORSDOMAIN="*"
RPC_VHOSTS="*"
​
# ws options setting
WS_ENABLE=1 # if this is set, the following options will be used
WS_API="klay" # available apis: admin,debug,klay,miner,net,personal,rpc,txpool,web3
WS_ADDR="0.0.0.0"
WS_PORT=8552
WS_ORIGINS="*"
​
# service chain options setting
SC_MAIN_BRIDGE=0 # if this is set, the following options will be used.
SC_MAIN_BRIDGE_PORT=50505
SC_MAIN_BRIDGE_INDEXING=0  # this option will be deprecated.
​
# Setting 1 is to enable options, otherwise disabled.
METRICS=1
PROMETHEUS=1
DB_NO_PARALLEL_WRITE=0
MULTICHANNEL=1
SUBPORT=$((PORT + 1)) # used for multi channel option
​
# discover options
NO_DISCOVER=0 # setting 1 to disable discovery
BOOTNODES=""
​
# Raw options e.g) "--txpool.nolocals"
ADDITIONAL=""
​
DATA_DIR=
LOG_DIR=$DATA_DIR/logs
The recommended txpool sizes based on EN type is as follows:

TXPOOL_EXEC_SLOTS_ALL=4096
TXPOOL_NONEXEC_SLOTS_ALL=4096
TXPOOL_EXEC_SLOTS_ACCOUNT=4096
TXPOOL_NONEXEC_SLOTS_ACCOUNT=4096
