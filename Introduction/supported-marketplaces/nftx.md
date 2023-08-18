---
title: "NFTX API"
slug: "nftx"
excerpt: "Access NFTX data & trading through Reservoir's developer tools"
hidden: false
createdAt: "2023-05-22T16:48:07.312Z"
updatedAt: "2023-06-14T03:02:35.456Z"
---
# Getting Started with NFTX on Reservoir

Reservoir offers access to NFTX & 150+ other marketplaces through our simple, and powerful APIs, SDKs & UI kits. To get started you can [get an API key](https://docs.reservoir.tools/reference/dashboard-sign-up) which has a generous [free plan & affordable paid subscriptions](https://reservoir.tools/pricing). NFTX orders and data are included in all of our endpoints. However, should you want to access NFTX data and trading specifically, you can. The following sections outline how to access NFTX data and trading using Reservoir.

# Getting NFTX Data & Orders

- **Sales** - Get NFTX Sales from our [Sales API](https://docs.reservoir.tools/reference/getsalesv5). Filtering using the API is not currently supported, so get all sales for a token, collection, or attribute, and filter on the front end using `"orderSource": "nftx.io"`or `"fillSource": "nftx.io"`. When using `orderSource` you are filtering by sales whose orders are native to NFTX, while filtering on `fillSource` will return all sales that were filled on NFTX, regardless of the order origination marketplace. 
- **Asks (Listings)** - NFTX asks (listings) can be accessed through our [Asks API.](https://docs.reservoir.tools/reference/getordersasksv4) To get NFTX listings, ensure to set the `source=nftx.io`. [An example of the response.](https://api.reservoir.tools/orders/asks/v4?source=nftx.io)
- **Bids (Offers)** - NFTX bids (offers) can be accessed through our [Bids API.](https://docs.reservoir.tools/reference/getordersbidsv5) To get NFTX Offers, ensure to set the `source=nftx.io`. [An example of the response.](https://api.reservoir.tools/orders/bids/v5?source=nftx.io)

# Trading on NFTX through Reservoir

- **Buying** - Get the [listings data](https://docs.reservoir.tools/reference/getordersasksv4) and fill those orders either using the [API ](https://docs.reservoir.tools/reference/postexecutebuyv7)or [SDK](https://docs.reservoir.tools/reference/buytoken) _(recommended)_
- **Sell Tokens** - Get the [bid data](https://docs.reservoir.tools/reference/getordersbidsv5) and fill the bids either using the [API ](https://docs.reservoir.tools/reference/postexecutesellv7)or [SDK](https://docs.reservoir.tools/reference/acceptoffer) _(recommended)_

\*\*Currently Reservoir does not support creating NFTX pools through our API or tools

# NFTX Overview

NFTX is a decentralized platform offering ERC20 tokens backed by NFT collectibles known as vault tokens.

- **NFT-backed ERC20 Tokens**: NFTX makes it possible to create and trade ERC20 tokens associated with popular NFT collectibles, offering a novel way to engage with these digital assets.

- **Fully Permissionless**: NFTX operates fully permissionless on-chain contracts. The NFTX.org interface is maintained by the NFTX DAO.

NFTX offers fungible and composable ERC20 tokens backed by NFTs. With its permissionless approach and community-built structure, it provides an accessible platform for investors, arbitrageurs, and NFT liquidity providers.