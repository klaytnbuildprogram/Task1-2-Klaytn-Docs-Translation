# caver.klay

The caver-klay package allows you to interact with the Klaytn nodes. The list below enumerates the API functions that are currently supported in caver-js.

## ​Account​
​defaultAccount​

​accountCreated​

​getAccount​

​getAccounts​

​getAccountKey​

​getBalance​

​getCode​

​getTransactionCount​

​isContractAccount​

​Block​
​defaultBlock​

​getBlockNumber​

​getBlock​

​getBlockReceipts​

​getBlockTransactionCount​

​getBlockWithConsensusInfo​

​getCommittee​

​getCommitteeSize​

​getCouncil​

​getCouncilSize​

​getStorageAt​

​isMining​

​isSyncing​

​Transaction​
​call​

​estimateGas​

​estimateComputationCost​

​getTransaction​

​getTransactionBySenderTxHash​

​getTransactionFromBlock​

​getTransactionReceipt​

​getTransactionReceiptBySenderTxHash​

​sendSignedTransaction​

​sendTransaction (Legacy)​

​sendTransaction (VALUE_TRANSFER)​

​sendTransaction (FEE_DELEGATED_VALUE_TRANSFER)​

​sendTransaction (FEE_DELEGATED_VALUE_TRANSFER_WITH_RATIO)​

​sendTransaction (VALUE_TRANSFER_MEMO)​

​sendTransaction (FEE_DELEGATED_VALUE_TRANSFER_MEMO)​

​sendTransaction (FEE_DELEGATED_VALUE_TRANSFER_MEMO_WITH_RATIO)​

​sendTransaction (ACCOUNT_UPDATE)​

​sendTransaction (FEE_DELEGATED_ACCOUNT_UPDATE)​

​sendTransaction (FEE_DELEGATED_ACCOUNT_UPDATE_WITH_RATIO)​

​sendTransaction (SMART_CONTRACT_DEPLOY)​

​sendTransaction (FEE_DELEGATED_SMART_CONTRACT_DEPLOY)​

​sendTransaction (FEE_DELEGATED_SMART_CONTRACT_DEPLOY_WITH_RATIO)​

​sendTransaction (SMART_CONTRACT_EXECUTION)​

​sendTransaction (FEE_DELEGATED_SMART_CONTRACT_EXECUTION)​

​sendTransaction (FEE_DELEGATED_SMART_CONTRACT_EXECUTION_WITH_RATIO)​

​sendTransaction (CANCEL)​

​sendTransaction (FEE_DELEGATED_CANCEL)​

​sendTransaction (FEE_DELEGATED_CANCEL_WITH_RATIO)​

​signTransaction​

## ​Configuration​
​gasPriceAt​

​getChainId​

​getGasPrice​

​getNodeInfo​

​getProtocolVersion​

​isSenderTxHashIndexingEnabled​

​isParallelDBWrite​

​rewardbase​

​writeThroughCaching​

## ​Filter​
​getFilterChanges​

​getFilterLogs​

​getPastLogs​

​newBlockFilter​

​newFilter​

​newPendingTransactionFilter​

​uninstallFilter​

​Miscellaneous​
​sha3​
