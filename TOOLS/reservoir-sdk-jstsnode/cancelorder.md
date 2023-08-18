---
title: "cancelOrder"
slug: "cancelorder"
excerpt: "This action is can be used to cancel and valid order (bids/listings)"
hidden: false
createdAt: "2023-04-06T16:20:48.984Z"
updatedAt: "2023-07-20T19:05:11.461Z"
---
You can supply an object of parameters listed below:

| Parameter      | Description                                                                                                                                                                                              | Required | Example                                                                                      |
| :------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------- | :------------------------------------------------------------------------------------------- |
| **id**         | An order id                                                                                                                                                                                              | `true`   | `"0x5c27af06f65deac22abb4307fb68ead818152fee9bc781558be12f8a6a590f97"`                       |
| **wallet**     | A valid [WalletClient](https://viem.sh/docs/clients/wallet.html) from viem or a ReservoirWallet generated from an adapter. Learn more about [adapters](https://docs.reservoir.tools/reference/adapters). | `true`   | Refer to viem's documentation on [WalletClients](https://viem.sh/docs/clients/wallet.html)\_ |
| **onProgress** | Callback to update UI state as execution progresses. Can also be used to get the transaction hash for a given step item.                                                                                 | `true`   | `(steps) => {            console.log(steps)      }`                                          |
| **options**    | Supports all of the parameters allowed in the [execute cancel api](/reference/getexecutecancelv2)                                                                                                        | `false`  | `{ maxFeePerGas: 2000, ... }`                                                                |
| **chainId**    | Override the current active chain                                                                                                                                                                        | `false`  | 1                                                                                            |

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

getClient()?.actions.cancelOrder({
  id: "0x5c27af06f65deac22abb4307fb68ead818152fee9bc781558be12f8a6a590f97",
  wallet,
  onProgress: (steps: Execute['steps']) => {
    console.log(steps)
  }
})
```