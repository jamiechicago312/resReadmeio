---
title: "buyToken"
slug: "buytoken"
excerpt: "This action is used to buy an ERC-1155 or ERC-721 token. You can also use it to buy multiple tokens of the same kind (sweeping)."
hidden: false
createdAt: "2023-04-06T16:17:09.522Z"
updatedAt: "2023-07-20T19:04:01.298Z"
---
You can supply an object of parameters listed below:

[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Description",
    "h-2": "Required",
    "h-3": "Example",
    "0-0": "**items**",
    "0-1": "An array of objects representing orders to be purchased. Refer to the the [execute buy api](/reference/postexecutebuyv7) for a full list of parameters",
    "0-2": "`true`",
    "0-3": "`[{ token: \"0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:1\" }]`",
    "1-0": "**wallet**",
    "1-1": "A valid [WalletClient](https://viem.sh/docs/clients/wallet.html) from viem or a ReservoirWallet generated from an adapter. Learn more about [adapters](https://docs.reservoir.tools/reference/adapters).",
    "1-2": "`true`",
    "1-3": "_Refer to viem's documentation on [Wallet Clients](https://viem.sh/docs/clients/wallet.html)_",
    "2-0": "**onProgress**",
    "2-1": "Callback to update UI state as execution progresses. Can also be used to get the transaction hash for a given step item.",
    "2-2": "`true`",
    "2-3": "`(steps) => { console.log(steps) }`",
    "3-0": "**expectedPrice**",
    "3-1": "Token price used to prevent & protect buyer from price moves.",
    "3-2": "`false`",
    "3-3": "20.5",
    "4-0": "**options**",
    "4-1": "Supports all of the parameters allowed in the [execute buy api](/reference/postexecutebuyv7)",
    "4-2": "`false`",
    "4-3": "{  \n  source: \"reservoir.market\",  \n  skipBalanceCheck: true  \n  ...  \n}",
    "5-0": "**chainId**",
    "5-1": "Override the current active chain",
    "5-2": "`false`",
    "5-3": "1",
    "6-0": "**precheck**",
    "6-1": "A boolean indicating whether to just get back the steps/path and not to execute them. This is useful for checking if marketplace approval is required before iterating over the steps.",
    "6-2": "`false`",
    "6-3": "`false`",
    "7-0": "**gas**",
    "7-1": "String of the gas provided for the transaction execution. Unused gas will be returned.",
    "7-2": "`false`",
    "7-3": "\"1000000000000000\""
  },
  "cols": 4,
  "rows": 8,
  "align": [
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]

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

getClient()?.actions.buyToken({
  items: [{ token: "0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:1", quantity: 1 }],
  wallet,
  onProgress: (steps: Execute['steps']) => {
    console.log(steps)
  }
})
```

**Notes**

- `expectedPrice` - A feature that protects the buyer when the price changes drastically in a less desirable direction. There’s a small threshold in which it’s ok for it to go up but once it’s crossed the SDK prevents the transaction from being submitted. This check is hardcoded into the SDK and occurs before the transaction hits the blockchain.