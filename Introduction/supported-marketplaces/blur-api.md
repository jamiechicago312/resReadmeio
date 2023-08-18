---
title: "Blur API"
slug: "blur-api"
excerpt: "Access Blur data & trading through Reservoir's developer tools"
hidden: false
createdAt: "2023-04-21T20:21:55.585Z"
updatedAt: "2023-06-14T02:46:59.972Z"
---
## Getting Started with Blur on Reservoir

Reservoir offers access to Blur & 150+ other marketplaces through our simple, and powerful APIs, SDKs & UI kits. To get started you can [get an API key](https://docs.reservoir.tools/reference/dashboard-sign-up) which has a generous [free plan & affordable paid subscriptions](https://reservoir.tools/pricing). Blur orders and data are included in all of our endpoints. We also include Blend orders, Blur's lending protocol. However, should you want to access Blur data and trading specifically, you can. The following sections outline how to access Blur data and trading using Reservoir.

## Getting Blur Data & Orders

- **Sales** -  Get Blur Sales from our [Sales API](https://docs.reservoir.tools/reference/getsalesv5). Filtering using the API is not currently supported, so get all sales for a token, collection, or attribute, and filter on the front end using `"orderSource": "blur.io"`or `"fillSource": "blur.io"`. When using `orderSource` you are filtering by sales whose orders are native to Blur, while filtering on `fillSource` will return all sales that were filled on Blur, regardless of the order origination marketplace. 
- **Asks (Listings)** - Blur asks (listings) can be accessed through our [Asks API.](https://docs.reservoir.tools/reference/getordersasksv4) To get Blur listings, ensure to set the `source=blur.io`. [An example of the response.](https://api.reservoir.tools/orders/asks/v4?source=blur.io)
- **Bids (Offers)** - Blur bids (offers) can be accessed through our [Bids API.](https://docs.reservoir.tools/reference/getordersbidsv5) To get Blur Offers, ensure to set the `source=blur.io`. [An example of the response.](https://api.reservoir.tools/orders/bids/v5?source=blur.io) When `source=blur.io` and `includeDepth=true` are passed, individual bids will be shown; otherwise Blur bids are pooled. Pass a `maker` and `source=blur.io` to see a maker's Blur specific bids; if only `maker` is passed, the maker's Blur bids will not be revealed. Please note our quantity of bids might be different than Blur's because we pool the bids.

## Trading on Blur through Reservoir

- **Buying** - Get the [listings data](https://docs.reservoir.tools/reference/getordersasksv4) and fill those orders either using the [API ](https://docs.reservoir.tools/reference/postexecutebuyv7)or [SDK](https://docs.reservoir.tools/reference/buytoken) _(recommended)_
- **Selling** - Get the [bid data](https://docs.reservoir.tools/reference/getordersbidsv5) and fill the bids either using the [API ](https://docs.reservoir.tools/reference/postexecutesellv7)or [SDK](https://docs.reservoir.tools/reference/acceptoffer) _(recommended)_
- **Creating Asks (Listings)** - Create the listing through the [API ](https://docs.reservoir.tools/reference/postexecutelistv5)or the [SDK](https://docs.reservoir.tools/reference/listtoken) _(recommended)_, set the `"orderKind": "blur"` & `"orderbook": "blur"` and [check the cross-post status](https://docs.reservoir.tools/reference/getcrosspostingordersv1) 
- **Creating Bids (Offers)** - Create the offer through the [API ](https://docs.reservoir.tools/reference/postexecutebidv5)or the [SDK](https://docs.reservoir.tools/reference/placebid) _(recommended)_ set the `"orderKind": "blur"` & `"orderbook": "blur"` and [check the cross-post status](https://docs.reservoir.tools/reference/getcrosspostingordersv1). 

## Blur limitations

Blur currently has a small number of restrictions in place:

- All orders require a signature from the Blur server to be filled
- To get a signature, the Blur server requires the buyer to sign a message
- Smart contracts wallets / routers/ relayers cannot sign in or fill orders

> 🚧 Filter Blur Orders Out with `excludeEOA`
> 
> To exclude Blur orders for APIs, please mark `excludeEOA` as `true`: [buy token](https://docs.reservoir.tools/reference/postexecutebuyv7), [sell token](https://docs.reservoir.tools/reference/postexecutesellv7), [User Top Bids](ref:getordersusersusertopbidsv4), [Bids (offers)](ref:getordersbidsv5), and [Asks (listings)](ref:getordersasksv4). With the SDK, you can add `excludeEOA: true` as an option: [buyToken](ref:buytoken) or [acceptOffer](ref:acceptoffer).  
> Smart contract wallets / routers should exclude Blur orders as they cannot sign / fill orders.

These restrictions mean that filling Blur orders comes with limitations:

- Before buying, users need to sign a message to sign into Blur
- Blur purchases can only be combined with purchases from marketplaces that the Blur router already supports (OpenSea, LooksRare, X2Y2). If you try to purchase from other marketplaces, we will break it into multiple transactions
- Features like normalizing royalties or collecting fees on top are not possible, because they require usage of the Reservoir Router contract
- If you accept an offer, you'll receive Blur Pool ETH, not ETH or WETH in your wallet, which needs to be withdrawn in a separate transaction

We do our best to abstract these limitations from end users and developers, making the experience as seamless as possible.

Hopefully, over time Blur will be upgraded, and some of these limitations removed.

## Blur Overview

Blur has quickly become one of the most popular NFT marketplaces, and it is one of the largest platforms for NFTs by volume. The platform is well-designed and easy to use, and it offers a number of features that are not available on other marketplaces. If you are looking to buy or sell NFTs, Blur is a great option.

Some core features & background about Blur:

- The platform is built on the Ethereum blockchain & has no marketplace fees.
- Blur is backed by a number of venture capital firms, including Paradigm.
- The platform has over 146,000 users and has facilitated over $1.4 billion in trading volume.

Blur is a rapidly growing NFT marketplace that has quickly become a major player in the industry. The platform offers a number of features that are not available on other marketplaces, and it is well-positioned to attract both professional and casual NFT traders.