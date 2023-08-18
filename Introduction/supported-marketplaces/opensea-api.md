---
title: "OpenSea API"
slug: "opensea-api"
excerpt: "Access OpenSea data & trading through Reservoir's developer tools"
hidden: false
createdAt: "2023-04-21T20:22:04.662Z"
updatedAt: "2023-06-22T18:55:37.724Z"
---
# Getting Started with OpenSea on Reservoir

Reservoir offers access to OpenSea & 150+ other marketplaces through our simple, and powerful APIs, SDKs & UI kits. To get started you can [get an API key](https://docs.reservoir.tools/reference/dashboard-sign-up) which has a generous [free plan & affordable paid subscriptions](https://reservoir.tools/pricing). OpenSea orders and data are included in all of our endpoints. However, should you want to access OpenSea data and trading specifically, you can. The following sections outline how to access OpenSea data and trading using Reservoir.

# Getting OpenSea Data & Orders

- **Sales** - Get OpenSea Sales from our [Sales API](https://docs.reservoir.tools/reference/getsalesv5). Filtering using the API is not currently supported, so get all sales for a token, collection, or attribute, and filter on the front end using `"orderSource": "opensea.io"`or `"fillSource": "opensea.io"`. When using `orderSource` you are filtering by sales whose orders are native to OpenSea, while filtering on `fillSource` will return all sales that were filled on OpenSea, regardless of the order origination marketplace.

- **Asks (Listings)** - OpenSea asks (listings) can be accessed through our [Asks API.](https://docs.reservoir.tools/reference/getordersasksv4) To get OpenSea listings, ensure to set the `source=opensea.io`. [An example of the response.](https://api.reservoir.tools/orders/asks/v4?source=opensea.io)

- **Bids (Offers)** - OpenSea bids (offers) can be accessed through our [Bids API.](https://docs.reservoir.tools/reference/getordersbidsv5) To get OpenSea Offers, ensure to set the `source=opensea.io`. [An example of the response.](https://api.reservoir.tools/orders/bids/v5?source=opensea.io)

# Trading on OpenSea through Reservoir

- **Buying** - Get the [listings data](https://docs.reservoir.tools/reference/getordersasksv4) and fill those orders either using the [API ](https://docs.reservoir.tools/reference/postexecutebuyv7)or [SDK](https://docs.reservoir.tools/reference/buytoken) _(recommended)_
- **Selling** - Get the [bid data](https://docs.reservoir.tools/reference/getordersbidsv5) and fill the bids either using the [API ](https://docs.reservoir.tools/reference/postexecutesellv7)or [SDK](https://docs.reservoir.tools/reference/acceptoffer) _(recommended)_
- **Creating Asks (Listings)** - Create the listing through the [API ](https://docs.reservoir.tools/reference/postexecutelistv5)or the [SDK](https://docs.reservoir.tools/reference/listtoken) _(recommended)_, set the `"orderKind": "seaport-v1.5"` & `"orderbook": "OpenSea"` and [check the cross-post status](https://docs.reservoir.tools/reference/getcrosspostingordersv1) 
- **Creating Bids (Offers)** - Create the offer through the [API ](https://docs.reservoir.tools/reference/postexecutebidv5)or the [SDK](https://docs.reservoir.tools/reference/placebid) _(recommended)_ set the `"orderKind": "seaport-v1.5"` & `"orderbook": "OpenSea"` and [check the cross-post status](https://docs.reservoir.tools/reference/getcrosspostingordersv1).

# OpenSea FAQ

- Is there a way to get OpenSea Verified status?
  - Yes, you can get OpenSea Verified status by using our [Collections API](https://docs.reservoir.tools/reference/getcollectionsv5) and checking the `"openseaVerificationStatus"` field. [Sample Response](https://api.reservoir.tools/collections/v5?id=0x8d04a8c79ceb0889bdd12acdf3fa9d207ed3ff63&source=opensea.io) 

- Do you have support for checking NFTs that are flagged on OpenSea?
  - Yes, we have a multitude of ways for including or excluding flagged results from our endpoints. [A full guide here](https://docs.reservoir.tools/docs/flagged-tokens)

# OpenSea Overview

OpenSea has firmly established itself as a leading NFT marketplace, boasting one of the highest volumes in the space. The platform's user-friendly design and an array of unique features make it an excellent choice for those wishing to buy or sell NFTs.

- OpenSea operates on the Ethereum, Polygon, Solana, Arbitrum, Avalanche, BNB, and Klaytn NFTs, providing users with flexibility across chains and lower fees.
- OpenSea has gained significant traction and is backed by heavyweight venture capital firms, such as Paradigm and Coatue.
- The platform boasts over 2 million users and has facilitated over $10 billion in trading volume, demonstrating its substantial reach in the NFT world.

OpenSea is a rapidly expanding NFT marketplace that has earned its status as a key player in the industry. Offering numerous features that are unmatched on other marketplaces, OpenSea is poised to cater to the needs of both professional NFT traders and enthusiasts alike.