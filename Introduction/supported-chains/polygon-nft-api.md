---
title: "Polygon NFT API"
slug: "polygon-nft-api"
excerpt: "Learn how to access Polygon NFT data & trading through Reservoir's developer tools"
hidden: false
createdAt: "2023-04-21T20:22:28.106Z"
updatedAt: "2023-06-14T03:07:22.930Z"
---
# Getting Started with Polygon on Reservoir

Reservoir offers access to Polygon & a number of EVM-compatible chains through our simple, yet powerful APIs, SDKs & UI kits for NFT trading and data. To get started you can [get an API key](https://docs.reservoir.tools/reference/dashboard-sign-up) which has a generous [free plan & affordable paid subscriptions](https://reservoir.tools/pricing). 

- **Polygon API Base URL** - You can access all Reservoir APIs by using the `https://api-polygon.reservoir.tools/` base URL. When using the API reference docs for Polygon, make sure to change the base URL to the one above.
- **Recommended Test Collection** - Our recommended Polygon NFT collection to test with is [Aww Friends x Reddit Collectible Avatars](https://polygonscan.com/address/0x6acb8fb82880d39c2b8446f8778a14d34ee6cfb7) contract address: `0x6acb8fb82880d39c2b8446f8778a14d34ee6cfb7`. When using the API reference docs, use the collection above to test responses. 

To get a better sense of what we offer, checkout of reference [Polygon marketplace](https://marketplace.reservoir.tools/collection/polygon/0x670fd103b1a08628e9557cd66b87ded841115190).

## Access Polygon Data with Reservoir

Reservoir gives you access to complete NFT metadata and market data aggregated from across all major marketplaces, including Opensea. You can learn more about our available data in our [NFT Data Overview](ref:nft-data-overview). 

- [Get Aggregated Polygon Listings](https://docs.reservoir.tools/reference/getordersasksv4) - [sample response](https://api-polygon.reservoir.tools/orders/asks/v4?contracts=0x6acb8fb82880d39c2b8446f8778a14d34ee6cfb7)
- [Get Aggregated Polygon Offers](https://docs.reservoir.tools/reference/getordersbidsv5) - [sample response](https://api-polygon.reservoir.tools/orders/bids/v5?contracts=0x6acb8fb82880d39c2b8446f8778a14d34ee6cfb7)
- [Get Polygon Floor Prices](https://docs.reservoir.tools/reference/getcollectionsv5) - [sample response](https://api-polygon.reservoir.tools/collections/0x6acB8fb82880d39c2B8446F8778A14d34Ee6cFb7/attributes/explore/v4)
- [Get Polygon Sales Volume](https://docs.reservoir.tools/reference/getcollectionsdailyvolumesv1) - [sample response](https://api-polygon.reservoir.tools/collections/daily-volumes/v1?id=0x6acB8fb82880d39c2B8446F8778A14d34Ee6cFb7)
- [Get Polygon Collection Metadata](https://docs.reservoir.tools/reference/gettokensv6) - [sample response](https://api-polygon.reservoir.tools/tokens/v6?collection=0x6acB8fb82880d39c2B8446F8778A14d34Ee6cFb7)

## Trading on Polygon with Reservoir

Reservoir makes it simple to not only get market data and orders, but execute and create orders directly through our APIs and tools. To learn more about trading with Reservoir, check out our [NFT Trading Overview](ref:creating-and-filling-orders). On Polygon, you can:

**Execute orders** from across major marketplaces, by using the trading APIs or the SDK, which wraps the APIs into simple methods. Check out the buy and sell endpoints below:

- [Buy Polygon NFTs](https://docs.reservoir.tools/reference/postexecutebuyv7)
- [Sell Polygon NFTs](https://docs.reservoir.tools/reference/postexecutesellv7)

**Create orders** with [custom fees](https://docs.reservoir.tools/docs/custom-fees) and [royalties](https://docs.reservoir.tools/docs/royalties) that will get distributed across the Reservoir ecosystem. Or cross-post orders to major marketplaces that have Polygon support. Check out our list and bid endpoints below:

- [List Polygon NFTs](https://docs.reservoir.tools/reference/postexecutelistv5)
- [Bid on Polygon NFTs](https://docs.reservoir.tools/reference/postexecutebidv5)

## Reservoir Tools Available on Polygon

All Reservoir tools including [APIs](https://docs.reservoir.tools/reference/overview), [SDKs](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode) & [ReservoirKit](https://docs.reservoir.tools/reference/reservoirkit) have full Polygon support.

# Understanding Polygon

Polygon is an Ethereum Layer 2 scaling solution that enhances Ethereum's capability by providing a faster, more efficient framework. By resolving the prevalent issues of slow block confirmations and high gas fees, Polygon allows for a seamless user experience in a secure and decentralized manner. Thanks to its compatibility with Ethereum's network and tooling, it's a perfect solution for developers looking to build scalable applications. Polygon's NFT ecosystem is burgeoning, with new major collections and applications launching on the chain.

## Polygon Blockchain Features

1. **Scalability:** Polygon offers a scalable environment that can handle a much higher number of transactions per second (TPS) compared to Ethereum.

2. **Low Transaction Costs:** The Polygon chain provides a more cost-effective solution for transactions, making micro-transactions more feasible and affordable.

3. **Interoperability:** Polygon supports the transfer of any type of data or asset across different blockchains, facilitating greater interaction between various protocols.

4. **Security:** Leveraging Ethereum's network security, Polygon offers a secure platform for developing and deploying smart contracts.