# PN Configuration

## PN Setup
After installing KPN package properly, you need to copy the initial files to the PN data directory. For example, assuming homi-output is under the home directory as well as the kpn data directory,

cp ~/homi-output/keys_pn/nodekey1 ~/pn_data/nodekey
cp ~/homi-output/keys_pn/validator1 ~/pn_data/validator
cp ~/homi-output/scripts/genesis.json ~/pn_data/genesis.json
cp ~/homi-output/scripts/static-nodes.json ~/pn_data/static-nodes.json
Then, initialize the genesis block with the following command.

$ ./kpn --datadir ~/pn_data init ~/pn_data/genesis.json
...
Now, we are ready to launch a PN node locally.

## KPN Start and Confirmation
You can run the configured PN with the following command.

$ ./kpnd start
Inspect the log outputs. Below logs are an example of under normal operation.

$ tail -f ~/pn_data/logs/kpnd.out
...
INFO[06/24,15:31:54 +09] [5] Imported new chain segment                number=4472 hash=0eec52…6a9473 blocks=1   txs=0 elapsed=917.694µs trieDBSize=1.36kB mgas=0.000 mgasps=0.000
INFO[06/24,15:31:55 +09] [5] Imported new chain segment                number=4473 hash=5ce333…21a418 blocks=1   txs=0 elapsed=858.57µs  trieDBSize=1.36kB mgas=0.000 mgasps=0.000
INFO[06/24,15:31:56 +09] [5] Imported new chain segment                number=4474 hash=8da93a…6f28a3 blocks=1   txs=0 elapsed=1.079ms   trieDBSize=1.36kB mgas=0.000 mgasps=0.000
INFO[06/24,15:31:57 +09] [5] Imported new chain segment                number=4475 hash=87864c…489b6d blocks=1   txs=0 elapsed=947.986µs trieDBSize=1.36kB mgas=0.000 mgasps=0.000
INFO[06/24,15:31:58 +09] [5] Imported new chain segment                number=4476 hash=a93f9b…591082 blocks=1   txs=0 elapsed=845.698µs trieDBSize=1.36kB mgas=0.000 mgasps=0.000
