---
title: "LooksRare API"
slug: "looksrare"
excerpt: "Access LooksRare data & trading through Reservoir's developer tools"
hidden: false
createdAt: "2023-05-22T16:48:01.526Z"
updatedAt: "2023-06-14T03:01:34.006Z"
---
# Getting Started with LooksRare on Reservoir

Reservoir offers access to LooksRare & 150+ other marketplaces through our simple, and powerful APIs, SDKs & UI kits. To get started you can [get an API key](https://docs.reservoir.tools/reference/dashboard-sign-up) which has a generous [free plan & affordable paid subscriptions](https://reservoir.tools/pricing). LooksRare orders and data are included in all of our endpoints. However, should you want to access LooksRare data and trading specifically, you can. The following sections outline how to access LooksRare data and trading using Reservoir.

# Getting LooksRare Data & Orders

- **Sales** - Get LooksRare Sales from our [Sales API](https://docs.reservoir.tools/reference/getsalesv5). Filtering using the API is not currently supported, so get all sales for a token, collection, or attribute, and filter on the front end using `"orderSource": "looksrare.org"`or `"fillSource": "looksrare.org"`. When using `orderSource` you are filtering by sales whose orders are native to LooksRare, while filtering on `fillSource` will return all sales that were filled on LooksRare, regardless of the order origination marketplace. 
- **Asks (Listings)** - LooksRare asks (listings) can be accessed through our [Asks API.](https://docs.reservoir.tools/reference/getordersasksv4) To get LooksRare listings, ensure to set the `source=looksrare.org`. [An example of the response.](https://api.reservoir.tools/orders/asks/v4?source=looksrare.org)
- **Bids (Offers)** - LooksRare bids (offers) can be accessed through our [Bids API.](https://docs.reservoir.tools/reference/getordersbidsv5) To get LooksRare Offers, ensure to set the `source=looksrare.org`. [An example of the response.](https://api.reservoir.tools/orders/bids/v5?source=looksrare.org)

# Trading on LooksRare through Reservoir

- **Buying** - Get the [listings data](https://docs.reservoir.tools/reference/getordersasksv4) and fill those orders either using the [API ](https://docs.reservoir.tools/reference/postexecutebuyv7)or [SDK](https://docs.reservoir.tools/reference/buytoken) _(recommended)_
- **Selling** - Get the [bid data](https://docs.reservoir.tools/reference/getordersbidsv5) and fill the bids either using the [API ](https://docs.reservoir.tools/reference/postexecutesellv7)or [SDK](https://docs.reservoir.tools/reference/acceptoffer) _(recommended)_
- **Create Asks (Listings)** - Create the listing through the [API ](https://docs.reservoir.tools/reference/postexecutelistv5)or the [SDK](https://docs.reservoir.tools/reference/listtoken) _(recommended)_, set the `"orderKind": "looks-rare-v2"` & `"orderbook": "looks-rare"` and [check the cross-post status](https://docs.reservoir.tools/reference/getcrosspostingordersv1) 
- **Create Bids (Offers)** - Create the offer through the [API ](https://docs.reservoir.tools/reference/postexecutebidv5)or the [SDK](https://docs.reservoir.tools/reference/placebid) _(recommended)_ set the `"orderKind": "looks-rare-v2"` & `"orderbook": "looks-rare"` and [check the cross-post status](https://docs.reservoir.tools/reference/getcrosspostingordersv1).

# LooksRare Overview

LooksRare, a renowned marketplace known for its high trading volume and variety of NFTs. Its unique features like low transaction fees, LOOKS token rewards, and option to bid on entire NFT collections have garnered attention from numerous investors.

- LooksRare charges a lower transaction fee of 0.5%, as compared to the standard 2.5% in most other platforms. This reduction in fees, from an initial 2%, came with the launch of LooksRare V2 in April 2023.

- Unlike many platforms that restrict you to single NFT purchases, LooksRare provides an option to bid on an entire collection. This feature provides a broader array of purchase options, including fixed sales or auctions.

- The platform offers its native Looks tokens as rewards for staking, trading, or listing on LooksRare. 

LooksRare, stands out in the NFT marketplace due to its competitive low transaction fees and substantial rewards system. Offering the unique ability to bid on entire collections and a community-focused platform, it positions itself as a compelling choice for NFT enthusiasts.