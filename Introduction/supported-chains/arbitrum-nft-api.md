---
title: "Arbitrum NFT API"
slug: "arbitrum-nft-api"
excerpt: "Learn how to access Arbitrum NFT data & trading through Reservoir's developer tools"
hidden: false
createdAt: "2023-04-21T20:22:39.634Z"
updatedAt: "2023-06-14T03:07:42.916Z"
---
# Getting Started with Arbitrum on Reservoir

Reservoir offers access to Arbitrum & a number of EVM-compatible chains through our simple, yet powerful APIs, SDKs & UI kits for NFT trading and data. To get started you can [get an API key](https://docs.reservoir.tools/reference/dashboard-sign-up) which has a [generous free plan & affordable paid subscriptions](https://reservoir.tools/pricing). 

- **Arbitrum API Base URL** - You can access all Reservoir APIs by using the `https://api-arbitrum.reservoir.tools/` base URL. When using the API reference docs for Arbitrum, make sure to change the base URL to the one above.
- **Recommended Test Collection** - Our recommended Arbitrum NFT collection to test with is [Dragon's Crossing Item NFTs](https://arbiscan.io//address/0x64f18f8158ad4ba764bd864d4ffa9df46eedb4ce) contract address: `0x64f18f8158ad4BA764bd864d4fFa9dF46eedB4Ce`. When using the API reference docs, use the collection above to test responses. 

To get a better sense of what we offer, checkout of reference [Arbitrum Marketplace](https://marketplace.reservoir.tools/collection/arbitrum/0x17f4baa9d35ee54ffbcb2608e20786473c7aa49f).

## Access Arbitrum Data with Reservoir

Reservoir gives you access to complete NFT metadata and market data aggregated from across all major marketplaces, including Opensea. You can learn more about our available data in our [NFT Data Overview](ref:nft-data-overview). 

- [Get Aggregated Arbitrum Listings](https://docs.reservoir.tools/reference/getordersasksv4) - [sample response](https://api-arbitrum.reservoir.tools/orders/asks/v4?contracts=0x64f18f8158ad4BA764bd864d4fFa9dF46eedB4Ce)
- [Get Aggregated Arbitrum Offers](https://docs.reservoir.tools/reference/getordersbidsv5) - [sample response](https://api-arbitrum.reservoir.tools/orders/bids/v5?contracts=0x64f18f8158ad4BA764bd864d4fFa9dF46eedB4Ce)
- [Get Arbitrum Floor Prices](https://docs.reservoir.tools/reference/getcollectionsv5) - [sample response](https://api-arbitrum.reservoir.tools/collections/v5?id=0x64f18f8158ad4BA764bd864d4fFa9dF46eedB4Ce)
- [Get Arbitrum Sales Volume](https://docs.reservoir.tools/reference/getcollectionsdailyvolumesv1) - [sample response](https://api-arbitrum.reservoir.tools/collections/daily-volumes/v1?id=0x64f18f8158ad4BA764bd864d4fFa9dF46eedB4Ce)
- [Get Arbitrum Collection Metadata](https://docs.reservoir.tools/reference/gettokensv6) - [sample response](https://api-arbitrum.reservoir.tools/tokens/v6?collection=0x64f18f8158ad4BA764bd864d4fFa9dF46eedB4Ce)

## Trading on Arbitrum with Reservoir

Reservoir makes it simple to not only get market data and orders, but execute and create orders directly through our APIs and tools. To learn more about trading with Reservoir, check out our [NFT Trading Overview](ref:creating-and-filling-orders). On Arbitrum, you can:

**Execute orders** from across major marketplaces, by using the trading APIs or the SDK, which wraps the APIs into simple methods. Check out the buy and sell endpoints below:

- [Buy Arbitrum NFTs](https://docs.reservoir.tools/reference/postexecutebuyv7)
- [Sell Arbitrum NFTs](https://docs.reservoir.tools/reference/postexecutesellv7)

**Create orders** with [custom fees](https://docs.reservoir.tools/docs/custom-fees) and [royalties](https://docs.reservoir.tools/docs/royalties) that will get distributed across the Reservoir ecosystem. Or cross-post orders to major marketplaces that have Arbitrum support. Check out our list and bid endpoints below:

- [List Arbitrum NFTs](https://docs.reservoir.tools/reference/postexecutelistv5)
- [Bid on Arbitrum NFTs](https://docs.reservoir.tools/reference/postexecutebidv5)

## Reservoir Tools Available on Arbitrum

All Reservoir tools including [APIs](https://docs.reservoir.tools/reference/overview), [SDKs](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode) & [ReservoirKit](https://docs.reservoir.tools/reference/reservoirkit) have full Arbitrum support.

# Understanding Arbitrum

Arbitrum, an emerging Layer 2 solution for Ethereum, offers an innovative environment for Non-Fungible Tokens (NFT) marketplaces. It improves upon the base features of Ethereum by enhancing transaction speed, reducing gas costs, and maintaining compatibility with Ethereum's tooling and network effects, leading to a more optimized NFT experience.

## Arbitrum Blockchain Features

1. **Faster Transactions:** Arbitrum significantly increases transaction speed, ensuring a smoother user experience.
2. **Lower Gas Fees:** It reduces Ethereum's notorious high gas fees, making NFT transactions more affordable.
3. **Ethereum Compatibility:** Despite its improvements, Arbitrum remains fully compatible with Ethereum, benefiting from its large-scale adoption.
4. **Secure and Decentralized:** Arbitrum retains the decentralized and secure nature of Ethereum, crucial for NFT marketplaces.