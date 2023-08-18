---
title: "Embedded Buying and Selling"
slug: "embedded-buying-selling"
excerpt: "Allow your users to buy any on-sale NFT or instantly sell directly from your app"
hidden: false
createdAt: "2022-12-22T19:09:05.367Z"
updatedAt: "2023-06-14T17:44:59.360Z"
---
One of the major advantages of leveraging Reservoir is that you can embed marketplace functionality you app without the need to build comprehensive marketplace infrastructure. 

# Why Embed Buying and Selling?

NFT marketplaces represent only a small fraction of all NFT applications. And historically there hasn't been an easy way for apps to embed marketplace functions in their experience without committing to build marketplace infrastructure and sourcing their own liquidity. This changes with Reservoir. 

By leveraging Reservoir, you can:

- Add marketplace functionality without building any backend infrastructure
- Access Reservoir’s open orderbook, including liquidity aggregated from all major marketplaces
- Add customs fees on all orders to generate application revenue
- Let your users create orders on your site that get distributed to major marketplace centers
- Leverage Reservoir’s ReservoirKit to get out-of-the-box checkout UI

Marketplace functionality is _not_ just for teams building marketplaces, but can be embedded right into the context you are building, whether it's a wallet, a social app, a creator platform, a game, or something else entirely. 

# How to Add Marketplace Functionality to your App

To most effectively leverage Reservoir to embed buying, bidding, listing, or selling into your application, we recommend you user either:

- [Reservoir SDK (JS/TS/Node)](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode): An abstracted SDK for interacting with the NFT market. All the function of the Reservoir API wrapped into easily-to-use, performant methods.
- [ReservoirKit (React)](https://docs.reservoir.tools/reference/reservoirkit): a react library that makes it easy to add marketplace functionality and UI into your project.

ReservoirKit is a react library that wraps the Reservoir SDK, so its less of a choice between these two and more a choice of whether you would like to use UI kit components in your application.