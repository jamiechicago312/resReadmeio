---
title: "Indexer"
slug: "indexer"
excerpt: "Reservoir's open-source indexer constructs the global NFT orderbook"
hidden: false
createdAt: "2023-02-28T17:08:52.607Z"
updatedAt: "2023-03-02T04:20:04.447Z"
---
The Reservoir Indexer is an open-source node responsible for reading from and writing to the [Data Lake](https://docs.reservoir.tools/docs/data-lake) and reconstructing the [Global NFT Orderbook](doc:global-nft-orderbook). The Indexer combines raw order data from Arweave, with ownership data from Ethereum, to trustlessly reconstruct the state of the orderbook and provides open [APIs](https://docs.reservoir.tools/docs/reservoir-api) for interacting with the data.

If you wish to run your own indexer, please check out our docs on self-hosting [Self-hosting](doc:hosted-vs-self-hosted) or go straight to the github repo [here](https://github.com/reservoirprotocol/indexer).