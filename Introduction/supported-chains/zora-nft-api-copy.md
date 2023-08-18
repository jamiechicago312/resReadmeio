---
title: "Binance Smart Chain (BSC) NFT API"
slug: "zora-nft-api-copy"
excerpt: "Learn how to access BSC NFT data & trading through Reservoir's developer tools"
hidden: true
createdAt: "2023-08-16T22:49:33.678Z"
updatedAt: "2023-08-17T00:27:20.395Z"
---
# Getting Started with Zora on Reservoir

Reservoir offers access to Zora & a number of EVM-compatible chains through our simple, yet powerful APIs, SDKs & UI kits for NFT trading and data. To get started you can [get an API key](https://docs.reservoir.tools/reference/dashboard-sign-up) which has a [generous free plan & affordable paid subscriptions](https://reservoir.tools/pricing). 

- **Zora API Base URL** - You can access all Reservoir APIs by using the `https://api-zora.reservoir.tools` base URL. When using the API reference docs for Zora, make sure to change the base URL to the one above.
- **Recommended Test Collection** - Our recommended Zora NFT collection to test with is [Gallery Zorb](https://explorer.zora.energy/address/0x5921A344e85553d8Ec7f8510917D38Aaa8D21081) contract address: `0x5921a344e85553d8ec7f8510917d38aaa8d21081`. When using the API reference docs, use the collection above to test responses.

To get a better sense of what we offer, check out of reference [Zora Marketplace & Explorer](https://explorer.reservoir.tools/Zora).

## Access Zora Data with Reservoir

Reservoir gives you access to complete NFT metadata and market data aggregated from across all major marketplaces, including Opensea. You can learn more about our available data in our [NFT Data Overview](ref:nft-data-overview). 

- [Get Aggregated Listings](https://docs.reservoir.tools/reference/getordersasksv4) - [sample response](https://api-zora.reservoir.tools.toolsorders/asks/v4?contracts=0x5921a344e85553d8ec7f8510917d38aaa8d21081)
- [Get Aggregated Offers](https://docs.reservoir.tools/reference/getordersbidsv5) - [sample response](https://api-zora.reservoir.tools.toolsorders/bids/v5?contracts=0x5921a344e85553d8ec7f8510917d38aaa8d21081)
- [Get Floor Prices](https://docs.reservoir.tools/reference/getcollectionsv5) - [sample response](https://api-zora.reservoir.tools.toolscollections/v5?id=0x5921a344e85553d8ec7f8510917d38aaa8d21081)
- [Get Sales Volume](https://docs.reservoir.tools/reference/getcollectionsdailyvolumesv1) - [sample response](https://api-zora.reservoir.tools.toolscollections/daily-volumes/v1?id=0x5921a344e85553d8ec7f8510917d38aaa8d21081)
- [Get Collection Metadata](https://docs.reservoir.tools/reference/gettokensv6) - [sample response](https://api-zora.reservoir.tools.toolstokens/v6?collection=0x5921a344e85553d8ec7f8510917d38aaa8d21081)

## Trading on Zora with Reservoir

Reservoir makes it simple to not only get market data and orders, but execute and create orders directly through our APIs and tools. To learn more about trading with Reservoir, check out our [NFT Trading Overview](ref:creating-and-filling-orders). On Zora, you can:

**Execute orders** from across major marketplaces, by using the trading APIs or the SDK, which wraps the APIs into simple methods. Check out the buy and sell endpoints below:

- [Buy NFTs](https://docs.reservoir.tools/reference/postexecutebuyv7)
- [Sell NFTs](https://docs.reservoir.tools/reference/postexecutesellv7)

**Create orders** with [custom fees](https://docs.reservoir.tools/docs/custom-fees) and [royalties](https://docs.reservoir.tools/docs/royalties) that will get distributed across the Reservoir ecosystem. Or cross-post orders to major marketplaces that have Zora support. Check out our list and bid endpoints below:

- [List NFTs](https://docs.reservoir.tools/reference/postexecutelistv5)
- [Bid on NFTs](https://docs.reservoir.tools/reference/postexecutebidv5)

## Reservoir Tools Available on Zora

All Reservoir tools including [APIs](https://docs.reservoir.tools/reference/overview), [SDKs](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode) & [ReservoirKit](https://docs.reservoir.tools/reference/reservoirkit) have full Zora support.

# Understanding Zora

Zora Network, announced on June 21, emerges as a layer 2 blockchain solution by the NFT marketplace Zora. This innovation is designed to enhance the digital framework for artists and brands that have utilized Zora's platform. Backed by over 35 Web3 entities, including Sound.XYZ, Rainbow Wallet, and PleasrDAO, this network is set to empower the platform's 100,000 monthly active users by optimizing structural advantages and ensuring scalability.