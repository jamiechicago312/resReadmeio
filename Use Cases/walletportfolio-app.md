---
title: "Wallets & Portfolios"
slug: "walletportfolio-app"
excerpt: "Build the most feature rich NFT wallet with Reservoir"
hidden: false
createdAt: "2023-02-20T21:27:47.825Z"
updatedAt: "2023-06-14T17:44:31.493Z"
---
Whether you are building NFT support into a wallet or a stand alone portfolio app, Reservoir has the tools you need to bring your application to the next level. 

# Add Comprehensive NFT Support to your Wallet or Portfolio App

Adding NFTs to your wallet or portfolio app is an important part of giving your users a full featured experience. With Reservoir you provide a comprehensive NFT experience by:

- Showing accurate NFT floor prices aggregated from all major marketplaces
- Easily add instant selling to your app by accessing global bid liquidity
- Get up-to-date metadata for your users’ tokens and collections

## Aggregated Floor Price Data

Floor price data is important for helping your users understand the current state of the market. Reservoir’s floor price data has some key benefits relative to other options: 

- [Aggregation](https://docs.reservoir.tools/reference/getcollectionscollectionsupportedmarketplacesv1) - Reservoir’s floor price data is aggregated from across all major marketplaces, making the data the most reliable and accurate representation of the market. 
- [Non-flagged token floors](https://docs.reservoir.tools/docs/flagged-tokens) - When collections have flagged tokens, they typically have a price discount, resulting in collection floor data being dominated by flagged tokens. Reservoir makes it easy to present non-flagged token floors to your users. 

**Getting floor price data**

You can access floor price data for your users using Reservoir’s API or react hooks: 

- User token data ([API](https://docs.reservoir.tools/v2.0/reference/getusersusertokensv6)/[hook](https://docs.reservoir.tools/v2.0/docs/useusertokens)) - get floor price data (and more) for a user’s tokens
- User collections data ([API](https://docs.reservoir.tools/v2.0/reference/getusersusercollectionsv2)/[hook](https://docs.reservoir.tools/v2.0/docs/useusercollections)) - get floor price data (and more) for a user’s collections

Learn more about floor price data [here](doc:floor-prices).

**Other relevant data**

Contextualizing the NFT market for your users requires a variety of data. Other highly relevant market data for wallets and portfolios follows:

- collection statistics and activity
- Token sales history
- Real-time and historical floor price events

Find out more about market data [here](doc:data-and-analytics).

## Embedded Buying and Selling

Reservoir makes it simple to embed buying, bidding, listing, and instant selling, right into your application. While portfolio apps and wallets may choose to embed a variety of market behaviors, we find that a valuable first step for these applications is to start with instant sell. If you want to integrate more market actions learn more about embedded buying and selling [here](https://docs.reservoir.tools/docs/embedded-buying-selling).

**Instant Sell**

For wallets and portfolio apps, we recommend starting by adding instant sell capabilities to your wallet. This lets your users instantly sell their tokens into the best bid from across the NFT ecosystem. With Reservoir you get: 

- [Aggregated bid liquidity](https://docs.reservoir.tools/reference/getordersusersusertopbidsv4) - Top bids aggregated from all major NFT markets.
- [Royalty normalization](https://docs.reservoir.tools/docs/royalties) - Opt-in to full royalty compliance. While not all orders have royalties baked in, Reservoir lets you fix orders to pay creator royalties on every order if you so choose.
- [Batch selling](https://docs.reservoir.tools/reference/postexecutesellv7) - Let your users sell multiple tokens with a single signature.
- [Top bid events](https://docs.reservoir.tools/reference/geteventscollectionstopbidv2) - Use Reservoir’s top bid events stream to notify your users about new top bids.

Implementing instant sell in your application is easy: 

Step 1: Get your users top bids using the [user-top-bids API endpoint](https://docs.reservoir.tools/v2.0/reference/getordersusersusertopbidsv3) or the [getUsersTopBids react hook](https://docs.reservoir.tools/v2.0/docs/useusertopbids). 

Step 2: When a user wants to sell, user the [Reservoir SDK](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode)’s [acceptOffer](https://docs.reservoir.tools/reference/acceptoffer) method or  [ReservoirKit](https://docs.reservoir.tools/reference/reservoirkit) [acceptBid modal](https://docs.reservoir.tools/reference/bidmodal) to initiate the transaction. 

Find out more about instant sell [here](https://docs.reservoir.tools/docs/add-instant-sell).

## Token and Collection Metadata

Representing NFT tokens accurately is a vital component of NFT support for any wallet or portfolio app. With Reservoir we provide all the data you need to represent users’ tokens and collections. 

- User token data ([API](https://docs.reservoir.tools/v2.0/reference/getusersusertokensv6)/[hook](https://docs.reservoir.tools/v2.0/docs/useusertokens)) - get floor price data (and more) for a user’s tokens
- User collections data ([API](https://docs.reservoir.tools/v2.0/reference/getusersusercollectionsv2)/[hook](https://docs.reservoir.tools/v2.0/docs/useusercollections)) - get floor price data (and more) for a user’s collections