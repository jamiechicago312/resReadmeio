---
title: "placeBid"
slug: "placebid"
excerpt: "This action is used to place a bid or multiple bids on an ERC-1155 or ERC-721 token. You can also use this action to bid on multiple exchanges/marketplaces."
hidden: false
createdAt: "2023-04-06T16:19:50.428Z"
updatedAt: "2023-07-20T19:04:26.738Z"
---
You can supply an object of parameters listed below:

| Parameter      | Description                                                                                                                                                                                              | Required | Example                                                                                                                                                                           |
| :------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **bids**       | An array of objects representing bids, mapping directly to the `params` property from the [execute bid api](/reference/postexecutebidv5). See API for options besides `token` bids.                      | `true`   | `[{         weiPrice: 10000000000000000,         orderbook: 'reservoir',         orderKind: 'seaport-v1.5',         token: "0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:0"     }]` |
| **wallet**     | A valid [WalletClient](https://viem.sh/docs/clients/wallet.html) from viem or a ReservoirWallet generated from an adapter. Learn more about [adapters](https://docs.reservoir.tools/reference/adapters). | `true`   | Refer to viem's documentation on [WalletClients](https://viem.sh/docs/clients/wallet.html)\_                                                                                      |
| **onProgress** | Callback to update UI state as execution progresses. Can also be used to get the transaction hash for a given step item.                                                                                 | `true`   | `(steps) => {            console.log(steps)      }`                                                                                                                               |
| **chainId**    | Override the current active chain                                                                                                                                                                        | `false`  | 1                                                                                                                                                                                 |

**Example**

```typescript
import { getClient, Execute } from "@reservoir0x/reservoir-sdk";
import { createWalletClient, http } from 'viem'

...

address = "0x8ba1f109551bD432803012645Ac136ddd6000000"
wallet = createWalletClient({
  account: address,
  transport: http()
})

getClient()?.actions.placeBid({
  bids: [{  
      weiPrice: 10000000000000000,  
      orderbook: 'reservoir',  
      orderKind: 'seaport-v1.5',  
      token: "0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:0"  
  }],
  wallet,
  onProgress: (steps: Execute['steps']) => {
    console.log(steps)
  }
})
```