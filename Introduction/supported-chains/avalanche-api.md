---
title: "Avalanche NFT API"
slug: "avalanche-api"
excerpt: "Learn how to access Avalanche NFT data & trading through Reservoir's developer tools"
hidden: false
metadata: 
createdAt: "2023-08-11T17:24:11.334Z"
updatedAt: "2023-08-11T18:31:59.752Z"
---
# Getting Started with Avalanche on Reservoir

Reservoir offers access to Avalanche & a number of EVM-compatible chains through our simple, yet powerful APIs, SDKs & UI kits for NFT trading and data. To get started you can [get an API key](https://docs.reservoir.tools/reference/dashboard-sign-up) which has a [generous free plan & affordable paid subscriptions](https://reservoir.tools/pricing). 

- **Avalanche API Base URL** - You can access all Reservoir APIs by using the `https://api-avalanche.reservoir.tools` base URL. When using the API reference docs for Avalanche, make sure to change the base URL to the one above.
- **Recommended Test Collection** - Our recommended Avalanche NFT collection to test with is [MadSkullz](https://snowtrace.io/address/0x3025C5c2aA6eb7364555aAC0074292195701bBD6) contract address: `0x3025C5c2aA6eb7364555aAC0074292195701bBD6`. When using the API reference docs, use the collection above to test responses.

To get a better sense of what we offer, check out of reference [Avalanche Marketplace & Explorer](https://explorer.reservoir.tools/Avalanche).

## Access Avalanche Data with Reservoir

Reservoir gives you access to complete NFT metadata and market data aggregated from across all major marketplaces, including Opensea. You can learn more about our available data in our [NFT Data Overview](ref:nft-data-overview). 

- [Get Aggregated Listings](https://docs.reservoir.tools/reference/getordersasksv4) - [sample response](https://api-avalanche.reservoir.tools.toolsorders/asks/v4?contracts=0x3025C5c2aA6eb7364555aAC0074292195701bBD6)
- [Get Aggregated Offers](https://docs.reservoir.tools/reference/getordersbidsv5) - [sample response](https://api-avalanche.reservoir.tools.toolsorders/bids/v5?contracts=0x3025C5c2aA6eb7364555aAC0074292195701bBD6)
- [Get Floor Prices](https://docs.reservoir.tools/reference/getcollectionsv5) - [sample response](https://api-avalanche.reservoir.tools.toolscollections/v5?id=0x3025C5c2aA6eb7364555aAC0074292195701bBD6)
- [Get Sales Volume](https://docs.reservoir.tools/reference/getcollectionsdailyvolumesv1) - [sample response](https://api-avalanche.reservoir.tools.toolscollections/daily-volumes/v1?id=0x3025C5c2aA6eb7364555aAC0074292195701bBD6)
- [Get Collection Metadata](https://docs.reservoir.tools/reference/gettokensv6) - [sample response](https://api-avalanche.reservoir.tools.toolstokens/v6?collection=0x3025C5c2aA6eb7364555aAC0074292195701bBD6)

## Trading on Avalanche with Reservoir

Reservoir makes it simple to not only get market data and orders, but execute and create orders directly through our APIs and tools. To learn more about trading with Reservoir, check out our [NFT Trading Overview](ref:creating-and-filling-orders). On Avalanche, you can:

**Execute orders** from across major marketplaces, by using the trading APIs or the SDK, which wraps the APIs into simple methods. Check out the buy and sell endpoints below:

- [Buy NFTs](https://docs.reservoir.tools/reference/postexecutebuyv7)
- [Sell NFTs](https://docs.reservoir.tools/reference/postexecutesellv7)

**Create orders** with [custom fees](https://docs.reservoir.tools/docs/custom-fees) and [royalties](https://docs.reservoir.tools/docs/royalties) that will get distributed across the Reservoir ecosystem. Or cross-post orders to major marketplaces that have Avalanche support. Check out our list and bid endpoints below:

- [List NFTs](https://docs.reservoir.tools/reference/postexecutelistv5)
- [Bid on NFTs](https://docs.reservoir.tools/reference/postexecutebidv5)

## Reservoir Tools Available on Avalanche

All Reservoir tools including [APIs](https://docs.reservoir.tools/reference/overview), [SDKs](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode) & [ReservoirKit](https://docs.reservoir.tools/reference/reservoirkit) have full Avalanche support.

# Understanding Avalanche

Avalanche is an open-source platform, offering a decentralized and highly scalable ecosystem for building interoperable decentralized applications. Driven by a groundbreaking consensus mechanism, Avalanche is tailored to meet the demands of global finance, boasting near-instant transaction finality.

## Key Features:

- **L2 Speeds:** Avalanche features the fastest consensus mechanism among layer 1 blockchains. This enables rapid transaction finality and low latency, processing and verifying transactions in under 2 seconds.

- **Built for Scale:** Developers on Avalanche can create application-specific blockchains with intricate rulesets or leverage existing private or public Subnets in any programming language. The network's energy efficiency allows it to operate seamlessly on standard hardware.

- **Flexible Development:** Avalanche supports Solidity developers by providing an out-of-the-box implementation of the EVM. For more advanced use cases, developers can craft custom Virtual Machines (VMs).

- **Enhanced Security:** Avalanche's consensus scales robustly, ensuring top-tier security for internet-scale systems. It supports permissionless and permissioned custom blockchains, allowing for tailored rulesets compliant with legal and jurisdictional standards.

Avalanche empowers developers to build efficiently and securely within a high-speed, scalable ecosystem, positioning itself as a prime choice for the decentralized application landscape.