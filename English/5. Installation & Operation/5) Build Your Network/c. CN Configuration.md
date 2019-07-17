# CN Configuration

## CN Setup
After installing KCN package properly, you need to copy the initial files to the CN data directory. For example, assuming homi-output is under the home directory as well as the kcn data directory,

cp ~/homi-output/keys/nodekey1 ~/cn_data/nodekey
cp ~/homi-output/keys/validator1 ~/cn_data/validator
cp ~/homi-output/scripts/genesis.json ~/cn_data/genesis.json
Then, initialize the genesis block with the following command.

$ ./kcn --datadir ~/cn_data init ~/cn_data/genesis.json
...
### Setup Rewardbase
You can find validator information in the validator file that you copied in the previous section. The example of the validator contents is shown as follows.

$ cat validator
{
    "Address": "0xed8aa7a845443552165383912f48394a77d77933",
    "Nodekey": "8e7a0684d58925b29bc93176e7ba806ddd1a611becc458b1361f6b4bf82cf2a4",
    "NodeInfo": "kni://7be41828e81fbf20e00868e858e86380cb0128896b6628666477448ade6f837be4310ac0abeea25e24b0f3b2347f154628aa6eb5b2e39d36f0c8fb2fa0ca9aa3@0.0.0.0:32323?discport=0\u0026ntype=cn"
}
Please update the REWARDBASE in the kcnd.conf with your validator address, that is, in the above example, "0xed8aa7a845443552165383912f48394a77d77933"),

...
REWARDBASE="0xed8aa7a845443552165383912f48394a77d77933"
...
Now, we are ready to launch a CN node locally.

## KCN Start and Confirmation
You can run the CN with the following command.

$ ./kcnd start
Inspect the log outputs. Below logs are an example of under normal operation.

$ tail -f ~/cn_data/logs/kcnd.out
...
INFO[06/24,15:31:44 +09] [49] Successfully sealed new block             number=4462 hash=3349ca…232497
INFO[06/24,15:31:44 +09] [49] Successfully wrote mined block            num=4462 hash=3349ca…232497 txs=0
INFO[06/24,15:31:44 +09] [49] Commit new mining work                    number=4463 txs=0 elapsed=219.591µs
INFO[06/24,15:31:45 +09] [24] Committed                                 number=4463 hash=644f2e…1adcf9 address=0xeD8aa7a845443552165383912F48394a77d77933
INFO[06/24,15:31:45 +09] [49] Successfully sealed new block             number=4463 hash=644f2e…1adcf9
INFO[06/24,15:31:45 +09] [49] Successfully wrote mined block            num=4463 hash=644f2e…1adcf9 txs=0
INFO[06/24,15:31:45 +09] [49] Commit new mining work                    number=4464 txs=0 elapsed=197.757µs
INFO[06/24,15:31:46 +09] [24] Committed                                 number=4464 hash=85499f…c8e232 address=0xeD8aa7a845443552165383912F48394a77d77933
INFO[06/24,15:31:46 +09] [49] Successfully sealed new block             number=4464 hash=85499f…c8e232
INFO[06/24,15:31:46 +09] [49] Successfully wrote mined block            num=4464 hash=85499f…c8e232 txs=0
INFO[06/24,15:31:46 +09] [49] Commit new mining work                    number=4465 txs=0 elapsed=204.702µs
