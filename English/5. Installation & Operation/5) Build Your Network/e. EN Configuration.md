# EN Configuration

## EN Setup
After installing KEN package properly, you need to copy the initial files to the EN data directory. For example, assuming homi-output is under the home directory as well as the ken data directory,

cp ~/homi-output/scripts/genesis.json ~/en_data/genesis.json
cp ~/homi-output/scripts_pn/static-nodes.json ~/en_data/static-nodes.json
Then, initialize the genesis block with the following command.

$ ./ken --datadir ~/en_data init ~/en_data/genesis.json
...
Now, we are ready to launch an EN node locally.

## KEN Start and Confirmation
You can run the configured EN with the following command.

$ ./kend start
Inspect the log outputs. Below logs are an example of under normal operation.

$ tail -f ~/en_data/logs/kend.out
...
INFO[06/24,15:32:03 +09] [5] Imported new chain segment                number=4481 hash=fde09b…7cf4e6 blocks=1   txs=0 elapsed=875.891µs trieDBSize=1.02kB mgas=0.000 mgasps=0.000
INFO[06/24,15:32:04 +09] [5] Imported new chain segment                number=4482 hash=b28ac7…751fd0 blocks=1   txs=0 elapsed=764.289µs trieDBSize=1.02kB mgas=0.000 mgasps=0.000
INFO[06/24,15:32:05 +09] [5] Imported new chain segment                number=4483 hash=e8404a…9f6a13 blocks=1   txs=0 elapsed=846.464µs trieDBSize=1.02kB mgas=0.000 mgasps=0.000
INFO[06/24,15:32:06 +09] [5] Imported new chain segment                number=4484 hash=3e38ee…596d2c blocks=1   txs=0 elapsed=823.968µs trieDBSize=1.36kB mgas=0.000 mgasps=0.000
INFO[06/24,15:32:07 +09] [5] Imported new chain segment                number=4485 hash=e781f5…13fd0d blocks=1   txs=0 elapsed=856.59µs  trieDBSize=1.36kB mgas=0.000 mgasps=0.000
