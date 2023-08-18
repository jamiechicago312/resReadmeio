---
title: "Other Supported Marketplaces (API)"
slug: "other-supported-marketplaces"
excerpt: "Access other Reservoir supported marketplaces data & trading"
hidden: false
createdAt: "2023-05-22T16:48:36.866Z"
updatedAt: "2023-07-12T18:37:42.415Z"
---
# Getting Started with Market on Reservoir

Reservoir offers access to [150+ marketplaces](https://docs.reservoir.tools/reference/supported-marketplaces) through our simple, and powerful APIs, SDKs & UI kits. You can find a list of supported marketplaces, [here](https://dash.readme.com/project/reservoirprotocol/v3.0/refs/supported-marketplaces). To access data or trading for one of these marketplaces get started with an [API key](https://docs.reservoir.tools/reference/dashboard-sign-up) which has a generous [free plan & affordable paid subscriptions](https://reservoir.tools/pricing). All Reservoir endpoints include orders from all of our supported marketplaces. Should you want to access a specific market's data and trading specifically, you can. However, Reservoir doesn't support posting orders to all marketplaces. The following sections outline how to access a specific marketplace's data and trading using Reservoir.

# Getting Market Data & Orders

- **Sales** - Get Sales from our [Sales API](https://docs.reservoir.tools/reference/getsalesv5). Filtering using the API is not currently supported, so get all sales for a token, collection, or attribute, and filter on the front end using `"orderSource": "MARKETPLACE_DOMAIN"`or `"fillSource": "MARKETPLACE_DOMAIN"`. When using `orderSource` you are filtering by sales whose orders are native to that marketplace, while filtering on `fillSource` will return all sales that were filled on that marketplace, regardless of the order origination marketplace. 
- **Asks (Listings)** - Asks (listings) can be accessed through our [Asks API.](https://docs.reservoir.tools/reference/getordersasksv4) To get listings, ensure to set the `source=MARKETPLACE_DOMAIN`. [An example of the response.](https://api.reservoir.tools/orders/asks/v4?source=opensea.io)
- **Bids (Offers)** - Bids (offers) can be accessed through our [Bids API.](https://docs.reservoir.tools/reference/getordersbidsv5) To get offers, ensure to set the `source=MARKETPLACE_DOMAIN`. [An example of the response.](https://api.reservoir.tools/orders/bids/v5?source=opensea.io)

# Trading on Market through Reservoir

- **Buying** - Get the [listings data](https://docs.reservoir.tools/reference/getordersasksv4) and fill those orders either using the [API ](https://docs.reservoir.tools/reference/postexecutebuyv7)or [SDK](https://docs.reservoir.tools/reference/buytoken) _(recommended)_
- **Selling** - Get the [bid data](https://docs.reservoir.tools/reference/getordersbidsv5) and fill the bids either using the [API ](https://docs.reservoir.tools/reference/postexecutesellv7)or [SDK](https://docs.reservoir.tools/reference/acceptoffer) _(recommended)_
- **Creating Asks (Listings)** - Create the listing through the [API ](https://docs.reservoir.tools/reference/postexecutelistv5)or the [SDK](https://docs.reservoir.tools/reference/listtoken) _(recommended)_, set the `"orderKind": "DESIRED_PROTOCOL"` & `"orderbook": "DESIRED_ORDERBOOK"` and [check the cross-post status](https://docs.reservoir.tools/reference/getcrosspostingordersv1)
- **Create Bids (Offers)** - Create the offer through the [API ](https://docs.reservoir.tools/reference/postexecutebidv5)or the [SDK](https://docs.reservoir.tools/reference/placebid) _(recommended)_ set the `"orderKind": "DESIRED_PROTOCOL"` & `"orderbook": "DESIRED_ORDERBOOK"` and [check the cross-post status](https://docs.reservoir.tools/reference/getcrosspostingordersv1).

\*\*Not all marketplaces allow posting orders using Reservoir