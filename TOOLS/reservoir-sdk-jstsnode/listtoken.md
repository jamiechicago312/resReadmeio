---
title: "listToken"
slug: "listtoken"
excerpt: "This action is used to list an ERC-1155 or ERC-721 token. You can also use this action to list to multiple exchanges/marketplaces."
hidden: false
createdAt: "2023-04-06T16:19:17.055Z"
updatedAt: "2023-07-20T19:04:16.657Z"
---
You can supply an object of parameters listed below:

| Parameter      | Description                                                                                                                                                                                              | Required | Example                                                                                                                                                                                                                                |
| :------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **listings**   | An array of objects representing listings, mapping directly to the `params` property from the [execute list api](/reference/postexecutelistv5).                                                          | `true`   | `[{             token: "0:0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d",             weiPrice: 10000000000000000,             orderbook: "reservoir",             orderKind: "seaport-v1.5",           expirationTime: 1667403808616 }]` |
| **wallet**     | A valid [WalletClient](https://viem.sh/docs/clients/wallet.html) from viem or a ReservoirWallet generated from an adapter. Learn more about [adapters](https://docs.reservoir.tools/reference/adapters). | `true`   | Refer to viem's documentation on [Wallet Clients](https://viem.sh/docs/clients/wallet.html)\_                                                                                                                                          |
| **onProgress** | Callback to update UI state as execution progresses. Can also be used to get the transaction hash for a given step item.                                                                                 | `true`   | `(steps) => {            console.log(steps)      }`                                                                                                                                                                                    |
| **precheck**   | A boolean indicating whether to just get back the steps/path and not to execute them. This is useful for checking if marketplace approval is required before iterating over the steps.                   | `false`  | `false`                                                                                                                                                                                                                                |
| **chainId**    | Override the current active chain                                                                                                                                                                        | `false`  | 1                                                                                                                                                                                                                                      |

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

getClient()?.actions.listToken({
  listings: [{  
          token: "0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:0",  
          weiPrice: 10000000000000000,  
          orderbook: "reservoir",  
          orderKind: "seaport-v1.5",  
          expirationTime: 1667403808616  
  }],
  wallet,
  onProgress: (steps: Execute['steps']) => {
    console.log(steps)
  }
})
```