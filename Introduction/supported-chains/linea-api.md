---
title: "Linea NFT API"
slug: "linea-api"
excerpt: "Learn how to access Linea NFT data & trading through Reservoir's developer tools"
hidden: false
createdAt: "2023-08-04T19:49:26.180Z"
updatedAt: "2023-08-14T14:56:55.534Z"
---
# Getting Started with Linea on Reservoir

Reservoir offers access to Linea & a number of EVM-compatible chains through our simple, yet powerful APIs, SDKs & UI kits for NFT trading and data. To get started you can [get an API key](https://docs.reservoir.tools/reference/dashboard-sign-up) which has a [generous free plan & affordable paid subscriptions](https://reservoir.tools/pricing). 

- **Linea API Base URL** - You can access all Reservoir APIs by using the `https://api-linea.reservoir.tools` base URL. When using the API reference docs for Linea, make sure to change the base URL to the one above.
- **Recommended Test Collection** - Our recommended Linea NFT collection to test with is [Linea Voyage](https://lineascan.build/address/0x0872ec4426103482a50f26ffc32acefcec61b3c9) contract address: `0xd6f1ed5cce372eff973215ebf7227386da42f023`. When using the API reference docs, use the collection above to test responses.

To get a better sense of what we offer, check out of reference [Linea Marketplace & Explorer](https://explorer.reservoir.tools/linea).

## Access Linea Data with Reservoir

Reservoir gives you access to complete NFT metadata and market data aggregated from across all major marketplaces, including Opensea. You can learn more about our available data in our [NFT Data Overview](ref:nft-data-overview). 

- [Get Aggregated Listings](https://docs.reservoir.tools/reference/getordersasksv4) - [sample response](https://api-linea.reservoir.tools.toolsorders/asks/v4?contracts=0xd6f1ed5cce372eff973215ebf7227386da42f023)
- [Get Aggregated Offers](https://docs.reservoir.tools/reference/getordersbidsv5) - [sample response](https://api-linea.reservoir.tools.toolsorders/bids/v5?contracts=0xd6f1ed5cce372eff973215ebf7227386da42f023)
- [Get Floor Prices](https://docs.reservoir.tools/reference/getcollectionsv5) - [sample response](https://api-linea.reservoir.tools.toolscollections/v5?id=0xd6f1ed5cce372eff973215ebf7227386da42f023)
- [Get Sales Volume](https://docs.reservoir.tools/reference/getcollectionsdailyvolumesv1) - [sample response](https://api-linea.reservoir.tools.toolscollections/daily-volumes/v1?id=0xd6f1ed5cce372eff973215ebf7227386da42f023)
- [Get Collection Metadata](https://docs.reservoir.tools/reference/gettokensv6) - [sample response](https://api-linea.reservoir.tools.toolstokens/v6?collection=0xd6f1ed5cce372eff973215ebf7227386da42f023)

## Trading on Linea with Reservoir

Reservoir makes it simple to not only get market data and orders, but execute and create orders directly through our APIs and tools. To learn more about trading with Reservoir, check out our [NFT Trading Overview](ref:creating-and-filling-orders). On Linea, you can:

**Execute orders** from across major marketplaces, by using the trading APIs or the SDK, which wraps the APIs into simple methods. Check out the buy and sell endpoints below:

- [Buy NFTs](https://docs.reservoir.tools/reference/postexecutebuyv7)
- [Sell NFTs](https://docs.reservoir.tools/reference/postexecutesellv7)

**Create orders** with [custom fees](https://docs.reservoir.tools/docs/custom-fees) and [royalties](https://docs.reservoir.tools/docs/royalties) that will get distributed across the Reservoir ecosystem. Or cross-post orders to major marketplaces that have Linea support. Check out our list and bid endpoints below:

- [List NFTs](https://docs.reservoir.tools/reference/postexecutelistv5)
- [Bid on NFTs](https://docs.reservoir.tools/reference/postexecutebidv5)

## Reservoir Tools Available on Linea

All Reservoir tools including [APIs](https://docs.reservoir.tools/reference/overview), [SDKs](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode) & [ReservoirKit](https://docs.reservoir.tools/reference/reservoirkit) have full Linea support.

# Understanding Linea

Linea, formerly known as ConsenSys zkEVM, is an innovative Layer 2 (L2) solution that opens its testnet to developers, users, and protocols, inviting the web3 community to help Ethereum scale. With Linea, developers can build new decentralized applications (dapps) with ease, ensuring easy accessibility through MetaMask.

## Key Features:

- **Ethereum l2:** Linea empowers a new generation of Ethereum builders, providing the freedom to innovate without cost or scalability constraints. It connects Ethereum's past and present to its future, delivering unparalleled possibilities in the web3 space.

- **Native Integrations:** Linea follows a developer-centric approach, offering native integrations with popular tools like MetaMask and Truffle. Builders can focus solely on innovation without worrying about code changes or rewriting smart contracts.

- **EVM Equivalence:** Linea combines the power of zero-knowledge proofs with full Ethereum Virtual Machine (EVM) equivalence. Developers can create scalable dapps or migrate existing ones with ease, while the innovative prover design ensures faster transaction speeds and reduced gas costs without compromising security.

- **Approachable and Composable:** Linea is designed to be approachable and highly composable, ensuring flexibility and scalability for developers. With Linea's zkEVM, even those without expertise in zero-knowledge technology can build scalable dapps confidently.