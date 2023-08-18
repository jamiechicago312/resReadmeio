---
title: "Arbitrum Nova API"
slug: "arbitrum-nova-api"
hidden: false
createdAt: "2023-06-08T18:26:00.654Z"
updatedAt: "2023-06-14T03:07:51.250Z"
---
# Getting Started with Arbitrum Nova on Reservoir

Reservoir offers access to Arbitrum Nova & a number of EVM-compatible chains through our simple, yet powerful APIs, SDKs & UI kits for NFT trading and data. To get started you can [get an API key](https://docs.reservoir.tools/reference/dashboard-sign-up) which has a [generous free plan & affordable paid subscriptions](https://reservoir.tools/pricing). 

- **Arbitrum Nova API Base URL** - You can access all Reservoir APIs by using the `https://api-arbitrum-nova.reservoir.tools` base URL. When using the API reference docs for Arbitrum, make sure to change the base URL to the one above.
- **Recommended Test Collection** - Our recommended Arbitrum Nova NFT collection to test with is [Nova Punks](https://nova.arbiscan.io/address/0xFCf6bEf0579D4e6Da537B8154fa3b28102a574ab) contract address: `0xFCf6bEf0579D4e6Da537B8154fa3b28102a574ab`. When using the API reference docs, use the collection above to test responses. 

To get a better sense of what we offer, check out of reference [Arbitrum Nova Marketplace](https://marketplace.reservoir.tools/collection/arbitrum/0xfcf6bef0579d4e6da537b8154fa3b28102a574ab).

## Access Arbitrum Nova Data with Reservoir

Reservoir gives you access to complete NFT metadata and market data aggregated from across all major marketplaces, including Opensea. You can learn more about our available data in our [NFT Data Overview](ref:nft-data-overview). 

- [Get Aggregated Arbitrum Nova Listings](https://docs.reservoir.tools/reference/getordersasksv4) - [sample response](https://api-arbitrum-nova.reservoir.toolsorders/asks/v4?contracts=0xFCf6bEf0579D4e6Da537B8154fa3b28102a574ab)
- [Get Aggregated Arbitrum Nova Offers](https://docs.reservoir.tools/reference/getordersbidsv5) - [sample response](https://api-arbitrum-nova.reservoir.toolsorders/bids/v5?contracts=0xFCf6bEf0579D4e6Da537B8154fa3b28102a574ab)
- [Get Arbitrum Nova Floor Prices](https://docs.reservoir.tools/reference/getcollectionsv5) - [sample response](https://api-arbitrum-nova.reservoir.toolscollections/v5?id=0xFCf6bEf0579D4e6Da537B8154fa3b28102a574ab)
- [Get Arbitrum Nova Sales Volume](https://docs.reservoir.tools/reference/getcollectionsdailyvolumesv1) - [sample response](https://api-arbitrum-nova.reservoir.toolscollections/daily-volumes/v1?id=0xFCf6bEf0579D4e6Da537B8154fa3b28102a574ab)
- [Get Arbitrum Nova Collection Metadata](https://docs.reservoir.tools/reference/gettokensv6) - [sample response](https://api-arbitrum-nova.reservoir.toolstokens/v6?collection=0xFCf6bEf0579D4e6Da537B8154fa3b28102a574ab)

## Trading on Arbitrum Nova with Reservoir

Reservoir makes it simple to not only get market data and orders, but execute and create orders directly through our APIs and tools. To learn more about trading with Reservoir, check out our [NFT Trading Overview](ref:creating-and-filling-orders). On Arbitrum Nova, you can:

**Execute orders** from across major marketplaces, by using the trading APIs or the SDK, which wraps the APIs into simple methods. Check out the buy and sell endpoints below:

- [Buy Arbitrum Nova NFTs](https://docs.reservoir.tools/reference/postexecutebuyv7)
- [Sell Arbitrum Nova NFTs](https://docs.reservoir.tools/reference/postexecutesellv7)

**Create orders** with [custom fees](https://docs.reservoir.tools/docs/custom-fees) and [royalties](https://docs.reservoir.tools/docs/royalties) that will get distributed across the Reservoir ecosystem. Or cross-post orders to major marketplaces that have Arbitrum Nova support. Check out our list and bid endpoints below:

- [List Arbitrum Nova  NFTs](https://docs.reservoir.tools/reference/postexecutelistv5)
- [Bid on Arbitrum Nova NFTs](https://docs.reservoir.tools/reference/postexecutebidv5)

## Reservoir Tools Available on Arbitrum Nova

All Reservoir tools including [APIs](https://docs.reservoir.tools/reference/overview), [SDKs](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode) & [ReservoirKit](https://docs.reservoir.tools/reference/reservoirkit) have full Arbitrum Nova support.

# Understanding Arbitrum Nova

Arbitrum Nova is a Layer 2 solution created by Offchain Labs, the team behind Arbitrum. This chain was launched with gaming and social aspects in mind. A number of features to create an environment that is suitable for those use cases, including "ultra-low" transaction costs and bridging from Arbitrum One. 

## Arbitrum Nova Blockchain Features

1. **Ultra-Low Transaction Speed:** Arbitrum Nova ensures faster transaction processing, delivering a seamless user experience by reducing transaction times.

2. **Reduced Transaction Costs:** By addressing Ethereum's high gas fees, Arbitrum Nova lowers transaction costs for NFT operations, making them more affordable.