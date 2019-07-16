# CC Operation Guide
This document is an operation guide describing how to set up and operate a Core Cell (CC), which plays a role of generating blocks in the Klaytn blockchain network.

Klaytn is a blockchain network (also a name of blockchain platform) where the multiple computers are connected to each other in a peer-to-peer manner and transmit transactions and blocks to record value transfers and execute smart contracts. Depending on the functions, duties, or purposes, the Klaytn network can logically be partitioned into subnetworks as shown in Figure 1.


Figure 1. Klaytn Network
Subnetwork

Description

Core Cell Network (CCN)

The network consists of Core Cells (CCs) that verify and execute submitted transactions.  CCN is also responsible for the creation and propagation of blocks with the transactions.

Endpoint Node Network (ENN)

The network consists of the Endpoint Nodes (ENs), which mainly create transactions, handle RPC API requests, or process the data from service chains.

Service Chain Network (SCN)

This network is an auxiliary blockchain network specialized for the services that require higher performance, different node configurations, or security levels compared to the mainchain.  SCN can be connected to the mainchain for data anchoring or value transfers across chains.


Figure 2. A Closeup of CCN and ENN in the Klaytn Network
Figure 2 illustrates details of CCN, which consists of Consensus Node Network (CNN) and Proxy Node Network (PNN), as well as ENN in the Klaytn network. Note that CCN is a network of connected CCs, but since each CC is again composed of one CN and two PNs, Figure 2 shows a different angle of node connections. CNs are linked to each other, and they form a full-mesh network called CNN. On the other hand, PNs are connected together only when they are not in the same CC. Specifically, one PN in one CC does not directly communicate with the other PN in the same CC and is connected to a PN in a different CC. The number of connections between PNs will typically be one, but it can be changed depending on the network situation. The network consisting of PNs in CCN is called PNN. The outermost network in Figure 2 is ENN including only ENs, which are connected to each other and also linked to some PNs in PNN. Bootnodes, such as PN bootnode and EN bootnodes, help PNs and ENs to register themselves in the network and to discover other nodes to connect to.

This guide focuses on CC as it is a core component in the Klaytn network and is a unit of node operation. Guides regarding other nodes or service chains will be provided as separate documents in the future.

Below are the main steps to install and operate a CC, and the next chapters will describe each step in detail.

Prepare proper infrastructure to run a CC (e.g., bare-metal machines or cloud VM instances).

Setup the subnet for CC.

Install and configure the CC executables.

Start the Klaytn service.
