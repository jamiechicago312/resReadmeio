---
title: "Ethereum NFT API"
slug: "ethereum"
excerpt: "Learn how to access Ethereum NFT data & trading through Reservoir's developer tools"
hidden: false
createdAt: "2023-05-22T16:49:03.160Z"
updatedAt: "2023-06-14T03:07:10.165Z"
---
# Getting Started with Ethereum on Reservoir

Reservoir offers access to Ethereum & a number of EVM-compatible chains through our simple, yet powerful APIs, SDKs & UI kits for NFT trading and data. To get started you can [get an API key](https://docs.reservoir.tools/reference/dashboard-sign-up) which has a [generous free plan & affordable paid subscriptions](https://reservoir.tools/pricing). 

- **Ethereum API Base URL** - You can access all Reservoir APIs by using the `https://api.reservoir.tools/` base URL. When using the API reference docs for Ethereum, make sure to change the base URL to the one above. 
- **Recommended Test Collection** - Our recommended Ethereum NFT collection to test with is [Blitmap](https://etherscan.io/address/0x8d04a8c79ceb0889bdd12acdf3fa9d207ed3ff63) contract address: `0x8d04a8c79ceb0889bdd12acdf3fa9d207ed3ff63`. When using the API reference docs, use the collection above to test responses. 

To get a better sense of what we offer, checkout of reference [Ethereum marketplace](https://marketplace.reservoir.tools/collection/ethereum/0x8d04a8c79ceb0889bdd12acdf3fa9d207ed3ff63). 

## Access Ethereum Data with Reservoir

Reservoir gives you access to complete NFT metadata and market data aggregated from across all major marketplaces including Opensea, Blur, X2Y2, and more. You can learn more about our available data in our [NFT Data Overview](ref:nft-data-overview). 

- [Get Aggregated Ethereum Listings](https://docs.reservoir.tools/reference/getordersasksv4) - [sample response](https://api.reservoir.tools/orders/asks/v4?contracts=0x8d04a8c79ceb0889bdd12acdf3fa9d207ed3ff63)
- [Get Aggregated Ethereum Offers](https://api.reservoir.tools/orders/bids/v5?tokenSetId=contract%3A0x8d04a8c79ceb0889bdd12acdf3fa9d207ed3ff63) - [sample response](https://api.reservoir.tools/orders/bids/v5?contracts=0x8d04a8c79ceb0889bdd12acdf3fa9d207ed3ff63)
- [Get Ethereum Floor Prices](https://docs.reservoir.tools/reference/getcollectionsv5) - [sample response](https://api.reservoir.tools/collections/0x63FA29Fec10C997851CCd2466Dad20E51B17C8aF/attributes/explore/v4)
- [Get Ethereum Sales Volume](https://docs.reservoir.tools/reference/getcollectionsdailyvolumesv1) - [sample response](https://api.reservoir.tools/collections/daily-volumes/v1?id=0x63FA29Fec10C997851CCd2466Dad20E51B17C8aF)
- [Get Ethereum Collection Metadata](https://docs.reservoir.tools/reference/gettokensv6) - [sample response](https://api.reservoir.tools/tokens/v6?collection=0x63FA29Fec10C997851CCd2466Dad20E51B17C8aF)

## Trading on Ethereum with Reservoir

Reservoir makes it simple to not only get market data and orders, but execute and create orders directly through our APIs and tools. To learn more about trading with Reservoir, check out our [NFT Trading Overview](ref:creating-and-filling-orders). On Ethereum, you can:

**Execute orders** from across major marketplaces, by using the trading APIs or the SDK, which wraps the APIs into simple methods. Check out the buy and sell endpoints below:

- [Buy Ethereum NFTs](https://docs.reservoir.tools/reference/postexecutebuyv7)
- [Sell Ethereum NFTs](https://docs.reservoir.tools/reference/postexecutesellv7)

**Create orders** with [custom fees](https://docs.reservoir.tools/docs/custom-fees) and [royalties](https://docs.reservoir.tools/docs/royalties) that will get distributed across the Reservoir ecosystem. Or cross-post orders to major marketplaces that have Ethereum support. Check out our list and bid endpoints below:

- [List Ethereum NFTs](https://docs.reservoir.tools/reference/postexecutelistv5)
- [Bid on Ethereum NFTs](https://docs.reservoir.tools/reference/postexecutebidv5)

## Reservoir Tools Available on Ethereum

All Reservoir tools including [APIs](https://docs.reservoir.tools/reference/overview), [SDKs](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode) & [ReservoirKit](https://docs.reservoir.tools/reference/reservoirkit) have full Ethereum support.

# Understanding Ethereum

Ethereum, a pioneering blockchain platform, provides a robust infrastructure for Non-Fungible Tokens (NFT) marketplaces, setting itself apart from other blockchains through its unique features. Its groundbreaking functionalities, such as Smart Contracts, the ERC-721 standard, decentralization, and large-scale adoption, have shaped the thriving NFT landscape.

## Ethereum Blockchain Features

1. **Smart Contracts:** At the heart of Ethereum are smart contracts - self-executing contracts with the terms of the agreement directly written into lines of code. These allow for secure and trustless transactions, making it perfect for conducting trades on NFT marketplaces.
2. **ERC-721 Standard:** Ethereum introduced a standard for NFTs known as ERC-721. This standard ensures that each token is unique, distinguishing Ethereum from other blockchains and making it ideal for minting and trading NFTs.
3. **Decentralization:** Ethereum's decentralized nature makes it immune to censorship and gives it resilience to attempts of control. This appeals to artists and creators who wish to have total ownership of their work.
4. **Large-scale Adoption:** As one of the first widely adopted blockchains, Ethereum is the backbone of many NFT transactions.