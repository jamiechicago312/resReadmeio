---
title: "How to Cross Post Orders"
slug: "how-to-cross-post-orders"
hidden: false
createdAt: "2023-05-08T19:16:10.325Z"
updatedAt: "2023-06-14T17:59:57.096Z"
---
Reservoir's developer tools allows you to list your NFT on multiple marketplaces within one execution. This allows you to get instant liquidity and aggregation for increased order visibility. Below are guides on how to cross post a single token onto multiple marketplaces with the SDK, ReservoirKit, and the API. _We recommend using the SDK or Kit instead of the API as they abstract the process of going through the steps and return callbacks._

> 📘 How to check cross posted order status?
> 
> When cross posting orders to multiple marketplaces, you can check the status using the [cross posting orders ](https://docs.reservoir.tools/reference/getcrosspostingordersv1)API. The API and SDK will return a `crossPostingOrderId` after submission. ReservoirKit will not return an `id` at this time.

### Using the Reservoir SDK

To cross post orders, you can modify [listToken](https://docs.reservoir.tools/reference/listtoken) like in the example below. You'll need to pass a `listings` object for each marketplace you want to list to. Below is a sample of listing the same token to three different marketplaces: Reservoir, OpenSea, and x2y2. You can reference the `orderbook` and `orderKind` params from the [Create asks (listings)](ref:postexecutelistv5) API to see the latest marketplaces available.

```typescript
import { getClient, Execute } from "@reservoir0x/reservoir-sdk";
import { createWalletClient, http } from 'viem'

...

address = "0x8ba1f109551bD432803012645Ac136ddd6000000"
signer = createWalletClient({
  account: address,
  transport: http()
})

getClient()?.actions.listToken({
  listings: [
    {  
      token: "0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:1",  
      weiPrice: 10000000000000000,  
      orderbook: "reservoir",  
      orderKind: "seaport-v1.5",  
      expirationTime: 1667403808616  
    },
    {
      token: "0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:1",
      weiPrice: 10000000000000000,
      orderbook: "opensea",
      orderKind: "seaport-v1.5",
      expirationTime: 1667403808616
    },
    {
      token: "0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:1",
      weiPrice: 10000000000000000,
      orderbook: "x2y2",
      orderKind: "x2y2",
      expirationTime: 1667403808616
    }
  ],
  signer,
  onProgress: (steps: Execute['steps']) => {
    console.log(steps)
  }
})
```

### Using the ReservoirKit

ReservoirKit allows you to cross-post your listings to different online marketplaces without needing any adjustments. You can use the [ListModal](https://docs.reservoir.tools/reference/listmodal). The Kit has a pre-selected list of marketplaces that tokens get cross posted on. You can explore what collections are allowed on what marketplaces with the [Supported marketplaces by collection](ref:getcollectionscollectionsupportedmarketplacesv1) endpoint. Some marketplaces restrict listing certain collections. 

### Using the Reservoir API

> 🚧 We recommend using Reservoir SDK
> 
> [Reservoir SDK ](#using-the-reservoir-sdk)includes helpers that abstract the process of iterating through steps, and returning callbacks that can be used to update your UI.

To crosspost with the API, you can pass multiple params for the token you want to list. Make sure to line up the `orderbook` with the `orderKind`. Reservoir accepts all seaport versions, but OpenSea only support `seaport-v1.4` and `seaport-v1.5`. We recommend to use `seaport-v1.5` when listing to OpenSea as that is the most current version.

```curl
curl --request POST \
     --url https://api.reservoir.tools/execute/list/v5 \
     --header 'accept: */*' \
     --header 'content-type: application/json' \
     --header 'x-api-key: demo-api-key' \
     --data '
{
  "params": [
    {
      "orderKind": "seaport-v1.5",
      "orderbook": "reservoir",
      "automatedRoyalties": true,
      "currency": "0x0000000000000000000000000000000000000000",
      "token": "0x8d04a8c79ceb0889bdd12acdf3fa9d207ed3ff63:123",
      "weiPrice": "1000000000000000000"
    },
    {
      "orderKind": "seaport-v1.5",
      "orderbook": "opensea",
      "automatedRoyalties": true,
      "currency": "0x0000000000000000000000000000000000000000",
      "token": "0x8d04a8c79ceb0889bdd12acdf3fa9d207ed3ff63:123",
      "weiPrice": "1000000000000000000"
    },
    {
      "orderKind": "x2y2",
      "orderbook": "x2y2",
      "automatedRoyalties": true,
      "currency": "0x0000000000000000000000000000000000000000",
      "token": "0x8d04a8c79ceb0889bdd12acdf3fa9d207ed3ff63:123",
      "weiPrice": "1000000000000000000"
    }
  ],
  "maker": "0xF296178d553C8Ec21A2fBD2c5dDa8CA9ac905A00"
}
'
```