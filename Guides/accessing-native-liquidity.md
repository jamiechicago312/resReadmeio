---
title: "Access Native Reservoir Liquidity"
slug: "accessing-native-liquidity"
hidden: false
createdAt: "2022-06-28T00:48:50.480Z"
updatedAt: "2023-04-24T19:44:37.933Z"
---
Reservoir's aggregated order book consists of two categories of orders:

1. **Mirrored**: from external marketplaces (OpenSea, LooksRare, X2Y2, etc)  
2. **Native**: from marketplaces built directly on top of Reservoir

There are now over 100 marketplaces creating native liquidity through Reservoir, including:

- [ENSVision](https://ens.vision) (Major ENS Marketplace doing ~50% of all ENS sales)
- [Truth Marketplace](https://marketplace.truthlabs.co/collections/0xbce3781ae7ca1a5e050bd9c4c77369867ebc307e) (Official Marketplace for Goblintown.wtf, IlluminatiNFT, etc)
- [Forgotten.Market](https://forgotten.market/) (Forgotten Runes Wizard Cult Community Marketplace)

Aggregators looking to ingest only native Reservoir liquidity (because they already have the rest), can do so easily by querying the Asks API with the filter `native=true`

<https://api.reservoir.tools/orders/asks/v3?native=true&includePrivate=false&includeMetadata=false&includeRawData=true&sortBy=createdAt&limit=1000>

This API is designed to be queried in bulk, returning up to 1000 orders at a time. To get all orders, follow the continuation until you see a result you've ingested already. To get real-time orders, poll every second for new results.

## Supported Protocols

The Reservoir Order Book supports the following order kinds:

- `seaport`
- `zeroex-v4-erc721`
- `zeroex-v4-erc1155`
- `wyvern-v2.3` (deprecated)

The vast majority of current orders (99.99%) use `seaport`. 

You can filter out protocols you don't support by looking at the `kind` field in the response.

## Marketplace Attribution

Reservoir is not a single marketplace, it's a dynamically growing collection of marketplaces, which can make integration slightly more complicated. 

To help with this, every order contains detailed `source` information, so you can correctly attribute the marketplace where the order came from. 

```coffeescript json
"source": {
        "domain": "ens.vision",
        "name": "ENSVision",
        "icon": "https://www.ens.vision/favicon.ico"
      },
```

When integrating, there are 3 options to consider:

1. Attribute everything to "Reservoir", ignoring the source marketplace
   1. This is the easiest, but not a great UX
2. Attribute everything to it's source marketplace 
   1. Most accurate, but complex to handle a dynamic set of marketplaces
3. Maintain a whitelist of known marketplaces, with fallback "Reservoir" category
   1. A middle ground between accurate attribution and simplicity

As an example, implementing Option 3 would work roughly like this:

- Internally in your system, create a fallback "Reservoir" marketplace, along with a handful of known marketplaces (ENSVision, Forgotten.Market, etc)
- Ingest all native Reservoir orders
- If the source is known, assign it to that market, otherwise assign to "Reservoir" 
- If a new marketplace launches, you're getting their orders with zero extra effort (shows "Reservoir" as source)
- If it starts to get traction, you add it internally and start classifying the orders correctly (shows actual marketplace name as source)