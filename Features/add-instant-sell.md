---
title: "Instant Sell"
slug: "add-instant-sell"
excerpt: "Leverage aggregated bid liquidity to serve your users the best bids on their NFTs"
hidden: false
createdAt: "2022-12-07T22:04:54.130Z"
updatedAt: "2023-06-14T17:47:37.247Z"
---
# What is instant sell?

Instant sell is a feature of Reservoir that lets users to sell their token at a fair market price without having to experience the hassle of listing on a marketplace, a process that is time consuming and uncertain. Developer teams can easily add this functionality to their products with Reservoir. It is particularly valuable for [Wallets & Portfolios](doc:walletportfolio-app) that are showcasing users' NFTs and want to make it easy to sell right out of their app. 

# How does it work?

Reservoir aggregates the best bids from [all major sources](doc:supported-marketplaces), including marketplaces like Opensea and Blur, AMM protocols like Sudoswap and NFTX, and professional market makers. Using this information, we determine the market-wide best bid on every token, allowing you to display prices next to each NFT in a user's portfolio. When the user wants to sell, we generate the calldata that is needed to accept the bid on the underlying protocol. All of the complexity of dealing with different protocols is abstracted away.

Want to see it in action? [Try the demo](https://instantsell.io/).

# Adding instant sell to your product

While there are many ways to take advantage of Reservoir’s aggregated bid liquidity, below is one example of how to add instant sell into your product in two simple steps using [ReservoirKit](https://docs.reservoir.tools/reference/reservoirkit).

1. **Find a user’s best bids from all their tokens using [user-top-bids endpoint](https://docs.reservoir.tools/reference/getordersusersusertopbidsv2) ([example](https://api.reservoir.tools/orders/users/0xD5c0D17cCb9071D27a4F7eD8255F59989b9aee0d/top-bids/v1?optimizeCheckoutURL=false&normalizeRoyalties=false&sortBy=floorDifferencePercentage&sortDirection=desc&limit=20))**

![](https://files.readme.io/afab20e-Screen_Shot_2022-12-07_at_5.36.18_PM.png)

2. **Initiate ResevoirKit’s [AcceptBidModal](https://docs.reservoir.tools/reference/acceptbid-modal) when user clicks Sell to accept the bid and handle the execute steps.**

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/60257b9-uikit.png",
        null,
        ""
      ],
      "align": "center",
      "sizing": "75% "
    }
  ]
}
[/block]