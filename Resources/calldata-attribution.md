---
title: "Marketplace Source Attribution"
slug: "calldata-attribution"
excerpt: "Understanding Reservoir's call data marketplace attribution - a burgeoning industry standard"
hidden: false
createdAt: "2022-08-30T11:47:30.046Z"
updatedAt: "2023-04-06T22:37:44.374Z"
---
# What's the problem?

One challenge for NFT Aggregation platforms is the most gas-efficient method to fill an order is directly through the exchange contract (Seaport, LooksRare, etc). However when doing so, the transaction is indistinguishable from an order that was filled on the marketplace where the order was created (e.g. OpenSea). This leads to significant misreporting of where NFT volume is happening, when looking at on-chain analytics. As an example, around 50% of all Gem transactions are filled directly via Seaport, without a novel attribution mechanic, it wouldn't be possible to tell that this volume is happening on Gem. 



# Call data attribution

To solve this problem, we are worked with the NFT community to develop a standard method for attributing sales to the appropriate order source and fill source that is:

- open 
- on-chain 
- gas-efficient 
- compatible with any exchange

## How does it work?

Call data attribution works by having sources pass their domain name in the calldata of each transaction they fill, so that on-chain analytics tools can parse it and determine who filled the order.

Domain names are used because:

- They are easy to read
- They can be visited to learn more
- Additional metadata (icon, etc) can be pulled from html tags

The way it works is that we use 4 bytes of the domain hash: 

`bytes4(keccak256("mydomain.com")`

This is already [live](https://mobile.twitter.com/vasa_develop/status/1572331744032067584) in production on Gem and used throughout Reservoir:

`gem.xyz` > `72db8c0b`

[Example Dune Query](https://dune.com/queries/1289755)

We will be rolling this out across Reservoir soon, along with tooling for reverse lookups on domain hashes.