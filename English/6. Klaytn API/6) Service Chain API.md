# Service Chain API

In Klaytn, there are two serviechain bridge nodes like below.

main-bridge: This bridge is on EN (Endpoint node) of the main chain (Mainnet or Baobab testnet).

sub-bridge: This bridge is on SCN (Service Chain Node) of the service chain.

Those bridge nodes provide the following APIs under mainbridge and subbridge namespace respectively.

## Common APIs
nodeInfo
The nodeInfo returns bridge node information including the KNI (Klaytn Network Identifier) of the node. A sub-bridge node can connect to a main-bridge node via the KNI.

Parameters

None

Return Value

Type

Description

JSON string

the bridge node information.

Example

> mainbridge.nodeInfo // or 'subbridge.nodeInfo'
{
  kni: "kni://f8a1f0cd1e2bebeece571e4fda16e215218fd4b9bc2eddd924f7cd5b5f950fcec8f4b8cd3851390d1d0bacf1b15e1c4a38c882252e429a28d16eeb6edbacd726@[::]:50505?discport=0",
  id: "f8a1f0cd1e2bebeece571e4fda16e215218fd4b9bc2eddd924f7cd5b5f950fcec8f4b8cd3851390d1d0bacf1b15e1c4a38c882252e429a28d16eeb6edbacd726",
  ip: "::",
  listenAddr: "[::]:50505",
  name: "-2",
  ports: {
    discovery: 0,
    listener: 50505
  },
  protocols: {
    servicechain: {
      config: {
        chainId: 2018,
        deriveShaImpl: 0,
        isBFT: true,
        istanbul: {...},
        unitPrice: 0
      },
      difficulty: 87860,
      genesis: "0x711ce9865492659977abb2758d29f68c2b0c82862d9376f25953579f64f95b58",
      head: "0x0d4b130731f1e7560e4531ac73d55ac8c6daccb178abd86af0d96b7aafded7c5",
      network: 1
    }
  }
}
addPeer
The addPeer method adds a new remote node to the peer list. The node will try to maintain connectivity to these nodes at all times, reconnecting every once in a while if the remote connection goes down.

The method accepts a single argument, the kni URL of the remote peer to start tracking and returns a BOOL indicating whether the peer was accepted for tracking or some error occurred.

Parameters

Name

Type

Description

url

string

Peer's  kni URL.

Return Value

Type

Description

bool

true if the peer was accepted, false otherwise.

Example

Console

> mainbridge.addPeer("kni://a979fb...1163c@10.0.0.1:50505") // or 'subbridge.addPeer'
true
HTTP RPC

$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"mainbridge_addPeer","params":["kni://a979fb575495b8d6db44f750317d0f4622bf4c2aa3365d6af7c284339968eef29b69ad0dce72a4d8db5ebb4968de0e3bec910127f134779fbcb0cb6d3331163c@10.0.0.1:50505"],"id":1}' http://localhost:8551
{"jsonrpc":"2.0","id":1,"result":true}
removePeer
The removePeer method disconnects and removes the remote node in the list of tracked static nodes. The method accepts a single argument, the kni URL of the remote peer to start tracking and returns a BOOL indicating whether the peer was accepted for tracking or some error occurred.

Parameters

Name

Type

Description

url

string

Peer's  kni URL.

Return Value

Type

Description

bool

true if the peer was removed, false otherwise.

Example

Console

> mainbridge.removePeer("kni://a979fb...1163c@10.0.0.1:50505") // or 'subbridge.removePeer'
true
HTTP RPC

$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"mainbridge_removePeer","params":["kni://a979fb575495b8d6db44f750317d0f4622bf4c2aa3365d6af7c284339968eef29b69ad0dce72a4d8db5ebb4968de0e3bec910127f134779fbcb0cb6d3331163c@10.0.0.1:50505"],"id":1}' http://localhost:8551
{"jsonrpc":"2.0","id":1,"result":true}
## Main-bridge APIs
convertServiceChainBlockHashToMainChainTxHash
mainbridge.convertServiceChainBlockHashToMainChainTxHash returns the anchoring transaction hash of the given child chain block hash.

Parameters

Type

Description

32-byte DATA

The childchain block hash which included the anchoring tx hash.

Return Value

Type

Description

32-byte DATA

The transaction hash whilch including the childchain block anchoring inforamtion.

Example

Console

> mainbridge.convertServiceChainBlockHashToMainChainTxHash("0xeadc6a3a29a20c13824b5df1ba05cca1ed248d046382a4f2792aac8a6e0d1880")
"0x9a68591c0faa138707a90a7506840c562328aeb7621ac0561467c371b0322d51"
HTTP RPC

$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"mainbridge_convertServiceChainBlockHashToMainChainTxHash","params":["0xeadc6a3a29a20c13824b5df1ba05cca1ed248d046382a4f2792aac8a6e0d1880"],"id":1}' http://localhost:8551
{"jsonrpc":"2.0","id":1,"result":"0x9a68591c0faa138707a90a7506840c562328aeb7621ac0561467c371b0322d51"}
## Sub-Bridge APIs
sendChainTxslimit
The sendChainTxslimit gets the maximum number of pending transactions to pick up for sending at once.

Parameters

None

Return Value

Type

Description

Uint64

the maximum number of pending transactions to pickup for sending at once.

Example

> subbridge.sendChainTxslimit
100
anchoring
The subbridge.anchoring can enable/disable the anchoring feature of the service chain.

Parameters

Name

Type

Description

enable

Bool

true enables the anchoring feature, false disables it.

Return Value

Type

Description

bool

true if the anchoring was enabled, false otherwise.

Example

Console

> subbridge.anchoring(true)
true
> subbridge.anchoring(false)
false
HTTP RPC

$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"subbridge_anchoring","params":[true],"id":1}' http://localhost:8551
{"jsonrpc":"2.0","id":1,"result":true}
$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"subbridge_anchoring","params":[false],"id":1}' http://localhost:8551
{"jsonrpc":"2.0","id":1,"result":false}
latestAnchoredBlockNumber
The subbridge.latestAnchoredBlockNumber returns the latest anchored block number of the service chain.

Parameters

None

Return Value

Type

Description

Uint64

The latest anchored block number.

Example

> subbridge.latestAnchoredBlockNumber
71025