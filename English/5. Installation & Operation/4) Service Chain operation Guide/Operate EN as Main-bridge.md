# Operate EN as Main-bridge

To Setup an EN as a main-bridge in main chain, it is required to Setup an EN first in the main chain (Mainnet, Testnet)

You can Setup an EN with EN Operation Guide.

After setup your EN, you can enable main-bridge by configuring kend.conf.

## Configuration of the Initial File
The kend.conf contains the following main-bridge properties.

Name

Description

MAIN_BRIDGE

Enable bridge service as main bridge for service chain 
 1 to be enabled

MAIN_BRIDGE_PORT

bridge listen port 
 e.g) default: 50505

MAIN_BRIDGE_INDEXING

Enable storing transaction hash of service chain transaction for fast access to service chain data 
 e.g) 1 to enabled

To enable main-bridge on EN, you should do like below.

define MAIN_BRIDGE

enable RPC/WS.

add mainbridge API for RPC like the below example.

# Configuration file for the kend
​
...
​
# rpc options setting
RPC_ENABLE=1 # if this is set, the following options will be used
RPC_API="klay,mainbridge" # available apis: admin,debug,klay,miner,net,personal,rpc,txpool,web3,mainbridge,subbridge
RPC_PORT=8551
RPC_ADDR="0.0.0.0"
RPC_CORSDOMAIN="*"
RPC_VHOSTS="*"
​
# ws options setting
WS_ENABLE=1 # if this is set, the following options will be used
WS_API="klay" 
WS_ADDR="0.0.0.0"
WS_PORT=8552
WS_ORIGINS="*"
​
...
​
# service chain options setting
MAIN_BRIDGE=1
MAIN_BRIDGE_PORT=50505
MAIN_BRIDGE_INDEXING=1
​
...
You should note the WS_PORT to use for SC_MAIN_CHAIN_WS in Setup Service Chain.

## EN Restart
See EN Operation Guide.
