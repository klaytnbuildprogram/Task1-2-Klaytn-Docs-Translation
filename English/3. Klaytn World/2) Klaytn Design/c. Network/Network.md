# Network
Figure 2. Klaytn Network and its Logical Subnetworks (CCN, ENN, SCN)
Klaytn blockchain network is a combination of peer-to-peer subnetworks of nodes transmitting transactions and blocks to execute value transfers and run smart contracts. Klaytn network can be partitioned into three logical subnetworks based on their roles and purposes, as shown in Figure 2.

## Core Cell Network (CCN)
CCN consists of Core Cells (CCs) that verify and execute transactions submitted through Endpoint Nodes (ENs). CCN is also responsible for creating and propagating blocks throughout the network.

## Endpoint Node Network (ENN)
ENN consists of Endpoint Nodes (ENs) that mainly create transactions, handle RPC API requests, and process data requests from service chains.

## Service Chain Network (SCN)
SCNs are Klaytn subnetworks composed of auxiliary blockchains independently operated by blockchain applications (BApps). Servicechains are connected via ENN to handle data requests together with Klaytn network.
