---
title: "Global NFT Orderbook"
slug: "global-nft-orderbook"
excerpt: "Create liquidity for your own marketplace or app with built-in distribution to over 100 apps and no protocol-fees."
hidden: false
createdAt: "2023-02-20T21:32:06.957Z"
updatedAt: "2023-06-14T18:14:22.673Z"
---
Reservoir’s open orderbook is a normalized and standardarized NFT orderbook consisting of aggregated NFT order data from across the NFT ecosystem. The goal is to create a global view of NFT liquidity, that’s real time, and executable. 

 Reservoir’s open orderbook is built from: 

- [Data Lake](doc:data-lake): Decentralized order storage on Arweave
- [Open-source Indexer](doc:indexer) An open-source node responsible for reading from the data lake and constructing the orderbook
- Order Relayer: The system responsible for aggregating NFT orders from major marketplaces and depositing them in the data lake.

## Accessing Reservoir’s orderbook

There are several ways to access the Reservoir orderbook, depending on what level of the system you wish to use: 

- [Reservoir API](doc:reservoir-api) - An all-in-one API for building NFT market applications. You get market data and metadata, order execution, and advanced order features like collection and trait level bids, all out of the box. All this functionality is wrapped into the SDK for a higher level of abstraction.
- [Reservoir SDK (JS/TS/Node)](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode)- An abstracted typescript SDK for interacting with the NFT market. All the function of the Reservoir API wrapped into easily-to-use, performant methods.
- [ReservoirKit UI (React)](https://docs.reservoir.tools/reference/reservoirkit) -  A react library that makes it easy to add marketplace functionality and UI into your project.