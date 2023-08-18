---
title: "Supported Testnets"
slug: "supported-testnets"
excerpt: "Learn how to access Testnet NFT data & trading through Reservoir's developer tools"
hidden: false
createdAt: "2023-05-22T16:49:36.018Z"
updatedAt: "2023-08-16T22:00:51.965Z"
---
# Getting Started with Testnets on Reservoir

Reservoir offers access to a number of EVM-compatible chains & testnets through our simple, yet powerful APIs, SDKs & UI kits for NFT trading and data. To get started you can [get an API key](https://docs.reservoir.tools/reference/dashboard-sign-up) which has a [generous free plan & affordable paid subscriptions](https://reservoir.tools/pricing). 

## Testnets Reservoir Supports & Base URLs

You can access all Reservoir APIs by changing the base URL. When using the API reference docs, make sure to change the base URL to the corresponding URL.

| Testnet      | Base URL                                   |
| :----------- | :----------------------------------------- |
| Goerli       | `https://api-goerli.reservoir.tools`       |
| Sepolia      | `https://api-sepolia.reservoir.tools`      |
| Base Goerli  | `https://api-base-goerli.reservoir.tools`  |
| Zora Goerli  | `https://api-zora-testnet.reservoir.tools` |
| Scroll Alpha | `https://api-scroll-alpha.reservoir.tools` |
| Mumbai       | `https://api-mumbai.reservoir.tools`       |

You can check out out the testnets on our [reference marketplace](https://marketplace.reservoir.tools/).

## Access Testnet Data with Reservoir

Reservoir gives you access to complete NFT metadata and market data aggregated from across all major marketplaces, including Opensea. You can learn more about our available data in our [NFT Data Overview](ref:nft-data-overview). 

- [Get Aggregated Testnet Listings](https://docs.reservoir.tools/reference/getordersasksv4)
- [Get Aggregated Testnet Offers](https://docs.reservoir.tools/reference/getordersbidsv5)
- [Get Testnet Floor Prices](https://docs.reservoir.tools/reference/getcollectionsv5)
- [Get Testnet Sales Volume](https://docs.reservoir.tools/reference/getcollectionsdailyvolumesv1)
- [Get Testnet Collection Metadata](https://docs.reservoir.tools/reference/gettokensv6)

## Trading on Testnet with Reservoir

Reservoir makes it simple to not only get market data and orders, but execute and create orders directly through our APIs and tools. To learn more about trading with Reservoir, check out our [NFT Trading Overview](ref:creating-and-filling-orders). On Testnet, you can:

**Execute orders** from across major marketplaces, by using the trading APIs or the SDK, which wraps the APIs into simple methods. Check out the buy and sell endpoints below:

- [Buy Testnet NFTs](https://docs.reservoir.tools/reference/postexecutebuyv7)
- [Sell Testnet NFTs](https://docs.reservoir.tools/reference/postexecutesellv7)

**Create orders** with [custom fees](https://docs.reservoir.tools/docs/custom-fees) and [royalties](https://docs.reservoir.tools/docs/royalties) that will get distributed across the Reservoir ecosystem. Or cross-post orders to major marketplaces that have Testnet support. Check out our list and bid endpoints below:

- [List Testnet NFTs](https://docs.reservoir.tools/reference/postexecutelistv5)
- [Bid on Testnet NFTs](https://docs.reservoir.tools/reference/postexecutebidv5)

## Reservoir Tools Available on Testnet

All Reservoir tools including [APIs](https://docs.reservoir.tools/reference/overview), [SDKs](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode) & [ReservoirKit](https://docs.reservoir.tools/reference/reservoirkit) have full Testnet support.

# Understanding Testnets

Testnets, or testing networks, are crucial elements in the blockchain ecosystem and play a significant role in the development and smooth operation of NFT marketplaces. They simulate the conditions of a live blockchain network for testing purposes, offering invaluable features like cost-free testing, safe environments, debugging facilities, and iterative development support.

## Optimism Blockchain Features

1. **Cost-Free Testing:** Test Nets allow developers to simulate transactions without incurring real-world costs.
2. **Safe Environment:** They provide a secure space for testing new features or smart contracts, reducing risks associated with live deployment.
3. **Debugging Facilities:** Test Nets enable developers to identify and rectify errors before deploying on the main network.
4. **Iterative Development Support:** They foster experimentation and iterative improvements, helping to create robust NFT marketplace platforms.