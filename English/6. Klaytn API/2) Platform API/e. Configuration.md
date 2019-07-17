# Configuration

## klay_chainID
Returns the chain ID of the chain.

### Parameters

None

### Return Value

Type

Description

QUANTITY

Integer of the chain ID of the chain.

### Example

// Request
curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"klay_chainID","id":1}' http://localhost:8551
​
// Result
{
    "jsonrpc":"2.0",
    "id":1,
    "result":"0x7e2"
}
## klay_clientVersion
Returns the current client version of a Klaytn node.

### Parameters

None

### Return Value

Type

Description

String

The current client version of a Klaytn node.

### Example

// Request
curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"klay_clientVersion","id":1}' http://localhost:8551
​
// Result
{
    "jsonrpc":"2.0",
    "id":1,
    "result":"Klaytn/v0.9.1+3518232250/linux-amd64/go1.11.2"
}
## klay_gasPrice
Returns the current price per gas in peb.

NOTE: This API has different behavior from Ethereum's and returns a gas price of Klaytn instead of suggesting a gas price as in Ethereum.

### Parameters

None

### Return Value

Type

Description

QUANTITY

Integer of the current gas price in peb.

### Example

// Request
curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"klay_gasPrice","params":[],"id":1}' http://localhost:8551
​
// Result
{
  "jsonrpc": "2.0",
  "id":1,
  "result": "0x5d21dba00" // 25,000,000,000 peb = 25 Gpeb
}
## klay_gasPriceAt
Returns the unit price of the given block in peb.

NOTE: This API has different behavior from Ethereum's and returns a gas price of Klaytn instead of suggesting a gas price as in Ethereum.

### Parameters

Type

Description

NUMBER

Block number. If omitted, latest unit price will be retruned.

### Return Value

Type

Description

QUANTITY

Integer of the current gas price in peb.

### Example

// Request
curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"klay_gasPriceAt","params":["0x64"],"id":1}' http://localhost:8551
​
// Result
{
  "jsonrpc": "2.0",
  "id":1,
  "result": "0x5d21dba00" // 25,000,000,000 peb = 25 Gpeb
}
## klay_isParallelDBWrite
Returns true if the node is writing blockchain data in parallel manner. It is enabled by default.

### Parameters

None

### Return Value

Type

Description

Boolean

true means the node is writing blockchain data in parallel manner. It is false if the node is writing the data in serial manner.

### Example

// Request
curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"klay_isParallelDBWrite","id":1}' http://localhost:8551
​
// Result
{
    "jsonrpc":"2.0",
    "id":1,
    "result":true
}
## klay_isSenderTxHashIndexingEnabled
Returns true if the node is indexing sender transaction hash to transaction hash mapping information. It is disabled by default and can be enabled by --sendertxhashindexing.

### Parameters

None

### Return Value

Type

Description

Boolean

true means the node is indexing sender transaction hash to transaction hash mapping information.

###Example

// Request
curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"klay_isSenderTxHashIndexingEnabled","id":1}' http://localhost:8551
​
// Result
{
    "jsonrpc":"2.0",
    "id":1,
    "result":true
}
## klay_protocolVersion
Returns the Klaytn protocol version of the node.

### Parameters

None

### Return Value

Type

Description

String

The Klaytn protocol version of the node.

### Example

// Request
curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"klay_protocolVersion","params":[],"id":1}' http://localhost:8551
​
// Result
{
   "jsonrpc":"2.0",
   "id":1,
   "result":"0x40"
}
## klay_rewardbase
Returns the rewardbase of the current node. Rewardbase is the address of the account where the block rewards goes to. It is only required for CNs.

### Parameters

None

### Return Value

Type

Description

20-byte DATA

Address.

### Example

// Request
curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"klay_rewardbase","id":1}' http://localhost:8551
​
// Result - If requested from non-CN nodes
{
    "jsonrpc":"2.0",
    "id":1,
    "error":{
        "code":-32000,
        "message":"rewardbase must be explicitly specified"
        }
}
​
// Result - If requested from CN nodes
{
    "jsonrpc":"2.0",
    "id":1,
    "result":"0x96Fd91f34Cc8da9f6338C106Ba37aA8B48FB4Fa5"
}
## klay_writeThroughCaching
Returns true if the node is using write through caching. If enabled, block bodies and receipts are cached when they are written to persistent storage. It is false by default.

### Parameters

None

### Return Value

Type

Description

Boolean

true means the node is using write through caching.

### Example

// Request
curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"klay_writeThroughCaching","id":1}' http://localhost:8551
​
// Result
{
    "jsonrpc":"2.0",
    "id":1,
    "result":false
}