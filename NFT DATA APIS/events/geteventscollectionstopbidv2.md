---
title: "Collection top bid changes"
slug: "geteventscollectionstopbidv2"
excerpt: "Every time the top offer of a collection changes (i.e. the 'top bid'), an event is generated. This API is designed to be polled at high frequency.\n\nThere are multiple event types, which describe what caused the change in price:\n\n- `new-order` > new bid at a higher price\n\n- `expiry` > the previous top bid expired\n\n- `sale` > the previous top bid was accepted\n\n- `cancel` > the previous top bid was cancelled\n\n- `balance-change` > the top bid was invalidated due NFT no longer available\n\n- `approval-change` > the top bid was invalidated due to revoked approval\n\n- `revalidation` > manual revalidation of orders (e.g. after a bug fixed)\n\n- `reprice` > price update for dynamic orders (e.g. dutch auctions)\n\n- `bootstrap` > initial loading of data, so that all tokens have a price associated\n\nSome considerations to keep in mind\n\n- Selling a partial quantity of available 1155 tokens in a listing will generate a `sale` and will have a new quantity.\n\n- Due to the complex nature of monitoring off-chain liquidity across multiple marketplaces, including dealing with block re-orgs, events should be considered 'relative' to the perspective of the indexer, ie _when they were discovered_, rather than _when they happened_. A more deterministic historical record of price changes is in development, but in the meantime, this method is sufficent for keeping an external system in sync with the best available prices.\n\n- Events are only generated if the top bid changes. So if a new order or sale happens without changing the top bid, no event is generated. This is more common with 1155 tokens, which have multiple owners and more depth. For this reason, if you need sales data, use the Sales API."
hidden: false
createdAt: "2023-03-24T14:10:57.645Z"
updatedAt: "2023-08-18T15:11:29.289Z"
---