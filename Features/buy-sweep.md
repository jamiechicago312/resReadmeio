---
title: "Buy & Sweep"
slug: "buy-sweep"
excerpt: "Easily add buying and sweeping into your app"
hidden: false
createdAt: "2022-12-23T16:48:29.185Z"
updatedAt: "2023-07-14T16:40:12.875Z"
---
# Buy and sweep NFTs from any app

Reservoir make it easy to add buying and sweeping functionality directly into your product. You can show your users the best prices across all major marketplaces and execute orders through one simple interface. 

1. Get aggregated listings from major marketplaces and buy using the [NFT Trading APIs](doc:reservoir-api) or [ReservoirKit](https://docs.reservoir.tools/reference/reservoirkit)
2. Let your users buy multiple on sale NFTs across many marketplaces in one transaction. See our guide on how to  [Add Sweeping using the ReservoirSDK](doc:sweeping)
3. Set your own referrer fees on-top of aggregated orders to generate revenue (see [Custom Fees](doc:custom-fees))
4. Automatically add missing royalty fees on-top of aggregated orders (see [Normalized Royalties](doc:royalties))

# How to add buy or sweep to your app

You can add buying and sweeping to your app using the Reservoir API or Reservoir SDK. 

> 🚧 We recommend using Reservoir SDK
> 
> [Reservoir SDK](https://docs.reservoir.tools/docs/reservoir-sdk) includes helpers that abstract the process of iterating through steps, and returning callbacks that can be used to update your UI.

## Trading API

Here is an example cURL request sweeping three tokens from the same collection. You can view `execute/buy/v7` here: (<https://docs.reservoir.tools/reference/postexecutebuyv7>)

```curl
curl --request POST \
     --url https://api.reservoir.tools/execute/buy/v6 \
     --header 'accept: */*' \
     --header 'content-type: application/json' \
     --header 'x-api-key: demo-api-key' \
     --data '
{
  "tokens": [
    "0x34d85c9cdeb23fa97cb08333b511ac86e1c4e258:61558",
    "0x34d85c9cdeb23fa97cb08333b511ac86e1c4e258:74395",
    "0x34d85c9cdeb23fa97cb08333b511ac86e1c4e258:80443"
  ],
  "onlyPath": false,
  "currency": "0x0000000000000000000000000000000000000000",
  "normalizeRoyalties": false,
  "partial": false,
  "skipBalanceCheck": false,
  "allowInactiveOrderIds": false,
  "excludeEOA": false,
  "taker": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c000000"
}
'
```

## ReservoirSDK

Here is an example with the SDK with the same tokens. You can view `buyToken` from the SDK here: (<https://docs.reservoir.tools/docs/buytoken>)

```typescript
import { getClient, Execute } from "@reservoir0x/reservoir-sdk";
import { createWalletClient, http } from 'viem'

...

address = "0x8ba1f109551bD432803012645Ac136ddd6000000"
signer = createWalletClient({
  account: address,
  transport: http()
})

getClient()?.actions.buyToken({
  items: [
    { token: "0x34d85c9cdeb23fa97cb08333b511ac86e1c4e258:61558"},
    { token: "0x34d85c9cdeb23fa97cb08333b511ac86e1c4e258:74395"},
    { token: "0x34d85c9cdeb23fa97cb08333b511ac86e1c4e258:80443"},
  ],
  signer,
  onProgress: (steps: Execute['steps']) => {
    console.log(steps);
  },
});
```