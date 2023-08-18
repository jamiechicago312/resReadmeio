---
title: "Data Lake"
slug: "data-lake"
excerpt: "Decentralized order storage on Arweave"
hidden: false
createdAt: "2023-02-20T21:34:17.163Z"
updatedAt: "2023-02-28T17:12:09.841Z"
---
The Reservoir Data Lake is an open and permissionless data repository built on top of Arweave. It is designed to bring off-chain liquidity on-chain, so that it's publicly available for anyone to leverage. This is critical for building composable protocols and applications that aren't dependent on a single centralized gatekeeper.

Reservoir's Data Lake is purely focused on storing raw order data, without actually checking if they are valid. This is partly to keep costs as low as possible, and partly because validity checking requires understanding the state of the parent blockchain in order to know who owns which tokens. This validation is performed at a higher level, by an Indexer node, which can reconstruct the state of the Orderbook from the raw data on each chain.

The Data Lake is a light-weight protocol on top of Arweave, with transactions that are published with the following tags:

`App-Name: Reservoir ProtocolApp-Version: 0.0.1Network: mainnet / goerli`

[Example Transaction](https://viewblock.io/arweave/tx/DomOJe5Efye10uJudxLQMubQPQtyFJTTxLoNO0ttjIw)

The data is an array of objects, each with a kind:

`{ "kind":"string", "data":"object"}`

[Example Blob](https://b2ey4jpoir7spnos4jxhoewqgltnapiloikjju6exigtws3nrsga.arweave.net/DomOJe5Efye10uJudxLQMubQPQtyFJTTxLoNO0ttjIw)

The system is designed to be extensible, with new kinds added over time. This can either be new exchanges, with their own order formats, or any other data that might be relevant. For example, mutable NFT metadata like collection descriptions or royalties could be stored in Reservoir's Data Lake, instead of needing to be configured on each NFT marketplace.