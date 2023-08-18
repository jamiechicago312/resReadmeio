---
title: "How to use Off-Chain Cancellation"
slug: "off-chain-cancellation"
hidden: false
createdAt: "2023-05-02T15:03:37.737Z"
updatedAt: "2023-07-26T19:47:23.703Z"
---
Reservoir has introduced the Seaport Oracle, which allows for off-chain cancellations and price changes for NFT listings and bids. When creating a listing or bid, an oracle needs to co-sign the order before it is filled. To cancel, users simply tell the oracle not to co-sign any further. The oracle server is fully open-source (See [GitHub](https://github.com/reservoirprotocol/seaport-oracle)). To use the Seaport Oracle, check out the code snippets below.

> 📘 orderKind's Available for Seaport Oracle on Ethereum, Goerli, Polygon, & Mumbai
> 
> For listing/asks, off chain cancellation can be used with orderKind's seaport-v1.4, seaport-v1.5, and alienswap. 
> 
> For bidding/offers, off chain cancellation can be used with orderKind's seaport-v1.4 and seaport-v1.5.

### Using the Reservoir SDK

You'll need to make sure to use the latest SDK version. You can run the below code to insure you're on the latest SDK:

```
yarn upgrade @reservoir0x/reservoir-sdk
```

When using [listToken](https://docs.reservoir.tools/reference/listtoken) or [placeBid](https://docs.reservoir.tools/reference/placebid), make sure to include the `"useOffChainCancellation": true` option for the `orderKind`. See the code snippet below for a `listToken` example.

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
          token: "0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:1",  
          weiPrice: 10000000000000000,  
          orderbook: "reservoir",  
          orderKind: "seaport-v1.5",
          expirationTime: 1667403808616  
    			options: {
                "seaport-v1.5": { //Should match orderKind
                  "useOffChainCancellation": true //true enables offchain cancellation
                }
              },
  }],
  signer,
  onProgress: (steps: Execute['steps']) => {
    console.log(steps)
  }
})
```

When cancelling a listing or offer, you can use the latest version of [cancelOrder](https://docs.reservoir.tools/reference/cancelorder). This will run through the steps of accessing the oracle order and allow off-chain, gasless cancellations.

### Using the ReservoirKit

Please make sure you're using the latest version of the ReservoirKit to enable off chain order cancellation. You can run the below code to make sure it's updated.

```shell
yarn upgrade @reservoir0x/reservoir-kit-ui
```

To enable gasless cancellation, you'll need to make sure `oracleEnabled={true}`. This setting can be applied to [ListModal](https://docs.reservoir.tools/reference/listmodal) or [BidModal](https://docs.reservoir.tools/reference/bidmodal). See below for a sample with the BidModal:

```typescript
import { BidModal } from '@reservoir0x/reservoir-kit-ui'
import { useState } from 'react'

const openState = useState(true)

<BidModal
  trigger={
    <button>
      Place Bid
    </button>
  }
  collectionId="0xf5de760f2e916647fd766b4ad9e85ff943ce3a2b"
  tokenId="1469875"
  openState={openState}
  attribute={{
   key: "Fur",
   value: "Gold"
  }}
  oracleEnabled={true} //Set to true, add to code to enable offchain cancellation
  onBidComplete={(data) => {
    console.log('Bid Complete', data)
  }}
  onBidError={(error, data) => {
    console.log('Bid Transaction Error', error, data)
  }}
  onClose={(data, stepData, currentStep) => {
    console.log('BidModal Closed')
  }}
/>
```

If certain criteria is met, like `oracleEnabled={true}`, then you can use [EditListingModal](https://docs.reservoir.tools/reference/editlistingmodal) or [EditBidModal](https://docs.reservoir.tools/reference/editbidmodal). Please go to Modal links to read more.

To cancel a listing or bid, just continue to use [CancelListingModal](https://docs.reservoir.tools/reference/cancellistingmodal) or [CancelBidModal](https://docs.reservoir.tools/reference/cancelbidmodal). The Kit automatically detects when the oracle was enabled for a free, off chain, and gassless cancellation.

### Using the API

> 🚧 We recommend using Reservoir SDK
> 
> [Reservoir SDK](#using-the-reservoir-sdk) includes helpers that abstract the process of iterating through steps, and returning callbacks that can be used to update your UI.

You'll need to make sure to use the latest API for access to the Seaport Oracle:

- [Listing API](https://docs.reservoir.tools/reference/postexecutelistv5)
- [Offers API](https://docs.reservoir.tools/reference/postexecutebidv5)
- [Cancel API](https://docs.reservoir.tools/reference/postexecutecancelv3)

Below is an example of creating a listing using `/list/v5` and implementing off chain cancellation. Options need to be added to `orderKind` where `useOffChainCancellation` is true. Everything else is the same as a normal listing.

```curl
curl --request POST \
     --url https://api.reservoir.tools/execute/list/v5 \
     --header 'accept: */*' \
     --header 'content-type: application/json' \
     --header 'x-api-key: 440c94e2-0f99-5c9e-8251-fee751d21aa1' \
     --data '
{
  "params": [
    {
      "orderKind": "seaport-v1.5",
      "options": {
        "seaport-v1.5": {
          "useOffChainCancellation": true
        }
      },
      "orderbook": "reservoir",
      "automatedRoyalties": true,
      "currency": "0x0000000000000000000000000000000000000000",
      "token": "0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d:1",
      "weiPrice": "1000000000000000000"
    }
  ],
  "maker": "0x8ba1f109551bD432803012645Ac136ddd64DBA72"
}
'
```

You can follow adding these options when making offers with `/bids/v5`.

When canceling an bid or listing, just use the most up to date [Cancel API](https://docs.reservoir.tools/reference/postexecutecancelv3). The latest Cancel API will iterate through the steps necessary to cancel Seaport oracle orders.