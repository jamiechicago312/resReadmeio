---
title: "Minting"
slug: "minting"
excerpt: "Integrate minting functionality & data right into your application through Reservoir. Supporting a number of direct mint platform integrations as well as auto-detecting most standard mint contracts."
hidden: false
createdAt: "2023-07-26T17:16:54.260Z"
updatedAt: "2023-08-07T18:43:48.690Z"
---
Reservoir now supports minting across multiple chains & multiple platforms. Our mint capabilities cover a wide of mints through direct platform integrations and auto-detection. You can add minting using our API directly or using reservoirKit's collect modal. We also provide a host of data around mints including surfacing trending mints. 

# Executing Mints with Reservoir

> 📘 How Reservoir defines "Collect"
> 
> Traditionally in the NFT ecosystem there was always a seperation between primary and secondary liquidity. Once a collection mints out, users are directed to secondary marketplaces to purchase NFTs. Reservoir now blends the line between primary and secondary liquidity. With our release of mints and aggregation of marketplace liquidity, rather than having a seperation minting & purchasing off secondary through Reservoir, end users are simply able to "collect" NFTs. Using Reservoir, if a collection is finished minting you can have your users collect by purchasing the lowest listing for that collection across Reservoir's ecosystem.

## API

To mint tokens via Reservoir's API you can call the [Buy Tokens](https://docs.reservoir.tools/reference/postexecutebuyv7) endpoint. By default when purchasing a token through this endpoint it will set the fillType to  `preferMint`. `preferMint` will attempt to mint the token, if the token is already minted, then it will purchase the token from aggregated secondary markets. If you exclusively want mint, ensure to set the `fillType` to `mint`.

## Collect Modal

Reservoir makes it easy to add minting functionality through ReservoirKit's **[Collect Modal](https://docs.reservoir.tools/reference/collectmodal-mint-sweep)**. Collect modal takes it a step beyond minting and integrates "collecting" which allows for purchases of lowest listings through Reservoir's aggregated ecosystem. 

# Trending Mints & other Mint Data

Reservoir offers access to mint data by surfacing **Trending mints**, **Mint Volume per Chain**, **Mint Activity**, **Collection Mint Stage** & **Tokens Minted.**

### Trending Mints

To surface trending mints you can use the **[Top Selling Collections](https://docs.reservoir.tools/reference/getcollectionstopsellingv1)** endpoint. By default, this endpoint will return both secondary trending and mint trending. To only return trending mints set the `fillType=mint` in the API URL. 

### Mint Volume per Chain

To retrieve the mint volume for a specific chain use the [Chain Stats](https://docs.reservoir.tools/reference/getchainstatsv1) endpoint. This endpoint will return the requested chain's stats for mint count & mint volume, among other data for the previous 24 hrs and 7 days.

### Mint Activities

Build mint feeds for [collections](https://docs.reservoir.tools/reference/getcollectionsactivityv6), [tokens ](https://docs.reservoir.tools/reference/gettokenstokenactivityv5)& [users ](https://docs.reservoir.tools/reference/getusersactivityv6)using the various activity endpoints. By default, these endpoints will return results for sales, asks, transfers, bids canceled bids, canceled asks, and mints. To filter for only mints simply append `?types=mint` to your API URL or Filter the response by `"type": "mint"`

### Collection Mint Stage

To find out if a collection is still minting you can query the [Collections](https://docs.reservoir.tools/reference/getcollectionsv6) API and enable the `includeMintStages` parameter. This will enable the response to return the `mintStage` array which will include the **stage **(public-sale or presale), **price**, **start / end time** & **max mints per wallet**. 

### Tokens Minted

View a stream of tokens minted from a collection by [subscribing ](https://docs.reservoir.tools/reference/websockets#interacting-with-the-websocket)to our `tokens.created` [websocket](https://docs.reservoir.tools/reference/token). 

# Mint Coverage

## Platform Support

We currently support minting from auto-detected mint contracts as well as direct integration with mints from [Zora](https://zora.co/), [ThirdWeb](https://thirdweb.com/solutions/minting), [Seadrop (OpenSea)](https://github.com/ProjectOpenSea/seadrop#seadrop) & [Manifold ](https://manifold.xyz/)

| Platform / Standard    | Method      | Allowlist          |
| :--------------------- | :---------- | :----------------- |
| Zora                   | Direct      | :white-check-mark: |
| ThirdWeb               | Direct      | :white-check-mark: |
| Seadrop                | Direct      | :x:                |
| Manifold               | Direct      | :x:                |
| Foundation             | Direct      | :white-check-mark: |
| Decent                 | Direct      | :white-check-mark: |
| Generic Mint Contracts | Auto-Detect | :x:                |



## Chain Support

Our minting functionality currently supports the following chains: [Ethereum](https://docs.reservoir.tools/reference/ethereum), [Optimism](https://docs.reservoir.tools/reference/optimism), BSC & Zora. More chain compatibility will be rolled out soon.

## Limitations

- Currently, Reservoir supports minting of **existing contracts** created on other platforms, Reservoir does not create the NFT contract for minting.
- We strive to have the most robust and accessible system possible, however, with minting, there is a limitation of how many types of contracts we can cover. At the moment we are only able to cover the mint contracts noted above and auto-detected mints, any others won't be covered and will return an error if attempted to execute.