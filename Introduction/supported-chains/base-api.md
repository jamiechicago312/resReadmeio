---
title: "Base NFT API"
slug: "base-api"
excerpt: "Learn how to access Base NFT data & trading through Reservoir's developer tools"
hidden: false
createdAt: "2023-07-31T19:36:08.760Z"
updatedAt: "2023-08-04T19:13:28.519Z"
---
# Getting Started with Base on Reservoir

Reservoir offers access to Base & a number of EVM-compatible chains through our simple, yet powerful APIs, SDKs & UI kits for NFT trading and data. To get started you can [get an API key](https://docs.reservoir.tools/reference/dashboard-sign-up) which has a [generous free plan & affordable paid subscriptions](https://reservoir.tools/pricing). 

- **Base API Base URL** - You can access all Reservoir APIs by using the `https://api-base.reservoir.tools` base URL. When using the API reference docs for Arbitrum, make sure to change the base URL to the one above.
- **Recommended Test Collection** - Our recommended Base NFT collection to test with is [Bridge to Base](https://basescan.org/address/0xea2a41c02fa86a4901826615f9796e603c6a4491) contract address: `0xea2a41c02fa86a4901826615f9796e603c6a4491`. When using the API reference docs, use the collection above to test responses. 

To get a better sense of what we offer, check out of reference [Base Marketplace & Explorer](https://explorer.reservoir.tools/base).

## Access Base Data with Reservoir

Reservoir gives you access to complete NFT metadata and market data aggregated from across all major marketplaces, including Opensea. You can learn more about our available data in our [NFT Data Overview](ref:nft-data-overview). 

- [Get Aggregated Base Listings](https://docs.reservoir.tools/reference/getordersasksv4) - [sample response](https://api-base.reservoir.toolsorders/asks/v4?contracts=0xEa2a41c02fA86A4901826615F9796e603C6a4491)
- [Get Aggregated Base Offers](https://docs.reservoir.tools/reference/getordersbidsv5) - [sample response](https://api-base.reservoir.toolsorders/bids/v5?contracts=0xEa2a41c02fA86A4901826615F9796e603C6a4491)
- [Get Base Floor Prices](https://docs.reservoir.tools/reference/getcollectionsv5) - [sample response](https://api-base.reservoir.toolscollections/v5?id=0xEa2a41c02fA86A4901826615F9796e603C6a4491)
- [Get Base Sales Volume](https://docs.reservoir.tools/reference/getcollectionsdailyvolumesv1) - [sample response](https://api-base.reservoir.toolscollections/daily-volumes/v1?id=0xEa2a41c02fA86A4901826615F9796e603C6a4491)
- [Get Base Collection Metadata](https://docs.reservoir.tools/reference/gettokensv6) - [sample response](https://api-base.reservoir.toolstokens/v6?collection=0xEa2a41c02fA86A4901826615F9796e603C6a4491)

## Trading on Base with Reservoir

Reservoir makes it simple to not only get market data and orders, but execute and create orders directly through our APIs and tools. To learn more about trading with Reservoir, check out our [NFT Trading Overview](ref:creating-and-filling-orders). On Base, you can:

**Execute orders** from across major marketplaces, by using the trading APIs or the SDK, which wraps the APIs into simple methods. Check out the buy and sell endpoints below:

- [Buy Base NFTs](https://docs.reservoir.tools/reference/postexecutebuyv7)
- [Sell Base NFTs](https://docs.reservoir.tools/reference/postexecutesellv7)

**Create orders** with [custom fees](https://docs.reservoir.tools/docs/custom-fees) and [royalties](https://docs.reservoir.tools/docs/royalties) that will get distributed across the Reservoir ecosystem. Or cross-post orders to major marketplaces that have Base support. Check out our list and bid endpoints below:

- [List Base  NFTs](https://docs.reservoir.tools/reference/postexecutelistv5)
- [Bid on Base NFTs](https://docs.reservoir.tools/reference/postexecutebidv5)

## Reservoir Tools Available on Base

All Reservoir tools including [APIs](https://docs.reservoir.tools/reference/overview), [SDKs](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode) & [ReservoirKit](https://docs.reservoir.tools/reference/reservoirkit) have full Base support.

# Understanding Base

Base operates as an Ethereum Layer 2 (L2) solution, created by Coinbase, providing security, stability, and scalability for dApps. Deploy any EVM codebase confidently and transition users and assets seamlessly from Ethereum L1, Coinbase, and other chains.

## Key Features:

- **Cost-Effective EVM Environment:** Base offers a cost-effective EVM environment with reduced fees and early access to Ethereum features like Account Abstraction (ERC4337) and gasless transactions.

- **Powered by Optimism:** Built on Optimism's open-source OP Stack, Base ensures a public good for all developers, contributing to funding public goods.

- **Leverage Coinbase's Scalability:** Integrate seamlessly with Coinbase's products and distribution, offering easy fiat onramps and access to the $130B assets on the platform.