---
title: "Bulk Order Creation"
slug: "bulk-order-creation"
excerpt: "Create orders across major NFT marketplaces from a common interface"
hidden: false
createdAt: "2022-12-23T18:12:29.316Z"
updatedAt: "2023-06-14T17:48:19.534Z"
---
Reservoir's APIs support bulk order creation enabling developers to cross-post orders across multiple marketplaces with one common interface. When you create bulk orders on Seaport, you'll be able to use just one signature. You can use the [Trading API](doc:trading-data-apis) or the [ReservoirSDK](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode) to bulk create orders. 

## Using the Reservoir SDK

To further simplify this process, Reservoir SDK abstracts the complexities around steps management making it even easier to bring this functionality to your users. Here is an example of using the SDK for bulk order creation. You can see the `listToken` method [here](https://docs.reservoir.tools/docs/listtoken).

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
      token: "8d04a8c79ceb0889bdd12acdf3fa9d207ed3ff63:5",  
      weiPrice: 10000000000000000,  
      orderbook: "reservoir",  
      orderKind: "seaport",  
      expirationTime: 1667403808616  
    },
    {
      token: "0x5FbDB2315678afecb367f032d93F642f64180aa3:1",
      weiPrice: 20000000000000000,
      orderbook: "reservoir",
      orderKind: "seaport",
      expirationTime: 1667403808616
    },
    {
      token: "0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2:2",
      weiPrice: 30000000000000000,
      orderbook: "reservoir",
      orderKind: "seaport",
      expirationTime: 1667403808616
    }
  ],
  signer,
  onProgress: (steps: Execute['steps']) => {
    console.log(steps)
  }
})
```

## Using the Trading API

> 🚧 We recommend using Reservoir SDK
> 
> [Reservoir SDK](https://docs.reservoir.tools/docs/reservoir-sdk) includes helpers that abstract the process of iterating through steps, and returning callbacks that can be used to update your UI.

Here is an example of using the `execute/list/v5` API with multiple tokens. Reference the execute API [here](https://docs.reservoir.tools/reference/postexecutelistv5).

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
      "orderKind": "seaport-v1.4",
      "orderbook": "reservoir",
      "automatedRoyalties": true,
      "currency": "0x0000000000000000000000000000000000000000",
      "token": "8d04a8c79ceb0889bdd12acdf3fa9d207ed3ff63:5",
      "weiPrice": "1000000000000000000"
    },
    {
      "orderKind": "seaport-v1.4",
      "orderbook": "reservoir",
      "automatedRoyalties": true,
      "currency": "0x0000000000000000000000000000000000000000",
      "token": "0x5FbDB2315678afecb367f032d93F642f64180aa3:1",
      "weiPrice": "2000000000000000000"
    },
    {
      "orderKind": "seaport-v1.4",
      "orderbook": "reservoir",
      "automatedRoyalties": true,
      "currency": "0x0000000000000000000000000000000000000000",
      "token": "0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2:2",
      "weiPrice": "3000000000000000000"
    }
  ],
  "maker": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c000000"
}
```