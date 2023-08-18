---
title: "How often is metadata refreshed?"
slug: "how-often-is-metadata-refreshed"
hidden: true
createdAt: "2023-03-29T18:49:05.565Z"
updatedAt: "2023-05-02T15:00:36.128Z"
---
Reservoir allows manual refreshing of token metadata and collection metadata. Token metadata, such as name, description, and image, will not be automatically updated on the platform, but users can manually refresh it using the API [here](https://docs.reservoir.tools/reference/posttokensrefreshv1). 

Collection metadata, on the other hand, is updated at 23:30 UTC daily for specific categories of collections:

- The top 500 collections by 24hr volume 
- Collections that were minted 1 day
- Collections that were minted 7 days ago

However, users can also manually refresh collection metadata using the API [here](https://docs.reservoir.tools/reference/postcollectionsrefreshv1).

Reservoir is an on-chain and off-chain trading infrastructure for non-fungible tokens (NFTs). The platform provides various APIs and tools for developers to create and manage NFT markets, including order book management, trade execution, and market data aggregation. 

> 🚧 Caution: These APIs should be used in moderation, e.g. only when missing data is discovered. Calling it in bulk or programmatically will result in your key getting rate limited.