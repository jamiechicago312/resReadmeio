---
title: "Bids (offers)"
slug: "getordersbidsv6"
excerpt: "Get a list of bids (offers), filtered by token, collection or maker. This API is designed for efficiently ingesting large volumes of orders, for external processing.\n\n- There are a different kind of bids than can be returned:\n\n To get all orders unflitered, select `sortBy` to `updatedAt`. No need to pass any other param. This will return any orders for any collections, token, attribute, etc. \n\n- Inputting a 'contract' will return token and attribute bids.\n\n- Inputting a 'collection-id' will return collection wide bids./n/n- Please mark `excludeEOA` as `true` to exclude Blur orders."
hidden: false
createdAt: "2023-06-28T10:04:51.265Z"
updatedAt: "2023-08-18T15:11:28.815Z"
---
