---
title: "How to Add feesOnTop"
slug: "how-to-add-feesontop"
hidden: false
createdAt: "2023-05-02T20:32:01.662Z"
updatedAt: "2023-08-01T17:12:53.136Z"
---
`feesOnTop` (referral fees) are fees paid to an individual or entity for facilitating a sale. For example, you can set `feesOnTop` on your marketplace built with Reservoir's SDK, ReservoirKit, or APIs for all orders purchased on your platform. This applies to orders coming from OpenSea or other aggregated marketplaces.

### Using the Reservoir SDK

To add `feesOnTop`, you can follow these steps for the [`buyToken` method](https://docs.reservoir.tools/reference/buytoken):

1. First, make sure you have installed and configured the Reservoir SDK. If you haven't, you can refer to the Reservoir SDK (JS/TS/Node) [here](https://docs.reservoir.tools/reference/reservoir-sdk-jstsnode).

2. Next, when executing a buy or sell order, you can include the `feesOnTop`  in the options (formatted as `feeRecipient:feeAmount`). The `feesOnTop` parameter is an array of objects, each containing a recipient (the address receiving the referral fee) and a fixed fee in wei.

Here's a sample code snippet for adding `feesOnTop` when buying a token:

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
  items: [{ token: "0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:1", quantity: 1 }],
  options: {
    feesOnTop: [
      "0xF296178d553C8Ec21A2fBD2c5dDa8CA9ac905A00:1000000000000000", 
      "0xF296178d553C8Ec21A2fBD2c5dDa8CA9ac905A00:1000000000000000"
    ]
  }
  signer,
  onProgress: (steps: Execute['steps']) => {
    console.log(steps)
  }
})

```

This example demonstrates how to add feesOnTop when buying a token using the Reservoir SDK. The `feesOnTop` parameter is included in the options object when calling the `buyToken` method.

### Using the ReservoirKit

You can add `feesOnTopBps` or `feesOnTopFixed` in ReservoirKit. This is for the [BuyModal](https://docs.reservoir.tools/reference/buymodal). Please note that `feesOnTopBps` will take precedence over the `feesOnTopFixed`. The `feesOnTopFixed` is in the atomic unit of the listing currency (e.g. wei is used for ETH). List of fees (formatted as `feeRecipient:feeAmount`) to be taken when filling. Unless overridden via the currency param, the currency used for any fees on top matches the buy-in currency detected by the backend.

Below is a sample configuration for the [BuyModal](doc:buymodal). Note that an array of referrers and fees cannot be passed, please see the [SDK](###using-the-reservoir-sdk) or [API](###using-the-execute-api) to pass an array.

```typescript
import { BuyModal } from '@reservoir0x/reservoir-kit-ui'

<BuyModal
  trigger={
    <button>
      Buy Token
    </button>
  }
  collectionId="0xf5de760f2e916647fd766b4ad9e85ff943ce3a2b"
  tokenId="1236715"
	feesOnTopBps={['0xF296178d553C8Ec21A2fBD2c5dDa8CA9ac905A00:250']}
  onPurchaseComplete={(data) => console.log('Purchase Complete')}
  onPurchaseError={(error, data) => console.log('Transaction Error', error, data)}
  onClose={(data, stepData, currentStep) => console.log('Modal Closed')}

/>
```

### Using the Reservoir API

> 🚧 We recommend using Reservoir SDK
> 
> [Reservoir SDK](#using-reservoir-sdk) includes helpers that abstract the process of iterating through steps, and returning callbacks that can be used to update your UI.

To set a `feesOnTop` for an order, input in the `feesOnTop` field (formatted as `feeRecipient:feeBps`) as an option for the [`/execute/buy` API](https://docs.reservoir.tools/reference/postexecutebuyv7).  In the example, the `feesOnTop` parameter is an array of objects, each containing a recipient (the address receiving the referral fee) and a fixed fee in wei.

```curl
curl --request POST \
     --url https://api.reservoir.tools/execute/buy/v7 \
     --header 'accept: */*' \
     --header 'content-type: application/json' \
     --header 'x-api-key: demo-api-key' \
     --data '
{
  "items": [
    {
      "quantity": 1,
      "token": "0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:1"
    }
  ],
  "onlyPath": false,
  "normalizeRoyalties": false,
  "allowInactiveOrderIds": false,
  "feesOnTop": [
      "0x43E9f2AaC7abEF1f7702136Bd0Db00000000000A:1000000000000000",
      "0x43E9f2AaC7abEF1f7702136Bd0Db00000000000B:1000000000000000",
  ],
  "partial": false,
  "skipBalanceCheck": false,
  "excludeEOA": false,
  "taker": "0x8ba1f109551bD432803012645Ac136ddd64DBA72"
}
'

```