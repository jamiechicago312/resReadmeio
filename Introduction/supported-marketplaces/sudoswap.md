---
title: "SudoSwap API"
slug: "sudoswap"
excerpt: "Access SudoSwap data & trading through Reservoir's developer tools"
hidden: false
createdAt: "2023-05-22T16:48:17.521Z"
updatedAt: "2023-06-14T03:02:06.012Z"
---
# Getting Started with SudoSwap on Reservoir

Reservoir offers access to SudoSwap & 150+ other marketplaces through our simple, and powerful APIs, SDKs & UI kits. To get started you can [get an API key](https://docs.reservoir.tools/reference/dashboard-sign-up) which has a generous [free plan & affordable paid subscriptions](https://reservoir.tools/pricing). SudoSwap orders and data are included in all of our endpoints. However, should you want to access SudoSwap data and trading specifically, you can. The following sections outline how to access SudoSwap data and trading using Reservoir.

# Getting SudoSwap Data & Orders

- **Sales** - Get SudoSwap Sales from our [Sales API](https://docs.reservoir.tools/reference/getsalesv5). Filtering using the API is not currently supported, so get all sales for a token, collection, or attribute, and filter on the front end using `"orderSource": "sudoswap.xyz"`or `"fillSource": "sudoswap.xyz"`. When using `orderSource` you are filtering by sales whose orders are native to SudoSwap, while filtering on `fillSource` will return all sales that were filled on SudoSwap, regardless of the order origination marketplace. 
- **Asks (Listings)** - SudoSwap asks (listings) can be accessed through our [Asks API.](https://docs.reservoir.tools/reference/getordersasksv4) To get SudoSwap listings, ensure to set the `source=sudoswap.xyz`. [An example of the response.](https://api.reservoir.tools/orders/asks/v4?source=sudoswap.xyz)
- **Bids (Offers)** - SudoSwap bids (offers) can be accessed through our [Bids API.](https://docs.reservoir.tools/reference/getordersbidsv5) To get SudoSwap Offers, ensure to set the `source=sudoswap.xyz`. [An example of the response.](https://api.reservoir.tools/orders/bids/v5?source=sudoswap.xyz)

# Trading on SudoSwap through Reservoir

- **Buying** - Get the [listings data](https://docs.reservoir.tools/reference/getordersasksv4) and fill those orders either using the [API ](https://docs.reservoir.tools/reference/postexecutebuyv7)or [SDK](https://docs.reservoir.tools/reference/buytoken) _(recommended)_
- **Sell Tokens** - Get the [bid data](https://docs.reservoir.tools/reference/getordersbidsv5) and fill the bids either using the [API ](https://docs.reservoir.tools/reference/postexecutesellv7)or [SDK](https://docs.reservoir.tools/reference/acceptoffer) _(recommended)_

\*\*Currently, Reservoir does not support liquidity pool creation on SudoSwap through our API or tools. 

# SudoSwap Overview

SudoSwap, an innovative NFT Marketplace and Automated Market Maker (AMM), introduces a fresh approach to NFT liquidity and trading. SudoSwap enables trustless, gas-efficient, and fully on-chain NFT swaps.

- **Trustless NFT Swaps**: The platform allows users to swap NFTs (ERC721s) in a secure, trustless manner, which is both gas-efficient and fully on-chain. 

- **Innovative AMM Model**: SudoSwap introduces an Automated Market Maker model for NFTs, which enables users to create pools that buy or sell NFT collections gradually along price curves. 

SudoSwap has made a promising entrance into the NFT marketplace with its unique AMM model and ability to offer trustless NFT swaps. It's early success and steady growth since its launch in late July 2022 indicates its potential to become a significant player in the NFT sector. The planned advancements and feature releases by the SudoSwap team are eagerly anticipated as the platform continues to evolve.