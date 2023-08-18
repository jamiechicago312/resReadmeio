---
title: "Optimism NFT API"
slug: "optimism"
excerpt: "Learn how to access Optimism NFT data & trading through Reservoir's developer tools"
hidden: false
createdAt: "2023-05-22T16:48:49.674Z"
updatedAt: "2023-06-14T03:07:31.636Z"
---
# Getting Started with Optimism on Reservoir

Reservoir offers access to Optimism & a number of EVM-compatible chains through our simple, yet powerful APIs, SDKs & UI kits for NFT trading and data. To get started you can [get an API key](https://docs.reservoir.tools/reference/dashboard-sign-up) which has a [generous free plan & affordable paid subscriptions](https://reservoir.tools/pricing). 

- **Optimism API Base URL** - You can access all Reservoir APIs by using the `https://api-optimism.reservoir.tools/` base URL. When using the API reference docs for Optimism, make sure to change the base URL to the one above.
- **Recommended Test Collection** - Our recommended Optimism NFT collection to test with is [Bored Town](https://optimistic.etherscan.io/address/0x8e56343adafa62dac9c9a8ac8c742851b0fb8b03) contract address: `0x8E56343adAFA62DaC9C9A8ac8c742851B0fb8b03`. When using the API reference docs, use the collection above to test responses. 

To get a better sense of what we offer, checkout of reference [Optimism Marketplace](https://marketplace.reservoir.tools/collection/optimism/0x8e56343adafa62dac9c9a8ac8c742851b0fb8b03).

## Access Optimism Data with Reservoir

Reservoir gives you access to complete NFT metadata and market data aggregated from across all major marketplaces, including Opensea. You can learn more about our available data in our [NFT Data Overview](ref:nft-data-overview). 

- [Get Aggregated Optimism Listings](https://docs.reservoir.tools/reference/getordersasksv4) - [sample response](https://api-optimism.reservoir.tools/orders/asks/v4?contracts=0x8E56343adAFA62DaC9C9A8ac8c742851B0fb8b03)
- [Get Aggregated Optimism Offers](https://docs.reservoir.tools/reference/getordersbidsv5) - [sample response](https://api-optimism.reservoir.tools/orders/bids/v5?contracts=0x8E56343adAFA62DaC9C9A8ac8c742851B0fb8b03)
- [Get Optimism Floor Prices](https://docs.reservoir.tools/reference/getcollectionsv5) - [sample response](https://api-optimism.reservoir.tools/collections/0x8E56343adAFA62DaC9C9A8ac8c742851B0fb8b03/attributes/explore/v4)
- [Get Optimism Sales Volume](https://docs.reservoir.tools/reference/getcollectionsdailyvolumesv1) - [sample response](https://api-optimism.reservoir.tools/collections/daily-volumes/v1?id=0x8E56343adAFA62DaC9C9A8ac8c742851B0fb8b03)
- [Get Optimism Collection Metadata](https://docs.reservoir.tools/reference/gettokensv6) - [sample response](https://api-optimism.reservoir.tools/tokens/v6?collection=0x8E56343adAFA62DaC9C9A8ac8c742851B0fb8b03)

## Trading on Optimism with Reservoir

Reservoir makes it simple to not only get market data and orders, but execute and create orders directly through our APIs and tools. To learn more about trading with Reservoir, check out our [NFT Trading Overview](ref:creating-and-filling-orders). On Optimism, you can:

**Execute orders** from across major marketplaces, by using the trading APIs or the SDK, which wraps the APIs into simple methods. Check out the buy and sell endpoints below:

- [Buy Optimism NFTs](https://docs.reservoir.tools/reference/postexecutebuyv7)
- [Sell Optimism NFTs](https://docs.reservoir.tools/reference/postexecutesellv7)

**Create orders** with [custom fees](https://docs.reservoir.tools/docs/custom-fees) and [royalties](https://docs.reservoir.tools/docs/royalties) that will get distributed across the Reservoir ecosystem. Or cross-post orders to major marketplaces that have Optimism support. Check out our list and bid endpoints below:

- [List Optimism NFTs](https://docs.reservoir.tools/reference/postexecutelistv5)
- [Bid on Optimism NFTs](https://docs.reservoir.tools/reference/postexecutebidv5)

## Reservoir Tools Available on Optimism

All Reservoir tools including [APIs](https://docs.reservoir.tools/reference/overview), [SDKs](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode) & [ReservoirKit](https://docs.reservoir.tools/reference/reservoirkit) have full Optimism support.

# Understanding Optimism

Optimism, a Layer 2 scaling solution for Ethereum, brings a new level of performance to Non-Fungible Tokens (NFT) marketplaces. It takes Ethereum's foundational features and enhances them through increasing transaction throughput, reducing gas fees, and maintaining Ethereum compatibility, thereby delivering a more efficient and cost-effective NFT trading experience.

## Optimism Blockchain Features

1. **Increased Throughput:** Optimism significantly boosts transaction speed, creating a more responsive user experience.
2. **Reduced Gas Fees:** It lowers the high transaction costs associated with Ethereum, making NFT transactions more cost-effective.
3. **Ethereum Compatibility:** Optimism is fully compatible with Ethereum's existing infrastructure, benefiting from its vast network and adoption.
4. **Security and Decentralization:** It upholds the decentralized and secure nature of Ethereum, which is vital for the integrity of NFT marketplaces.