# Check Your Network

After running all nodes, you need to check if the network is operating properly.

## Check Block Number
You can check the latest block number on each node to verify if blocks are propagating. To check the latest block number, connect to the Klaytn JavaScript console. If you installed the nodes successfully, the file klay.ipc should be found under the data directory. On each node, attach to the JavaScript console and execute klay.blocknumber from the console prompt as illustrated below.

KCN

$ ./kcn attach ~/cn_data/klay.ipc
> klay.blocknumber
6154
KPN

$ ./kpn attach ~/pn_data/klay.ipc
> klay.blocknumber
6154
KEN

$ ./ken attach ~/en_data/klay.ipc
> klay.blocknumber
6154
## Check Network Topology
On the above JavaScript console, you can also check which nodes are connected to the current node. The expected results are as follows.

KCN

> net.peerCountByType()
{
pn: 1,
total: 1
}
KPN

> net.peerCountByType()
{
cn: 1,
en: 1,
total: 2
}
KEN

> net.peerCountByType()
{
pn: 1,
total: 1
}
