---
title: "How to list in different ERC-20's"
slug: "how-to-list-in-different-erc20s"
hidden: false
createdAt: "2023-05-03T19:38:06.518Z"
updatedAt: "2023-06-14T17:59:17.951Z"
---
You can list in any supported ERC-20 currencies. If the token is listed and traded on [CoinGecko](https://www.coingecko.com/), then you'll just need the contract address. If the token is not listed and traded on CoinGecko, you can follow the steps in the [customer ERC-20 guide](doc:adding-support-for-custom-erc-20-token)

### Using the Reservoir SDK

For the [listToken](https://docs.reservoir.tools/reference/listtoken), you will need to add a currency contract address as a param. By default, the listing is in the native currency of the chain.

In the example below, I am setting the currency to USDC using the contract address `0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48`.

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
  listings: [{  
    currency: "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",  
    token: "0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:1",  
    weiPrice: 10000000000000000,  
    orderbook: "reservoir",  
    orderKind: "seaport-v1.4",  
    expirationTime: 1714765672  
  }],
  signer,
  onProgress: (steps: Execute['steps']) => {
    console.log(steps)
  }
})
```

### Using the ReservoirKit

If there are multiple currencies supplied in the [ListModal](https://docs.reservoir.tools/reference/listmodal), the end user will be able to select from them; otherwise the currency will be selected by default. If no currencies are supplied, the modal will default to the chain's native currency.

```typescript
const currencies = [
  {
    contract: '0x0000000000000000000000000000000000000000',
    symbol: 'ETH',
  },
  {
    contract: '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2',
    symbol: 'WETH',
  },
  {
    contract: '0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48',
    symbol: 'USDC',
    decimals: 6
  },
]

...

<ListModal
  trigger={
    <button>List Item</button>
  }
  collectionId="0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d"
  tokenId="1"
  currencies={currencies} // supported currencies 
  openState={isOpen}
  nativeOnly={false}
  oracleEnabled={false}
  ...
/>
```

### Using the Reservoir API

> 🚧 We recommend using Reservoir SDK
> 
> [Reservoir SDK](###using-the-reservoir-sdk) includes helpers that abstract the process of iterating through steps, and returning callbacks that can be used to update your UI.

For the [`/execute/list/`](https://docs.reservoir.tools/reference/postexecutelistv5) endpoint, you will just need to add the contract address for the currency param. By default, the listing is in the native currency of the chain.

In the example below, the native currency (ETH) is replaced with USDC using the contract address `0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48`.

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
      "currency": "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
      "token": "0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:1",
      "weiPrice": "1000000000000000000"
    }
  ],
  "maker": "0xF296178d553C8Ec21A2fBD2c5dDa8CA900000000"
}
'
```