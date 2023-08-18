---
title: "NFT Liquidity Router"
slug: "nft-liquidity-router"
excerpt: "Reservoir’s liquidity router lets you create, fill, and distribute NFT liquidity across all major marketplaces and the Reservoir ecosystem, through one universal interface."
hidden: false
createdAt: "2023-02-20T21:30:00.047Z"
updatedAt: "2023-06-14T18:14:11.164Z"
---
Reservoir's NFT liquidity router is built of two constituent components, our Router API and Router Contract. The API is also wrapped into the Reservoir SDK, which abstracts some of the complexities of creating and executing liquidity. The goal of Reservoir’s liquidity router is to simplify the creation and execution of NFT orders  across the ecosystem. 

**Core Benefits**

- Execute orders from Reservoir’s open orderbook, including orders aggregated from major NFT marketplaces
- Create native Reservoir orders and/or push orders to major NFT marketplaces
- Leverage Reservoir’s router contract for advanced buying and selling, like sweeping, multi-sell, and buying and selling in other erc-20 currencies.
- Abstraction of the underlying exchanges means you get exchange upgrades for free. 

## Using Reservoir’s Liquidity Router

There are three levels at which you can use Reservoir's liquidity router. For most applications we recommend using the Reservoir SDK because it offers the highest level of abstraction for developers. 

[Reservoir SDK (JS/TS/Node)](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode) - includes helpers that abstract the process of iterating through steps, and returning callbacks that can be used to update your UI.

[Router API](ref:creating-and-filling-orders) - APIs for buying, selling, and cancelling any order on any marketplace.

[Router Contract](doc:security-and-smart-contract-audits) - execute multi-item sales through Reservoir’s Router contract, enabling users to purchase items from different marketplaces in one transaction.