---
title: "Professional Trading"
slug: "market-making"
excerpt: "Use Reservoir's Trading API to trade across all major NFT marketplaces"
hidden: false
createdAt: "2022-12-23T16:08:47.497Z"
updatedAt: "2023-06-14T17:46:16.024Z"
---
# Market making with Reservoir's Trading API

Reservoir's aggregated liquidity and easy-to-use APIs make it a useful tool for market makers in the NFT ecosystem who want to quickly and effectively provide liquidity across NFT markets. Reservoir provides the tools to understand the market, create robust trading strategies, and create and publish orders. Market makers can publish orders to the Reservoir ecosystem _and_ other major NFT marketplaces using Reservoir's tooling. 

## Create trading strategies with Reservoir Data

Reservoir has an comprehensive set of real-time and historical data for NFT collections, sales, and liquidity. You can see some of that data in use here: <https://dune.com/reservoir0x/nft-marketplace-overview> This data is particularly useful for creating models of NFT prices, and building robust market making strategies. All this data and more is available using our [Data APIs](https://docs.reservoir.tools/reference/overview). If you need more comprehensive data access, feel free to reach out. 

### Data

- Historical and real-time [sales](https://docs.reservoir.tools/reference/getsalesv5), [listings](https://docs.reservoir.tools/reference/getordersasksv4), and [bids](https://docs.reservoir.tools/reference/getordersbidsv5)

- [Token](https://docs.reservoir.tools/reference/gettokensv6) and [collection](https://docs.reservoir.tools/reference/getcollectionsv5) metadata, including [token attributes](https://docs.reservoir.tools/reference/getcollectionscollectionattributesallv4)

- Real time [floor price data](https://docs.reservoir.tools/reference/geteventscollectionsflooraskv2) including [TWAPs](https://docs.reservoir.tools/reference/getoraclecollectionsflooraskv5)

- Real-time and historical [bid data](https://docs.reservoir.tools/reference/geteventscollectionstopbidv2) including [TWAPs](https://docs.reservoir.tools/reference/getoraclecollectionstopbidv2)

## Using Reservoir's Trading API

You can utilize Reservoir's trading API to create and execute orders across all major marketplaces. While you can use the API directly, we recommend you use the ReservoirSDK, which wraps the API into a performant set of methods.

### ReservoirSDK

Reservoir SDK allows you to interact with major NFT marketplaces easily. In order to showcase this SDK we walk you through an example of market making activity below.  
Feel free to check out the full example code here.

Installing and Configuring the Reservoir SDK

```shell
> yarn add @reservoir0x/reservoir-sdk
```

The Reservoir SDK also requires viem to be installed, make sure that's added to your package.json if it isn't already.

```shell
> yarn add viem
```

To configure the SDK we first need to create a global instance of it:

```typescript
import { createClient } from "@reservoir0x/reservoir-sdk"

const client =  createClient({
  apiBase: "https://api.reservoir.tools",
  apiKey: "YOUR_API_KEY",
  source: "YOUR.SOURCE"
});

export default client
```

More details about the Reservoir SDK are available [here](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode).

### Bidding and Listing on Different Marketplaces

We are going to assume here that you have the price that you want to bid or list a token already computed. Where data can be useful for this calculation, see the Data APIs for real time data. 

#### Bidding

In order to bid you must first set the bid order params. For a collection bid, you simply set the collection as follows:

**Collection Bid Example**

```typescript
let bidPrice = x; //example bid price  
let expirationTime = dayjs().add(20, "minutes").unix().toString(); 
let bidOrder = {
  collection: contract,
  orderKind: "seaport",
  orderbook: "reservoir",
  automatedRoyalties: true,
  excludeFlaggedTokens: true,
  weiPrice: parseEther(bidPrice).toString(),
  expirationTime,
};
```

To make a token bid, In order to bid on a single token, you pass token: tokenId into the params in addition to the collection contract.

**Token Bid Example**

```typescript
let bidPrice = x; //example bid price  
let expirationTime = dayjs().add(20, "minutes").unix().toString();
let bidOrder = {
  collection: contract,
  token: tokenId,
  orderKind: "seaport",
  orderbook: "reservoir",
  automatedRoyalties: true,
  excludeFlaggedTokens: true,
  weiPrice: parseEther(bidPrice).toString(),
  expirationTime,
};
```

You can also place trait and arbitrary token set bids, depending on the orderbook you choose. 

Here `orderKind` and `orderbook` set the marketplace you wish to interact with:

| Marketplace | orderKind  | orderbook  | Marketplace Fee | Available Features                                |
| :---------- | :--------- | :--------- | :-------------- | :------------------------------------------------ |
| OpenSea     | seaport    | opensea    | 2.5%            | Collection, token bids                            |
| LooksRare   | looks-rare | looks-rare | 2%              | Collection, token bids                            |
| X2Y2        | x2y2       | x2y2       | 0.5%            | Collection, token bids                            |
| Reservoir   | seaport    | reservoir  | 0%              | Collection, trait, token arbitrary token set bids |

Then, you can simply use the the Reservoir SDK for bidding:

```typescript
await reservoirClient.actions
  .placeBid({
    signer: signer,
    onProgress: () => {},
    bids: [bidOrder],
  })
```

The place bid function takes an array of bid objects that match the params passed to the execute bid api 

#### Listing

In order to list you must first set the listing params:

**Example System Set-up**

```typescript
let listPrice = x //example list price 
let expirationTime = dayjs().add(20, "minutes").unix().toString();
 
let listOrder = {
  token: `${contract}:${token}`,
  orderKind: "seaport",
  orderbook: "reservoir",
  weiPrice: parseEther(listPrice).toString(),
  expirationTime: listingTime,
};

await reservoirClient.actions
  .listToken({
    signer: signer,
    onProgress: () => {},
    listings: [listOrder],
  })
```

## Example Server-side Setup

To submit list and bid orders server-side using OpenZeppelin, you must first configure an [OpenZeppelin defender relayer](https://www.openzeppelin.com/defender). Once this is done, sending transactions through your relay is as simple as creating a custom signer as follows:

```javascript
const { DefenderRelaySigner, DefenderRelayProvider } = require('defender-relay-client/lib/ethers');
const { ethers } = require('ethers');

const credentials = { apiKey: YOUR_API_KEY, apiSecret: YOUR_API_SECRET };
const provider = new DefenderRelayProvider(credentials);
const signer = new DefenderRelaySigner(credentials, provider, { speed: 'fast' });
```

One could set up a programmatic trading system in a number of ways. But one simple set up is as follows:  

- Design a trading strategy using Reservoir’s APIs to get all the data needed to set buys and sells or bids and asks appropriately
- Use Reservoir’s abstracted SDK for creating orders
- For on-chain actions use Ethers.js and connect to an OpenZeppelin defender relayer and Reservoir SDK takes care of everything that needs to happen behind the scenes (including approvals, making safety checks, etc.)
- Deploy a node server to execute a cron job, loop the job over a collections list and executes a market making strategy above