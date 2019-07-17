# Platform API

The Klaytn platform API is provided under the klay namespace. The list below enumerates the API functions that are currently supported in Klaytn.

## ​Account​
​klay_accountCreated​

​klay_accounts​

​klay_getAccount​

​klay_getAccountKey​

​klay_getBalance​

​klay_getCode​

​klay_getTransactionCount​

​klay_isContractAccount​

​klay_sign​

## ​Block​
​klay_blockNumber​

​klay_getBlockByNumber​

​klay_getBlockByHash​

​klay_getBlockReceipts​

​klay_getBlockTransactionCountByNumber​

​klay_getBlockTransactionCountByHash​

​klay_getBlockWithConsensusInfoByHash​

​klay_getBlockWithConsensusInfoByNumber​

​klay_getCommittee​

​klay_getCommitteeSize​

​klay_getCouncil​

​klay_getCouncilSize​

​klay_getStorageAt​

​klay_mining​

​klay_syncing​

## ​Transaction​
​klay_call​

​klay_estimateGas​

​klay_estimateComputationCost​

​klay_getTransactionByBlockHashAndIndex​

​klay_getTransactionByBlockNumberAndIndex​

​klay_getTransactionByHash​

​klay_getTransactionBySenderTxHash​

​klay_getTransactionReceipt​

​klay_getTransactionReceiptBySenderTxHash​

​klay_sendRawTransaction​

​klay_sendTransaction​

​klay_signTransaction​

## ​Configuration​
​klay_chainID​

​klay_clientVersion​

​klay_gasPrice​

​klay_gasPriceAt​

​klay_isParallelDBWrite​

​klay_isSenderTxHashIndexingEnabled​

​klay_protocolVersion​

​klay_rewardbase​

​klay_writeThroughCaching​

## ​Filter​
​klay_getFilterChanges​

​klay_getFilterLogs​

​klay_getLogs​

​klay_newBlockFilter​

​klay_newFilter​

​klay_newPendingTransactionFilter​

​klay_uninstallFilter​

## ​Miscellaneous​
​klay_sha3​
