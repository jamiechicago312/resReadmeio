---
title: "Reservoir API Overview"
slug: "overview"
excerpt: "Learn how to use the Reservoir API to get NFT data, create orders, and execute trades"
hidden: false
createdAt: "2022-06-09T21:24:29.775Z"
updatedAt: "2023-06-14T03:19:04.030Z"
---
# Overview

The Reservoir API is an all-in-one endpoint for building NFT applications. Get started for free by creating an account on our [Developer Dashboard](https://auth.reservoir.tools/u/login?state=hKFo2SBJUmJTUXhzc1lpVVpEdDZaZm5sZnRfdnRvc0NiRmlUTqFur3VuaXZlcnNhbC1sb2dpbqN0aWTZIDVGQktHcFJDV3V0UnhfYzl1ZXBaWjJKZmNSNG0wQk9Do2NpZNkgN3BPWXNyNDE5c0ROUnB3Qm13NE5KZXRnNWQ4RUhWWEU).

## NFT trading

- [Buy tokens](ref:postexecutebuyv7) and [accept bids](ref:postexecutesellv7) from major marketplaces
- Create your own [orderbook](ref:postorderv4), including advanced order types
- Cross post [bids](ref:postexecutebidv5) and [asks](ref:postexecutelistv5) to other major marketplaces

Learn more about our NFT trading APIs [here](ref:creating-and-filling-orders).

## NFT data

- [Granular token price data](ref:gettokensfloorv1) with flexible querying options
- Real-time [collection floor price](ref:geteventscollectionsflooraskv2) and [top bid](ref:geteventscollectionstopbidv2) events
- Aggregated NFT [orders](ref:orders), for executing buys and sells
- Detailed [metadata](ref:getcollectionsv5) that can be used to analyze data (e.g. [Collection attributes](ref:attributes))
- Token [ownership data](ref:owners) and [collection statistics](ref:getstatsv2)
- Leverage NFT price and token status oracles
- Get real-time and historical [royalty data](doc:royalties)

Learn more about all our NFT data endpoints [here](ref:nft-data-overview).

# Hosted API

The Reservoir API is powered by an open-source indexer that runs entirely off open and permissionless data sources. This means there are no centralized gatekeepers to depend on. The core team runs a production-ready instance of the Reservoir API that supports Ethereum Mainnet, Polygon, Arbitrum, Optimism and Goerli. The following documentation shows you how to intereact with this hosted version of the API:

**Stable**  
`<https://api.reservoir.tools/`>  
`<https://api-goerli.reservoir.tools/`>  
`<https://api-polygon.reservoir.tools/`>

**Beta**  
`<https://api-arbitrum.reservoir.tools/`>  
`<https://api-optimism.reservoir.tools/`>  
`<https://api-arbitrum-nova.reservoir.tools/`>  
`<https://api-sepolia.reservoir.tools/`>  
`<https://api-base-goerli.reservoir.tools/`>  
`<https://api-scroll-alpha.reservoir.tools/`>

`<https://api-zora-testnet.reservoir.tools/`>

# Versioning

In order to ensure backwards compatibility, any changes to API endpoints are deployed as new versions. We will strive to keep old versions available for as long as possible, while also working closely with you to help upgrade.