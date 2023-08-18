---
title: "Floor Price Data"
slug: "floor-prices"
excerpt: "Access real-time and historical floor price data aggregated from across major NFT marketplaces."
hidden: false
createdAt: "2022-12-23T18:10:15.455Z"
updatedAt: "2023-06-14T17:49:22.010Z"
---
Reservoir offers access to both **real-time** and **historical ** floor prices and floor price change events for NFTs in a particular collection.  Accurate aggregated floor price data is important for any application or use where users benefit from market context, including [wallet & portfolios](doc:walletportfolio-app), [analytics applications](doc:data-and-analytics), or any application where [embedded buying and selling](https://docs.reservoir.tools/docs/embedded-buying-selling) is used. 

# What floor price data does Reservoir have?

Reservoir has up-to-date floor price data for all NFT collections on supported chains aggregated from all major marketplaces, including Blur and Opensea. Furthermore, with Reservoir you can:

- Get floor data with and without [flagged tokens](ref:gettokensflagchangesv1)
- [Normalized royalties](doc:royalties) to adjust floor data to include royalties on royalty-free orders
- Execute floor listings using the [Trading API](doc:trading-data-apis) or [ReservoirKit](doc:reservoirkit)

# How to get floor price data

There are several ways to get floor price data depending on your use case. 

1. Get floor price data from the collections API when you want to show floors alongside collection data and statistics
2. Get floor price change events using the events API
3. Get floor orders from the asks endpoint to execute floor listings

## Getting floor price data from the collections API

You can get the floor price for a collection or set of collections using the [collections API](https://docs.reservoir.tools/reference/getcollectionsv5). This allows you to get floor prices alongside:

- Collection ranks
- Top bids
- Collection Metadata
- Collection statistics

This is useful for showing collection details in a collection overview page. 

## Getting floor price data from the floor price events API

You can get floor price data for a collection using the [floor price events API](ref:geteventscollectionsflooraskv2), which gives you granular floor price changes over time. This allows you to graph floor prices over time, or understand floor price changes in real time. You can use this endpoint to get historical floor price data back until April of 2022. 

## Getting floor listings from the orderbook to execute buys

You can get floor orders from the aggregated orderbook by calling the [asks API](https://docs.reservoir.tools/reference/getordersasksv4). To get the floor ask, make sure you `sortBy = price`. This allows you to get the full order data so that you can use the [trading API ](doc:trading-data-apis) or [ReservoirSDK](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode) to execute the order.