---
title: "Adapters"
slug: "adapters"
excerpt: "Override core logic for signing messages and sending transactions"
hidden: false
createdAt: "2023-06-22T20:14:28.380Z"
updatedAt: "2023-08-16T01:13:10.422Z"
---
The Reservoir SDK normalizes wallets allowing developers to override the underlying handlers for signing messages and sending transactions. This functionality opens the door to many use cases, some examples are:

- Using a different underlying library to sign messages and submit transactions (ethersjs, web3, viem, etc)
- Adding additional logs/analytics during these steps
- Integrating with third party services such as [gelato](https://www.gelato.network/)

All Reservoir SDK actions require passing in either a ReservoirWallet object or a viem WalletClient object. The ReservoirWallet interface normalizes the following methods:

[block:parameters]
{
  "data": {
    "h-0": "Method Name",
    "h-1": "Description",
    "h-2": "Arguments",
    "0-0": "**handleSignMessageStep**",
    "0-1": "This handler is triggered whenever the SDK encounters a signature step and requires a signature.",
    "0-2": "**item:** This is a `SignatureStepItem`, referring to the item returned from the execute api call. It has all the necessary data to sign a message depending on the `signatureKind`. Refer to the [type](https://github.com/reservoirprotocol/reservoir-kit/blob/main/packages/sdk/src/types/index.ts#L12) for more information.  \n**step:** This is a step returned from the execute api call. The key piece here is the `id`, `description` and `action` which will give you more context around the step and what it's purpose is. Refer to the [type](https://github.com/reservoirprotocol/reservoir-kit/blob/main/packages/sdk/src/types/index.ts#L56) for more information.",
    "1-0": "**handleSendTransactionStep**",
    "1-1": "This handler is triggered whenever the SDK encounters a transaction step and needs to send a transaction.",
    "1-2": "**chainId:** This is the chainId that the step is targeting.  \n**item:** This is a `TransactionStepItem`, referring to the item returned from the execute api call. It has all the necessary data to send the transaction (data, from, to, etc). Refer to the [type](https://github.com/reservoirprotocol/reservoir-kit/blob/main/packages/sdk/src/types/index.ts#L36) for more information.  \n**step:** This is a step returned from the execute api call. The key piece here is the `id`, `description` and `action` which will give you more context around the step and what it's purpose is. Refer to the [type](https://github.com/reservoirprotocol/reservoir-kit/blob/main/packages/sdk/src/types/index.ts#L56) for more information.",
    "2-0": "**address**",
    "2-1": "This method is an abstraction for retrieving the address performing the signing/sending of the transaction. It's mainly used to fill in the taker/maker in the SDK actions.",
    "2-2": "_N/A_",
    "3-0": "**transport**",
    "3-1": "This object is automatically extracted from the wallet so long as you're using viem (the default) wallet adapter. Otherwise you can create and pass in a [viem transport](https://viem.sh/docs/clients/intro.html#transports) which will be used internally to check the transaction status. ",
    "3-2": "_N/A_ This is a property, not a function"
  },
  "cols": 3,
  "rows": 4,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]

Refer to the [ReservoirWallet](https://github.com/reservoirprotocol/reservoir-kit/blob/main/packages/sdk/src/types/index.ts#L82) type definition for more information.

### Writing a custom adapter

Below is a stubbed out example illustrating the anatomy of the adapter, in your implementation you would add your custom logic:

```typescript
import { ReservoirWallet } from '@reservoir0x/reservoir-sdk'

//Add any additional parameters required to create the adapter
export const yourCustomAdapter = (): ReservoirWallet => {
  return {
    address: async () => {
      //Your custom code, must return an address string
    },
    handleSignMessageStep: async (stepItem, step) => {
      //Your custom code to sign a message, must return a signature
    },
    handleSendTransactionStep: async (chainId, stepItem, step) => {
      //Your custom code to send a transaction, must return a transaction hash
    },
    transport: http()
  }
}
```

### Official Adapters

- [Viem wallet adapter:](https://github.com/reservoirprotocol/reservoir-kit/blob/main/packages/sdk/src/utils/viemWallet.ts#L12) This is used internally to convert the viem WalletClient into a ReservoirWallet, making the SDK easier to use for the standard library (viem). There's no need to use this externally but we do expose it. It's also great reference material for making your own adapter.
- [Ethers wallet adapter:](https://github.com/reservoirprotocol/reservoir-kit/tree/main/packages/ethers-wallet-adapter) This adapter was created to allow applications using the Reservoir SDK to continue receiving updates while planning their migration to viem. While we urge teams to upgrade to viem we understand that adequate planning is required to make such a vital migration, we hope that this adapter can help bridge the gap until then.
- [Gelato adapter:](https://github.com/reservoirprotocol/reservoir-kit/tree/main/packages/gelato-adapter) This adapter was created to support applications wanting to provide gasless transactions via [gelato](https://www.gelato.network/relay) to their users. This package was developed by [Privy](https://www.privy.io/) in partnership with the Reservoir team. For now only [sponsored transactions](https://docs.gelato.network/developer-services/relay/erc-2771-recommended/sponsoredcallerc2771) are supported.